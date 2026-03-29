# PDF Render Flow

Dokumen ini menjelaskan alur lengkap dari input form hingga file PDF selesai didownload.

## Diagram

```
Input Form
    │
    ▼
updatePreview()  ◄──── setiap perubahan input (event: input/change)
    │
    │  Render HTML string ke #invoice-preview (innerHTML)
    │  Hitung subtotal, diskon, pajak, grand total
    │
    ▼
#invoice-preview (live DOM)
    │
    │  User klik "Download Invois"
    │
    ▼
Guard Check
    │  typeof html2canvas === "undefined" || typeof window.jspdf === "undefined"
    │  → jika belum load: alert + return
    │
    ▼
Clone Preview Element
    │  createElement("div")
    │  innerHTML = preview.innerHTML
    │  Posisi fixed off-screen (-9999px) agar tidak terlihat user
    │  Lebar dikunci ke 794px (A4 @ 96dpi)
    │  append ke document.body
    │
    ▼
onclone callback (html2canvas)
    │  Remove semua <link rel="stylesheet"> dan <style> dari clone
    │  → Menghilangkan Tailwind CSS yang menggunakan oklch/oklab
    │     (tidak didukung html2canvas)
    │  Inject minimal CSS dengan hex values murni
    │  → Cukup untuk merender teks, grid, tabel, warna
    │
    ▼
html2canvas(el, { scale: 1.5, ... })
    │  Render clone element ke HTMLCanvasElement
    │  Resolusi output: 1191 x 1685px (794 * 1.5 × 1123 * 1.5)
    │  useCORS: true → izinkan gambar dari domain lain
    │  backgroundColor: "#ffffff" → pastikan background putih
    │
    ▼
canvas.toDataURL("image/jpeg", 0.92)
    │  Konversi canvas ke base64 JPEG
    │  Quality 0.92 → keseimbangan antara ukuran file dan ketajaman teks
    │  Hasil: ~300–700KB (vs ~13MB jika PNG dengan scale: 2)
    │
    ▼
jsPDF
    │  new jsPDF({ orientation: "portrait", unit: "mm", format: "a4" })
    │  addImage(imgData, "JPEG", 0, 0, pageW, pageH)
    │  → Gambar di-stretch pas ke seluruh halaman A4 (210 × 297mm)
    │
    ▼
pdf.save(`${invoiceNo}.pdf`)
    │  Trigger download di browser
    │
    ▼
File PDF tersimpan di komputer user
```

## Catatan Teknis

### Kenapa clone element, bukan langsung capture #invoice-preview?

Preview di browser menggunakan Tailwind CSS yang di-generate dengan `oklch`/`oklab` color functions. `html2canvas` tidak bisa mem-parse color functions tersebut dan akan crash. Dengan clone + remove stylesheet + inject CSS bersih, capture bisa berjalan tanpa error.

### Kenapa JPEG bukan PNG?

PNG adalah lossless — untuk canvas 1191×1685px ukurannya bisa mencapai 10–15MB. JPEG dengan quality 0.92 menghasilkan file ~300–700KB dengan kualitas yang masih tajam untuk dokumen teks. Invoice ini background putih dengan teks hitam, sehingga artefak JPEG tidak signifikan pada quality tinggi.

### Kenapa scale 1.5?

- `scale: 1` → resolusi pas A4, teks bisa terlihat kasar
- `scale: 2` → resolusi 2x, terlalu besar untuk JPEG sekalipun
- `scale: 1.5` → sweet spot: teks tajam, ukuran file tetap kecil

### Limitasi

- Seluruh invoice di-fit ke 1 halaman PDF. Jika item sangat banyak dan preview overflow, bagian bawah akan terpotong.
- PDF adalah gambar (raster), bukan teks — tidak bisa di-select atau di-search di PDF reader.

# Simpel Invois

Aplikasi web untuk membuat invoice dengan cara yang simpel. Isi form, preview langsung jadi, download PDF.

## Tech Stack

- [Astro 6](https://astro.build) — static site framework
- [Tailwind CSS 4.2](https://tailwindcss.com) — styling
- [html2canvas](https://html2canvas.hertzen.com) + [jsPDF](https://github.com/parallax/jsPDF) — PDF export (via CDN)

## Fitur

- Form invoice dengan validasi realtime
- Preview invoice realtime di samping form
- Dukungan 2 bahasa: Indonesia & Inggris (label preview otomatis berubah)
- Dukungan 2 mata uang: IDR & USD (dengan konversi kurs)
- Tambah/hapus item dinamis
- Diskon, pajak/PPN, dan catatan (opsional)
- Download hasil invoice sebagai PDF
- Desain mobile-first, responsif di semua device

## Halaman

| Route | Deskripsi |
|-------|-----------|
| `/` | Landing page |
| `/create` | Halaman pembuatan invoice |

## Menjalankan Project

```sh
npm install       # install dependencies
npm run dev       # dev server di localhost:4321
npm run build     # build production ke ./dist/
npm run preview   # preview build
```

## Desain

- **Font**: Plus Jakarta Sans (heading), PT Sans (body)
- **Warna**: `#14110F` (primer), `#B3B4B3` (sekunder), `#f3f3f4` (background)

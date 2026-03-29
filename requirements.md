## Deskripsi
Aplikasi berbasis web untuk membuat invoice dengan cara yang simpel.

## Tech Stack
Vanilla Javascript, Astro 6 dan Tailwind CSS 4.2

## User Flow
Cek file UserFlow-SimpelInvois.png di folder Wireframe.

## Desain
### Warna
Primer (#14110F) untuk teks heading dan background button
Secondary (#B3B4B3) untuk teks body
Background (#f3f3f4) untuk background dan teks di button

### Font
Plus Jakarta Sans untuk heading
PT Sans untuk body

#### Ukuran Font
- 3xl : 6.854 rem (110px)
- 2xl : 4.236 rem (68px)
- xl: 2.618 rem (42px)
- lg: 1.618 rem (26px)
- base: 1 rem (16px)
- sm: 0.618rem (10px)

### Wireframe
Cek pada folder wireframe

Input yang opsional  :
1. Diskon
2. Pajak / PPn
3. Catatan

Sisanya, masuk ke wajib diisi.
### Hal yang harus diperhatikan
1. JIka memerlukan library tertentu, jangan langsung install. Konfirmasi terlebih dahulu.
2. Gunakan pendekatan mobile-first untuk desain supaya responsif di segala device.
3. Kombinasikan penggunaan grid dan flex untuk layouting.
4. Input pada form yang wajib diisi, berikan tanda * berwarna merah disampingnya.
5. Tambahkan validasi di bawah input form secara realtime saat user mengosongi input wajib diisi, lalu tambahkan disabled state pada button Download Invois.
6. Invois yang dibuat, hasilnya dapat didownload dalam bentuk PDF.
7. Website harus mendapatkan skor setinggi mungkin di Google Page Speed untuk segala aspek.
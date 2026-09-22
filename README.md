git# ppw-2026-week2-12S24017

Halaman portofolio profesional (single page) **Arya Pratama Sinambela**, mahasiswa S1 Sistem Informasi Institut Teknologi Del. Dibuat untuk **Tugas Mandiri Praktikum Minggu 02** mata kuliah Pemrograman dan Pengujian Aplikasi Web (12S3101): *Pengembangan Halaman Web Portofolio & Layanan Interaktif Accessible Berbasis HTML5 dan Modern CSS*.

🔗 **Demo live:** https://aryasinambela.github.io/ppw-2026-week2-12S24017/

📁 **Repositori:** https://github.com/AryaSinambela/ppw-2026-week2-12S24017

## Fitur

- Header sticky dengan navigasi ke 6 bagian dan tautan "Lewati ke konten utama".
- **Tentang Saya:** kartu profil (foto, peran, keahlian, statistik) dan panel info kontak singkat.
- **Galeri Keahlian** dan **Portofolio Karya:** 8 kartu proyek dari GitHub dan CV.
- **Riwayat:** tabel semantik, daftar pendidikan, dan sertifikasi.
- **Layanan:** 4 kartu layanan dengan tombol Formulir dan WhatsApp yang teks pesannya sudah terisi.
- **Formulir Layanan:** 3 kelompok `fieldset`, 8 tipe kontrol, dan validasi bawaan HTML5.
- **Kontak:** kartu Email, WhatsApp, LinkedIn, GitHub, domisili, dan kampus.
- Responsif dengan `@media (max-width: 768px)` dan menghormati `prefers-reduced-motion`.

## Struktur Folder

```
ppw-2026-week2-12S24017/
├── index.html          # struktur & konten halaman
├── style.css           # seluruh styling (CSS eksternal)
├── Foto_Profile.jpeg   # foto profil pada kartu
├── screenshots/        # gambar untuk README
├── README.md
└── LICENSE             # MIT
```

## Cara Menjalankan

1. Clone repositori: `git clone https://github.com/AryaSinambela/ppw-2026-week2-12S24017.git`
2. Buka folder di VS Code, lalu jalankan **Live Server** pada `index.html`.
3. Tekan `F12` → *Toggle Device Emulation* untuk melihat tampilan mobile.

Deployment: **Settings → Pages → Branch `main` → Save**.

---

## Penjelasan Kode

### 1. Struktur HTML semantik (`index.html`)

| Elemen | Dipakai untuk | Alasan |
|---|---|---|
| `<header>` + `<nav>` | Logo dan menu utama | Landmark bagi pembaca layar dan mesin pencari |
| `<main>` | Seluruh konten inti (satu per dokumen) | Sesuai aturan HTML5 |
| `<section>` (7 buah) | Tentang, Keahlian, Portofolio, Riwayat, Layanan, Formulir, Kontak | Tiap section punya judul `<h2>` dan `aria-labelledby` |
| `<article>` | Kartu profil, kartu keahlian, proyek, dan layanan | Blok konten yang berdiri sendiri |
| `<aside>` | Info Singkat dan Alur Layanan | Konten pelengkap |
| `<address>` | Daftar kanal kontak | Elemen khusus untuk informasi kontak |
| `<footer>` | Hak cipta dan tautan profil | Penutup dokumen |

Hanya ada satu `<h1>`. Judulnya disembunyikan visual dengan kelas `.sr-only`, karena nama tampil di kartu profil. Urutan heading berjalan `h1 → h2 → h3 → h4`.

### 2. Tabel dan list

- **Tabel Riwayat** memakai `<caption>`, `<thead>`, `<tbody>`, `<tfoot>`, `scope="col"` untuk judul kolom, dan `scope="row"` untuk nama proyek. Pembungkusnya `.table-wrap` (`overflow-x: auto`) supaya tabel bisa digeser di layar kecil.
- **List:** `<ul>` (tag keahlian, daftar sertifikasi), `<ol>` (pendidikan dan alur layanan), dan `<dl>` (info singkat).


### 3. Fitur Layanan

Setiap kartu layanan (`.service-card`) berisi deskripsi, daftar cakupan (`.check-list`), tag teknologi, dan dua tombol:

```html
<a class="btn btn-primary" href="#formulir">Isi Formulir</a>
<a class="btn btn-secondary"
   href="https://wa.me/6285260168713?text=Halo%20Arya%2C%20saya%20tertarik%20..."
   target="_blank" rel="noopener noreferrer">WhatsApp</a>
```

- `#formulir` menuju formulir di halaman yang sama.
- `wa.me/<nomor>?text=<pesan>` membuka WhatsApp dengan pesan yang sudah terisi (tanpa JavaScript). Nomor memakai kode negara `62` tanpa angka `0` di depan, dan karakter khusus dalam pesan di-*encode* (`%20` untuk spasi, `%26` untuk `&`).
- `rel="noopener noreferrer"` menjaga keamanan tautan yang dibuka di tab baru.
- Tiap tautan punya `aria-label` yang menyebut layanannya, karena teks "WhatsApp" berulang di beberapa kartu.

CSS-nya: `.service-card` memakai flexbox kolom dan `.card-actions { margin-top: auto }`, sehingga tombol selalu rata di dasar kartu walaupun panjang teksnya berbeda. Tanda centang pada `.check-list` dibuat dengan `::before` sehingga tidak perlu gambar.


### 4. Formulir Layanan

- **3 `<fieldset>` + `<legend>`:** Data Identitas, Detail Permintaan, dan Preferensi & Persetujuan. Grup radio dan checkbox punya `<fieldset>` sendiri.
- **8 tipe kontrol:** `text`, `email`, `tel`, `number`, `radio`, `checkbox`, `select`, dan `textarea`.
- **Aksesibilitas:** setiap kontrol punya `<label for="id">`. Teks bantuan dihubungkan lewat `aria-describedby`. Tanda bintang wajib berupa `aria-hidden` dan diganti teks tersembunyi untuk pembaca layar.
- **Validasi native:** `required`, `type="email"`, `pattern` pada telepon, `min`/`max` pada angka, dan `minlength` pada pesan. Kolom yang tidak valid mendapat border merah lewat `:user-invalid`.
- **Pengiriman:** GitHub Pages tidak punya server, jadi `action="mailto:..."` dipakai dan formulir akan membuka aplikasi email dengan isi yang sudah terisi.

### 5. Fitur Kontak

Kanal kontak dibungkus `<address>` berisi `<ul class="contact-grid">`. Empat kartu pertama adalah tautan penuh (`mailto:`, `wa.me`, LinkedIn, GitHub), sedangkan Domisili dan Kampus hanya informasi (`<p>`, bukan tautan). Ikon berupa teks singkat dengan `aria-hidden="true"`, sehingga pembaca layar hanya membaca label dan nilainya.

CSS-nya:

- `.contact-address { font-style: normal }` menghilangkan italic bawaan `<address>`.
- `grid-template-columns: repeat(auto-fit, minmax(min(240px, 100%), 1fr))` membuat kartu menyusun diri otomatis tanpa media query dan tidak melebar di layar kecil.
- Kartu berupa tautan mendapat efek hover (naik 4px, bayangan, border aksen), dan efek ini dimatikan di mobile serta saat pengguna memilih `prefers-reduced-motion`.

### 6. CSS (`style.css`)

| Bagian | Isi |
|---|---|
| 1. Reset & variabel | `*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0 }` dan *design token* di `:root` |
| 2. Header & navigasi | Flexbox, `position: sticky`, `backdrop-filter` |
| 3. Kontainer & bagian | `.page-container` (maks. 1080px) dan `.section` dengan `scroll-margin-top` |
| 4. Kartu profil | Banner gradien, avatar bulat, badge status, statistik (gaya dari modul) |
| 5. Tombol | `.btn-primary` dan `.btn-secondary` dengan transisi hover |
| 6. Panel samping | `<aside>`, `<dl>`, daftar langkah bernomor dengan `counter` |
| 7. Grid kartu | CSS Grid `auto-fit`/`auto-fill` |
| 8. Tabel | Zebra, hover baris, `caption`, `tfoot` |
| 9. Formulir | Focus ring, radio/checkbox dengan `accent-color`, `:user-invalid` |
| 10. Footer, layanan, kontak | Footer flex, `.check-list`, `.contact-card` |
| 11. Responsif | `@media (max-width: 768px)` dan `prefers-reduced-motion` |

**Palet warna 60-30-10**

- **60% netral:** putih dan abu-biru lembut (`--surface`, `--bg-1`, `--bg-2`).
- **30% teks:** slate gelap (`--ink`, `--text`).
- **10% aksen:** biru sky (`--accent`, `--accent-strong`) untuk tombol, badge, dan tautan.

**Aksesibilitas kontras (WCAG 2.2 AA).** Warna teks kecil abu-abu terang diganti `#64748b`, sedangkan tombol dan tautan memakai `#0369a1`, supaya rasio kontrasnya mencapai minimal 4.5:1. Fokus keyboard ditandai `:focus-visible`.

**Responsif.** Di bawah 768px, grid dua kolom (Tentang dan Formulir) menjadi satu kolom, header tidak lagi *sticky*, dan padding diperkecil.

## Pemenuhan Rubrik

| Komponen | Bobot | Implementasi |
|---|---|---|
| Struktur Semantik HTML5 | 20% | `header`, `nav`, `main`, 7 `section`, `article`, 2 `aside`, `address`, `footer` |
| Data (List & Table) | 15% | Tabel lengkap + `ul`, `ol`, `dl` |
| Form & Aksesibilitas | 20% | 3 `fieldset`, 8 tipe kontrol, `label for`, `required`, `aria-describedby` |
| Estetika & CSS Modern | 25% | Flexbox/Grid, 60-30-10, `border-radius`, `box-shadow`, transisi hover, `@media` |
| Git & Deployment | 20% | Repositori `ppw-2026-week2-12S24017`, README ini, GitHub Pages |

# ppw-2026-week3-12S24017

Modernisasi dan refactoring halaman **Personal Portfolio & Service Portal** dari Minggu 2 (HTML5 + CSS murni) menjadi **Bootstrap 5.3** yang dipadukan dengan **Advanced Custom CSS**.

- **Nama:** Arya Pratama Sinambela
- **NIM:** 12S24017
- **Kelas:** 13 SI 1
- **Mata kuliah:** Pemrograman dan Pengujian Web (12S3101)
- **Live demo:** https://aryasinambela.github.io/ppw-2026-week2-12S24017/
- **Repositori:** https://github.com/AryaSinambela/ppw-2026-week2-12S24017
- **Branch:** `week3-bootstrap`

| | |
|---|---|
| **Nama** | Arya Pratama Sinambela |
| **NIM** | 12S24017 |
| **Kelas** | [isi kelas] |
| **Mata kuliah** | Pemrograman dan Pengujian Web (12S3101), Semester Ganjil 2026/2027 |
| **Dosen pengampu** | Chandro Pardede, S.Kom., M.Sc. |
| **Tugas** | Tugas Mandiri Minggu 3: Penguasaan CSS Lanjutan, Spesifisitas, dan Integrasi Bootstrap 5 |
| **Live demo** | https://aryasinambela.github.io/ppw-2026-week2-12S24017/ |
| **Repositori** | https://github.com/AryaSinambela/ppw-2026-week2-12S24017 |
| **Branch** | `week3-bootstrap` |

---

## 1. Ringkasan Pembaruan

- **Bootstrap 5.3.3** (CSS + JS bundle) dan **Bootstrap Icons 1.11.3** dimuat via CDN. `custom-style.css` dimuat **setelah** Bootstrap agar override berjalan lewat urutan cascade.
- **Navbar responsif** `navbar-expand-lg` dengan hamburger collapse. Header menempel di atas (`sticky-top`) dengan latar solid sehingga konten tidak tembus.
- **Indikator menu aktif berupa pil animasi.** Pil meluncur mengikuti bagian yang sedang dibaca: **biru + teks putih** saat sudah berada di bagian itu, **kuning + teks hitam** saat sedang berpindah.
- **Hero dua kolom** dengan tombol CTA.
- **Grid portofolio** `row-cols-1 row-cols-md-2 row-cols-lg-3 g-4` berisi 6 kartu proyek. Masing-masing terhubung ke **Modal** dengan isi berbeda.
- **Formulir layanan modern:** floating labels, input group berikon, select kategori, checkbox syarat, dan umpan balik validasi visual.
- **Tema kustom** dengan 13 variabel CSS di `:root`. Tidak ada satu pun `!important`.

---

## 2. Sebelum vs Sesudah Integrasi Framework

| Aspek | Sebelum (Minggu 2) | Sesudah (Minggu 3) |
|---|---|---|
| Layout | Grid buatan sendiri (`repeat(auto-fit, minmax(...))`) dan media query manual | Grid 12-kolom Bootstrap (`container` → `row` → `col-*`, `row-cols-*`) |
| Navbar | Flexbox biasa; tidak ada toggle di mobile | `navbar-expand-lg` + tombol hamburger collapse |
| Header | `position: sticky` lewat CSS sendiri, latar semi-transparan | `header.sticky-top` dengan latar solid dan bayangan tipis |
| Menu aktif | Skrip scroll sederhana yang hanya menambah kelas `active` | Deteksi posisi scroll + pil animasi dua warna (biru/kuning) |
| Detail proyek | Artikel panjang berjajar di halaman | Kartu ringkas + **Modal Bootstrap** per proyek |
| Formulir | `input` dan `textarea` polos | Floating labels, input group berikon, select, checkbox, `.valid-feedback` / `.invalid-feedback` |
| Tombol | `.btn.primary` dan `.btn.ghost` buatan sendiri | `.btn-del` / `.btn-del-outline` yang memakai variabel `--bs-btn-*` |
| Responsivitas | Satu breakpoint manual (800px) | Lima breakpoint Bootstrap (`xs`, `sm`, `md`, `lg`, `xl`) |
| Ikon | Emoji | Bootstrap Icons (emoji tetap dipakai sebagai banner kartu) |
| Tema | Variabel di `style.css` | Variabel yang sama + override variabel Bootstrap (`--bs-*`) |

---

## 3. Struktur Folder

```
ppw-2026-week2-12S24017/
├── index.html                      # struktur halaman + skrip (proyek, navigasi, formulir)
├── custom-style.css                # override & tema, dimuat setelah Bootstrap
├── Foto_Profile.jpeg               # foto profil
├── Arya_Pratama_Sinambela_CV.pdf   # CV (tombol Unduh CV)
├── screenshots/                    # gambar untuk README
├── README.md
└── LICENSE                         # MIT
```

`style.css` dari Minggu 2 digantikan `custom-style.css`. Versi lamanya tetap tersimpan di branch `main`.

---

## 4. Penjelasan Teknis Sesuai Modul

### 4.1 Fondasi Framework & Semantik (Bobot 15%)

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css" rel="stylesheet">
<link href="custom-style.css" rel="stylesheet">   <!-- setelah Bootstrap -->
...
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

- Urutan pemuatan penting: Bootstrap dulu, `custom-style.css` sesudahnya. Dengan begitu aturan kustom yang spesifisitasnya sama akan menang tanpa `!important`.
- Struktur semantik HTML5 tetap utuh: `<header>` + `<nav>`, `<main>` berisi 6 `<section>` (masing-masing punya `id`), `<address>` untuk kanal kontak, dan `<footer>`.
- Bundle JS sudah menyertakan Popper, dipakai untuk collapse dan modal.

### 4.2 Responsive Navbar & Hero (Bobot 20%)

**Navbar**

```html
<header class="sticky-top">
  <nav class="navbar navbar-expand-lg navbar-del py-2">
    <div class="container">
      <a class="navbar-brand" href="#beranda">Arya<span>.</span>Sinambela</a>
      <button class="navbar-toggler border-0" data-bs-toggle="collapse" data-bs-target="#mainNavbar" ...>
      <div class="collapse navbar-collapse" id="mainNavbar"> ... </div>
```

- `sticky-top` ditaruh di `<header>`, bukan di `<nav>`. `position: sticky` hanya menempel selama elemen induknya masih terlihat, dan induk `<nav>` hanya setinggi navbar itu sendiri.
- Latar navbar dibuat solid (`background: var(--paper)`) dan diberi bayangan tipis, supaya konten yang digulir tidak tembus dan tidak menimpa tulisan menu.
- Menu hamburger otomatis menutup setelah sebuah link diklik (`bootstrap.Collapse.getInstance('#mainNavbar')?.hide()`).
- `section[id] { scroll-margin-top: 72px; }` menjaga judul bagian tidak tertutup navbar saat menu diklik.

**Indikator menu aktif (pil animasi)**

| Status | Warna pil | Warna teks |
|---|---|---|
| Sedang berada di bagian tersebut | Biru (`--nav-active`) | Putih (`--nav-active-text`) |
| Baru diklik / sedang digulir menuju bagian itu | Kuning (`--nav-going`) | Hitam (`--nav-going-text`) |

- Di desktop (≥ 992px), elemen `.nav-pill` meluncur ke menu tujuan dengan `transform`, `width`, dan `height` yang ditransisikan. Di mobile, warnanya langsung dipasang di latar link.
- Bagian aktif dihitung sendiri dari posisi scroll (`getBoundingClientRect`, ambang 120px dari atas layar). Jika halaman sudah mentok di dasar, menu terakhir (Kontak) otomatis aktif.
- Deteksi ini menggantikan ScrollSpy bawaan Bootstrap. ScrollSpy hanya membaca satu pita sempit di layar, sehingga bagian yang pendek atau paling bawah bisa terlewat.
- Semua animasi dimatikan pada `prefers-reduced-motion: reduce`.

**Hero:** `row align-items-center` dengan `col-lg-7` (teks + CTA) dan `col-lg-5` (foto). Di mobile, foto tampil lebih dulu berkat `order-1` / `order-lg-2`. Dua tombol CTA: **Lihat Proyek** dan **Unduh CV**.

### 4.3 Grid Portofolio & Modal Dialog (Bobot 20%)

```html
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4" id="projectGrid"></div>
```

- Kartu dan modal dibuat dari satu array `projects` di JavaScript. Satu sumber data menghasilkan 6 kartu dan 6 modal, jadi tidak ada markup yang diduplikasi.
- Setiap kartu memuat banner (`.thumb`), badge teknologi (`.badge`), deskripsi singkat, dan tombol **Lihat Detail** (`data-bs-toggle="modal"`).
- Setiap modal berisi data berbeda: tiga kotak meta, uraian panjang, badge, dan tautan dokumen bila ada. Modal memakai `modal-dialog-centered modal-dialog-scrollable modal-lg`, `aria-labelledby`, tombol `btn-close`, dan bisa ditutup dengan tombol Tutup atau tombol `Esc`.
- Enam proyek: TitikMu, Antony Mart SyRS, Academic Record Management, Del-Laundry, Sistem Reservasi Hotel, dan UI/UX Aplikasi Pelacak Kesehatan.

Sistem breakpoint yang dipakai:

| Breakpoint | Lebar | Kolom kartu proyek |
|---|---|---|
| `xs` | < 576px | 1 |
| `md` | ≥ 768px | 2 |
| `lg` | ≥ 992px | 3 |

### 4.4 Modernisasi Formulir Layanan (Bobot 15%)

| Komponen Bootstrap | Penerapan |
|---|---|
| Floating Labels (`.form-floating`) | Nama, email, kategori, dan pesan |
| Input Groups | Nama (`bi-person`) dan email (`bi-envelope`) |
| Select | Kategori layanan (5 pilihan) |
| Checkbox | Persetujuan syarat & ketentuan |
| Umpan balik validasi | `.valid-feedback` dan `.invalid-feedback` pada setiap kolom |

- Formulir memakai atribut `novalidate`. Validasi dijalankan oleh JavaScript dengan `checkValidity()`, lalu kelas `is-valid` / `is-invalid` dipasang pada kontrol dan pada pembungkus `.form-floating`. Pembungkus perlu ikut diberi kelas karena kotak umpan balik adalah saudara pembungkus, bukan saudara `<input>`.
- Aturan validasi: nama ≥ 3 karakter, email valid, kategori wajib dipilih, pesan ≥ 10 karakter, checkbox wajib dicentang.
- Validasi diperbarui saat mengetik (`input`), saat berubah (`change`), dan saat submit.
- GitHub Pages tidak punya server, jadi data yang valid dikirim lewat `mailto:` dengan subjek dan isi yang sudah terisi.

### 4.5 Custom Overrides & Theming (Bobot 15%)

**Variabel CSS di `:root` (13 buah, syarat minimal 6):**

| Kelompok | Variabel |
|---|---|
| Warna identitas | `--navy`, `--navy-2`, `--amber`, `--ink`, `--muted`, `--paper`, `--line` |
| Bentuk & bayangan | `--radius`, `--shadow-lift` |
| Status navigasi | `--nav-active`, `--nav-going`, `--nav-active-text`, `--nav-going-text` |

Variabel Bootstrap juga ditimpa langsung, yaitu `--bs-body-font-family`, `--bs-body-bg`, `--bs-body-color`, `--bs-body-line-height`, dan `--bs-link-color-rgb`.

**Palet personal:** navy (`#2b2554`) dan amber (`#ffb957`) di atas kertas krem (`#f6f5f1`) dengan font Poppins, bukan tema biru bawaan Bootstrap.

**Mikro-interaksi:**
- Kartu terangkat 4px dengan bayangan saat di-hover atau saat fokus berada di dalamnya (`.card-del:is(:hover, :focus-within)`).
- Tombol berganti warna dan naik 2px saat di-hover.
- Pil navigasi meluncur dan berganti warna; teks menu aktif melakukan efek "pop".
- Input group berubah kuning saat kolomnya difokuskan.

**Tanpa `!important`.** Tombol dikustomisasi lewat variabel bawaan Bootstrap, misalnya:

```css
.btn-del {
  --bs-btn-color: #fff;
  --bs-btn-bg: var(--navy);
  --bs-btn-hover-bg: var(--amber);
  --bs-btn-hover-color: var(--ink);
}
```

### 4.6 Kalkulasi Spesifisitas dan Selektor Lanjutan

**Spesifisitas (A, B, C, D) pada aturan kustom:**

| Selektor | Skor | Catatan |
|---|---|---|
| `h2` | (0, 0, 0, 1) | Kalah dari `.h5` (0, 0, 1, 0), sehingga `.modal-title.h5` tetap berukuran kecil |
| `.card-del:is(:hover, :focus-within)` | (0, 0, 2, 0) | `:is()` mengambil spesifisitas argumen terkuat |
| `.navbar-del .navbar-nav .nav-link` | (0, 0, 3, 0) | Sama dengan aturan Bootstrap; menang karena dimuat belakangan |
| `.navbar-del .navbar-nav .nav-link.active` | (0, 0, 4, 0) | Mengalahkan `.navbar-nav .nav-link.active` milik Bootstrap (0, 0, 3, 0) |
| `.timeline > .tl-item:nth-child(odd)::before` | (0, 0, 3, 1) | 2 class + 1 pseudo-class + 1 pseudo-element |
| `#mainNavbar .navbar-nav .nav-link.is-going` | (0, 1, 3, 0) | 1 ID + 3 class |
| `#mainNavbar.is-traveling .navbar-nav .nav-link.active:not(.is-going)` | (0, 1, 5, 0) | `:not()` mengambil skor argumennya |

**Selektor lanjutan yang dipakai:**

| Fitur | Contoh di `custom-style.css` |
|---|---|
| Child combinator `>` | `.timeline > .tl-item` |
| Adjacent sibling `+` | `.timeline > .tl-item + .tl-item` (jarak antaritem) |
| `:nth-child()` | Titik timeline bergantian navy/amber (`odd` / `even`) |
| `:is()` | `.card-del:is(:hover, :focus-within)` |
| `:not()` | Menu lama dibersihkan saat berpindah (`.nav-link.active:not(.is-going)`) |
| `:focus-within` | `.input-group:focus-within .input-group-text` |
| `::before` / `::after` | Lingkaran amber di belakang foto, lingkaran di header bagian, titik timeline |

Selektor sibling umum `~` dipakai oleh Bootstrap sendiri untuk menampilkan `.invalid-feedback` (`.is-invalid ~ .invalid-feedback`).

---

## 5. Pemenuhan Checklist Modul

| Area Evaluasi | Bobot | Implementasi |
|---|---|---|
| 1. Fondasi Framework & Semantik | 15% | Bootstrap 5.3.3 CSS + JS bundle + Icons; struktur semantik utuh; meta viewport; `custom-style.css` dimuat setelah Bootstrap |
| 2. Responsive Navbar & Hero | 20% | `sticky-top` + brand; hamburger collapse berfungsi; hero dengan dua CTA |
| 3. Grid Portofolio & Modal | 20% | 6 kartu dalam `row-cols-1 row-cols-md-2 row-cols-lg-3 g-4`; 6 modal dengan konten berbeda |
| 4. Modernisasi Formulir | 15% | Floating labels, input group berikon, select, checkbox, feedback valid/invalid |
| 5. Custom Overrides & Theming | 15% | 13 variabel `:root`; palet navy-amber; hover halus; nol `!important` |
| 6. Git & Deployment | 15% | Branch `week3-bootstrap`; README ini (tabel komparasi + screenshot); GitHub Pages |

---

## 6. Checklist Pengujian

Uji dengan Live Server dan DevTools (`F12` → Toggle Device Emulation), lalu centang setelah diperiksa:

- [ ] 375px (< 576px): grid 1 kolom, tidak ada scroll horizontal
- [ ] 768px (`md`): grid 2 kolom
- [ ] 992px (`lg`): grid 3 kolom, menu tampil horizontal, pil navigasi aktif
- [ ] ≥ 1200px (`xl`): tata letak tetap rapi
- [ ] Hamburger membuka dan menutup menu; menu menutup setelah link diklik
- [ ] Console DevTools tanpa error JavaScript
- [ ] Navbar tetap menempel di atas saat digulir dan tidak tertimpa konten
- [ ] Pil navigasi berpindah di semua menu, ke bawah dan ke atas; Kontak aktif saat mentok di bawah
- [ ] Klik menu: pil kuning + teks hitam saat menuju, lalu biru + teks putih setelah tiba
- [ ] Setiap modal terbuka, isinya berbeda, dan bisa ditutup (tombol X, Tutup, `Esc`)
- [ ] Formulir menampilkan pesan invalid saat kosong dan pesan valid saat benar
- [ ] Navigasi keyboard: `Tab` menampilkan fokus yang jelas di semua tombol dan kolom
- [ ] GitHub Pages terbuka tanpa 404

---

## 7. Screenshot

| Tampilan | Berkas |
|---|---|
| Desktop: navbar + hero | `screenshots/desktop.png` |
| Menu aktif biru | `screenshots/nav-biru.png` |
| Menu berpindah (kuning) | `screenshots/nav-kuning.png` |
| Mobile: navbar terbuka | `screenshots/mobile-navbar.png` |
| Grid proyek | `screenshots/grid-proyek.png` |
| Modal detail | `screenshots/modal.png` |
| Formulir: state invalid | `screenshots/form-invalid.png` |
| Formulir: state valid | `screenshots/form-valid.png` |

![Desktop](screenshots/desktop.png)
![Menu aktif biru](screenshots/nav-biru.png)
![Menu berpindah kuning](screenshots/nav-kuning.png)
![Mobile](screenshots/mobile-navbar.png)
![Grid proyek](screenshots/grid-proyek.png)
![Modal](screenshots/modal.png)
![Form invalid](screenshots/form-invalid.png)
![Form valid](screenshots/form-valid.png)

---

## 8. Git & Deployment

```bash
git checkout -b week3-bootstrap
git add index.html custom-style.css
git commit -m "feat(week3): refactor portfolio to bootstrap 5 grid and modern components"
git add custom-style.css
git commit -m "style(week3): sticky solid navbar and animated blue/yellow nav pill"
git add README.md screenshots/
git commit -m "docs(week3): add before/after comparison table and screenshots"
git push -u origin week3-bootstrap
```

Aktifkan GitHub Pages: **Settings → Pages → Source: Branch `week3-bootstrap` → Save**, lalu tunggu 1 sampai 2 menit dan buka tautan live demo.

Pesan commit memakai konvensi `feat`, `style`, dan `docs` agar riwayat perubahan mudah dibaca.

---

## 9. Keterbatasan

- Bootstrap dan Poppins dimuat dari CDN, sehingga halaman memerlukan koneksi internet.
- Pengiriman formulir memakai `mailto:` karena GitHub Pages tidak memiliki server. Formulir membuka aplikasi email bawaan perangkat.
- Warna "biru" pada navigasi memakai navy tema (`--navy`). Ubah nilai `--nav-active` di `:root` jika ingin biru yang lebih terang.

## Lisensi

MIT. Lihat berkas `LICENSE`.
# ppw-2026-week3-12S24017

- **Nama:** Arya Pratama Sinambela
- **NIM:** 12S24017
- **Kelas:** 13 SI 1
- **Mata kuliah:** Pemrograman dan Pengujian Web (12S3101)
- **Live demo:** https://aryasinambela.github.io/ppw-2026-week2-12S24017/
- **Repositori:** https://github.com/AryaSinambela/ppw-2026-week2-12S24017
- **Branch:** `week3-bootstrap`

# Portofolio & Service Portal (Minggu 3: Bootstrap 5)

Refactoring halaman portofolio Minggu 2 (HTML5 + CSS murni) menjadi Bootstrap 5.3.3 yang dipadukan dengan Custom CSS Overrides. Tema navy–amber dan font Poppins tetap dipertahankan.

## Ringkasan Pembaruan

- Bootstrap 5.3.3 (CSS + JS bundle) dan Bootstrap Icons via CDN; `custom-style.css` dimuat setelah Bootstrap.
- Navbar `sticky-top` responsif dengan hamburger collapse, ditambah ScrollSpy untuk menu aktif.
- Hero dua kolom dengan tombol CTA.
- Grid proyek `row-cols-1 row-cols-md-2 row-cols-lg-3 g-4` berisi 6 kartu dan 6 modal detail.
- Formulir: floating labels, input group berikon, select kategori, checkbox syarat, dan validasi visual.
- Tema lewat CSS variables di `:root`, tanpa `!important`.

## Sebelum vs Sesudah Integrasi Framework

| Aspek | Sebelum (Minggu 2) | Sesudah (Minggu 3) |
|---|---|---|
| Layout | `.grid` buatan sendiri (`auto-fit`) dan media query manual | Grid 12-kolom Bootstrap (`row`, `col-*`, `row-cols-*`) |
| Navbar | Flex biasa, tanpa toggle mobile | `navbar-expand-lg` + hamburger collapse, `sticky-top` |
| Menu aktif | Skrip `scroll` manual | Bootstrap ScrollSpy (`data-bs-spy`) |
| Detail proyek | Artikel panjang di halaman | Kartu ringkas + Modal Bootstrap per proyek |
| Formulir | `input` dan `textarea` polos | Floating labels, input group berikon, select, checkbox, feedback valid/invalid |
| Tombol | `.btn.primary` / `.btn.ghost` buatan sendiri | `.btn-del` / `.btn-del-outline` (variabel `--bs-btn-*`) |
| Tema | Variabel CSS di `style.css` | Variabel yang sama + override variabel Bootstrap (`--bs-*`) |
| Ukuran CSS | ±150 baris CSS penuh | Bootstrap + ±140 baris override |

## Struktur Folder

```
├── index.html
├── custom-style.css
├── Foto_Profile.jpeg
├── Arya_Pratama_Sinambela_CV.pdf
├── screenshots/
└── README.md
```
# Joomax Custom Cursor

Library JavaScript ringan (±8 KB, tanpa dependency) untuk **cursor lingkaran kustom + efek ripple saat klik**. Pasang di website mana pun dengan satu script tag.

Demo: https://designjoomax.github.io/custom-cursor/demo/

## Fitur
- Lingkaran yang mengikuti mouse dengan halus (warna dan ukuran bebas), panah bawaan tetap terlihat (bisa disembunyikan).
- Ripple saat klik, beberapa klik berurutan aman, elemen dihapus setelah animasi.
- Efek hover (cursor membesar) di link, tombol, dan elemen interaktif.
- Shadow DOM: tidak bentrok dengan CSS website, tidak mengubah `body` atau `html` secara default, `pointer-events: none`.
- Otomatis nonaktif di layar sentuh, menghormati `prefers-reduced-motion`, aman dimuat dua kali.

## Pasang (paling sederhana)
Tambahkan sebelum `</body>` (atau di `<head>`):
```html
<script src="https://designjoomax.github.io/custom-cursor/cursor.js"></script>
```
Cursor langsung aktif.

## Contoh konfigurasi
```html
<script
  src="https://designjoomax.github.io/custom-cursor/cursor.js"
  data-color="#ff3b30"
  data-size="18"
  data-ripple="true"
  data-ripple-color="#ff3b30"
  data-ripple-size="90"
  data-ripple-duration="600"
  data-hover-effect="true"
  data-hide-native-cursor="false"
></script>
```
Daftar lengkap opsi, JavaScript API, dan perilaku otomatis: [docs/configuration.md](docs/configuration.md).

## JavaScript API (ringkas)
```js
JoomaxCursor.configure({ color: "#0a84ff", size: 24 }); // ubah langsung
JoomaxCursor.disable(); JoomaxCursor.enable();
JoomaxCursor.ripple(200, 200);                           // ripple manual
JoomaxCursor.destroy();
```
Untuk mengendalikan sendiri kapan mulai: `data-auto="false"` lalu `JoomaxCursor.init({ ... })`.

## Struktur repo
```text
custom-cursor/
├── cursor.js            versi terbaru (URL tetap)
├── releases/1.0.0/      salinan beku tiap versi
├── demo/                halaman demo (memakai ../cursor.js)
├── docs/configuration.md
├── README.md
└── LICENSE
```

## Deploy ke GitHub Pages
1. Buat repo publik `custom-cursor` di akun `designjoomax`.
2. Upload semua isi folder ini ke root repo.
3. Settings > Pages > Source: Deploy from a branch > `main` / `(root)` > Save.
4. Tunggu 1 sampai 2 menit. Script aktif di `https://designjoomax.github.io/custom-cursor/cursor.js` dan demo di `.../demo/`.

## Versi dan update
- **Latest**: `https://designjoomax.github.io/custom-cursor/cursor.js`. Website pengguna otomatis dapat pembaruan setelah `cursor.js` diganti (GitHub Pages menyimpan cache sekitar 10 menit).
- **Versi tetap (Pages)**: `https://designjoomax.github.io/custom-cursor/releases/1.0.0/cursor.js`
- **Rilis baru**: ubah `VERSION` dan komentar versi di `cursor.js`, salin ke `releases/<versi>/cursor.js`, commit, lalu buat tag Git `v<versi>`.
- Gunakan versi tetap untuk website penting, latest untuk website yang ingin selalu terbaru.

## CDN (jsDelivr)
jsDelivr mengambil langsung dari repo GitHub (perlu tag rilis, mis. `v1.0.0`):
```html
<script src="https://cdn.jsdelivr.net/gh/designjoomax/custom-cursor@1.0.0/cursor.js"></script> <!-- versi tetap -->
<script src="https://cdn.jsdelivr.net/gh/designjoomax/custom-cursor@1/cursor.js"></script>     <!-- terbaru 1.x -->
```
Jangan pakai `@main` di produksi (cache bisa lama).

## Troubleshooting
- **Cursor tidak muncul**: cek tab Network (script 404?), pastikan Pages aktif, dan pakai mouse (bukan layar sentuh). Ketik `JoomaxCursor` di Console untuk memastikan terpasang.
- **Tidak ada ripple**: `prefers-reduced-motion` aktif di sistem, atau `data-ripple="false"`.
- **Perubahan tidak terlihat**: cache. Muat ulang paksa (Ctrl+Shift+R) atau pakai URL versi.
- **Efek hover tidak muncul di elemen kustom**: tambahkan atribut `data-cursor-hover` atau atur `data-selector`.
- **Cursor tertutup elemen lain**: naikkan `data-z-index`, dan pastikan tidak ada elemen `popover`/`dialog` modal yang menutupinya (lapisan top-layer browser selalu di atas).

## Batasan
- Tidak bekerja di dalam `<iframe>` (pasang script di tiap halaman iframe yang sama origin).
- Situs dengan CSP yang melarang script dari `designjoomax.github.io` harus mengizinkannya di `script-src`.
- `dialog.showModal()` dan elemen top-layer menutupi cursor kustom.
- Perangkat hibrida: hanya gerakan mouse yang diikuti, sentuhan diabaikan.
- Ripple memerlukan Web Animations API (semua browser modern).

## Lisensi
MIT

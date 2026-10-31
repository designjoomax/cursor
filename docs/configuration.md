# Konfigurasi

Urutan prioritas (yang bawah menimpa yang atas): default, `window.JoomaxCursorConfig`, atribut `data-*` di script tag, lalu JavaScript API.

## Opsi

| Opsi (JS) | Atribut `data-*` | Default | Keterangan |
|---|---|---|---|
| `color` | `data-color` | `#e60020` | Warna lingkaran cursor (warna CSS apa pun) |
| `size` | `data-size` | `18` | Diameter lingkaran dalam px |
| `smoothing` | `data-smoothing` | `0.22` | Kehalusan gerak, 0.02 (sangat lembut) sampai 1 (instan) |
| `zIndex` | `data-z-index` | `2147483647` | Urutan tumpukan cursor |
| `ripple` | `data-ripple` | `true` | Aktifkan efek ripple saat klik |
| `rippleColor` | `data-ripple-color` | warna cursor | Warna ripple |
| `rippleSize` | `data-ripple-size` | `90` | Diameter akhir ripple (px) |
| `rippleDuration` | `data-ripple-duration` | `600` | Durasi ripple (ms) |
| `rippleWidth` | `data-ripple-width` | `2` | Tebal garis ripple (px) |
| `hoverEffect` | `data-hover-effect` | `true` | Cursor membesar di atas elemen interaktif |
| `hoverScale` | `data-hover-scale` | `1.8` | Faktor pembesaran saat hover |
| `hideNativeCursor` | `data-hide-native-cursor` | `false` | Sembunyikan panah bawaan (kolom teks tetap memakai cursor bawaan) |
| `selector` | `data-selector` | link, tombol, select, checkbox, radio, `[role=button]`, `[data-cursor-hover]`, dll | Selector elemen yang memicu efek hover |
| (khusus atribut) | `data-auto` | `true` | `false` = tidak aktif otomatis, panggil `JoomaxCursor.init()` sendiri |

Nilai boolean: `true`/`false`. Atribut `data-*` yang salah isi diganti default.

## Contoh

```html
<script src="https://designjoomax.github.io/custom-cursor/cursor.js"
  data-color="#ff3b30" data-size="18" data-ripple-size="120" data-hide-native-cursor="true"></script>
```

Lewat variabel global (sebelum script dimuat):
```html
<script>window.JoomaxCursorConfig = { color: "#0a84ff", size: 14 };</script>
<script src="https://designjoomax.github.io/custom-cursor/cursor.js"></script>
```

## JavaScript API

| Method | Fungsi |
|---|---|
| `JoomaxCursor.init(opts?)` | Mulai (otomatis dipanggil kecuali `data-auto="false"`) |
| `JoomaxCursor.configure(opts)` | Ubah opsi langsung, tanpa memuat ulang |
| `JoomaxCursor.enable()` / `.disable()` | Nyalakan / matikan sementara |
| `JoomaxCursor.ripple(x, y, opts?)` | Munculkan ripple manual di koordinat layar (px) |
| `JoomaxCursor.destroy()` | Hapus semua elemen dan listener |
| `JoomaxCursor.options` | Salinan opsi yang sedang aktif |
| `JoomaxCursor.version` | Versi library |

## Perilaku otomatis
- Tidak aktif di layar sentuh atau perangkat tanpa mouse. Aktif lagi jika mouse tersambung.
- `prefers-reduced-motion`: ripple dimatikan dan cursor mengikuti tanpa animasi.
- Di input teks, textarea, dan `contenteditable` lingkaran disembunyikan dan cursor bawaan dipakai.
- Elemen `disabled` atau `aria-disabled="true"` tidak memicu efek hover.
- Dimuat dua kali tidak menimbulkan error atau cursor ganda.

# EVOMI — Landing Page Flash Sale (Scalev)

Landing page satu halaman (single-file HTML) untuk kampanye **Flash Sale EVOMI Eau de Parfum 50 ml**, dibuat untuk dipasang di **Scalev** sebagai halaman custom HTML. Seluruh CSS dan JavaScript berada di dalam satu file, sehingga cukup salin isi file ke editor Scalev tanpa proses build.

- **Live checkout:** https://evomi-parfum.myscalev.com/checkout-flow-baru
- **Toko Shopee:** https://shopee.co.id/evomiindonesia
- **Aset (CDN):** https://github.com/ramadhan42/parfum-rama-assets via jsDelivr

---

## Daftar isi

1. [Fitur utama](#fitur-utama)
2. [Struktur halaman](#struktur-halaman)
3. [Struktur folder](#struktur-folder)
4. [Cara pakai di Scalev](#cara-pakai-di-scalev)
5. [Preview lokal](#preview-lokal)
6. [Aset dan CDN](#aset-dan-cdn)
7. [Responsif dan breakpoint](#responsif-dan-breakpoint)
8. [Tracking dan integrasi Scalev](#tracking-dan-integrasi-scalev)
9. [Cara mengubah konten](#cara-mengubah-konten)
10. [Catatan teknis](#catatan-teknis)

---

## Fitur utama

- **Satu file, nol dependensi build.** Hanya `landing-page-scalev.html`. Tidak ada npm, bundler, atau framework.
- **Mobile-first dan sudah diuji** pada lebar 360, 390, 412 (Galaxy A55 / iPhone), 768 (tablet), dan 1366 px (desktop).
- **4 varian aroma** dalam kartu kompak: Purpose Prestige, Peaceful Calm, Rebel Brave, Sweet Shy, lengkap dengan notes, sillage, longevity, dan karakter.
- **Dua tombol beli** dengan tinggi dan gaya seragam: *Lebih Murah Beli di Website* (checkout Scalev) dan *Beli di Shopee*.
- **Tracking klik CTA** otomatis lewat `window.Scalev.analytics` (Facebook, TikTok, Kwai) tanpa mengganggu halaman jika Scalev belum siap.
- **Aksesibilitas dasar:** `lang="id"`, `aria-label` pada section, dukungan `prefers-reduced-motion`.
- **SEO dasar:** `<title>` dan `<meta name="description">` sudah terisi.

---

## Struktur halaman

| Urutan | Section | `id` / anchor | Isi |
|---|---|---|---|
| 1 | Hero | `#top` | Logo EVOMI (PNG), tagline *Every Version of Me*, judul **FLASH SALE** dengan ikon petir, visual produk, dan marquee. |
| 2 | Features | — | 4 kartu keunggulan: EDP Long Lasting, Unisex, Aroma Premium, 4 Versi Aroma. Ikon PNG dari `assets/section 2`. |
| 3 | Celebration for Every Version of You | `#aroma` | 4 kartu aroma. Di HP tampil 2 kolom, botol di kiri, nama di kanan atas, notes 4 kolom, spesifikasi dalam panel 2×2. |
| 4 | Kapan & Di Mana | `#kapan` | 4 kartu kolase (Daily, Evening, Formal, Office, dll). Selalu 2 kolom, caption di tengah tiap foto menjauhi botol. |
| 5 | Testimoni | `#testimoni` | 4 ulasan, satu per varian aroma. 2 kolom di HP, 4 kolom di desktop. |
| 6 | Beli | `#beli` | Kartu harga *Lebih Murah Beli di Website* (Rp165RB/pcs, panah kanan) dan kartu *Beli di Shopee*. Tinggi kedua kartu disamakan via CSS grid. |

---

## Struktur folder

```
Parfum Evomi/
├─ landing-page-scalev.html                    ← file utama yang dipasang di Scalev
├─ landing-page-scalev-backup-2026-10-29.html  ← backup sebelum revisi besar
├─ landing-page-baru.html                      ← draft versi sebelumnya
├─ landing-page-lama-backup.html               ← versi lama (arsip)
├─ README.md
├─ .gitignore
└─ assets/                                     ← sumber gambar & font (di-mirror ke CDN)
   ├─ fonts/        Nohemi Regular / SemiBold / Bold (.otf)
   ├─ hero/         logo evomi.png, botol 2 ml, petir, truk, dsb.
   ├─ section 2/    ikon fitur: time, unisex, diamond, star (.png)
   ├─ notes/        gambar notes aroma (bergamot, vanilla, musk, …)
   ├─ scenes/       foto suasana (daily, evening, formal, office, …)
   ├─ reviews/      foto testimoni
   └─ bundling/     aset bundling (tidak lagi dipakai di halaman)
```

---

## Cara pakai di Scalev

1. Buka file `landing-page-scalev.html`, salin **seluruh isinya** (dari `<!doctype html>` sampai `</html>`).
2. Di dashboard Scalev, buat atau buka halaman custom HTML, lalu tempel kode tersebut.
3. Pastikan dua tautan CTA sudah benar:
   - Tombol website → `https://evomi-parfum.myscalev.com/checkout-flow-baru`
   - Tombol Shopee → `https://shopee.co.id/evomiindonesia#product_list`
4. Simpan, lalu cek pratinjau Scalev di mode mobile (390 px) dan desktop.

Tidak ada file lain yang perlu diunggah ke Scalev. Semua gambar dimuat dari CDN, dan aset kecil (logo hero, ikon fitur) sudah disematkan sebagai data URI di dalam HTML.

---

## Preview lokal

Jalankan server statis dari folder proyek, lalu buka di browser:

```bash
# Python 3
python -m http.server 8765
# buka http://localhost:8765/landing-page-scalev.html
```

Untuk screenshot cepat di berbagai lebar layar dengan Chrome headless (Windows):

```powershell
& "C:\Program Files\Google\Chrome\Application\chrome.exe" --headless=new --disable-gpu --hide-scrollbars `
  --virtual-time-budget=8000 --window-size=390,2400 `
  --screenshot="preview-390.png" "http://localhost:8765/landing-page-scalev.html"
```

Ganti `390` dengan `360`, `412`, `768`, atau `1366` sesuai kebutuhan.

---

## Aset dan CDN

Gambar dan font dimuat dari repo publik **`ramadhan42/parfum-rama-assets`** melalui jsDelivr dengan pola:

```
https://cdn.jsdelivr.net/gh/ramadhan42/parfum-rama-assets@main/assets/<folder>/<nama-file>
```

Folder yang dipakai: `fonts/`, `hero/`, `notes/`, `scenes/`, `reviews/`.

**Menambah atau mengganti gambar:**

1. Taruh file di folder `assets/` yang sesuai di repo ini **dan** di repo `parfum-rama-assets`.
2. Push ke branch `main` repo aset.
3. Jika file dengan nama sama diganti, bersihkan cache jsDelivr:
   `https://purge.jsdelivr.net/gh/ramadhan42/parfum-rama-assets@main/assets/<folder>/<nama-file>`

**Aset yang disematkan (data URI), bukan dari CDN:**

- `assets/hero/evomi.png` → logo di hero (100×34 px).
- `assets/section 2/*.png` → 4 ikon kartu fitur (±56 px).

Karena resolusinya kecil, keduanya tampak sedikit lembut di layar retina. Untuk hasil paling tajam, ekspor ulang sebagai SVG atau PNG ≥ 400 px lalu ganti data URI-nya.

---

## Responsif dan breakpoint

| Rentang | Perilaku utama |
|---|---|
| ≥ 1501 px | Skala hero maksimum (`--u` = 1 px). |
| ≥ 1180 px | Kartu aroma 2 kolom lebar di desktop. |
| ≥ 1024 px | Testimoni 4 kolom. |
| ≥ 900 px | Layout desktop untuk hero, aroma, dan scene. |
| 600–899 px | Mode tablet: botol aroma lebih besar, notes lebih rapat. |
| ≤ 899 px | Mode mobile: aroma dan scene 2 kolom, hero memakai unit `--u` berbasis lebar layar. |
| ≤ 639 px | Testimoni 2 kolom, kartu CTA satu baris (`Hanya Rp165RB /pcs` tidak pecah). |
| ≤ 599 px | Padding container 16 px. |
| ≤ 520 px | Ikon fitur 40 px. |
| ≤ 379 px | Penyesuaian HP kecil: font notes 6,7 px, panel aroma lebih pendek. |

Hero memakai variabel CSS `--u` (`min(1px, 100vw/1500)` di desktop, `min(1.1px, (100vw - 32px)/690)` di mobile) agar semua elemen hero menskala proporsional terhadap lebar layar.

---

## Tracking dan integrasi Scalev

Skrip di bagian bawah file bersifat **defensif**: jika `window.Scalev` tidak ada (misalnya saat preview lokal), halaman tetap berjalan normal.

- Saat halaman dimuat → event `ViewContent` dengan `content_name: "evomi-flash-sale"` dan `page_id` dari `Scalev.data.get()`.
- Saat CTA diklik → event `CTAClick` dengan nilai `data-cta`:
  - `harga-website` → kartu *Lebih Murah Beli di Website*
  - `beli-shopee` → kartu *Beli di Shopee*
- Event dikirim ke provider `facebook`, `tiktok`, dan `kwai` lewat `Scalev.analytics.track`.

Untuk menambah CTA baru yang ikut terlacak, cukup beri class `js-cta` dan atribut `data-cta="nama-event"` pada elemen tautannya.

---

## Cara mengubah konten

| Yang diubah | Lokasi di `landing-page-scalev.html` |
|---|---|
| Harga, label, teks tombol beli | `<section class="offer" id="beli">`, elemen `.price-card--web` dan `.price-card--shopee` |
| Link checkout / Shopee | atribut `href` pada dua `.price-card` di atas |
| Nama aroma, notes, sillage, longevity | `<section class="aroma" id="aroma">`, tiap `.aroma-card` |
| Caption scene (Daily, Evening, …) | `<section class="scenes" id="kapan">`, tiap `.collage` |
| Ulasan testimoni | `<section class="reviews" id="testimoni">`, tiap `.review` |
| Logo hero | `<a class="logo">` → ganti `src` data URI |
| Ikon fitur | `<img class="feature-icon">` → ganti `src` data URI |
| Judul dan deskripsi SEO | `<title>` dan `<meta name="description">` di `<head>` |

Membuat data URI dari PNG (Python):

```bash
python -c "import base64,sys;print('data:image/png;base64,'+base64.b64encode(open(sys.argv[1],'rb').read()).decode())" "assets/hero/evomi.png"
```

---

## Catatan teknis

- **Font:** Nohemi (Regular, SemiBold, Bold) via `@font-face` dari CDN untuk judul dan body; DM Sans dari Google Fonts khusus kartu testimoni, sesuai desain Figma.
- **Equal-height CTA:** `.offer .container` memakai `display: grid; grid-auto-rows: 1fr`, tiap `.price-card` adalah flex column dengan `.body { flex: 1 }`, sehingga kartu Shopee selalu setinggi kartu website.
- **Bundling Buy 1 Get 1** sudah dihapus dari halaman. Aset di `assets/bundling/` dibiarkan untuk arsip.
- **File backup** (`*-backup-*.html`, `landing-page-lama-backup.html`) hanya arsip lokal dan tidak dipakai di produksi.
- Folder `evomi.shop - dns records - cloudflare/` berisi ekspor DNS domain dan **tidak terkait** dengan landing page ini; sebaiknya tidak ikut dipublikasikan.

---

## Lisensi

Hak cipta © EVOMI. Kode dan aset di repo ini digunakan untuk kebutuhan internal brand EVOMI.

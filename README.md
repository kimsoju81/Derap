# Derap — Navigasi Jalan Raya Pintar Malaysia

**Derap** ialah aplikasi web progresif (PWA) navigasi jalan raya pintar yang direka khusus untuk pemanduan di Malaysia dengan paparan peta moden, panduan lorong berketepatan tinggi, kawalan bulatan pintar, carian POI masa nyata, serta sokongan peta luar talian automatik.

---

## Ciri Utama Navigasi

### 1. Enjin Peta Pelbagai Sumber & Kesegaran Data Automatik
- **3 Pilihan Peta Kolaj**:
  - **OpenFreeMap** (Vektor moden & ringan)
  - **Peta Satelit** (Imej satelit resolusi tinggi)
  - **GrabMaps** (Laluan bandar & komersial Malaysia)
- **Auto-Sync & Cache-Busting Pintar**: Versi data peta diselaraskan secara automatik mengikut minggu/bulan semasa (`YYYY-MM-WW`) setiap kali aplikasi dilancarkan tanpa membebankan CPU atau memanaskan telefon.
- **Kemas Kini Peta Terkini**: Butang pembersihan cache jubin & carian lama beserta penunjuk status kesegaran data secara langsung.

### 2. Panduan Lorong (Lane Guidance) & Kawalan Bulatan Pintar
- **Peka Simpang & Susur Keluar Bertingkat (Flyover / Ramp)**: Mengesan laluan utama, susur keluar turun taraf (jalan kampung) dan susur masuk naik taraf (jalan persekutuan/lebuh raya) tanpa melangkau simpang kritikal.
- **Paparan Lorong Sebenar**: Menunjukkan bilangan lorong sebenar (termasuk jalan 4 lorong) serta lorong tepat yang perlu diikuti.
- **Kawalan Keluar Bulatan (1 hingga 6 Susur Keluar)**: Mengira semua jenis susur keluar termasuk jalan kecil dan pusingan-U, serta **menahan arahan baharu sehingga pemandu keluar sepenuhnya daripada bulatan, simpang, atau laluan bergabung (merge road)**.
- **Pengiraan Semula Pusingan-U Waktu Puncak**: Pada waktu puncak, sistem mencari pusingan-U yang dibenarkan secara sah atau melalui simpang tiga/empat di hadapan apabila laluan dikira semula.

### 3. Carian POI Masa Nyata & Susun Atur Skrin Pintar
- **Carian Selari Overpass API (Radius 25km)**: Menarik data terus daripada pangkalan data langsung OpenStreetMap supaya kedai, warung, stesen petrol, dan jalan baharu terus ditemui.
- **Susun Atur Carian Hentian**:
  - Apabila butang **Tambah Hentian (`+`)** dibuka:
    1. Barisan 1: **Lokasi anda**
    2. Barisan 2: **Ke mana?**
    3. Barisan 3: **Tambah hentian**
  - Butang tukar atas-bawah (`⇅`) di bawah butang `+` menukar kedudukan antara **Lokasi anda** dan **Tambah hentian** secara langsung.
- **Susun Atur Lanskap Pintar**: Panel kawalan bergerak ke sebelah kiri dan kedudukan pemandu dipusatkan pada separuh bahagian kanan skrin untuk penglihatan jalan hadapan yang lebih luas.

### 4. Peta Luar Talian Automatik (Seamless Auto Offline) & Penjimatan Haba
- Jubin peta dan data laluan di-cache secara automatik semasa penggunaan biasa untuk peralihan lancar apabila isyarat internet lemah.
- Pengoptimuman kadar bingkai GPS, pengurangan panggilan latar belakang, dan penjimatan bateri bagi mengelakkan telefon menjadi panas semasa navigasi panjang.

---

## Keupayaan Progressive Web App (PWA)

Derap dibina sebagai PWA lengkap melalui `/public/manifest.json` dan `/public/sw.js`:

| Keupayaan | Konfigurasi / API | Fungsi dalam Derap |
| :--- | :--- | :--- |
| **Pemasangan Aplikasi** | `manifest.json`, `usePWAInstall`, `PWAInstallButton` | Pemasangan terus ke skrin utama Android, Desktop, dan panduan iOS Safari. |
| **Tangkapan Skrin (Screenshots)** | `screenshots` (`wide` & `narrow`) | Memaparkan pratonton antara muka Derap pada dialog pemasangan PWA. |
| **Pelanjutan Skop (Scope Extensions)** | `scope_extensions` | Memastikan navigasi domain peta (`openfreemap.org`, `openstreetmap.org`, `overpass-api.de`) kekal lancar. |
| **Aplikasi Berkaitan** | `related_applications` | Menghubungkan identiti web app dan rujukan aplikasi natif berkaitan. |
| **Penarafan Umur IARC** | `iarc_rating_id` | Kod pensijilan International Age Rating Coalition (IARC) untuk kesesuaian semua peringkat umur. |
| **Pengendali Fail (File Handlers)** | `file_handlers` | Membuka fail laluan `.gpx`, `.kml`, dan `.geojson` terus dengan Derap. |
| **Pengendali Pelancaran** | `launch_handler` (`focus-existing`) | Mengelakkan tetingkap berganda dengan memfokuskan sesi Derap sedia ada. |
| **Pengendali Protokol** | `protocol_handlers` (`geo:`, `web+derap:`) | Membuka koordinat `geo:lat,lon` dan pautan khas `web+derap:` terus ke peta Derap. |
| **Sasaran Kongsi (Share Target)** | `share_target` | Menerima lokasi atau pautan peta yang dikongsi daripada aplikasi lain. |
| **Mod Bertab (Tabbed Mode)** | `display_override: ["tabbed", ...]` & `tab_strip` | Menyokong berbilang tab laluan dalam satu tetingkap PWA pada desktop. |
| **Panel Sisi Edge** | `edge_side_panel` | Menyokong pembukaan Derap pada panel sisi pelayar Microsoft Edge (`420px`). |
| **Ambil Nota (Note Taking)** | `note_taking` | Laluan pantas mencipta nota perjalanan/lokasi baharu (`/?action=new-note`). |
| **Widget Sistem Operasi** | `widgets` + Adaptive Cards (`/public/widgets/`) | Memaparkan status navigasi dan akses pantas **Ke Mana?** terus pada papan pemuka OS. |
| **Segerak Latar Belakang** | Background Sync API (`sync`) | Menyegerakkan data tertunda secara automatik sebaik sahaja sambungan internet pulih. |
| **Segerak Berkala** | Periodic Background Sync API (`periodicsync`) | Menyemak kesegaran versi peta dan mengemas kini widget secara berkala di latar belakang. |
| **Notifikasi Tolak Web** | Web Push API (`push` & `notificationclick`) | Memaparkan amaran trafik atau kemas kini laluan walaupun aplikasi sedang ditutup. |

---

## Struktur Projek Ringkas

- `public/manifest.json` — Konfigurasi lengkap Web App Manifest PWA
- `public/sw.js` — Service Worker (Offline Cache, Background Sync, Periodic Sync, Web Push, Widgets)
- `public/widgets/` — Templat & data Adaptive Card bagi PWA Widget
- `public/screenshots/` — Tangkapan skrin rasmi (`wide` 1280×720 & `narrow` 720×1280)
- `src/App.tsx` — Orkestrasi peta utama, navigasi, menu Derap, dan pengendalian intent PWA
- `src/components/RouteInfoSearchLayer.tsx` — Panel carian *Ke Mana?*, susunan 3 baris hentian, dan carian POI
- `src/components/PWAInstallButton.tsx` & `src/hooks/usePWAInstall.ts` — Antara muka pemasangan PWA dalam aplikasi
- `src/utils/pwaManager.ts` — Pengurus pendaftaran Service Worker, Sync, Push, Share Target, dan Protocol/File Handlers

---

## Menjalankan Projek Secara Tempatan

```bash
# 1. Pasang pakej bergantung
npm install

# 2. Jalankan pelayan pembangunan (port 3000)
npm run dev

# 3. Bina versi produksi
npm run build
```

## Lesen

Hak Cipta Terpelihara © Derap Navigasi Malaysia.

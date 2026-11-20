# Derap — Aplikasi Navigasi Jalan Raya Malaysia (OpenStreetMap)

**Derap** ialah aplikasi web navigasi jalan raya pintar untuk kegunaan di Malaysia yang dibina menggunakan **React, TypeScript, Vite, Leaflet, OpenStreetMap, Nominatim, dan OSRM**. Aplikasi ini tidak menggunakan sebarang SDK atau API proprietari Google Maps.

## 1. Aliran Skrin & Reka Bentuk Utama

1. **Layer Menu Utama Derap (Muncul Paling Hadapan Sebaik Dilancarkan)**:
   - Memaparkan identiti jenama **Derap** berinspirasikan motif batik/songket Malaysia dengan dua pilihan utama bersaiz besar: **Ke Mana?** (carian laluan) dan **Lihat Peta** (terus ke peta penuh).
   - Dilengkapi bar bawah untuk **Telefon** (talian kecemasan & bantuan lebuhraya Malaysia), **Bunyi** (kawalan suara arahan Bahasa Melayu), dan **Peralatan** (status koordinat GPS & pengurusan data tempatan).
2. **Layer Carian "Route Info" (Selepas Butang "Ke Mana?" Ditekan)**:
   - Panel carian lama dimansuhkan dan digantikan sepenuhnya dengan skrin **Route Info** yang menyokong input **Your location (Lokasi Mula)**, **Perhentian (A)**, dan **Choose destination (Destinasi)** berserta ringkasan masa dan jarak (`Total trip: X min (Y km)`) dan butang **Done**.
   - Senarai lokasi di bawah memaparkan bulatan ikon pin dengan jarak dalam `km` di bawah setiap bulatan, carian tempat masa nyata Nominatim, serta bar bawah **Choose on map (`Map`)** untuk memilih titik secara terus di atas peta.
2. **Mod Navigasi Aktif (Gaya Garmin Maps)**:
   - Apabila pengguna menekan **MULA NAVIGASI**, antara muka bertukar kepada paparan pemanduan ala **Garmin Drive**:
     - **Papan Tanda Lebuhraya Hijau di Atas**: Memaparkan ikon anak panah belokan besar, jarak ke simpang seterusnya, nama jalan/lebuhraya dalam Bahasa Melayu, serta jalur **"Kemudian:"** untuk belokan berikutnya.
     - **Bar Kokpit Telemetri di Bawah**: Memaparkan kelajuan semasa (`km/j` daripada GPS), baki jarak, baki masa, waktu ketibaan (ETA), kawalan suara arahan (Web Speech API), mod **Simulasi**, dan butang **HENTIKAN**.
3. **Mod Laporan Keadaan Jalan (Gaya Waze)**:
   - Butang laporan kuning/jingga membuka laci kategori laporan berinspirasikan Waze (*Trafik Sesak, Polis & Penguatkuasa, Kemalangan, Bahaya Atas Jalan, Cuaca & Banjir*).
   - **Ketelusan Data**: Aplikasi ini **tidak mereka-reka data trafik masa nyata atau laporan palsu**. Ia memaparkan notis jelas bahawa pelayan komuniti pusat dan suapan trafik langsung belum disambungkan; sebarang pin laporan yang ditandakan hanya disimpan secara tempatan di dalam `localStorage` pelayar pengguna.

---

## 2. Pemasangan dan Cara Menjalankan Aplikasi

```bash
# 1. Pasang semua kebergantungan
npm install

# 2. Jalankan pelayan pembangunan (Vite)
npm run dev

# 3. Bina untuk produksi
npm run build
```

---

## 3. Polisi Penggunaan API Awam & Had Perkhidmatan

Aplikasi ini menggunakan servis komuniti terbuka bagi tujuan prototaip dan pembangunan:

- **Jubin Peta OpenStreetMap (`https://tile.openstreetmap.org/{z}/{x}/{y}.png`)**:
  - Tertakluk kepada [OpenStreetMap Tile Usage Policy](https://operations.osmfoundation.org/policies/tiles/).
  - Atribusi `© OpenStreetMap contributors` dipaparkan secara jelas dengan pautan rasmi. Jangan memuat turun jubin secara pukal untuk kegunaan luar talian menggunakan pelayan jubin awam ini.
- **Carian Geokod Nominatim (`https://nominatim.openstreetmap.org`)**:
  - Tertakluk kepada [Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/).
  - Kod dalam `src/services/geocoding.ts` menggunakan *debounce* (850ms), pembatalan permintaan (`AbortController`), dan simpanan sementara dalam memori (*in-memory cache*) bagi mengelakkan permintaan pada setiap aksara.
- **Pengiraan Laluan OSRM (`https://router.project-osrm.org`)**:
  - Pelayan demo awam OSRM sesuai untuk ujian dan prototaip tetapi tidak menjamin ketersediaan SLA produksi.

---

## 4. Cara Menukar Penyedia Routing & Peta Pada Masa Hadapan

1. **Menukar Penyedia Routing**:
   - Buka `src/services/routing.ts` dan ubah pemalar `OSRM_BASE_URL` kepada URL pelayan OSRM peribadi anda, Valhalla, GraphHopper, atau OpenRouteService.
2. **Menukar Pelayan Jubin Peta**:
   - Buka `src/components/MapView.tsx` dan kemas kini prop `url` pada komponen `<TileLayer />` kepada pelayan jubin komersial atau hos sendiri sekiranya aplikasi digunakan secara berskala besar.
3. **Menyambungkan Backend Trafik & Laporan Komuniti**:
   - Sambungkan fungsi `handleAddLocalReport` dalam `src/App.tsx` kepada pangkalan data masa nyata (seperti Firebase Firestore atau PostgreSQL/WebSocket) untuk berkongsi laporan pengguna merentas peranti.w

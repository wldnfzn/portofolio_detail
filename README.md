# SWORD: Service Workflow & Operational Resource Dashboard

**Sistem Informasi Manajemen Servis, Inspeksi Armada, & Logistik Suku Cadang Terpadu (Web & Mobile Android)**  
**Studi Kasus:** Operasional Pemeliharaan Armada Forklift & Baterai Traksi (PT United Multilift Perkasa)

---

## 1. Tentang Proyek

**SWORD** adalah platform operasional terintegrasi berbasis Web dan Mobile Android yang dirancang untuk mendigitalisasi seluruh alur pemeliharaan armada alat berat (forklift dan baterai traksi). Sistem ini menghubungkan tim sales, pemimpin divisi servis (*Customer Care Leader*), staf gudang (*Technical & Inventory*), tim manajemen eksekutif, serta mekanik lapangan ke dalam satu alur kerja yang terpantau secara langsung.

Sebelum sistem ini dibangun, pelaporan inspeksi di lapangan, penjadwalan teknisi, permintaan suku cadang, dan pencatatan stok gudang berjalan secara terpisah menggunakan formulir manual. SWORD menggantikan proses tersebut dengan formulir inspeksi digital berbasis QR Code, perhitungan skor kesehatan unit otomatis, persetujuan berjenjang, serta sinkronisasi stok gudang secara otomatis.

---

## 2. Alur Kerja Sistem (*End-to-End Flow*)

```mermaid
flowchart LR
    A["1. Permintaan & Jadwal\nSales buat Tiket Order\natau CCL buat Jadwal Rutin"] --> B["2. Penugasan Tim\nCCL tugaskan Regu Mekanik\n(Notifikasi Push ke HP)"]
    B --> C["3. Inspeksi Lapangan\nMekanik scan QR Code unit,\ncek riwayat terakhir, isi checklist"]
    C --> D["4. Laporan & Rekomendasi\nSkor kesehatan unit dihitung\n& Service Report PDF terbuat"]
    D --> E{"Ada Pengajuan\nSparepart?"}
    E -->|Ya| F["5. Approval CCL & Gudang\nCCL verifikasi -> Gudang siapkan\n& terbitkan PIN 4-digit"]
    F --> G["6. Serah Terima & Stok\nMekanik input PIN 4-digit\nStok gudang terpotong otomatis"]
    E -->|Tidak| H["7. Selesai & Analitik\nDashboard KPI & Audit Log\nterbarui secara langsung"]
    G --> H
```

### Ringkasan Alur Operasional

1. **Inisiasi Pekerjaan:** Pekerjaan dapat berasal dari keluhan pelanggan yang dibuat tim Sales (*Tiket Order*), jadwal pemeliharaan rutin dari *Customer Care Leader* (CCL), maupun inspeksi mendadak/tambahan di lapangan.
2. **Penugasan Berbasis Tim:** CCL menugaskan regu mekanik (Leader dan anggota) untuk menangani unit tertentu. Seluruh anggota tim langsung menerima notifikasi push pada aplikasi Android mereka.
3. **Inspeksi Mobile Berbasis QR Code:** Di lokasi pelanggan, mekanik memindai QR Code pada unit forklift atau baterai, meninjau riwayat *Service Report* terakhir, lalu mengisi formulir inspeksi digital (dilengkapi foto bukti kerusakan, koordinat lokasi GPS, dan *autosave draft* lokal maupun server).
4. **Penilaian Kesehatan Unit & Laporan Standar:** Sistem menghitung persentase kesehatan unit berdasarkan bobot skor item pemeriksaan dan menandai statusnya (`Healthy`, `Attention`, atau `Critical`), lalu menghasilkan dokumen *Service Report* standar A4 siap cetak/ekspor PDF.
5. **Pengadaan Suku Cadang & Verifikasi PIN Gudang:** Rekomendasi maupun pemakaian suku cadang dari mekanik melewati verifikasi CCL terlebih dahulu sebelum diproses tim gudang. Saat barang siap diambil, gudang menerbitkan PIN 4 digit yang wajib dimasukkan mekanik pada aplikasi saat serah terima, sekaligus memotong stok katalog gudang secara otomatis.
6. **Pengawasan Eksekutif:** Direktur dan General Manager memantau KPI armada, ketersediaan tim mekanik, peringatan temuan kritis, menyetujui permohonan pembatalan/revisi tiket, dan meninjau *Audit Log* dari Dashboard Web.

---

## 3. Fitur Utama

### A. Portal Web Manajemen (7 Peran Pengguna / RBAC)
* **Dashboard Eksekutif:** Ringkasan KPI armada, grafik tren inspeksi dan kesehatan unit, komposisi sumber tugas, status kesiapan tim mekanik, serta daftar peringatan temuan kritis (*Critical Alerts*).
* **Manajemen Pelanggan, Aset, & QR Code:** Pengelolaan data pelanggan serta unit Forklift dan Baterai, lengkap dengan fitur impor/ekspor Excel massal dan generator cetak label QR Code.
* **Tiket Order & Persetujuan Pembatalan GM:** Pengelolaan keluhan pelanggan dan inspeksi mendadak dengan alur persetujuan General Manager apabila ada pengajuan revisi ke *draft* atau pembatalan permanen.
* **Manajemen Tim & Penjadwalan Inspeksi:** Pengaturan komposisi regu mekanik, pemantauan beban kerja tim, serta penjadwalan rutin satuan maupun massal via template Excel.
* **Pengadaan Sparepart & Inventaris Gudang:** Alur persetujuan berjenjang (`Mekanik -> CCL -> Gudang`), pembuatan PIN serah terima 4 digit, pemotongan dan pengembalian stok otomatis yang tercatat di log mutasi gudang, serta pemantauan stok menipis/habis.
* **Laporan Service & Cetak PDF A4:** Tampilan rekap seluruh laporan inspeksi dengan template cetak A4 standar perusahaan dan ekspor Excel.
* **Pengaturan Template & Audit Log:** Kustomisasi kategori dan item *checklist* inspeksi secara dinamis serta pencatatan rekam jejak aktivitas seluruh pengguna.

### B. Aplikasi Mobile Android Mekanik
* **Pemindai QR Code Unit & Input Manual:** Akses cepat identitas unit dan *Service Report* inspeksi terakhir langsung setelah memindai QR Code di lapangan.
* **Formulir Inspeksi Digital & Diagnostik Baterai:** Pengisian *checklist* forklift (skala 1 sampai 3 dengan unggah foto temuan) serta formulir servis baterai 40 sel.
* **Autosave Draft Dua Lapis:** Penyimpanan draf otomatis di perangkat (*local storage*) dan server untuk mencegah kehilangan data saat sinyal lapangan tidak stabil.
* **Riwayat Inspeksi & Ekspor PDF:** Akses dokumen laporan yang telah diselesaikan langsung dari ponsel untuk dibagikan dalam format PDF.
* **Notifikasi Push Real-Time & Pembaruan OTA:** Pemberitahuan instan tugas baru dan status suku cadang, serta dukungan pembaruan aplikasi *Over-The-Air* tanpa instalasi ulang APK.

---

## 4. Tech Stack

| Lapisan | Teknologi yang Digunakan |
| :--- | :--- |
| **Web Frontend** | React 19, TypeScript, Vite, Tailwind CSS, React Router v7, Recharts, QRCode.react, Axios |
| **Mobile App (Android)** | React Native, Expo SDK 57, React Navigation, Expo Camera, Location, Notifications (FCM), Print & Sharing, AsyncStorage, Expo Updates (OTA) |
| **Backend API** | Node.js, TypeScript, Hono, `@hono/node-server`, ExcelJS, `web-push` (VAPID) |
| **Database** | PostgreSQL (relational schema + JSONB, transaction-safe row locking) |
| **Autentikasi & Keamanan** | JWT (HS256), Rolling Refresh Token Session (90 hari), `bcryptjs`, RBAC 7 peran, *Anti-Double-Submit* middleware, HMAC signed media URLs |
| **Shared Package** | Monorepo npm workspaces (`@digital-inspect/shared`) untuk berbagi tipe data dan kalkulator skor kesehatan |
| **CI/CD & Infrastruktur** | GitHub Actions (otomatisasi build Android Release APK via Gradle), Nginx reverse proxy, Docker Compose (PostgreSQL dev), Self-hosted Expo OTA |

---

## 5. Cuplikan Antarmuka Sistem (*Screenshots*)

### A. Portal Web Manajemen (`apps/web`)

#### 1. Beranda Publik, Login, & Profil Pengguna
![Landing Page](screenshots/01-web-landing-page.png)
*Beranda publik portal web dengan tombol masuk portal dan unduhan APK Android.*

![Halaman Login](screenshots/02-web-login-page.png)
*Halaman login autentikasi akun perusahaan.*

![Profil Saya](screenshots/23-web-profile.png)
*Pengaturan profil akun, unggah foto profil, dan ubah kata sandi.*

#### 2. Dashboard Eksekutif & Notifikasi Real-Time
![Dashboard Utama](screenshots/03-web-dashboard-top.png)
*Ringkasan armada, jumlah inspeksi selesai, komposisi sumber pekerjaan, dan kontrol operasional.*

![Dashboard Tabel & Grafik](screenshots/04-web-dashboard-kpi-charts.png)
*Tabel operasional tiket, sparepart, dan grafik aktivitas inspeksi serta status kesehatan aset.*

![Dashboard Alerts & Tim](screenshots/05-web-dashboard-alerts-teams.png)
*Panel Active Alerts dan status ketersediaan tim mekanik secara langsung.*

![Dropdown Notifikasi](screenshots/06-web-notifications-dropdown.png)
*Panel notifikasi real-time pada bilah atas lengkap dengan kontrol suara dan tautan langsung ke modul.*

#### 3. Tiket Order, Pengadaan Sparepart, & Inventaris Gudang
![Tiket Order](screenshots/07-web-tickets.png)
*Pengelolaan Tiket Order keluhan service dan inspeksi dadakan.*

![Pengadaan Sparepart](screenshots/08-web-spareparts.png)
*Alur persetujuan sparepart (Approval CCL hingga Validasi PIN Gudang 4-digit).*

![Inventaris Gudang](screenshots/09-web-inventory.png)
*Katalog inventaris suku cadang, status stok aman/menipis/habis, serta lokasi rak gudang.*

![Log Pergerakan Stok](screenshots/10-web-inventory-stock-log-modal.png)
*Riwayat mutasi stok otomatis (keluar saat serah terima/tiket selesai dan masuk kembali saat pembatalan).*

#### 4. Pelanggan, Aset (Forklift & Baterai), & QR Code
![Manajemen Pelanggan](screenshots/11-web-customers.png)
*Data pelanggan beserta fitur template dan impor massal Excel.*

![Aset Forklift](screenshots/12-web-assets-forklifts.png)
*Daftar armada forklift lengkap dengan Serial Number, pelanggan, dan skor kesehatan.*

![Aset Baterai](screenshots/13-web-assets-batteries.png)
*Tab manajemen unit baterai traksi.*

![Manajemen QR Code](screenshots/17-web-qr-codes.png)
*Generator dan pratinjau cetak label QR Code untuk ditempel pada setiap unit aset.*

#### 5. Tim Mekanik, Penjadwalan, Laporan, Audit, & Pengaturan
![Manajemen Tim & Penjadwalan](screenshots/14-web-inspections-teams-schedule.png)
*Pengelolaan komposisi tim mekanik serta penjadwalan inspeksi satuan maupun Excel.*

![Laporan Inspeksi](screenshots/15-web-reports.png)
*Rekap laporan hasil inspeksi lengkap dengan ekspor Excel dan bilah gulir atas.*

![Detail Laporan Forklift](screenshots/16-web-report-detail-forklift.png)
*Rincian Service Report Forklift lengkap dengan metadata tim, koordinat GPS, skor kesehatan, dan cetak PDF A4.*

![Manajemen Pengguna](screenshots/18-web-users.png)
*Pengelolaan akun pengguna dan pembagian peran akses (RBAC).*

![Audit Log Sistem](screenshots/19-web-audit-log.png)
*Catatan rekam jejak seluruh aktivitas pengguna beserta ekspor CSV.*

![Template Checklist Forklift](screenshots/20-web-settings-forklift-template.png)
*Pengaturan dinamis kategori dan item pemeriksaan checklist Forklift.*

![Template Battery Service Report](screenshots/21-web-settings-battery-template.png)
*Pratinjau standar formulir Battery Service Report.*

![Konfigurasi Skor Kesehatan](screenshots/22-web-settings-scoring-config.png)
*Pengaturan ambang batas kesehatan unit (`Healthy`, `Attention`, `Critical`) dan rumus kalkulasi.*

---

### B. Aplikasi Mobile Android Mekanik (`apps/app`)

![Mobile Login](screenshots/24-mobile-login.png)
*Layar login aplikasi mobile mekanik.*

![Mobile Home](screenshots/25-mobile-home.png)
*Beranda mekanik dengan tombol Scan QR Code Unit, ringkasan tugas harian, dan daftar jadwal aktif.*

![Mobile Home Tugas Selesai](screenshots/26-mobile-home-selesai.png)
*Daftar tugas inspeksi yang telah diselesaikan pada tab Selesai.*

![Mobile Input Kode Aset](screenshots/27-mobile-input-kode-aset-modal.png)
*Modal input kode aset manual sebagai alternatif apabila QR fisik sulit dipindai kamera.*

![Mobile Notifikasi](screenshots/28-mobile-notifications-modal.png)
*Panel notifikasi operasional pada aplikasi mobile.*

![Mobile Scan QR](screenshots/29-mobile-scan-qr.png)
*Layar pemindai QR Code kamera.*

![Mobile Detail Aset](screenshots/33-mobile-asset-detail.png)
*Layar Detail Aset setelah pencarian/pemindaian unit.*

![Mobile Riwayat](screenshots/30-mobile-riwayat.png)
*Riwayat dokumen inspeksi mekanik dengan filter tipe unit dan rentang waktu.*

![Mobile Detail Laporan](screenshots/31-mobile-report-detail.png)
*Detail laporan Service Report pada perangkat mobile lengkap dengan fitur Export PDF.*

![Mobile Profil](screenshots/32-mobile-profil.png)
*Layar profil akun mekanik untuk ubah nama, kata sandi, dan keluar dari sesi.*

---

> **Catatan Portofolio:** Untuk dokumentasi teknis mendalam (skema 23 tabel basis data, daftar lengkap endpoint API, dan rincian validasi), lihat [Deskripsi-Sistem.md](Deskripsi-Sistem.md). Apabila portofolio ini akan dipublikasikan secara terbuka di luar tim internal, pertimbangkan untuk menyensor nama perusahaan pelanggan dan nomor seri unit yang tampak pada sebagian *screenshot*.

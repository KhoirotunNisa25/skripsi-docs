# Catatan Perubahan (*Change Log*)

## Log Perubahan Dokumen Riset

### 2026-11-01 (Sesi 21)
- **Perubahan**:
  - **Penyelesaian Unduhan Dataset Kontinu 1 Minggu (165 Video @ 10 Menit, ~74 GB)**:
    - Seluruh berkas video rekaman 24 jam kontinu selama 7 hari (24–31 Oktober 2026) berhasil diunduh 100% tanpa kegagalan (165/165 file) ke penyimpanan lokal laptop pada pukul 05:27 WIB.
  - **Restrukturisasi Arsitektur Proyek Menjadi Dua Repositori Terpisah**:
    - **Pemisahan Repositori Naskah & Riset (`skripsi-docs`)**:
      - Mengarahkan *remote* origin ke `git@github.com:KhoirotunNisa25/skripsi-docs.git`.
      - Merapikan struktur ruang kerja: memindahkan CSV pencarian dan PDF literatur ke `articles/searches/`, memindahkan berkas observasi awal 3 hari ke `research/observasi_awal/`, serta membersihkan file temporer di direktori *root*.
      - Memperbarui dokumentasi `README.md` dengan penegasan peran repositori sebagai *source of truth* akademik dan naskah LaTeX Polinema.
    - **Inisialisasi & Setup Repositori Source Code & Engine (`skripsi-engine`)**:
      - Menginisialisasi repositori Git baru di `https://github.com/KhoirotunNisa25/skripsi-engine.git`.
      - Membangun struktur modular: `configs/`, `src/core/` (MotionDetector MOG2 & baseline), `src/dataset/` (ManifestLoader), `src/extraction/` (VideoEventExtractor), `src/edge/` (server Flask `app.py` & web UI Raspberry Pi 5), `scripts/` (`run_batch_extraction.py`, `run_single_extraction.py`, `generate_visualizations.py`, `deploy_to_raspi.sh`), dan `results/` (`events/`, `summary/`, `figures/`, `montages/`).
      - Memverifikasi keberhasilan pipeline ekstraksi otomatis: uji coba batch pada video sesi `2026-10-24_120014` berhasil mendeteksi 5 event riak lele dan langsung mengekspor CSV Log Event, Rekap Sesi, serta montase visual frame.
- **Klasifikasi Perubahan**: *Major* (Restrukturisasi arsitektur repositori, pemisahan kode dan naskah, serta verifikasi operasional pipeline ekstraksi video).
- **Status**: Selesai (*Completed*)

---

### 2026-10-31 (Sesi 20)
- **Perubahan**:
  - **Penegasan Domain Siklus Pakan Eksisting Peternak (07.00 & 19.00 WIB) & Rasional Pemrosesan Kontinu 24 Jam**:
    - Mengklarifikasi bahwa jadwal pemberian pakan default oleh peternak kolam (*baseline operasional*) adalah 2 kali sehari: pukul **07.00 WIB (pagi)** dan **19.00 WIB (malam)**.
    - Menetapkan rasional ilmiah bahwa sistem tidak dapat berasumsi lele hanya lapar pada jam default tersebut. Sistem pakan adaptif (*smart feeder*) berbasis *computer vision* harus mampu mendeteksi nafsu makan aktual (*real feeding demand*) yang dapat bergeser akibat dinamika suhu, cuaca, atau kondisi air.
    - Menetapkan keputusan metodologis untuk memproses dan menganalisis **seluruh data video rekaman kontinu 24 jam selama 1 minggu (165 berkas video @ 10 menit)** guna memetakan profil fluktuasi derau aerator, dinamika riak lele di luar jam makan, serta korelasi telemetri sensor kualitas air secara menyeluruh.
  - **Re-inisialisasi Background Downloader Dataset (Low-Memory Serial Worker)**:
    - Menangani insiden penghentian paksa oleh kernel Linux (*systemd-oomd*) dengan merestrukturisasi eksekusi downloader menjadi mode serial tunggal (*1 worker*, konsumsi RAM ~45 MB) agar proses unduh 165 video (~107 GB) berjalan stabil di latar belakang tanpa memicu *memory exhaustion*.
- **Klasifikasi Perubahan**: *Major* (Penegasan batasan logika domain biologis lele, kebutuhan analisis dataset 24 jam penuh, dan optimasi arsitektur data ingestion).
- **Status**: Selesai (*Completed*)

---

### 2026-10-26 (Sesi 19)
- **Perubahan**:
  - **Implementasi Fitur Thermal Cooldown, Power Control (Reboot/Shutdown), & Optimasi CPU Kamera**:
    - Menambahkan tombol **Mode Cooldown** pada antarmuka web [`scratch/index.html`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/scratch/index.html) dan endpoint API `/api/system/cooldown` di [`scratch/app.py`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/scratch/app.py) untuk mengistirahatkan prosesor dan sensor kamera saat suhu Raspberry Pi 5 melonjak tinggi (>70°C).
    - Menambahkan tombol kontrol daya **Reboot** (`/api/system/reboot`) dan **Matikan / Shutdown** (`/api/system/shutdown`) dengan modal peringatan konfirmasi aman.
    - Menambahkan overlay *Standby Cooldown* interaktif pada kartu video dengan pemantauan temperatur waktu nyata (*real-time*).
    - Mengoptimalkan *capture loop* kamera secara pasif: encoding JPEG preview hanya aktif saat ada klien web yang melihat aliran video (menghemat penggunaan CPU dari 25% menjadi ~1% saat idle).
    - Menyinkronkan dan memverifikasi perubahan langsung pada unit Raspberry Pi 5 (`100.126.141.31`). Suhu CPU berhasil diturunkan dari 76,0°C ke 68,8°C dan terus menurun.
- **Klasifikasi Perubahan**: *Minor* (Fitur manajemen termal, kestabilan perangkat keras edge node, dan optimasi siklus daya).
- **Status**: Selesai (*Completed*)

---

### 2026-10-26 (Sesi 18)
- **Perubahan**:
  - **Penyesuaian Timeout Unggah Google Drive & Sinkronisasi Ulang Rekaman Siang Hari**:
    - Menaikkan batas waktu *timeout* `rclone` pada [`scratch/app.py`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/scratch/app.py#L786) dan `/home/raspi5/Nisa/app.py` dari 60 menit (`3600s`) menjadi **120 menit (`7200s`)** guna mengakomodasi proses transfer video mentah tanpa kompresi (~550–630 MB) melalui jaringan modem seluler 4G kolam saat jam sibuk.
    - Memicu antrean unggah ulang via API `/api/sync_pending` untuk berkas tertunda jam 13.00 (`lele_20261026_130004.mp4` - 560,1 MB) dan jam 14.00 (`lele_20261026_140004.mp4` - 548,88 MB).
- **Klasifikasi Perubahan**: *Minor* (Konfigurasi kestabilan pipeline data capture & cloud storage di edge node Raspberry Pi 5).
- **Status**: Selesai (*Completed*)

---

### 2026-10-26 (Sesi 17)
- **Perubahan**:
  - **Perancangan Detail Metodologi Komparasi Ilmiah: Computer Vision Konvensional vs. Lightweight Deep Learning**:
    - Merumuskan rancangan studi komparasi *head-to-head* antara metode konvensional (*Adaptive Three-Frame Differencing* + *Welford Running Gaussian* + HSV *S-channel*) melawan model *Lightweight Deep Learning* untuk membuktikan metode mana yang paling efektif dan efisien mendeteksi nafsu makan bibit lele pada perangkat *edge* Raspberry Pi 5.
    - Menetapkan 2 sub-arsitektur Deep Learning utama:
      1. **YOLOv8-nano Murni**: Deteksi *bounding box* riak/cipratan makan (`ripple_splash`) per-frame (rujukan: Qian et al., 2025; Vijayalakshmi, 2025).
      2. **Hibrida Spatio-Temporal YOLOv8n + LSTM**: YOLOv8n mengekstrak 5 vektor fitur spasial per-frame ($N_{\text{splash}}$, luas rata-rata, varians luas, confidence, dispersi spasial) yang kemudian dirangkum oleh jaringan Bi-LSTM 2 layer sepanjang jendela 10-frame (1 detik) menjadi probabilitas 3 kelas nafsu makan (*Lapar, Sedang, Kenyang*) (rujukan: Hu et al., 2026; Dong et al., 2024).
      3. **Baseline Pembanding: MobileNetV3-Small + LSTM**: Model *end-to-end video classification*.
    - Menerbitkan dokumen rancangan master: [`research/rancangan-komparasi-metode-cv-dan-dl.md`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/research/rancangan-komparasi-metode-cv-dan-dl.md).
    - Memutakhirkan [`research/business-logic.md`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/research/business-logic.md) pada Bagian 4 dengan menambahkan dimensi studi komparasi algoritma.
  - **Penyusunan Protokol Evaluasi & Benchmark Raspberry Pi 5**:
    - Merancang matriks komparasi 4 dimensi: (1) Akurasi & F1-Score 3 kelas, (2) Ketahanan derau (*false alarm rate* akibat silau matahari, angin, aerator), (3) Beban komputasi *edge* (FPS, latensi ms, CPU %, RAM MB, suhu prosesor °C), dan (4) Kebutuhan rekayasa data latih.
  - **Penyusunan Prompt Pencarian Akademik Terstruktur untuk Consensus.app**:
    - Menyusun 5 set prompt bahasa Inggris berstandar akademik tinggi untuk penelusuran bukti empiris spesifik jika diperlukan tambahan verifikasi literatur.
- **Klasifikasi Perubahan**: *Moderate* (Penambahan dimensi studi komparasi algoritma dan arsitektur Deep Learning hibrida YOLO+LSTM tanpa mengubah objek dan batasan fisik kolam lele).
- **Status**: Selesai (*Completed*)

---

### 2026-10-17 (Sesi 16)
- **Perubahan**:
  - **Ingesti & Ekstraksi Materi Perkuliahan Metodologi Penelitian 2025 (Google Drive Bu Ulla)**:
    - Mengakses dan mengunduh 17 file presentasi (.pptx) dari Google Drive resmi Bu Ulla Delfana Rosiani (`PPT Metpen 2025`) ke dalam repositori lokal pada folder `panduan_metpen_dr_ulla/`.
    - Mengekstrak teks lengkap dari ke-17 modul: `MT1_Penentuan_Kalimat_Judul`, `MT2_Menyusun_Bab_1`, `MT3_Menyusun_Bab_2`, `MT4_Menyusun_Bab_3`, `M1` s.d. `M14`.
  - **Penyusunan Buku Panduan Resmi Penulisan Proposal Skripsi Polinema**:
    - Menerbitkan dokumen master: [`research/panduan-penulisan-proposal-skripsi.md`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/research/panduan-penulisan-proposal-skripsi.md) dan salinan di `panduan_metpen_dr_ulla/PANDUAN_TATA_CARA_PENULISAN_PROPOSAL_SKRIPSI_POLINEMA.md`.
    - Menyusun sintesis komprehensif seluruh kaidah baku:
      1. Penentuan kalimat judul (3 unsur: objek, tujuan, metode; $<20$ kata; tanpa tools sekunder).
      2. Struktur Bab 1 (pola alur narasi OMKKMasaSolTu Romi Satrio Wahono; penegasan RP eksplisit di akhir Latar Belakang; korespondensi 1-ke-1 RP $\to$ RQ $\to$ RO; minimal 8+ sitasi APA 7th 5 tahun terakhir).
      3. Struktur Bab 2 (teori umum ke khusus; tabel matriks SOTA 6 kolom; perumusan Research Gap, Novelty, dan *Method Improvement*).
      4. Struktur Bab 3 (sub-bab 3.1 s.d. 3.7; flowchart alur metodologi; kriteria keberhasilan kuantitatif; tabel hardware & software).
      5. Etika penulisan (7 bentuk pelanggaran LIPI, teknik parafrase Knowles 2007) dan etika AI generatif (format deklarasi *AI-assisted writing* bahasa Indonesia).
  - **Penyusunan & Kompilasi Draf Bab 1 (Pendahuluan) & Daftar Pustaka Standar Polinema**:
    - Menyusun naskah lengkap Bab 1 pada `latex/sections/01-introduction.tex` dan dokumen mandiri `latex/proposal-bab1.tex` mengikuti kaidah narasi OMKKMasaSolTu (Romi Satrio Wahono / Dr. Ulla Delfana Rosiani):
      1. Objek: Nilai strategis lele nasional, data KKP 2023--2024 (1,14--1,16 juta ton/tahun), kebutuhan benih 12--14 miliar ekor/tahun, krisis mortalitas 30--50% pada fase pendederan lele, regulasi SNI 01-6484.2-2000.
      2. Metode Eksisting: Penjadwalan waktu tetap (*fixed timer*) & manual (risiko *overfeeding* amonia vs *underfeeding* kanibalisme lele).
      3. Kelebihan & Keterbatasan Metode SOTA: *Deep learning* (YOLO, Optical Flow, CNN, ViT) menghadapi keterbatasan pada air keruh ($\le 3$ cm), gerak transien sub-detik (0,3--0,6 detik), derau luar ruangan, dan komputasi *edge* CPU Raspberry Pi.
      4. Pernyataan Masalah Penelitian (*Research Problem*): Ditegaskan secara eksplisit di akhir Sub-bab 1.1 Latar Belakang.
      5. Solusi Usulan: *Adaptive Three-Frame Differencing* (TFD) + *bitwise AND* + HSV *S-channel* + filter CPL + FAI + FSM servo.
      6. Rumusan Masalah (1--4) & Tujuan Penelitian (1--4): Berkorespondensi 1-ke-1 tanpa label RQ/RO.
      7. Batasan Masalah (1--6): Kolam tenang siang hari tanpa aerator, kamera nadir 30--50 cm, objek benih lele pendederan, kuota harian maks 5% biomassa.
      8. Manfaat Penelitian: Dikelompokkan menjadi manfaat teoretis dan manfaat praktis.
  - **Penyesuaian Ruang Lingkup Objek Riset hingga Pendederan IV (2--12 cm)**:
    - Memperluas cakupan benih ikan lele (*Clarias sp.*) dari sebelumnya terbatas pada Pendederan II (2--7 cm) menjadi mencakup seluruh fase pendederan: **Pendederan I hingga Pendederan IV (rentang ukuran panjang tubuh 2 sampai 12 cm)** sesuai siklus pendederan budidaya nasional dan SNI 01-6484.2-2000.
    - Menyelaraskan seluruh dokumen terkait (`01-introduction.tex`, `proposal-bab1.tex`, `matriks-rp-rq-ro.tex`, dan berkas aturan panduan).
  - **Penerapan Preferensi Tipografi & Format Sitasi Khusus**:
    - Mengatur tata letak standar Polinema (margin kiri 4 cm, atas 3 cm, kanan 3 cm, bawah 3 cm, spasi 1.5, Times New Roman 12 pt) menggunakan perintah primitif TeX yang kompatibel dengan instalasi minimal TeX Live lokal.
    - Meniadakan seluruh penekanan tebal (*bold*) pada batang tubuh paragraf naratif.
    - Menghilangkan tanda pisah ganda (`--` / `---`) pada narasi, digantikan dengan tanda koma atau kata 'sampai'.
    - Mengubah format daftar rincian (*enumerate*) agar subjudul diikuti baris baru (enter), bukan format sebaris (*inline bold*).
    - Menerapkan format sitasi pengarang-tahun (*author-year*) pada teks, dan membuat *BibTeX style* khusus `latex/apalike-doi.bst` untuk menghasilkan Daftar Pustaka bergaya APA 7th lengkap dengan URL/DOI aktif.
    - Menghilangkan halaman sampul (*cover page*) sehingga naskah langsung diawali dengan judul BAB I PENDAHULUAN pada Halaman 1 sebagai draf laporan kemajuan bimbingan.
  - **Penerbitan Berkas PDF Siap Bimbingan**:
    - Berkas draf Bab 1: [`Proposal_Bab1_Khoirotun_Nisa.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/Proposal_Bab1_Khoirotun_Nisa.pdf) (10 halaman, Bab 1 + Daftar Pustaka APA 7th lengkap).
    - Berkas matriks RP-RQ-RO: [`matriks-rp-rq-ro-kolam-tenang.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/matriks-rp-rq-ro-kolam-tenang.pdf) (2 halaman landscape, objek Pendederan I--IV).
- **Klasifikasi Perubahan**: *Major* (Penyusunan naskah draf Bab 1, perluasan cakupan Pendederan I--IV, penyesuaian sitasi APA 7th ber-DOI, dan penerbitan berkas PDF bimbingan).
- **Status**: Selesai (*Completed*)

---

### 2026-10-16 (Sesi 15)
- **Perubahan**:
  - **Penyesuaian Konteks Riset ke Kolam Tenang Tanpa Aerator**:
    - Mengakomodasi arahan terbaru bahwa kondisi aktual kolam penelitian adalah **kolam luar ruangan tenang tanpa aerator**.
    - Mengidentifikasi implikasi metodologis: tantangan pemodelan *moving baseline* gelembung aerator dieliminasi, dan fokus bergeser penuh ke penanganan derau visual lingkungan luar ruangan (*outdoor visual noise*: silau matahari/glare, bayangan angin, daun mengapung, burung liar) serta pembuktian korelasi empiris riak permukaan air tenang dengan rasa lapar lele.
  - **Penyusunan Matriks Formal RP, RQ, dan RO (Tabel 3 Kolom dengan Merge Kolom 1)**:
    - Merumuskan Research Problem (RP) terpadu yang mencakup 4 tantangan utama (derau visual outdoor, durasi transien lele 3--6 frame @ 10 FPS, komputasi edge Raspberry Pi, dan validasi empiris).
    - Merumuskan 4 Research Questions (RQ1: Deteksi Gerak, RQ2: Reduksi Derau Outdoor, RQ3: Validasi Empiris Lapar, RQ4: Logika Pakan Terkendali & Evaluasi Budidaya).
    - Merumuskan 4 Research Objectives (RO1--RO4) yang berkorespondensi 1-ke-1 secara presisi dengan RQ1--RQ4.
    - Mengeliminasi seluruh penyebutan kata aerator/aerasi pada naskah rumusan masalah.
  - **Penerbitan Dokumen PDF Siap Cetak (A4 Landscape 2 Halaman)**:
    - Berkas LaTeX: `latex/matriks-rp-rq-ro.tex`.
    - Berkas PDF Resmi: `output/rp-rq-ro/matriks-rp-rq-ro.pdf` dan salinan cepat di root: `matriks-rp-rq-ro-kolam-tenang.pdf`.
    - Halaman 1 memuat tabel matriks utama dengan Kolom 1 (RP) di-merge vertikal penuh, Halaman 2 memuat pemetaan metodologi, metrik terukur, batasan sistem, dan logika *daily quota budgeting*.
- **Klasifikasi Perubahan**: *Moderate* (Penyesuaian ruang lingkup lingkungan kolam dan penegasan matriks RP-RQ-RO).
- **Status**: Selesai (*Completed*)

---

### 2026-10-12 (Sesi 14)
- **Perubahan**:
  - **Troubleshooting Jaringan & Modem MiFi 4G LTE Lapangan**:
    - Mendiagnosis kendala modem MiFi portabel Telkomsel yang hanya menyala lampu indikator baterai (modul Wi-Fi masuk mode *power saving / sleep* akibat ketiadaan kuota data seluler dan auto-disconnect klien).
    - Memandu langkah re-aktivasi (*single click wake-up* dan pengisian daya), memverifikasi integrasi jaringan lokal pada subnet baru `192.168.100.0/24`.
    - Memindai dan memverifikasi alamat IP lokal Raspberry Pi 5 (`192.168.100.193`) via interface Wi-Fi `wlp0s20f3` laptop.
  - **Penambahan Mekanisme Auto-Recovery Status Riwayat Rekaman Terputus (`app.py`)**:
    - Mengidentifikasi anomali entri riwayat rekaman `lele_20261012_090021.mp4` (ukuran 44 byte) yang berstatus `"🔴 Sedang Merekam"` akibat insiden Raspberry Pi mati mendadak saat sesi rekam pagi hari berlangsung.
    - Menambahkan logika *self-healing recovery* pada fungsi `load_history()` di `/home/raspi5/Nisa/app.py`: jika sistem baru melakukan *booting* dan menemukan entri riwayat lama yang masih berstatus `"Sedang Merekam"`, status otomatis dialihkan menjadi `"⚠️ Terputus (Mati Listrik / Reboot)"`.
  - **Integrasi Pemantauan Nama Wi-Fi & Parameter Jaringan di Dashboard**:
    - Menambahkan modul `NetworkManager` di `/home/raspi5/Nisa/app.py` yang secara asinkron mendeteksi nama SSID Wi-Fi aktif dan kekuatan sinyal via `nmcli`, IP lokal via `socket`, serta IP Tailscale.
    - Menambahkan indikator visual di antarmuka web [`templates/index.html`](file:///home/raspi5/Nisa/templates/index.html):
      1. Badge status Wi-Fi di *navigation header* atas (`Wi-Fi: <SSID> (<Sinyal>%)`).
      2. Kartu informasi baru *"Wi-Fi Terhubung"* pada grid status perangkat lengkap dengan informasi IP lokal & Tailscale.
    - Memverifikasi keberhasilan integrasi langsung pada Raspberry Pi 5 (`nisa-dashboard.service`).
- **Status**: Selesai (*Completed*)

---

### 2026-10-11 (Sesi 13)
- **Perubahan**:
  - **Penyusunan Kajian Komprehensif Berdasarkan Setup Aktual Kamera Dekat (`image.png`)**:
    - Menganalisis kondisi optik nyata setup lapangan: ketinggian kamera rendah ($h \approx 30\text{--}50\text{ cm}$ nadir $90^\circ$), air kolam keruh kehijauan pendederan lele, percabangan selang aerator Y di dasar dengan letupan buih melayang, serta lipatan dinding terpal biru pada $30\%$ bagian atas frame.
    - Merumuskan *Static Polygonal ROI Masking* untuk membuang getaran terpal biru akibat angin luar ruangan.
  - **Sintesis Kritis 20 Literatur Global & Penegasan Kecukupan Literatur**:
    - Memverifikasi bahwa 20 literatur CV yang ada + 14 literatur pakan lokal sudah **sangat cukup dan tuntas**; tidak memerlukan pencarian baru via Consensus.
    - Menegaskan 4 *Research Gap*: (1) Oklusi bentuk tubuh di air keruh $\to$ beralih ke analisis riak mikro, (2) Asumsi naif air tenang $\to$ pemodelan baseline aerator kontinu, (3) Asumsi buih tebal ikan dewasa $\to$ setup kamera berjarak dekat menangkap gelombang mikro, (4) Model DL workstation mahal $\to$ algoritma deterministik hemat daya di Raspberry Pi 5.
  - **Formulasi Matematis Pemisahan Gerakan Lele vs. Derau Aerator**:
    - Pemodelan *Running Gaussian Baseline* rekursif Welford ($\mu_{\text{base}}, \sigma_{\text{base}}^2$).
    - Uji anomali deviasi baku $Z$-Score ($Z_t \ge 3,5$) terverifikasi jendela temporal $N \ge 3$ frame berturut-turut ($0,3\text{--}0,5\text{ s}$).
  - **Metodologi Reduksi Derau Outdoor**:
    - Eliminasi pantulan kilau matahari (*sun glint*) via konversi ruang warna HSV (normalisasi kanal $V$ via CLAHE, deteksi pada kanal $S$) serta rekomendasi filter optik polarisasi sirkular (CPL).
    - Eliminasi daun mengapung via filter kecepatan dan koherensi arah vektor (*unidirectional laminar drift*).
    - Eliminasi bayangan burung/petani via batas ambang luas kontur maksimum ($A_i > 0,15 A_{\text{ROI}}$).
  - **Kuantifikasi Skor $FAI$ & Logika Kendali Aktuator Servo (PCA9685)**:
    - *Three-Frame Differencing* biner Otsu + bitwise AND untuk menghapus *ghosting*.
    - Perumusan indeks aktivitas makan ($FAI_t$) dengan skala keputusan: $FAI < 2,0$ (Quiescent/OFF), $2,0 \le FAI < 4,0$ (Standby), $FAI \ge 4,0$ (Trigger Servo ON).
    - Arsitektur *Finite State Machine* (FSM) terikat kuota harian petani (*daily quota budgeting*) dengan jeda *cooldown* pasca-pakan 3--5 menit.
  - **Penerbitan Berkas Luaran Resmi Siap Cetak**:
    - Dokumen Markdown: `research/synthesis/kajian-lengkap-metodologi-cv-dan-noise-kolam.md`.
    - Naskah LaTeX: `latex/kajian-lengkap-metodologi-cv-dan-noise-kolam.tex`.
    - Dokumen PDF Siap Cetak (7 halaman rapi tanpa overfull): `output/kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf`.
- **Alasan**: Permintaan pengguna untuk mendalami 4 poin kunci riset visi komputer bibit lele secara tuntas ("lengkap kap kap") dan siap cetak untuk dipelajari, serta mengintegrasikan foto setup aktual kamera di atas air (`image.png`).
- **Status**: Selesai (*Completed*)

---

### 2026-09-26 (Sesi 12)
- **Perubahan**:
  - **Identifikasi Detail Merk & Spesifikasi Hardware Kamera di Literatur CV**:
    - Mengekstrak data riil dari seluruh 20 artikel CV mengenai merk dan model spesifik yang digunakan:
      1. Qian et al. (2025): Hikvision DS-2CD1245-LA (PoE Bullet Cam, 1/2.8'' CMOS, 1440p/2K QHD, overhead 3 m).
      2. Fukae et al. (2023): Canon VB-H651V (2.1 MP CMOS, optical zoom 2.8x, PoE Gigabit, 1080p 30 FPS).
      3. Marliza & Aisuwarya (2021): Raspberry Pi Camera Module-V2 (Sony IMX219 8 MP, MIPI-CSI).
      4. Zhou et al. (2018): AVT Mako G-223B (GigE NIR CMOS) + iluminator Near-Infrared HEROWEI MVIR0460 850 nm.
      5. Liu et al. (2014): Micro-vision MV-VS078FC (1/3'' Sony CCD) + capture card IEEE-1394.
      6. Zhao et al. (2016, 2017): Hikvision DS-2CD6233F-SDI (CCD HDV 1080p) + LED Kingbright 100W.
      7. Kamal et al. (2025): Piezoelectric Underwater Acoustic Hydrophone (Non-kamera optik).
    - Memperbarui Tabel Master 1 di LaTeX dan Markdown dengan detail merk dan hardware kamera ini.
  - **Penegasan Posisi Kajian Model Temporal (LSTM, Multi-Stream, dkk.)**:
    - Menegaskan bahwa LSTM **bukan rumusan final skripsi yang sudah dikunci**, melainkan **telaah literatur kritis** terhadap bagaimana paper-paper terdahulu (Hu et al. 2026, Dong et al. 2024, Fukae et al. 2023, Li et al. 2020) menerapkan pemodelan sekuensial deret waktu:
      - Mengapa model temporal dibutuhkan: menangkap siklus makan dinamis (lapar $\to$ riak puncak $\to$ kenyang) dan mengeliminasi alarm palsu aerator sesaat.
      - Bagaimana model Hu et al. bekerja: ResNet18 + ViT $\to$ sekuens $T=5$ frame $\to$ single-layer LSTM 256 unit. Keterbatasan komputasi: butuh GPU RTX 3090, 28.6 juta parameter.
      - Bagaimana model Dong et al. bekerja: Three-Stream CNN (Optical Flow + Spasial Biner + Tekstur GLCM).
      - Implikasi bagi skripsi: Jika kelak menguji model temporal, masukan bukan raw video melainkan vektor 1D terkompresi ternormalisasi baseline aerator (Z-Score). Model temporal ringan ini ditempatkan sebagai **salah satu hipotesis pembanding** terhadap model *baseline rule-based*, bukan formula final mutlak.
  - **Perluasan Sintesis 4 Research Gap Kunci Terhadap Seluruh Literatur Global (20 Artikel)**:
    - Mengoreksi kotak sintesis *research gap* di LaTeX dan Markdown yang sebelumnya terkesan sempit menjadi sintesis 4 klaster kesenjangan fundamental yang memetakan seluruh 20 artikel:
      1. *Oklusi Deteksi Visual Tubuh di Air Keruh* (Qian et al. 2025, Vijayalakshmi 2025, Zhao et al. 2025, Alahmad et al. 2025).
      2. *Asumsi Permukaan Air Tenang Tanpa Pemodelan Aerator Konstan* (Fukae et al. 2023, Liu et al. 2014, Marliza & Aisuwarya 2021, Atoum et al. 2015, Zhou et al. 2018).
      3. *Kegagalan Asumsi Deteksi Cipratan Buih Kasar pada Benih* (Wu et al. 2024, Atoum et al. 2015).
      4. *Beban Komputasi Workstation GPU vs Kerentanan Derau Akustik* (Hu et al. 2026, Dong et al. 2024, Kamal et al. 2025).
      5. *Posisi & Kebaruan Solusi Skripsi Mahasiswa* (Riak gerak 1D hemat komputasi ternormalisasi baseline aerator).
  - **Kompilasi Ulang LaTeX**:
    - Kompilasi ulang `latex/laporan-analisis-pakan-dan-cv.tex` menghasilkan `output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf` tepat 4 halaman tanpa overfull hbox.
- **Alasan**: Klarifikasi pengguna mengenai cakupan sintesis research gap kunci yang harus merepresentasikan seluruh literatur global, bukan hanya 2 penelitian.
- **Status**: Selesai (*Completed*)

---

### 2026-09-26 (Sesi 11)
- **Perubahan**:
  - **Sinkronisasi Hasil Bimbingan Dosen (Bu Ulla)**:
    - Memperbarui `research/business-logic.md` dan `research/research-requirements.md` sesuai 5 butir utama arahan dosen:
      1. Penegasan objek spesifik: **BIBIT IKAN LELE** (*fry/fingerlings*, pendederan).
      2. Perumusan konsep kendali: "Mengamati riak $\to$ menentukan pemberian pakan terkontrol" (bukan *timer* kaku, porsi harian ditentukan petani misal 1 kg/hari lalu dibagi adaptif mengikuti riak lele).
      3. Penegasan batasan mutlak: **TIDAK berfokus pada kualitas air** (kualitas air adalah ranah terpisah/Varizky atau batasan lingkungan) dan **TIDAK fokus pada diagnosis kesehatan**.
      4. Perumusan masalah CV utama: Membedakan pergerakan riak normal aerator (*baseline*) dengan riak/cipratan lele.
      5. Perumusan rancangan evaluasi lapang 1 bulan (didahului 1 minggu observasi baseline riak) dengan pembanding kolam manual tanpa alat, mencakup metrik FCR, bobot, panjang, survival, dan kuota pakan.
  - **Penyusunan Dua Output Analisis Mendalam**:
    - Output 1: Analisis kebiasaan bibit lele dan respon biologis jika pakan dibatasi vs *loss* (*ad libitum*) berdasarkan literatur lokal (`pakannya bibit lele/`).
    - Output 2: Riset mendalam computer vision yang diperluas mencakup **seluruh 20 artikel CV terverifikasi** (19 Full-Text PDF lokal + Wu et al. 2024), menyajikan:
      - **Tabel Master 1**: Spesifikasi fisik kamera (jenis, posisi top-view/oblique/side/underwater, ketinggian, sudut, resolusi, FPS), objek, lingkungan kolam, dan kondisi aerator.
      - **Tabel Master 2**: Metode computer vision, model machine learning/deep learning, input, output, penanganan noise visual, hasil eksperimen, dan keterbatasan utama terhadap skripsi bibit lele outdoor ber-aerator.
      - Analisis karakteristik 6 metode visual & formulasi spesifikasi teknis model temporal LSTM (input vektor 1D, sliding window $T=15$, target biner, normalisasi Z-score baseline aerator).
  - **Kompilasi Luaran PDF Resmi**:
    - Menghasilkan berkas PDF resmi 4 halaman: `output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf` bebas overfull.
- **Alasan**: Permintaan pengguna untuk memperluas kajian ke seluruh 20 artikel CV yang telah ditemukan, mengekstrak rincian kamera, sudut, ketinggian, resolusi, metode, dan modelnya.
- **Status**: Selesai (*Completed*)


---

### 2026-09-25 (Sesi 10)
- **Perubahan**:
  - **Integrasi & Standardisasi Literatur Pakan Lele**:
    - Memindahkan dan menstandarkan 8 artikel PDF yang ditambahkan pengguna dari root ke subfolder `articles/artikel bibit lele/pakannya bibit lele/`.
    - Total koleksi lokal fisik Full-Text PDF pakan lele kini berjumlah **14 berkas PDF otentik** (70% ketercakupan penuh dari `pakannya bibit lele.csv`):
      1. `[01] - Hildebrand et al. (2025)` (*Fishes*, 832 KB) - *Feeding time management & stress response*.
      2. `[02] - Ojelade et al. (2022)` (*Frontiers in Vet Sci*, 1,0 MB) - *Environmental enrichment & behavior*.
      3. `[03] - Ojelade et al. (2025)` (*Scientific African*, 1,2 MB) - *Unpredictable feeding patterns & blood responses*.
      4. `[05] - Abdel-Aziz et al. (2021)` (*Scientific African*, 670 KB) - *Feeding frequencies, density, & protein*.
      5. `[08] - Agunbiade-Olu et al. (2022)` (*J. Vet. Biomed. Sci.*, 1,6 MB) - *Intermittent feed deprivation & compensatory growth*.
      6. `[09] - Oboh (2022)` (*FUDMA J. of Sci.*, 818 KB) - *Feeding frequency on performance indices*.
      7. `[10] - Ikeogu et al. (2020)` (*Global J. Fish. Sci.*, 385 KB) - *Two feeding rates & 5% body weight*.
      8. `[13] - Hossain & Beveridge (2001)` (*Aquaculture Research*, 82 KB) - *Night feeding & feed demand*.
      9. `[14] - Al-salahy & Ibrahim (2018)` (*Acta Ecologica Sinica*, 874 KB) - *Starvation & oxidative stress*.
      10. `[15] - Abalaka et al. (2025)` (*Nigerian Vet. J.*, 451 KB) - *Starvation & water additives*.
      11. `[16] - Tiamiyu et al. (2018)` (*Iranian J. Fish. Sci.*, 3,0 MB) - *Feeding rates in static vs flow through*.
      12. `[18] - Khormi et al. (2026)` (*Frontiers in Physiology*, 689 KB) - *Growth dynamics under fasting-refeeding*.
      13. `[19] - Li et al. (2020)` (*JWAS*, 536 KB) - *Reducing dietary protein & porcine meat meal*.
      14. `[20] - Aderolu et al. (2010)` (*African J. of Food Sci.*, 447 KB) - *Feeding frequency 3 times daily*.
  - **Penyusunan Indeks & Katalog**:
    - Memperbarui `articles/artikel bibit lele/pakannya bibit lele/README.md` dengan tabel inventaris 14 PDF aktif.
- **Alasan**: Permintaan pengguna untuk memindahkan artikel yang baru ditambahkan ke folder pakan bibit lele dan menyesuaikan penomoran serta penamaannya secara baku.
- **Status**: Selesai (*Completed*)

---

### 2026-09-25 (Sesi 9)
- **Perubahan**:
  - **Restrukturisasi & Pengelompokan Berkas di Folder `output/`**:
    - Membuat 3 subdirektori terpisah di dalam `output/` agar berkas PDF dan file bantu kompilasi LaTeX (`.aux`, `.log`, `.out`, `.bbl`, `.toc`) tidak bercampur aduk:
      1. `output/skripsi-proposal/`: Berisi `main.pdf` (naskah proposal lengkap 25 halaman), `references.bib`, serta berkas *build* terkait.
      2. `output/studi-literatur/`: Berisi `Laporan_Studi_Literatur_Khoirotun_Nisa.pdf` (laporan telaah literatur 8 bagian) dan berkas *build* terkait.
      3. `output/standar-bibit-lele/`: Berisi `Standar_Bibit_dan_Pendederan_Lele.pdf` (laporan standar benih dan manajemen pakan lele) dan berkas *build* terkait.
    - Menambahkan `output/README.md` sebagai katalog navigasi direktori luaran dengan tautan langsung ke masing-masing dokumen PDF.
- **Alasan**: Permintaan pengguna untuk merapikan berkas luaran ke subfolder khusus agar mudah dibedakan dan dikelola.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 8)
- **Perubahan**:
  - **Fokus Ketat pada Literatur Terunduh (9 Berkas PDF Fisik)**:
    - Menghilangkan pemaksaan 22 artikel referensi; membatasi dokumen hanya mengacu pada **9 artikel ilmiah yang berkas fisik Full-Text PDF-nya benar-benar telah diunduh secara lokal** di `articles/artikel bibit lele/`.
    - Melakukan penomoran ulang berkas PDF di folder `articles/artikel bibit lele/` secara teratur dari `[01]` hingga `[09]`:
      1. `[01]` Gisbert et al. (2021) - *Reviews in Aquaculture*
      2. `[02]` Kurdowi et al. (2025) - *Jurnal Perikanan Unram*
      3. `[03]` Afia et al. (2020) - *Sumerianz J. of Biotech*
      4. `[04]` Pranat et al. (2025) - *Jurnal Perikanan Unram*
      5. `[05]` Essien et al. (2024) - *Acta Nat. Sci.*
      6. `[06]` Jibrin et al. (2024) - *Int. J. Fish. Aquat. Stud.*
      7. `[07]` Uche et al. (2023) - *Agrobiological Records*
      8. `[08]` Srivastava et al. (2012) - *J. Aquac. Res. Dev.*
      9. `[09]` Pelu & Liubana (2025) - *Jurnal Akuakultur Sungai dan Danau*
    - Menyinkronkan ulang seluruh naskah agar hanya menyitir ke-9 artikel terunduh ini:
      - `articles/artikel bibit lele/STANDAR_BIBIT_DAN_PAKAN_LELE.md` (9 dari 9 disitir dan ada di Daftar Pustaka).
      - `research/synthesis/standar-bibit-dan-pakan-lele.md`
      - `articles/artikel bibit lele/README.md`
      - `latex/bibit-lele-references.bib`
      - `latex/laporan-standar-bibit-dan-pendederan.tex`
  - **Pembersihan Berkas PDF Ganda di `output/`**:
    - Menghapus berkas ganda `output/laporan-standar-bibit-dan-pendederan.pdf` dan berkas *auxiliary*-nya.
    - Mengompilasi naskah LaTeX secara langsung menghasilkan **1 berkas PDF utama tunggal**:
      - `output/Standar_Bibit_dan_Pendederan_Lele.pdf` (5 halaman, 0 error, tata letak tabel rapi).
- **Alasan**: Permintaan pengguna untuk tidak memaksakan 22 artikel dan hanya menggunakan artikel yang sudah diunduh secara fisik, serta klarifikasi dan pembersihan file PDF output yang ganda.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 7)
- **Perubahan**:
  - **Pembersihan & Standardisasi Direktori Literatur (`articles/`)**:
    - Menghapus semua folder duplikat, file PDF tersebar di `articles/pdf/`, serta Windows junction link yang membuat pengguna bingung (`articles/artikel-bibit-lele`, `articles/artikel-computer-vision`, `articles/pdf/`).
    - Menstandarkan `articles/` menjadi tepat **2 folder bersih**:
      1. `articles/artikel computer vision/` (berisi 19 Full-Text PDF Computer Vision + `README.md`).
      2. `articles/artikel bibit lele/` (berisi Full-Text PDF bibit lele, `STANDAR_BIBIT_DAN_PAKAN_LELE.md`, dan `README.md`).
  - **Integrasi Informasi Pendederan Lele (`pedederean.csv` & `pedederan.pdf`)**:
    - Mengekstrak data tahapan budidaya operasional di Indonesia dan membedakannya secara tegas dengan klasifikasi ontogenetik/fase biologis.
    - Menambahkan Bab 3: *Integrasi Sistem Pendederan Operasional (Pendederan I, II, dan III) vs Fase Biologis* pada:
      - `research/synthesis/standar-bibit-dan-pakan-lele.md`
      - `articles/artikel bibit lele/STANDAR_BIBIT_DAN_PAKAN_LELE.md`
    - Rincian parameter pendederan:
      - **Pendederan I (14–21 hari)**: Benih 2–3 cm (umur 10–14 hari); padanan Late Fry $\to$ Fingerling Awal; pakan beralih dari cacing sutra ke pelet mikro 0,5 mm (protein 35–40%).
      - **Pendederan II (21–28 hari)**: Benih 5–7 cm (bobot 1,65–2,55 g); padanan Fingerling Pertengahan; fase paling rawan kanibalisme; ransum harian 5–10% biomassa (optimum 5%), frekuensi 3–4x sehari, wajib sortasi/grading tiap 7–10 hari.
      - **Pendederan III (28–35 hari)**: Benih >7–8 cm (>3,8 g hingga 5–10 g); padanan Fingerling Akhir / Juvenil; pelet 1–2 mm; dosis ransum diturunkan ke 2–3% biomassa/hari; persiapan kolam pembesaran akhir.
    - Menambahkan parameter kualitas air pendederan berdasarkan studi Pelu & Liubana (2025) di BBI Teun (suhu 26–30°C dengan aerasi konstan, pH 6,5–8,5, DO $\ge 5$ mg/L) dan persiapan kolam pendederan Sadiana & Rahmanto (2021).
    - Memperbarui `latex/bibit-lele-references.bib` dan `articles/artikel bibit lele/README.md` dengan sitasi Pelu & Liubana (2025) dan Sadiana & Rahmanto (2021).
  - **Penyusunan & Kompilasi Laporan PDF di `output/`**:
    - Membuat naskah LaTeX `latex/laporan-standar-bibit-dan-pendederan.tex` lengkap dengan metadata mahasiswa (Khoirotun Nisa', NIM: 2341720057, Dosen Pembimbing: Dr. Ulla Delfana Rosiani, ST., MT.).
    - Mengompilasi naskah menjadi berkas PDF berkualitas tinggi tanpa overflow:
      - `output/laporan-standar-bibit-dan-pendederan.pdf` (5 halaman, 0 error).
      - `output/Standar_Bibit_dan_Pendederan_Lele.pdf` (salinan nama intuitif).
- **Alasan**: Permintaan pengguna untuk menambahkan data dari `pedederean.csv` dan `pedederan.pdf` ke informasi bibit lele serta menghasilkan output berkas PDF.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 6)
- **Perubahan**:
  - **Fokus Domain Bibit Lele (*Catfish Fry & Fingerlings*)**:
    - Memproses data literatur konsensus dari `bibit lele.csv` dan laporan `bibit lele consensus.pdf` (20 entri artikel ilmiah).
    - Melakukan restrukturisasi dan pengelompokan direktori artikel ilmiah di `articles/`:
      - Direktori `articles/artikel-computer-vision/` (menampung 19 artikel Full-Text PDF domain Visi Komputer & Analisis Gerakan).
      - Direktori `articles/artikel-bibit-lele/` (menampung artikel ilmiah domain Biologi Pembenihan, Nutrisi & Manajemen Pakan Bibit Lele).
      - Menambahkan junction folder Windows `articles/artikel computer vision` dan `articles/artikel bibit lele` untuk kenyamanan navigasi tanpa duplikasi ruang disk.
    - Mengunduh berkas fisik Full-Text PDF artikel bibit lele yang berstatus Open Access (`[01] Gisbert et al. 2021`, `[02] Kurdowi et al. 2025`, `[03] Afia et al. 2020`, `[06] Pranat et al. 2025`, `[08] Essien et al. 2024`, `[11] Jibrin et al. 2024`, `[20] Srivastava et al. 2012`) ke `articles/artikel-bibit-lele/`.
  - **Penyusunan Dokumen Sintesis Standar Bibit & Manajemen Pakan**:
    - Membuat naskah panduan akademik komprehensif `research/synthesis/standar-bibit-dan-pakan-lele.md` yang memuat:
      1. Klasifikasi 5 fase perkembangan bibit lele (*Sac-fry* D0–D3, *Early fry* D4–D7, *Late fry/Transisi* D8–D12, *Fingerling* D13–D30, *Juvenil* >D30).
      2. Standar baku kualitas air kolam benih (suhu 28–31°C, pH 6,5–8,0, DO $\ge 5,0$ mg/L, densitas tebar 500–700 ekor/m³).
      3. Kebutuhan nutrisi pakan alami (Cacing sutra *Tubifex sp.*, *Artemia*, *Daphnia*) dan pelet mikro protein tinggi (35–42% CP).
      4. Standar takaran pakan harian (*Feeding Rate*): Rekomendasi optimum 5% bobot tubuh/hari pada fase fingerling untuk keseimbangan laju pertumbuhan dan efisiensi FCR, serta penurunan bertahap ke 2–2,5% pada fase juvenil.
      5. Frekuensi pakan (3–4 kali/hari) dan metode sebar merata (*broadcast feeding*) di seluruh permukaan kolam untuk mencegah dominasi spasial dan kanibalisme.
      6. Integrasi langsung dengan sistem visi komputer pada Raspberry Pi (pemicuan kuota pakan otomatis berbasis deteksi lonjakan aktivitas kinetik menyambar pakan).
      7. Daftar Pustaka lengkap 20 artikel referensi standar APA dengan DOI aktif.
  - **Katalog & Berkas Sitasi**:
    - Menyusun `articles/artikel-bibit-lele/README.md` (katalog 20 artikel dan pengelompokan tematik).
    - Menyusun `articles/README.md` sebagai master index navigasi seluruh literatur.
    - Menghasilkan berkas BibTeX `latex/bibit-lele-references.bib` berisi 20 entri sitasi terverifikasi.
- **Alasan**: Permintaan pengguna untuk pemfokusan objek penelitian pada fase bibit lele, pengunduhan referensi pendukung dari Consensus, pengelompokan folder artikel, dan pembuatan dokumen standar benih & takaran pakan beserta sitasi dan dafpus.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 5)
- **Perubahan**:
  - **Audit Integritas Sitasi & Penghapusan Halusinasi AI**:
    - Memverifikasi secara langsung berkas fisik PDF `articles/pdf/[01]` (Qian et al., *Discover Applied Sciences* 2026, DOI: 10.1007/s42452-025-08043-5) dan `articles/pdf/[19]` (Vijayalakshmi & Sasithradevi, *Scientific Reports* 2025, DOI: 10.1038/s41598-025-89611-y).
    - Menghapus klaim angka ekstrapolasi/halusinasi AI sebelumnya: menghapus klaim "latensi 68 ms di Raspberry Pi" pada Qian et al. (paper aslinya hanya menguji di GPU 8,1 ms dan menyebut edge deployment sebagai *future work*), serta mengoreksi klaim AquaYOLO menjadi metrik asli paper (Precision 0,889, Recall 0,848, mAP@50 0,909 pada dataset DePondFi tanpa klaim fiktif ketahanan silau/daun).
    - Menghapus seluruh klaim angka performa spekulatif yang belum pernah diuji secara empiris di lab/lapangan (seperti latensi <25 ms, throughput $\ge 10$ FPS, memori <60 MB) dari naskah LaTeX dan dokumen sintesis.
  - **Perampingan Dokumen Sesuai Permintaan Nyata Dosen Pembimbing (Bu Ulla)**:
    - Merombak total `research/synthesis/literature-review-report.md` dari gaya pseudo-tesis yang *over-scoped* menjadi laporan studi literatur yang proporsional, jujur (*humble*), dan fokus pada 4 bagian konkret:
      1. Tabel 19 artikel terverifikasi (Judul, Penulis, Tahun, Jurnal/Konferensi, Link/DOI).
      2. Ringkasan 3–5 kalimat per artikel (100% fakta murni dari teks paper asli tanpa bumbu).
      3. Insight kasar & pola bacaan (metode konvensional vs deep learning, kondisi riil kolam luar ruangan & aerator kontinu, kendala komputasi edge).
      4. Arah metode tentatif untuk dicoba (bukan klaim rekomendasi mutlak).
      5. Daftar Pustaka lengkap 19 referensi standar IEEE.
  - **Sinkronisasi Naskah LaTeX & Tabel**:
    - Memperbarui `latex/tables/article-comparison.tex`, `latex/sections/03-literature-review.tex`, `latex/sections/06-positioning.tex`, dan `latex/sections/07-conclusion.tex`.
    - Kompilasi ulang `output/main.pdf` (27 halaman, 0 error).
- **Alasan**: Umpan balik kritis dan tepat dari pengguna mengenai bahaya sitasi bermasalah, integritas akademik, dan penyelarasan dengan lingkup tugas riil Bu Ulla.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 4)
- **Perubahan**:
  - Menyusun dokumen studi literatur komprehensif 8 bagian sesuai format penugasan Bu Ulla dan hasil brainstorming pengguna di `research/synthesis/literature-review-report.md`.
  - Mengintegrasikan analisis perbandingan mendalam 4 kelompok metode deteksi gerakan (*Frame Differencing*, *Optical Flow*, *GMM Background Subtraction*, dan *Deep Learning*) ke dalam `research/synthesis/comparison.md` dan tabel LaTeX `latex/tables/method-comparison.tex`.
  - Mengembangkan seluruh bab naskah LaTeX Polinema:
    - `latex/main.tex`: Halaman judul resmi Polinema, data mahasiswa (Khoirotun Nisa), dosen pembimbing (Siti Nurul Hidayah, S.Kom., M.Kom. / Bu Ulla), dan abstrak formal.
    - `latex/sections/01-introduction.tex`: Latar belakang komprehensif kolam lele outdoor, over/underfeeding, 4 kendala teknis (aerator kontinu, event 3--6 frame @ 10 FPS, Raspberry Pi edge, telemetri numerik), rumusan masalah, tujuan, dan manfaat.
    - `latex/sections/02-background.tex`: Landasan teori lengkap biologi lele, formulasi matematika *frame differencing*, *optical flow*, GMM, dan arsitektur komputasi Raspberry Pi.
    - `latex/sections/03-literature-review.tex`: Strategi penelusuran basis data, taksonomi query Boolean, dan ulasan mendalam 8 artikel kunci.
    - `latex/sections/04-comparison.tex`: Analisis naratif tabel perbandingan 19 artikel dan tabel perbandingan 4 metode deteksi gerak.
    - `latex/sections/05-research-gap.tex`: Formulasi tiga kesenjangan penelitian berbasis bukti (*Continuous Aeration Baseline Gap*, *Edge Sub-Second Latency Gap*, *Low-Cost Outdoor Monitoring Gap*).
    - `latex/sections/06-positioning.tex`: Posisi penelitian terhadap literatur global dan 3 poin kebaruan penelitian (*research novelty*).
    - `latex/sections/07-conclusion.tex`: Kesimpulan sintesis dan rekomendasi metode utama (*Adaptive Temporal Variance Subtraction*) serta metode alternatif (*Quantized YOLOv8n + FSM*).
  - Berhasil mengompilasi naskah proposal/studi literatur lengkap ke `output/main.pdf` (**25 halaman, 0 error, 0 undefined reference**).
- **Alasan**: Permintaan penugasan studi literatur dari Bu Ulla dengan format 8 bagian yang disesuaikan secara presisi dengan kondisi riil kolam lele ber-aerator.
- **Dampak**: Dokumen siap diserahkan/dikonsultasikan kepada dosen pembimbing.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 3)
- **Perubahan**: Penapisan `result 2.csv`, audit integritas berkas PDF (penghapusan berkas salah Massimo Cacciari 2005), pengunduhan 6 artikel Open Access mutakhir 2023--2025, pembaruan katalog 19 artikel terverifikasi, dan inisialisasi Git commit.
- **Alasan**: Pembaruan literatur fokus 5 tahun terakhir (2022–2026).
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 2)
- **Perubahan**: Integrasi topik skripsi baru pengguna ("Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar Berbasis Computer Vision") dari `conteks.md`, penapisan 100 entri `consensus result.csv`, pengunduhan 14 artikel ilmiah teks lengkap (*full-text PDF*) ke `articles/pdf/`.
- **Status**: Selesai (*Completed*)

---

### 2026-10-11 (Sesi 8)
- **Perubahan**:
  - **Pencegahan Kamera Mati / Freeze Akibat Gangguan Kabel USB**:
    - Menganalisis log kernel `dmesg` pada Raspberry Pi 5 yang mencatat diskoneksi perangkat USB Logitech Brio 100 (`usb disconnect`) dan penyambungan ulang ke port USB lain.
    - Menemukan kendala pada `_capture_loop` di mana OpenCV `cap.isOpened()` tetap bernilai `True` meski perangkat fisik terlepas, sehingga pembacaan `read()` gagal terus-menerus tanpa memicu re-inisialisasi.
    - Menambahkan mekanisme *self-healing / auto-reconnect* di `/home/raspi5/Nisa/app.py`: jika terjadi 15 kegagalan pembacaan frame berturut-turut (~1,5 detik), loop akan otomatis melepaskan objek kamera lama dan memindai ulang perangkat video yang aktif via `_init_camera()`.
    - Merestart dan memverifikasi `nisa-dashboard.service`: aliran video stream `/video_feed` kembali normal dan responsif via Wi-Fi lokal (`192.168.0.106:5000`) maupun Tailscale (`100.126.141.31:5000`).
- **Alasan**: Pemecahan masalah kamera yang mendadak mati/tidak menampilkan gambar saat kabel USB kamera tersenggol atau dipindah port.
- **Status**: Selesai (*Completed*)

---

### 2026-10-26 (Sesi 9)
- **Perubahan**:
  - **Penonaktifan Kompresi FFMPEG pada Raspberry Pi 5 Kolam**:
    - Menambahkan toggle `ENABLE_COMPRESSION = False` pada [`scratch/app.py`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/scratch/app.py) dan menyinkronkannya ke `/home/raspi5/Nisa/app.py`.
    - Merestart layanan `nisa-dashboard.service` via Tailscale secara terjadwal setelah sesi rekaman jam 11.00 selesai, memastikan video mentah OpenCV (~600–700 MB) diunggah utuh tanpa penurunan kualitas encoding ke Google Drive.
  - **Integrasi 4 Diagram Alur (Flowchart) ke Dokumen PDF Metodologi Komparasi**:
    - Membuat generator grafik publikasi resolusi tinggi (`scratch/generate_all_flowcharts.py`):
      - **Gambar 1**: Diagram Alur Sistem Pakan Adaptif Siklus Tertutup (*Closed-Loop Demand-Feeding FSM Architecture*).
      - **Gambar 2**: Pipeline Pemrosesan Citra Konvensional (*Adaptive TFD + HSV S-Channel + Running Gaussian Baseline*).
      - **Gambar 3**: Arsitektur Tiga Model Komparasi Deep Learning (*YOLOv8n Murni, YOLOv8n + Bi-LSTM, MobileNetV3 + LSTM*).
      - **Gambar 4**: Protokol Evaluasi Komparatif *Head-to-Head* pada Raspberry Pi 5 (27.000 frame uji riil).
    - Memperbarui naskah LaTeX [`latex/rancangan-komparasi-metode-cv-dan-dl.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/rancangan-komparasi-metode-cv-dan-dl.tex) menjadi 7 halaman terstruktur rapi.
    - Mengompilasi dan menerbitkan berkas PDF resmi ke [`output/komparasi-cv-dan-dl/Rancangan_Komparasi_CV_dan_Deep_Learning.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/komparasi-cv-dan-dl/Rancangan_Komparasi_CV_dan_Deep_Learning.pdf) beserta pratinjau gambar per-halaman.
- **Alasan**: Memenuhi permintaan pengguna untuk memvisualisasikan alur detail algoritma pakan adaptif ke dalam naskah proposal ilmiah agar mudah dipahami oleh dosen pembimbing dan penguji sidang.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 1)
- **Perubahan**: Reset repositori dan pembersihan total dari data skripsi teman.
- **Status**: Selesai (*Completed*)

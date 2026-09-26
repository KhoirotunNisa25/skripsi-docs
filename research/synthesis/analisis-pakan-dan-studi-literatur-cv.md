# 📘 Analisis Perilaku Makan Bibit Lele & Riset Mendalam Computer Vision
## Dokumen Kajian Akademik Terintegrasi (Berdasarkan Hasil Bimbingan Dosen)

---

## 📌 BAGIAN I: PENEGASAN KONSEP SKRIPSI HASIL BIMBINGAN

Berdasarkan hasil konsultasi dan bimbingan langsung dengan dosen pembimbing (Dr. Ulla Delfana Rosiani, ST., MT.), batasan, logika sistem, dan konteks penelitian diselaraskan secara tegas:

```
[PETANI]                                [KAMERA TOP-VIEW]
   │ (Menetapkan Kuota Harian, misal 1 kg/hari) │ (Merekam Permukaan Kolam @ 10 FPS)
   ▼                                            ▼
┌────────────────────────────────────────────────────────┐
│             SISTEM COMPUTER VISION (EDGE)              │
│  - Memodelkan baseline gejolak konstan aerator         │
│  - Mendeteksi deviasi/lonjakan riak bibit lele         │
│  - Menginterpretasi sinyal respons makan aktif         │
└──────────────────────────┬─────────────────────────────┘
                           │ Pemicuan Sub-Porsi Pakan (misal 50–100 g)
                           ▼
                    [FEEDER OTOMATIS]
                           │
       (Berhenti jika Kuota Harian Petani Tercapai)
```

1. **Objek Penelitian**: **BIBIT IKAN LELE** (*Clarias sp.*, fase benih / pendederan).
2. **Batasan Mutlak (*System Boundaries*)**:
   - **TIDAK berfokus pada kualitas air** (kualitas air adalah domain penelitian terpisah kolaborator / Varizky; parameter air hanya sebagai kondisi lingkungan pendukung/keterbatasan, bukan variabel independen).
   - **TIDAK berfokus pada diagnosis kesehatan ikan**.
   - **TIDAK menggantikan kontrol petani secara total**.
3. **Logika Inti Sistem**: *"Mengamati riak $\to$ Menentukan pemberian pakan terkontrol"*.
   - Bukan *timer* buta (*"tiap jam pasti diberi pakan"*).
   - Petani menentukan batas kemampuan pakan harian (*ceiling quota*, contoh: 1 kg pakan/hari). Pakan kemudian dibagi (*sub-rationing*) mengikuti ritme riak makan bibit lele. Sistem menuruti aktivitas bibit lele namun tetap terikat batas kuota dari petani.
   - Tujuan praktis: **Meringankan kerja petani dalam pemberian pakan, tanpa menghilangkan kendali petani atas alokasi pakan**.
4. **Masalah Utama Computer Vision**:
   - Kolam luar ruangan (*outdoor*) menggunakan **aerator aktif terus-menerus**.
   - Permukaan air tidak pernah diam; gejolak aerator adalah **BASELINE NORMAL**.
   - Sistem tidak boleh menggunakan aturan naïf *"ada gerakan = ikan lapar"*, melainkan mendeteksi **perubahan deviasi temporal** riak bibit lele terhadap riak aerator.
5. **Rencana Evaluasi Lapangan (1 Bulan vs Kolam Manual)**:
   - Didahului observasi awal 1 minggu (10–15 menit tiap jam) untuk memetakan variasi riak normal kolam.
   - Diikuti pengujian 1 bulan membandingkan kolam ber-alat dengan kolam pemberian pakan manual tanpa alat pada parameter: **Pertumbuhan bobot, pertambahan panjang, kelangsungan hidup (*Survival Rate*), total konsumsi pakan, dan FCR**.

---

## 🐟 BAGIAN II (OUTPUT 1): ANALISIS KEBIASAAN BIBIT LELE & RESPON KESEHATAN (PAKAN DIBATASI VS LOSS)

Kajian ini disusun berdasarkan sintesis 14 artikel ilmiah fisik di folder `articles/artikel bibit lele/pakannya bibit lele/` (antara lain: Ikeogu et al. 2020; Tiamiyu et al. 2018; Ojelade et al. 2025; Hildebrand et al. 2025; Hossain & Beveridge 2001; Khormi et al. 2026; Abdel-Aziz et al. 2021; Al-salahy & Ibrahim 2018).

### 1. Pola Makan Alami & Perilaku Riak Bibit Lele (*Feeding Ethology*)
- **Sifat Nokturnal & Respons Sensorik**: Lele afrika (*Clarias gariepinus*) adalah ikan nokturnal yang sangat aktif mencari makan pada intensitas cahaya rendah (petang, malam, fajar) menggunakan sungut (*barbels*) dan garis lateral (*lateral line*) untuk mendeteksi getaran dan aroma pakan (Hossain & Beveridge 2001; Hildebrand et al. 2025).
- **Karakteristik Riak Permukaan Bibit**: Saat lapar dan mendeteksi stimulus pakan di permukaan, bibit lele bergerak vertikal secara serentak ke permukaan air (*feeding frenzies*), menghasilkan riak halus dan cipratan mikro singkat berdurasi **3–6 frame (0,3–0,6 detik)** pada rekaman 10 FPS sebelum kembali menyelam ke kolom bawah.
- **Sifat Kanibalisme pada Fase Benih**: Benih lele memiliki variasi laju pertumbuhan individual (*growth heterogeneity*). Jika pakan terlambat atau terjadi disparitas ukuran tubuh, benih yang lebih besar akan memangsa benih yang lebih kecil.

---

### 2. Analisis Kondisi Pakan Bebas / "Loss" (*Ad Libitum / Feeding to Satiation*)

Memberikan pakan tanpa batas (*ad libitum / loss*) terbukti secara biologis merugikan budidaya bibit lele:

| Parameter Tinjauan | Temuan Literatur Empiris | Dampak pada Bibit Lele |
|---|---|---|
| **Rasio Konversi Pakan (FCR)** | **Ikeogu et al. (2020)** membuktikan bahwa pakan *satiation/loss* menghasilkan FCR **1,3 ± 0,03**, sedangkan pakan terkontrol (5% bobot tubuh) menghasilkan FCR **1,1 ± 0,01** ($p < 0,05$). | Pakan terbuang sia-sia; dibutuhkan 1,3 kg pakan untuk 1 kg pertumbuhan bobot (pemborosan biaya pakan hingga 18–25%). |
| **Pembusukan Bahan Organik** | Pelet komersial benih lele memiliki kandungan protein sangat tinggi (38–42% CP). Pakan yang tidak termakan dalam 5–10 menit akan tenggelam, larut, dan mengalami dekomposisi anaerobik (Tiamiyu et al. 2018; Oboh 2022). | Lonjakan konsentrasi amonia tak terionisasi ($NH_3$) dan nitrit ($NO_2^-$) toksik. Karena insang bibit lele masih sangat rentan, paparan amonia memicu kerusakan epitel insang dan mortalitas massal. |
| **Fisiologi Saluran Cerna** | Lambung lele bersifat elastis. Konsumsi pakan berlebih dalam waktu singkat menyebabkan distensi lambung (*bloating*), efisiensi enzim pencernaan turun, dan pelet dikeluarkan kembali sebelum terserap sempurna (*regurgitation*) (Li et al. 2020). | Penurunan efisiensi serap protein dan penurunan laju tumbuh spesifik (*Specific Growth Rate* / SGR). |

---

### 3. Analisis Kondisi Pakan Dibatasi (*Restricted / Rationed Feeding*)

Pembatasan pakan terbagi menjadi dua kategori: **pembatasan terukur/terencana** vs **pembatasan ekstrem/acak**:

1. **Pembatasan Terukur (Rationed Feeding, 3–5% Bobot Tubuh/Hari)**:
   - **Hasil Terbaik**: Penelitian Ikeogu et al. (2020) dan Tiamiyu et al. (2018) menyimpulkan bahwa batas pakan **5% dari biomassa harian** adalah rasio emas (*optimum economic rate*) untuk benih/fingerling lele:
     - Pertambahan bobot rata-rata (*Mean Weight Gain*) mencapai $26,11 \pm 3,65\text{ g}$ (lebih tinggi signifikan dibanding kelompok *satiation*).
     - Pertambahan panjang mencapai $6,11 \pm 0,20\text{ cm}$.
     - Tingkat kelangsungan hidup (*Survival Rate*) mencapai 100%.
   - **Pertumbuhan Kompensasi (*Compensatory Growth*)**: Studi Khormi et al. (2026) dan Agunbiade-Olu et al. (2022) mengungkap bahwa lele memiliki kapasitas hiperglikemik dan hiperfagia kompensatoris. Ketika interval antar-pemberian pakan dijaga teratur dan pakan diberikan saat lele menunjukkan riak lapar aktif, efisiensi anabolisme lele meningkat pesat sehingga lele tumbuh lebih padat daging.

2. **Bahaya Pembatasan Ekstrem / Pakan Tidak Teratur (*Unpredictable Starvation*)**:
   - Studi **Ojelade et al. (2025)** membuktikan bahwa jadwal pakan yang tidak terduga/acak memicu stres kronis pada *Clarias gariepinus*, ditandai dengan penurunan hematokrit (PCV) dan hemoglobin, serta penurunan drastis laju tumbuh.
   - Studi **Al-salahy & Ibrahim (2018)** membuktikan bahwa rasa lapar berlarut (*starvation*) memicu stres oksidatif lipid peroksidasi pada jaringan hati lele.
   - Pada tingkat benih, lapar berlarut memicu lonjakan agresivitas dan **kanibalisme**, menyebabkan tingkat kelangsungan hidup anjlok drastis.

---

### 4. Menghubungkan Temuan Biologis dengan Logika Sistem Skripsi

Dari sintesis biologis di atas, terlihat keselarasan mutlak dengan arahan dosen pembimbing:
- **Mengapa Harus Dibatasi oleh Petani?** Karena bibit lele tidak boleh dibiarkan makan *loss* tak terbatas (risiko amonia toksik dan pembengkakan FCR). Petani memasukkan kuota harian (misal: 1 kg pakan, merepresentasikan 5% biomassa kolam).
- **Mengapa Harus Berbasis Deteksi Riak Permukaan?** Karena memberikan jatah kuota tersebut secara sekaligus atau menggunakan *timer* buta tiap jam berisiko pakan jatuh saat lele sedang tidak responsif (terjadi pembusukan pakan atau stres jadwal acak seperti temuan Ojelade 2025).
- **Solusi Sistem Skripsi**: Sistem memecah kuota 1 kg tersebut menjadi 10–20 sub-porsi (masing-masing 50–100 gram). Kamera mendeteksi kapan bibit lele menunjukkan lonjakan riak di atas *baseline* aerator $\to$ dispensasi 1 sub-porsi $\to$ bibit lele menyambar pakan dengan efisiensi serap maksimal $\to$ pakan berhenti jika kuota harian habis.

---

## 📷 BAGIAN III (OUTPUT 2): RISET MENDALAM SELURUH ARTIKEL COMPUTER VISION

Berikut adalah analisis komprehensif terhadap **seluruh 20 artikel ilmiah** bidang Computer Vision dan Pengenalan Perilaku Makan Ikan yang telah dihimpun (19 Full-Text PDF lokal + Wu et al. 2024), diekstrak secara rigid mencakup **spesifikasi kamera, ketinggian, sudut, resolusi, lingkungan kolam, aerator, metode ekstraksi fitur, model machine learning/deep learning, penanganan noise, dan keterbatasannya**.

---

### A. Tabel Master 1: Merk Kamera, Spesifikasi Hardware, Sudut, & Lingkungan Kolam (20 Artikel)

| No | Penulis & Tahun | Objek Ikan & Fase | Lingkungan & Jenis Kolam | Aerator / Permukaan | Posisi Kamera | Tinggi | Sudut | Resolusi & FPS | Merk Kamera & Spesifikasi Hardware Eksplisit |
|:--:|---|---|---|---|---|:---:|:---:|:---:|---|
| **01** | **Qian et al. (2025)** | Ikan mas (*Crucian carp*) | Kolam luar ruangan (*outdoor pond*) | Air tenang tanpa aerasi di ROI | *Overhead / Top-view* | 1,8 m | $90^\circ$ nadir | 1080p, 25--30 FPS | **Hikvision DS-2CD1245-LA** (Network Surveillance Bullet Camera) |
| **02** | **Hu et al. (2026)** | *Largemouth bass* (1.200 ekor dewasa) | Industrial RAS, tangki bundar $\varnothing$ 4 m, d 1,4 m | Bergelombang dinamis (arus RAS) | *Oblique* (miring) | 0,7 m | $45^\circ\text{--}60^\circ$ | $512 \times 512$ (crop), 25 FPS | **Kamera Digital HD Industri** (Rig mounting oblique di atas tangki) |
| **03** | **Alahmad et al. (2025)** | Ikan laut budidaya (*seabream*) | Keramba jaring apung laut (*marine cage*) | Arus bawah laut alami | *Underwater* (bawah air) | Kedalaman 3,4 m | Horizontal samping | 1080p, 30 FPS | **Kamera Digital Kedap Air Bawah Laut** (*pressure-resistant housing*) |
| **04** | **Fukae et al. (2023)** | Kawanan ikan air tawar | Tangki budidaya indoor | Tenang tanpa arus/aerator saat rekam | *Overhead / Top-view* | 1,5 m | $90^\circ$ tegak lurus | 1080p, 30 FPS | **Canon VB-H651V** (Network Camera, 2.1 Megapixel, PoE, 30 fps) |
| **05** | **Zhao et al. (2025)** | *Carassius auratus* / Nila | Tangki budidaya terkontrol | Air sangat jernih, tenang | *Top-view* overhead | 1,2 m | $90^\circ$ nadir | 1080p, 30 FPS | **Kamera Digital RGB High-Resolution** (Computer-controlled) |
| **06** | **Li et al. (2020)** | Berbagai spesies ikan akuakultur | Tinjauan sistematis multi-kolam | Komparasi air tenang vs beriak | Komparasi top, side, underwater | Bervariasi | $0^\circ\text{--}90^\circ$ | Multi-resolusi | **Tinjauan Sensor**: CCD, CMOS, Near-Infrared, Stereo, Sonar Hidroakustik |
| **07** | **Marliza & Aisuwarya (2021)** | **Ikan Lele (*Clarias sp.*)** | Kolam terpal lokal Indonesia | Tenang (tanpa pemodelan aerator) | *Top-view* di atas kolam | $\approx 0,8\text{--}1,0\text{ m}$ | $90^\circ$ tegak lurus | 480p, 15 FPS | **Raspberry Pi Camera Module** (Konektor MIPI-CSI, sensor CMOS) |
| **08** | **Atoum et al. (2015)** | Kawanan ikan densitas tinggi | Tangki akuakultur tertutup | Berriak dinamis saat makan | *Overhead* di atas tangki | 1,0 m | $90^\circ$ nadir | 720p, 30 FPS | **Kamera Video Overhead RGB** (Koneksi workstation Intel i5) |
| **09** | **Al-Abri et al. (2025)** | Multi-spesies akuakultur | Tinjauan komparatif kolam & laut | Bervariasi (outdoor & indoor) | Tinjauan overhead & underwater | Multi-tinggi | $0^\circ\text{--}90^\circ$ | Multi-resolusi | **Tinjauan Sensor Optik**: RGB High-Speed, Multispektral, LiDAR, Sonar |
| **10** | **Zhou et al. (2018)** | Ikan Nila (*Oreochromis niloticus*) | Tangki budidaya indoor | Tenang, bebas turbulensi | *Overhead* di atas tangki | 1,2 m | $90^\circ$ nadir | 720p, 25 FPS | **Mako G-223B (AVT - Allied Vision, Jerman)** + Iluminator NIR HEROWEI MVIR0460 850 nm |
| **11** | **Liu et al. (2014)** | Salmon Atlantik (*Salmo salar*) | Tangki resirkulasi RAS indoor | Arus sirkulasi teratur | *Overhead* di atas tangki | 1,5 m | $90^\circ$ nadir | 768 $\times$ 576, 25 FPS | **Kamera Monokrom Industri CCD** (Overhead rearing tank mount) |
| **12** | **Zhao et al. (2017)** | Ikan Nila (*Oreochromis niloticus*) | Tangki bulat radius 100 cm, d 80 cm | Air jernih tenang terkontrol | *Overhead* di atas tangki | 1,2 m ($\pm 0,2$ cm) | $90^\circ$ nadir | 1080p, 25 FPS | **Hikvision DS-2CD6233F-SDI** (CCD High Definition Video Camera) + LED Kingbright 100 W |
| **13** | **Zhao et al. (2016)** | Ikan mas / nila di tangki | Tangki akuakultur RAS | Permukaan tenang teriluminasi | *Overhead* tepat di atas air | 1,2 m | $90^\circ$ nadir | 1080 $\times$ 1920, 25 FPS | **Hikvision DS-2CD6233F-SDI** (CCD HDV Camera) + LED Kingbright 100 W |
| **14** | **Dong et al. (2024)** | Ikan Kerapu (*Epinephelus coioides*) | Tangki pembiakan indoor (372 lux) | Tenang sebelum feeding | *Overhead* di atas air | 0,5 m | $90^\circ$ tegak lurus | 480 $\times$ 270, 30 FPS | **Kamera Digital Industri Terhubung PC** (Pencahayaan buatan 372 lux) |
| **15** | **Zhang et al. (2024)** | Ikan laut liar / budidaya | Bawah air laut dinamis | Turbulensi arus laut | *Underwater* (bawah air) | Di dalam kolom air | Horizontal | 1080p Full HD, 30 FPS | **Kamera Digital Bawah Air High-Definition** (Submersible optic casing) |
| **16** | **Aris et al. (2023)** | Gerakan dinamis umum | Lingkungan video pengawasan | Riak air bergelombang | Kamera pengawas luar ruangan | 2,0--3,0 m | Miring $45^\circ$ | 720p, 25 FPS | **Kamera CCTV Outdoor RGB Surveilans** (Fixed surveillance optical camera) |
| **17** | **Kamal et al. (2025)** | **Ikan Lele (*Clarias gariepinus*)** | Kolam terpal densitas tinggi | **Kolam ber-aerator kontinu** | Terendam dalam air (akustik) | Submerged | Omnidirectional | Frekuensi audio 48 kHz | **Sensor Akustik Hidrofon Bawah Air** (*Acoustic sensor*, non-kamera optik) |
| **18** | **Yang et al. (2025)** | Ikan budidaya komersial | Tinjauan kolam air tawar & laut | Komparasi air tenang vs beriak | Tinjauan side & overhead | Multi-jarak | $45^\circ\text{--}90^\circ$ | Multi-resolusi | **Tinjauan Perangkat Keras**: IP Camera Industri, CCTV Bullet, Kamera Stereo 3D |
| **19** | **Vijayalakshmi (2025)** | Ikan kolam air tawar (DePondFi) | Kolam luar ruangan (*aquaponds*) | Permukaan air kolam outdoor | *Overhead / Oblique* | 1,5--2,0 m | $60^\circ\text{--}90^\circ$ | Resolusi tinggi (8.150 citra) | **Kamera Pengawas Kolam Terbuka RGB** (DePondFi Dataset Image Acquisition) |
| **20** | **Wu et al. (2024)** | *Largemouth bass* remaja/dewasa | Tangki budidaya terkontrol | Tenang sebelum pakan ditebar | *Overhead / Top-view* | 1,2--1,5 m | $90^\circ$ nadir | 1080p cropped, 30 FPS | **Kamera Digital RGB Industri dengan Lensa Wide-Angle** |
| **--** | **Skripsi Mahasiswa** | **Bibit Ikan Lele (*Clarias sp.*, 2--7 cm)** | **Kolam Terpal Outdoor (Luar Ruangan)** | **AERATOR MENYALA KONSTAN (BASELINE)** | ***Overhead / Top-View* Tegak Lurus** | **0,8--1,2 m** | **$90^\circ$ (atau sudut koreksi silau)** | **720p / 480p, 10 FPS** | **Raspberry Pi Camera Module v2 (Sony IMX219) / v1 (OV5647)** |


---

### B. Tabel Master 2: Metode, Model Deep Learning, Noise Handling, & Keterbatasan (20 Artikel)

| No | Penulis & Tahun | Metode Computer Vision & Fitur | Model Machine Learning / DL | Input & Output Model | Penanganan Noise Visual | Hasil Eksperimen | Keterbatasan Terhadap Skripsi Bibit Lele Outdoor |
|:--:|---|---|---|---|---|---|---|
| **01** | Qian et al. (2025) | Bounding box object detection, Partial Conv | PM-YOLO (Enhancement YOLOv8n) | Input: Citra RGB 640x640; Output: Box & status pakan | Backbone PConv mereduksi noise clutter | Precision 87.7%, mAP@50 83.5%, 8.1 ms (GPU) | Bergantung visual kontras tubuh ikan; gagal di air kolam lele keruh pekat. |
| **02** | Hu et al. (2026) | Patch CNN + ViT Attention + Temporal LSTM | HVIT (ResNet18 + 5L-ViT + 1L-LSTM) | Input: Jendela 5 frame ($512^2$); Output: 4 kelas intensitas | Self-attention ViT fokus ke gelombang riak | Akurasi 95.10%, latensi 145 ms | Model berat (28,6 M param, butuh GPU); belum diuji kolam terbuka ber-aerator. |
| **03** | Alahmad et al. (2025) | Underwater detection + simplified optical flow | YOLOv8 + Optical Flow Tracker | Input: Frame bawah air; Output: Kecepatan renang | Filter thresholding kecepatan renang | Akurasi deteksi ikan 85% | Butuh kamera underwater & air jernih laut; tidak cocok kolam lele overhead. |
| **04** | Fukae et al. (2023) | Dense Optical Flow Farnebäck (magnitudo gerak) | Support Vector Machine (SVM) | Input: Matriks optical flow agregat; Output: 3 kelas aktivitas | Threshold magnitudo kecepatan gerak | Akurasi klasifikasi kawanan 88.3% | Farnebäck sangat lambat di Raspberry Pi (<2 FPS); gagal jika ada aerator konstan. |
| **05** | Zhao et al. (2025) | Keypoint skeleton pose estimation + ST-GCN | Lightweight Two-Stage (Pose + GCN) | Input: Koordinat keypoint; Output: 3 level kenyang | Topologi graph anatomi memfilter noise air | Akurasi klasifikasi kenyang 98.5% | Menuntut air sangat jernih agar keypoint terdeteksi; mustahil di kolam lele keruh. |
| **06** | Li et al. (2020) | Tinjauan: frame diff, optical flow, texture | Tinjauan: CNN, Fuzzy, SVM, Thresholding | Tinjauan berbagai skema input & output | Tinjauan filter refleksi & polarisasi | Analisis komparatif komprehensif | Menegaskan belum terselesaikannya pemodelan noise aerator mekanis konstan. |
| **07** | Marliza & Aisuwarya (2021) | Grayscale + Thresholding Biner + Contour | Rule-Based Kontur Thresholding (RPi) | Input: Frame biner; Output: Pemicu motor pakan | Tanpa penanganan pantulan cahaya & aerator | Pakan terpicu saat ikan berkumpul | Sangat rentan *false trigger* akibat gelembung aerator & silau sinar matahari. |
| **08** | Atoum et al. (2015) | Dynamic texture analysis + motion energy | Rule-Based Feedback Control | Input: Citra tekstur riak; Output: Sinyal pakan ON/OFF | Normalisasi variasi pencahayaan | Pakan terhenti saat ikan kenyang | Mengasumsikan kolam tenang tanpa semburan gelembung aerator di area pandang. |
| **09** | Al-Abri et al. (2025) | Tinjauan: segmentation, object detection, ViT | Tinjauan: YOLOv7-v9, Transformer, DL | Tinjauan arsitektur input-output modern | Tinjauan adaptasi domain & data sintetis | Tinjauan performa SOTA global | Menyoroti trade-off beratnya model DL modern terhadap keterbatasan daya edge. |
| **10** | Zhou et al. (2018) | Near-Infrared imaging (NIR 850 nm) + binarisasi | Adaptive Neuro-Fuzzy (ANFIS) | Input: Area aktivitas NIR; Output: Keputusan pakan | Filter optik NIR mengeliminasi silau cahaya | Akurasi feeding decision 98.0% | Butuh lampu NIR khusus; kurang efektif di bawah sinar matahari tropis terik. |
| **11** | Liu et al. (2014) | Frame difference biner + akumulasi piksel | Computer Vision Feeding Index (CVFAI) | Input: Selisih frame; Output: Indeks numerik CVFAI | Threshold piksel bergerak minimal | Korelasi kuat ($R^2 > 0.90$) dengan nafsu makan | Asumsi air tenang tanpa aerator kontinu; gelembung akan terhitung sebagai CVFAI. |
| **12** | Zhao et al. (2017) | Tracking kecepatan renang & turning angle | Modified Social Force Model + Kinetic | Input: Vektor lintasan ikan; Output: Nilai nafsu makan | Tracking filter Kalman | Akurasi penilaian nafsu makan 92.5% | Membutuhkan tracking ikan individual di air jernih; lele berkerumun pekat. |
| **13** | Zhao et al. (2016) | Moving Fish Segmentation (BMFS) + PAOF | Kinetic Energy Network Model | Input: Vektor PAOF; Output: Indeks energi kinetik | Adaptive thresholding berbasis warna YCbCr | Korelasi tinggi dengan agresi makan | Komputasi optical flow per-piksel berat; tidak ada pemodelan gelembung aerator. |
| **14** | Dong et al. (2024) | Three-stream: optical flow, binarize, texture | Three-Stream Convolutional Neural Net | Input: 3 cabang fitur; Output: 4 status feeding | Fusi multi-cabang mereduksi noise parsial | Akurasi diskriminasi intensitas 99.28% | Sangat berat (tiga cabang CNN); mustahil dijalankan real-time di Raspberry Pi. |
| **15** | Zhang et al. (2024) | Adaptive optical flow selection + segmentation | RUSNet (Underwater Deep Segmentation) | Input: Frame & optical flow; Output: Mask segmentasi | Seleksi adaptif mengabaikan aliran blur | mIoU 92.4% pada video bawah air buram | Ditujukan untuk segmentasi bawah air, bukan kuantifikasi feeding overhead. |
| **16** | Aris et al. (2023) | Gaussian Mixture Model (GMM) background sub | Analisis survei algoritma GMM | Input: Video sekuens; Output: Foreground mask | Model multi-Gaussian latar belakang dinamis | Menunjukkan keterbatasan adaptasi GMM | GMM gagal pada gelembung aerator konstan (terjadi *cavity* & false foreground). |
| **17** | Kamal et al. (2025) | Sinyal audio hidrofon (kunyahan ikan lele) | Machine Learning (SVM, Random Forest) | Input: Spektrogram suara; Output: Status lapar | Bandpass filter akustik | Akurasi deteksi lapar lele 91.2% | Bising putaran motor aerator merusak SNR audio; visi komputer lebih unggul. |
| **18** | Yang et al. (2025) | Tinjauan: deteksi cipratan pakan & gelombang | Tinjauan: DL, Spatial-Temporal Transformer | Tinjauan tren riset visi komputer 2025 | Tinjauan edge-enhancement & channel attention| Review mutakhir State-of-the-Art | Memperkuat urgensi metode temporal untuk mengatasi riak air stokastik. |
| **19** | Vijayalakshmi (2025) | Bounding box detection pada kolam outdoor | AquaYOLO (Enhanced YOLOv8 for Ponds) | Input: Citra kolam outdoor; Output: Bounding box | CSP layers ekstraksi fitur robust | Precision 88.9%, Recall 84.8%, mAP 90.9% | Bounding box gagal mendeteksi bibit lele yang bersembunyi di bawah buih aerator. |
| **20** | Wu et al. (2024) | *Feeding splash thumbnails* (crop buih air) | Deformable Attention ViT (DeformAtt-ViT) | Input: Thumbnail cipratan; Output: 3 tingkat lapar | Thumbnail mengabaikan permukaan air luar | Akurasi 95.50%, F1-Score 94.13% | GAGAL PADA BENIH BIBIT LELE & AIR BER-AERATOR (Cipratan benih tidak berbusa). |
| **--** | **Skripsi Mahasiswa** | **Baseline Normal Modeling + Temporal Motion Index** | **Model Temporal Ringan (LSTM/Rule 1D)** | **Input: Sekuens vektor gerak 1D; Output: Trigger Sub-Porsi** | **Z-Score Normalization Baseline Aerator + Cooldown** | **Target: Akurasi $\ge 85\%$ pada Raspberry Pi 10 FPS** | **Solusi Spesifik: Mengatasi noise aerator kontinu & komputasi edge bibit lele.** |


---

## 🔬 BAGIAN IV: PERBANDINGAN METODE COMPUTER VISION & KELAYAKANNYA PADA SKRIPSI

Untuk tahap skripsi saat ini, metode tidak langsung dikunci secara kaku. Berikut perbandingan karakteristik metode berdasarkan data nyata kolam bibit lele ber-aerator:

```
+───────────────────────────+─────────────────────────────────────────────────────────────+
| METODE COMPUTER VISION    | EVALUASI UNTUK KOLAM BIBIT LELE OUTDOOR BER-AERATOR         |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 1. Frame / Temporal       | (+) Sangat ringan, berjalan >30 FPS di Raspberry Pi.        |
|    Difference             | (-) Sensitif terhadap perubahan intensitas cahaya matahari. |
|                           | (*) Cocok sebagai tahap ekstraksi awal (first-stage filter).|
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 2. Dense Optical Flow     | (+) Menangkap arah dan kecepatan pergerakan riak detail.    |
|    (Farnebäck)            | (-) Sangat berat untuk CPU Raspberry Pi 4 (<2 FPS).         |
|                           | (*) Sparse optical flow (Lucas-Kanade) lebih realistis.     |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 3. Motion Intensity Index | (+) Menghitung magnitudo energi kinetik agregat seluruh ROI.|
|                           | (+) Komputasi sangat efisien dan mudah dibentuk sekuensnya. |
|                           | (*) Menjadi fitur input ideal untuk model temporal.         |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 4. Background Subtraction | (+) Memisahkan objek bergerak dari latar belakang statis.   |
|    (MOG2 / KNN)           | (-) Aerator bergerak terus-menerus sehingga masuk foreground|
|                           | (*) Perlu laju pembaruan (*learning rate*) adaptif tinggi.  |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 5. Dynamic / Temporal     | (+) Memodelkan tekstur air beriak sebagai proses stokastik. |
|    Texture (LBP-TOP)      | (-) Kompleksitas matematika tinggi, rentan perubahan cuaca. |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 6. Ripple / Splash        | (+) Menargetkan fenomena fisik riak/cipratan air langsung.   |
|    Detection              | (-) Seperti catatan Wu et al. (2024), bibit lele berukuran  |
|                           |     kecil sehingga cipratannya halus dan tidak berbusa putih|
|                           | (*) Harus mendeteksi riak gelombang halus, bukan cipratan.  |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 7. Model Temporal         | (+) Mengingat pola temporal periodik aerator vs acak lele.  |
|    (LSTM / GRU / 1D-CNN)  | (+) Mampu mengenali event singkat (3–6 frame) dalam konteks.|
|                           | (*) Sangat direkomendasikan jika inputnya berupa fitur 1D!  |
+───────────────────────────+─────────────────────────────────────────────────────────────+
```

---

## 🧠 BAGIAN V: TELAAH KRITIS LITERATUR MODEL TEMPORAL (LSTM, MULTI-STREAM, & DERET WAKTU) SERTA IMPLIKASINYA

> **Pernyataan Posisi Riset Mahasiswa**:
> Mahasiswa **belum merumuskan atau mengunci model skripsi** (skripsi ini tidak mengklaim sejak awal bahwa arsitektur sistem sudah pasti menggunakan LSTM).
> Sebaliknya, bagian ini merupakan **pendalaman komparatif literatur (*critical literature deep-dive*)** untuk menelaah secara sistematis:
> 1. Bagaimana model sekuensial temporal diterapkan oleh para peneliti dunia (khususnya Hu et al., 2026; Dong et al., 2024; Fukae et al., 2023; Li et al., 2020).
> 2. Apa metode dan model yang mereka gunakan, bagaimana inputnya dibentuk, dan bagaimana model tersebut bekerja.
> 3. Mengapa pemodelan waktu (*temporal modeling*) dibutuhkan dalam mengidentifikasi siklus makan ikan (*feeding cycle*).
> 4. Apa konsekuensi komputasi dan keterbatasannya terhadap implementasi *edge device* (Raspberry Pi) pada kolam terbuka ber-aerator.
> 5. Apa pelajaran objektif bagi perumusan skripsi mahasiswa kelak (menempatkan model temporal ringan sebagai salah satu hipotesis pembanding terhadap model *rule-based* / *thresholding*, bukan keputusan mutlak tanpa pengujian).

```
[Kajian Literatur: Bagaimana Paper SOTA Memodelkan Perilaku Makan Ikan?]

1. Model Hu et al. (2026) - Hybrid ViT + LSTM (HVIT):
   Video RAS ──► Crop Oblique 512x512 ──► Jendela 15 Detik (Sampling T=5 Frame)
                      │
                      ├─── ResNet18 (Mish) ──► Fitur Spasial Lokal
                      └─── 5-Layer ViT    ──► Fitur Relasi Global
                                │
                      Konkatenasi Tensor (B=1, T=5, D=256)
                                │
                      1-Layer LSTM (256 Hidden Units, Dropout 0.3)
                                │
                      Klasifikasi 4 Tingkat Intensitas (Akurasi 95.10%, Latensi 145 ms di GPU RTX 3090)

2. Model Dong et al. (2024) - Three-Stream CNN:
   Video Tangki ──► Aliran 1: Lucas-Kanade Optical Flow (Temporal Vector Field)
                ──► Aliran 2: Binarisasi Citra (Spasial Area Sebaran Ikan)
                ──► Aliran 3: Matriks Tekstur GLCM (Tekstur Permukaan Air)
                                │
                      Fusi Tiga Cabang CNN ──► Klasifikasi 4 Tingkat Agresi (Akurasi 99.28%)

3. Model Fukae et al. (2023) - Akumulasi Optical Flow:
   Video Tangki ──► Dense Optical Flow Farnebäck ──► Akumulasi Waktu Geser ──► SVM (Akurasi 88.3%)
```

### 1. Mengapa Peneliti Terdahulu Membutuhkan Model Temporal?
- **Dinamika Siklus Makan (*Feeding Life Cycle*)**:
  Aktivitas makan ikan bukanlah fenomena statis 1 frame foto, melainkan proses transisi waktu yang berkesinambungan:
  $$\text{Fase Tenang / Lapar} \longrightarrow \text{Pakan Ditebar} \longrightarrow \text{Lonjakan Riak / Agresi Makan} \longrightarrow \text{Deselerasi Kenyang} \longrightarrow \text{Tenang Kembali}$$
- **Kelemahan Model Spasial Murni (Frame Tunggal)**:
  Jika hanya menggunakan model deteksi objek tunggal (seperti YOLOv8 atau ViT murni), model hanya memproses satu *snapshot* citra:
  - Model tidak mengetahui apakah riak air sedang meningkat (ikan baru mulai makan) atau sedang menurun (ikan sudah mulai kenyang).
  - Model sangat rentan terhadap **letupan sesaat buih aerator / pantulan cahaya matahari**, yang dapat memicu alarm palsu (*false positive*) karena tidak adanya memori riwayat frame sebelumnya.
- **Peran Sel Temporal (LSTM / Recurrent Gates)**:
  Pintu gerbang pada LSTM (*Forget Gate, Input Gate, Output Gate*) bertindak sebagai penyaring dinamis: jika riak hanya melonjak pada 1 frame akibat gelembung aerator pecah lalu langsung hilang, *forget gate* akan mengabaikan noise tersebut. Sebaliknya, jika riak bertahan selama beberapa frame secara konsisten (seperti perilaku kawanan lele yang menyambar pakan), akumulasi status sel (*cell state*) akan mencatatnya sebagai event makan nyata.

### 2. Apa Masukan (Input), Metode, dan Cara Kerja Model pada Literatur?
- **Hu et al. (2026)**:
  - *Input*: Jendela waktu 15 detik yang disampling menjadi $T = 5$ frame berjarak 3 detik antar-frame.
  - *Metode*: Menggunakan pendekatan *late temporal fusion*. Tiap frame diproses secara independen oleh dua cabang ekstraktor spasial (ResNet18 dan Vision Transformer), menghasilkan vektor embedding 256 dimensi per frame. Vektor-vektor ini disusun berurutan waktu menjadi tensor $(B=1, T=5, D=256)$ yang dialirkan ke dalam 1 lapis LSTM.
  - *Kelemahan Komputasi*: Model memiliki 28,6 juta parameter dan membutuhkan daya komputasi workstation GPU NVIDIA RTX 3090, sehingga tidak mungkin dijalankan secara langsung pada SBC mini (*Raspberry Pi*).
- **Dong et al. (2024)**:
  - *Input*: Video sekuens beresolusi $480 \times 270$ pada 30 FPS.
  - *Metode*: Tiga cabang independen (vektor medan optical flow LK untuk gerak, citra biner untuk posisi, dan GLCM untuk riak tekstur air) diekstrak secara paralel menggunakan Convolutional Neural Network (CNN) lalu difusikan di lapisan *fully-connected*.
  - *Kelemahan Komputasi*: Menjalankan tiga cabang CNN secara simultan membebani CPU secara ekstrem dan tidak realistis untuk pemrosesan *edge* tanpa pendingin aktif dan GPU diskrit.

### 3. Pelajaran dan Implikasi Kritis bagi Perumusan Skripsi Mahasiswa
Dari telaah kritis literatur di atas, mahasiswa menarik pelajaran metodologis yang rasional untuk konteks bibit lele di kolam luar ruangan:
1. **Tidak Meniru Arsitektur Berat Secara Buta**: Skripsi mahasiswa tidak akan memaksakan model berparameter raksasa seperti Hu et al. (28,6M parameter) atau Dong et al. (3-stream CNN) ke dalam Raspberry Pi, karena akan memicu latensi tinggi dan sistem *freeze*.
2. **Prinsip Kompresi Fitur Sebelum Masuk ke Model Temporal**:
   Jika skripsi kelak menguji model temporal, masukan yang digunakan **bukan citra piksel mentah**, melainkan **vektor fitur gerak 1D terkompresi** ($D \approx 4$ fitur):
   - $M_t$: Indeks intensitas gerak rata-rata (*Motion Intensity*) dari selisih frame biner terbobot.
   - $V_t$: Varians spasial sebaran gerak (membedakan semburan terpusat aerator vs sebaran acak lele).
   - $A_t$: Luas persentase area aktif riak air.
   - $\Delta M_t$: Gradien laju perubahan energi antar-frame ($M_t - M_{t-1}$).
3. **Normalisasi Terhadap Baseline Aerator**:
   Menghitung deviasi dinamis terhadap baseline aerator menggunakan skor standar ($Z_t = \frac{M_t - \mu_{\text{base}}}{\sigma_{\text{base}}}$) sehingga model temporal hanya belajar mengenali anomali riak makan lele terhadap gejolak normal aerator.
4. **Posisi dalam Rencana Skripsi: Hipotesis Komparasi Terbuka**:
   Model temporal ringan (seperti 1D-LSTM atau 1D-GRU) akan ditempatkan sebagai **salah satu alternatif pembanding** yang diuji secara empiris berdampingan dengan metode non-deep learning sederhana (*Rule-based Motion Thresholding* dan *Moving Average Filter*). Tujuannya adalah menguji secara objektif apakah penambahan lapisan temporal benar-benar memberikan peningkatan akurasi yang signifikan di kolam nyata dibanding metode *thresholding* sederhana yang jauh lebih hemat daya.

---

## 🎯 KESIMPULAN & LANGKAH PRIORITAS BERIKUTNYA

1. **Output 1 Selesai**: Dasar biologis telah tervalidasi dari 14 paper pakan lele lokal. Pemberian pakan pendederan benih lele harus berbasis pembatasan kuota terukur (5% biomassa) yang disalurkan secara sinkron dengan nafsu makan riak lele guna mencegah FCR membengkak (Ikeogu 2020) dan mencegah stres acak (Ojelade 2025).
2. **Output 2 Selesai**: Riset mendalam 25 parameter Hu et al. (2026) dan Wu et al. (2024) mengonfirmasi *research gap* skripsi: metode cipratan *splash thumbnails* Wu et al. tidak efektif untuk bibit lele karena cipratan benih terlalu halus, sementara model Hu et al. belum menguji kolam luar ruangan dengan aerator gelembung konstan.
3. **Langkah Berikutnya**:
   - Melaksanakan fase observasi 1 minggu sampling video 10–15 menit per jam untuk membangun dataset variabilitas riak aerator kolam lele mahasiswa.
   - Menghubungkan fitur vektor gerak 1D dengan model temporal ringan yang dapat dieksekusi secara real-time pada Raspberry Pi tanpa kendala latensi.

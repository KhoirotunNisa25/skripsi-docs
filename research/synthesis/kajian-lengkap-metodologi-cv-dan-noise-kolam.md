# 📑 KAJIAN KOMPREHENSIF METODOLOGI COMPUTER VISION & ELIMINASI DERAU (NOISE) PADA DETEKSI AKTIVITAS MAKAN BIBIT IKAN LELE DI KOLAM TERPAL OUTDOOR BER-AERATOR

**Penulis / Peneliti**: Khoirotun Nisa  
**Dosen Pembimbing**: Dr. Ulla Delfana Rosiani, ST., MT.  
**Program Studi**: D4 Teknik Informatika, Jurusan Teknologi Informasi, Politeknik Negeri Malang  
**Topik Skripsi**: Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar Berbasis *Computer Vision* pada Kolam Pendederan *Outdoor* Ber-Aerator Kontinu  

---

## 📌 RINGKASAN EKSEKUTIF (*EXECUTIVE SUMMARY*)

Dokumen ini disusun sebagai panduan akademik dan teknis terlengkap untuk dipelajari, dipahami, dan dijadikan rujukan utama dalam penyusunan **Bab 2 (Tinjauan Pustaka)** dan **Bab 3 (Metodologi Penelitian)** proposal/skripsi. Dokumen ini mengintegrasikan:
1. **Analisis Kondisi Lapangan Riil** berdasarkan setup kamera *overhead close-range* di atas permukaan kolam terpal ber-aerator (merujuk langsung pada citra setup aktual `image.png`).
2. **Sintesis Kritis 20 Literatur Ilmiah Global** (Computer Vision, Akuakultur Presisi, dan Perilaku Makan Ikan) untuk memetakan keterbatasan State-of-the-Art dan mempertegas posisi kebaruan (*novelty*) skripsi.
3. **Formulasi Matematis Pemisahan Gerakan Ikan vs Derau Aerator** menggunakan pemodelan *Dynamic Spatial-Temporal Baseline* dan normalisasi skor standar ($Z$-Score).
4. **Strategi Eliminasi Derau Lingkungan Luar Ruangan (*Outdoor Noise Reduction*)** terhadap pantulan silau cahaya matahari (*sun glint*), daun rontok, dan bayangan burung.
5. **Kuantifikasi Perubahan Piksel Menjadi Skor Indeks Aktivitas Makan (*Feeding Activity Index / FAI*)** yang menghubungkan sinyal video dengan keputusan kendali aktuator pakan.
6. **Desain Sistem Terintegrasi & Logika Kontrol Aktuator Servo (PCA9685)** berbasis *Finite State Machine* (FSM) yang taat pada batasan kuota pakan harian petani (*daily feed quota budgeting*).

---

## 📸 BAGIAN 1: ANALISIS VISUAL SETUP AKTUAL KAMERA DI ATAS AIR (BEDAH CITRA `image.png`)

Berdasarkan dokumentasi aktual kolam terpal pendederan mahasiswa pada berkas `image.png`, terdapat karakteristik fisik dan optik yang sangat spesifik yang membedakan penelitian ini dari seluruh penelitian visi komputer terdahulu di dunia:

```
                  ┌──────────────────────────────┐
                  │   Kamera Logitech Brio 100   │
                  │   (Resolusi 720p @ 10 FPS)   │
                  └──────────────┬───────────────┘
                                 │
                     Jarak Dekat │ h ≈ 30 – 50 cm
                     Sudut Top   │ θ ≈ 80° – 90° (Nadir)
                                 ▼
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   [Permukaan Air Kolam]:
    - Latar Belakang Dinding Terpal Biru (Atas Frame)
    - Buih/Gelembung Udara Melayang dari Percabangan Selang Y
    - Pantulan Cahaya Langit (Specular Reflection)
    - Air Gelap Keruh Khas Pendederan Lele
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

### 1.1 Karakteristik Optik Berjarak Sangat Dekat (*Close-Range Overhead*)
* **Jarak Kamera ke Air ($h \approx 30\text{--}50\text{ cm}$)**: 
  Sebagian besar literatur global menempatkan kamera pada tiang tinggi ($h = 1,2\text{--}1,8\text{ meter}$, seperti Qian et al. 2025; Hu et al. 2026; Zhou et al. 2018). Pada jarak jauh tersebut, riak halus bibit lele akan melebur dan hilang menjadi noise buram. 
  Sebaliknya, pada setup mahasiswa (`image.png`), penempatan kamera sangat dekat dengan permukaan air memberikan **keuntungan resolusi spasial tinggi (*high spatial resolution*)**:
  * Buih mikro dan gelembung berdiameter $2\text{--}10\text{ mm}$ terproyeksikan ke sensor kamera dengan diameter puluhan piksel.
  * Setiap letupan buih dan riak gelombang mikro saat benih lele menyambar pelet pakan **terlihat sangat tajam dan jelas**, tidak hilang oleh blur jarak jauh.
* **Tantangan Bidang Pandang (*Field of View / FOV*)**:
  Karena jarak kamera sangat dekat, sepertiga bagian atas bingkai citra menangkap **lipatan dinding terpal biru kolam** dan gantungan selang aerator berbentuk cabang Y. Oleh karena itu, langkah pertama pemrosesan citra wajib melakukan **Pemotongan Wilayah Minat (*Region of Interest / ROI Masking*)** untuk membuang dinding terpal dan hanya menganalisis bidang permukaan air aktif.

### 1.2 Fenomena Visual Buih Aerator vs Permukaan Air Kolam
Pada `image.png`, permukaan air kolam terpal menampilkan fenomena visual yang nyata:
1. **Buih Aerator**: Gelembung udara yang keluar dari batu aerasi di dasar kolam naik ke permukaan dan meletup, membentuk cincin/cakram lingkaran putih berkilau (*specular highlights*) yang melayang dan pecah di permukaan air gelap.
2. **Pantulan Spekular (*Sun Glint*)**: Permukaan air bertindak sebagai cermin parsial yang memantulkan cahaya langit dan awan, menghasilkan gradien terang-gelap di permukaan kolam.
3. **Kekeruhan Air (*Turbidity*)**: Air kolam berwarna hijau kecokelatan pekat akibat fitoplankton dan feses bibit lele. Tubuh bibit lele berukuran $2\text{--}7\text{ cm}$ tidak dapat terlihat saat berada di bawah kedalaman air $> 3\text{ cm}$. Namun, **saat lapar, benih lele memecah permukaan air untuk menyambar pakan**, menciptakan semburan riak mikro dan buih sesaat yang kontras di atas permukaan.

---

## 🔬 BAGIAN 2: SINTESIS KRITIS 20 ARTIKEL LITERATUR GLOBAL & PENETAPAN GAP PENELITIAN

Tabel berikut menyajikan pemetaan komparatif terhadap 20 literatur kunci Computer Vision dan Akuakultur Presisi untuk membandingkan pendekatan mereka dengan kondisi riil skripsi mahasiswa:

### 2.1 Matriks Komparasi 20 Literatur Terhadap Parameter Skripsi

| No | Penulis & Tahun | Objek Ikan & Lingkungan | Setup Kamera & Jarak | Metode & Model Komputasi | Penanganan Noise | Hasil Evaluasi | Keterbatasan Kritis Terhadap Skripsi Mahasiswa |
|:--:|---|---|---|---|---|---|---|
| **01** | **Qian et al. (2025)** | Ikan mas, kolam outdoor | Top-view, $h = 1,8\text{ m}$ | PM-YOLO (YOLOv8n + PConv) | PConv reduksi clutter | Precision 87.7%, mAP 83.5% | Mengandalkan kontras fisik tubuh ikan di air jernih; gagal di kolam lele keruh pekat. |
| **02** | **Hu et al. (2026)** | *Largemouth bass*, tangki RAS | Miring $45^\circ$, $h = 0,7\text{ m}$ | HVIT (ResNet18 + ViT + LSTM) | Self-attention ViT | Akurasi 95.10%, latensi 145 ms | Model raksasa (28,6M parameter), butuh GPU RTX 3090; tidak bisa jalan di Raspberry Pi. |
| **03** | **Alahmad et al. (2025)** | Ikan laut, keramba laut | Bawah air, $d = 3,4\text{ m}$ | YOLOv8 + Optical Flow Tracker | Filter thresholding kecepatan | Akurasi deteksi 85% | Butuh kamera underwater mahal & air jernih laut; tidak cocok kolam lele terpal. |
| **04** | **Fukae et al. (2023)** | Kawanan ikan, tangki indoor | Top-view, $h = 1,5\text{ m}$ | Dense Optical Flow Farnebäck + SVM | Threshold magnitudo gerak | Akurasi klasifikasi 88.3% | Optical flow Farnebäck sangat lambat di CPU Raspi (<2 FPS); gagal jika aerator aktif konstan. |
| **05** | **Zhao et al. (2025)** | *Carassius auratus*, tangki jernih | Top-view, $h = 1,2\text{ m}$ | Keypoint Pose + ST-GCN | Topologi graph anatomi | Akurasi kenyang 98.5% | Menuntut air sangat jernih agar kerangka tulang ikan terbaca; mustahil di kolam terpal keruh. |
| **06** | **Li et al. (2020)** | Multi-spesies akuakultur | Tinjauan multi-posisi | Tinjauan sistematis metode CV | Filter polarisasi & refleksi | Analisis komparatif global | Menegaskan bahwa pemodelan noise semburan gelembung aerator belum terpecahkan. |
| **07** | **Marliza & Aisuwarya (2021)**| **Lele (*Clarias sp.*), kolam terpal** | Top-view, $h \approx 1,0\text{ m}$ | Grayscale + Threshold Biner (RPi) | Tanpa filter aerator & silau | Pakan terpicu saat ikan kumpul | Sangat rentan *false alarm* akibat buih aerator dan silau matahari; tanpa kuota harian. |
| **08** | **Atoum et al. (2015)** | Kawanan ikan, tangki indoor | Top-view, $h = 1,0\text{ m}$ | Dynamic Texture Analysis + Energy | Normalisasi pencahayaan | Pakan berhenti saat kenyang | Mengasumsikan kolam tenang tanpa aerator aktif terus-menerus di area pandang. |
| **09** | **Al-Abri et al. (2025)** | Tinjauan akuakultur global | Tinjauan komparatif | Tinjauan YOLOv7--v9, Transformer | Domain adaptation | Analisis performa SOTA | Menyoroti disparitas antara kompleksitas model DL modern dan keterbatasan daya komputasi edge. |
| **10** | **Zhou et al. (2018)** | Nila, tangki indoor | Top-view, $h = 1,2\text{ m}$ | Near-Infrared (NIR 850 nm) + ANFIS | Filter optik NIR potong silau | Akurasi feeding 98.0% | Membutuhkan lampu proyektor NIR khusus; kurang efektif di bawah sinar terik matahari tropis. |
| **11** | **Liu et al. (2014)** | Salmon, tangki RAS indoor | Top-view, $h = 1,5\text{ m}$ | Frame Difference biner (CVFAI) | Threshold piksel gerak minimal | Korelasi nafsu makan $R^2 > 0.90$ | Asumsi air tenang tanpa aerator; gelembung aerator akan selalu terhitung sebagai pakan. |
| **12** | **Zhao et al. (2017)** | Nila, tangki sirkular indoor | Top-view, $h = 1,2\text{ m}$ | Trajectory Tracking + Kinetic Energy | Tracking filter Kalman | Akurasi feeding 92.5% | Menuntut pelacakan individu di air bening; bibit lele berenang berkerumun pekat (*swarming*). |
| **13** | **Zhao et al. (2016)** | Ikan mas, tangki terkontrol | Top-view, $h = 1,2\text{ m}$ | BMFS + Partition Optical Flow (PAOF) | Adaptive thresholding YCbCr | Korelasi agresi makan tinggi | Komputasi optical flow per-piksel berat; tidak memodelkan letupan aerator konstan. |
| **14** | **Dong et al. (2024)** | Kerapu, tangki terkontrol | Top-view, $h = 0,5\text{ m}$ | Three-Stream CNN (OF + Binary + GLCM) | Multi-stream fusion | Akurasi klasifikasi 99.28% | Tiga cabang CNN simultan mustahil dieksekusi secara real-time pada CPU Raspberry Pi. |
| **15** | **Zhang et al. (2024)** | Ikan bawah laut dinamis | Underwater horizontal | RUSNet (Deep Segmentation) | Seleksi adaptif aliran blur | mIoU 92.4% di video buram | Khusus segmentasi bawah air laut, tidak relevan untuk kuantifikasi riak pakan overhead. |
| **16** | **Aris et al. (2023)** | Gerakan dinamis umum | Sudut miring CCTV outdoor | Gaussian Mixture Model (GMM) | Model multi-Gaussian latar | Evaluasi background subtraction | GMM gagal pada gelembung aerator konstan (terjadi *cavity* & false foreground berkepanjangan). |
| **17** | **Kamal et al. (2025)** | **Lele, kolam ber-aerator** | Sensor akustik hidrofon | Machine Learning Audio (SVM, RF) | Bandpass filter akustik | Akurasi kunyahan lele 91.2% | Suara bising getaran motor aerator merusak SNR audio; metode visi komputer lebih handal. |
| **18** | **Yang et al. (2025)** | Tinjauan gelombang pakan | Multi-sudut komparatif | Tinjauan Spatial-Temporal Transformer | Attention channel | Sintesis tren riset 2025 | Menegaskan pentingnya pemodelan deret waktu (*temporal modeling*) untuk memisahkan gelombang air. |
| **19** | **Vijayalakshmi (2025)**| Ikan air tawar, kolam outdoor | Top-view & Oblique | AquaYOLO (Enhanced YOLOv8) | CSP layers ekstraksi fitur | mAP 90.9% | Bounding box gagal saat bibit lele bersembunyi di bawah buih aerator atau air keruh. |
| **20** | **Wu et al. (2024)** | *Bass*, tangki terkontrol | Top-view, $h = 1,2\text{ m}$ | DeformAtt-ViT (*Splash Thumbnails*) | Thumbnail crop buih air | Akurasi 95.50%, F1 94.13% | GAGAL PADA BENIH LELE (Cipratan benih tidak berbusa putih tebal seperti ikan dewasa). |
| **--** | **Skripsi Mahasiswa** | **Bibit Lele, Kolam Terpal Outdoor** | **Top-view Dekat, $h \approx 40\text{ cm}$** | **Adaptive Baseline + Temporal FAI** | **Z-Score Normalization + HSV Filter** | **Target: Akurasi $\ge 85\%$ @ RPi 10 FPS** | **SOLUSI SPESIFIK: Mengatasi aerator kontinu, air keruh, & komputasi edge Raspberry Pi.** |

### 2.2 Sintesis Empat Kesenjangan Penelitian (*Research Gaps*)
Dari penelaahan 20 artikel di atas, dirumuskan empat *research gap* berbasis bukti:
1. **Gap 1: Kegagalan Deteksi Tubuh pada Air Keruh & Benih Mikro**:
   Literatur terkini (Qian 2025; Vijayalakshmi 2025; Zhao 2025) bertumpu pada *bounding box* tubuh ikan di air jernih. Pada benih lele pendederan air keruh, deteksi fisik tubuh mengalami kegagalan oklusi 100%. Solusi: Mengamati **dinamika riak gelombang permukaan air**, bukan visual fisik tubuh ikan.
2. **Gap 2: Asumsi Naif Permukaan Air Tenang (*Zero-Motion Baseline*)**:
   Literatur klasik (Liu 2014; Marliza 2021; Atoum 2015; Fukae 2023) mengasumsikan kolam tenang sebelum pakan diberikan. Pada kolam nyata ber-aerator, aerator berputar 24 jam. Tanpa pemodelan baseline aerator, sistem akan mengalami *infinite false trigger*. Solusi: **Pemodelan dinamis baseline normal aerator menggunakan running statistics**.
3. **Gap 3: Ketidaksesuaian Asumsi Buih Kasar Ikan Dewasa**:
   Wu et al. (2024) mengandalkan buih putih tebal ikan dewasa (*splash thumbnails*). Benih lele kecil tidak menghasilkan buih putih kasar melainkan riak gelombang mikro halus. Solusi: **Penempatan kamera berjarak dekat ($30\text{--}50\text{ cm}$) yang menangkap riak mikro secara beresolusi tinggi**.
4. **Gap 4: Keterbatasan Daya Komputasi Edge Device**:
   Model Hu et al. (2026) dan Dong et al. (2024) menuntut workstation GPU puluhan juta rupiah. Solusi: **Pipelines komputasi ringan (Three-Frame Differencing + Z-Score) yang berjalan lancar pada CPU Raspberry Pi 5 pada 10 FPS**.

---

## 🌊 BAGIAN 3: METODOLOGI MEMBEDAKAN GERAKAN BIBIT LELE VS NOISE BUIH AERATOR

Pada citra nyata `image.png`, gelembung aerator terlihat jelas melayang di atas permukaan air. Bagaimana sistem secara deterministik membedakan gelembung aerator tersebut dari riak bibit lele yang sedang menyambar pakan?

```
                      [FRAME KAMERA TERPOTONG (ROI)]
                                    │
                  ┌─────────────────┴─────────────────┐
                  ▼                                   ▼
        [KOMPONEN AERATOR]                  [KOMPONEN BIBIT LELE]
  - Terpusat di sekitar selang Y      - Tersebar acak di seluruh kolam
  - Frekuensi osilasi konstan (1 Hz)  - Muncul mendadak / burst (3–6 frame)
  - Varians energi rendah & stabil    - Lonjakan energi kinetik tinggi (Z > 3)
                  │                                   │
                  ▼                                   ▼
        [Baseline Normal (μ, σ)]           [Deviasi Positif Signifikan]
```

### 3.1 Karakterisasi Fisik & Perilaku (*Physical Behavioral Signatures*)
1. **Pola Spasial (*Spatial Dispersion*)**:
   * *Aerator*: Sumber semburan bersifat titik stasioner (*point source*). Gelembung bergerak melayang menjauhi percabangan selang Y secara laminar dan berulang pada radius yang terlokalisasi.
   * *Bibit Lele*: Saat lapar, benih lele muncul dari berbagai sudut kolom air bawah secara acak dan serentak (*stochastic multi-point distribution*), menciptakan riak di area yang luas.
2. **Pola Temporal (*Temporal Rhythm & Dynamics*)**:
   * *Aerator*: Frekuensi letupan gelembung bersifat siklik dan quasi-periodik dengan amplitudo energi yang relatif konstan sepanjang waktu.
   * *Bibit Lele*: Respons makan bersifat lonjakan transien singkat berdurasi **3–6 frame (0,3–0,6 detik pada 10 FPS)**. Terjadi percepatan mendadak (*abrupt acceleration*) pada energi kinetik permukaan.

### 3.2 Algoritma Pemodelan Baseline Berjalan (*Running Gaussian Baseline Modeling*)
Untuk memisahkan kedua sinyal ini tanpa mematikan aerator, sistem menerapkan algoritma statistik berjalan (*Welford's Online Running Statistics*).
Pada setiap jendela waktu tanpa pakan (misal 30 detik terakhir), sistem memperbarui nilai rata-rata ($\mu_{\text{base}}$) dan standar deviasi ($\sigma_{\text{base}}$) dari intensitas pergerakan kolam:

$$\mu_{\text{base}}(t) = \alpha \cdot M_t + (1 - \alpha) \cdot \mu_{\text{base}}(t-1)$$

$$\sigma_{\text{base}}^2(t) = \alpha \cdot (M_t - \mu_{\text{base}}(t))^2 + (1 - \alpha) \cdot \sigma_{\text{base}}^2(t-1)$$

Di mana:
* $M_t$ adalah total besaran piksel pergerakan pada frame ke-$t$.
* $\alpha$ adalah laju adaptasi (*learning rate*, disetel rendah $\alpha \approx 0,05$ agar gejolak sesaat tidak merusak baseline).

### 3.3 Uji Deviasi Baku ($Z$-Score Anomaly Detection)
Setiap frame yang masuk dinilai menggunakan skor deviasi standar:

$$Z_t = \frac{M_t - \mu_{\text{base}}(t)}{\sigma_{\text{base}}(t)}$$

* **Jika $Z_t \le 2,0$**: Pergerakan air berada dalam batas wajar gejolak aerator $\to$ **Ditolak / Diabaikan (*Background Noise*)**.
* **Jika $Z_t > 3,5$**: Terjadi anomali pergerakan yang melebihi 3,5 kali standar deviasi aerator $\to$ **Diduga Kuat Riak Sambaran Bibit Lele**.
* **Verifikasi Durasi Temporal (3–6 Frame)**:
  Untuk mencegah alarm palsu akibat satu gelembung besar yang meletup keras pada 1 frame, sistem menuntut kondisi $Z_t > 3,5$ harus bertahan selama **minimal 3 frame berturut-turut ($0,3\text{ detik}$)**.

---

## ☀️ BAGIAN 4: METODOLOGI REDUKSI NOISE LINGKUNGAN OUTDOOR (CAHAYA, DAUN, BURUNG)

Kolam luar ruangan (*outdoor*) menghadapi gangguan lingkungan dinamis yang dapat memicu kesalahan deteksi (*false positive*). Berikut metodologi penanganannya:

### 4.1 Eliminasi Silau Pantulan Cahaya Matahari (*Sun Glint & Specular Reflection*)
Pada `image.png`, pantulan cahaya langit terlihat jelas di permukaan air. Jika matahari terik atau awan bergerak, intensitas piksel dapat melonjak drastis menyerupai gerakan ikan.

* **Solusi Perangkat Lunak: Konversi ke Ruang Warna HSV / CIE-Lab**:
  Kanal warna RGB memadukan intensitas cahaya dan informasi warna dalam setiap kanal ($R, G, B$). Oleh karena itu, frame dikonversikan ke ruang warna **HSV (Hue, Saturation, Value)**:
  $$\text{Frame RGB} \longrightarrow \text{Frame HSV}$$
  * Komponen **V (Value / Intensitas Kecerahan)** dibuang atau dinormalkan menggunakan pemerataan histogram kontras adaptif (*Contrast Limited Adaptive Histogram Equalization / CLAHE*).
  * Pemrosesan selisih frame dilakukan pada kanal **S (Saturation)** dan **H (Hue)**, karena pantulan kilau air menghasilkan desaturasi putih yang mudah dinetralkan pada kanal saturasi.
* **Solusi Perangkat Keras: Filter Polarisasi Sirkular (CPL)**:
  Sesuai rujukan Li et al. (2020), memasang filter lensa optik CPL (*Circular Polarizer*) di depan lensa Logitech Brio 100 secara fisik memblokir gelombang cahaya terpolarisasi pantulan air hingga $80\%$, sehingga permukaan air tampak tembus dan bebas kilau silau.

### 4.2 Eliminasi Noise Daun Rontok & Serangga Mengapung
* **Karakteristik Daun**: Daun rontok mengapung dan bergerak pasif mengikuti arah tiupan angin atau arus sirkulasi secara searah (*unidirectional drift*) dengan kecepatan rendah ($v < 5\text{ cm/s}$).
* **Solusi**: Filter Ambang Kecepatan & Arah Vektor (*Directional Velocity Filter*). Riak ikan bergerak bolak-balik frekuensi tinggi secara omnidirectional, sementara daun bergerak laminar satu arah. Gerakan laminar di bawah ambang kecepatan dieliminasi.

### 4.3 Eliminasi Bayangan Burung, Kucing, atau Petani Melintas
* **Karakteristik Bayangan Luar**: Bayangan burung melintas atau tubuh manusia membentuk satu gumpalan kontur raksasa (*large continuous silhouette blob*) yang menutupi $> 30\%$ area permukaan kolam secara tiba-tiba.
* **Karakteristik Riak Bibit Lele**: Bibit lele pendederan menghasilkan riak-riak mikro kecil yang terfragmentasi (*cluster of micro-blobs*), di mana luas masing-masing riak hanya berkisar $50\text{--}500\text{ piksel}$.
* **Solusi (Filter Luas Kontur Maksimum)**:
  $$\text{Jika Luas Kontur } A_i > A_{\text{max}} \quad (\text{misal } > 15\% \text{ Luas Kolam}) \longrightarrow \text{Filter Keluar (Abaikan Bayangan)}$$

---

## 📈 BAGIAN 5: KUANTIFIKASI PERUBAHAN PIKSEL MENJADI SKOR INDEKS AKTIVITAS MAKAN (*FAI*)

Bagaimana sinyal aliran video mentah dikonversi menjadi angka kuantitatif yang objektif?

```
  [Frame t-2]       [Frame t-1]       [Frame t]
       │                 │                 │
       └────────┬────────┴────────┬────────┘
                ▼                 ▼
          |I_t - I_t-1|     |I_t-1 - I_t-2|
                │                 │
                └────────┬────────┘
                         ▼
             [Three-Frame AND Intersection]
                         │ (Menghapus Ghosting)
                         ▼
             [Adaptive Thresholding Biner]
                         │
                         ▼
             [Penjumlahan Piksel Aktif M_t]
                         │
                         ▼
       [Z-Score Terhadap Baseline Aerator]
                         │
                         ▼
           Skor FAI (0.0 s/d 10.0+)
```

### 5.1 Three-Frame Differencing (Menghilangkan Masalah Ghosting)
Frame difference dua frame standar sering menghasilkan bayangan semu (*ghosting*) di belakang objek bergerak. Untuk menghasilkan tepi riak yang presisi, sistem menggunakan metode selisih tiga frame berurutan:

$$D_1(x,y) = |I_t(x,y) - I_{t-1}(x,y)|$$

$$D_2(x,y) = |I_{t-1}(x,y) - I_{t-2}(x,y)|$$

$$D_{\text{motion}}(x,y) = D_1(x,y) \cap D_2(x,y)$$

Di mana operasi $\cap$ adalah *bitwise AND* biner setelah melewati ambang adaptif Otsu.

### 5.2 Penghitungan Energi Gerak Spasial Terbobot ($M_t$)
Total piksel gerakan dihitung hanya di dalam wilayah minat aktif kolam (*Masked ROI*):

$$M_t = \frac{\sum_{(x,y) \in \text{ROI}} D_{\text{motion}}(x,y)}{\text{Luas Total Piksel ROI}} \times 100\%$$

### 5.3 Perumusan Feeding Activity Index ($FAI_t$)
Skor kuantitatif aktivitas makan dirumuskan sebagai:

$$FAI_t = \frac{M_t - \mu_{\text{base}}(t)}{\sigma_{\text{base}}(t)}$$

### 5.4 Skala Tingkat Aktivitas Makan & Interpretasi Keputusan

| Rentang Skor $FAI$ | Klasifikasi Status | Karakteristik Visual Kolam | Keputusan Aktuator Pakan |
|:---:|---|---|---|
| **$FAI < 2,0$** | **Tenang / Kenyang (*Quiescent*)** | Hanya semburan buih aerator normal dari selang Y. Permukaan air stabil. | **Diam (Servo OFF)**. Pakan tidak boleh ditebar karena bibit lele pasif di dasar. |
| **$2,0 \le FAI < 4,0$** | **Aktivitas Ringan (*Moderate Activity*)** | Beberapa ekor benih berenang naik ke kolom tengah air, riak sporadis kecil. | **Standby Monitoring**. Sistem meningkatkan frekuensi pengamatan, belum memicu pakan. |
| **$FAI \ge 4,0$** | **Sangat Lapar / Agresi Tinggi (*High Feeding Frenzy*)** | Kawanan benih lele serentak memecah permukaan air, riak dan buih menyebar masif. | **TRIGGER SERVO ON!** Dispensi satu sub-porsi pakan (50–100 gram). |

---

## ⚙️ BAGIAN 6: LOGIKA KONTROL SISTEM & PEMICUAN SERVO PAKAN (PCA9685)

Sistem pakan otomatis tidak boleh bekerja membabi buta. Pemicuan pakan wajib mematuhi **Batas Kuota Harian Petani (*Farmer Daily Quota Budgeting*)** dan memiliki fase jeda makan (*feeding cooldown*).

```
                      ┌────────────────────────┐
                      │  PETANI INPUT KUOTA    │
                      │  (Misal: 1.000 gram)   │
                      └───────────┬────────────┘
                                  │
                                  ▼
                     ┌──────────────────────────┐
                     │   STATE 1: MONITORING    │◄─────────────────┐
                     │   Kamera Evaluasi FAI    │                  │
                     └────────────┬─────────────┘                  │
                                  │                                │
                                  ▼ FAI >= 4.0 selama >= 0.5s?     │
                     ┌──────────────────────────┐                  │
                     │  STATE 2: CEK KUOTA SISA │                  │
                     └────────────┬─────────────┘                  │
                                  │                                │
                 ┌────────────────┴────────────────┐               │
                 ▼                                 ▼               │
         [KUOTA MASIH ADA]                 [KUOTA SUDAH HABIS]     │
                 │                                 │               │
                 ▼                                 ▼               │
     ┌───────────────────────┐             ┌───────────────┐       │
     │ STATE 3: BUKA SERVO   │             │ SISTEM KUNCI  │       │
     │ Putar 90° (50 gram)   │             │ Kirim Notif   │       │
     └───────────┬───────────┘             └───────────────┘       │
                 │                                                 │
                 ▼                                                 │
     ┌───────────────────────┐                                     │
     │  STATE 4: COOLDOWN    │                                     │
     │  Jeda 3 – 5 Menit     │─────────────────────────────────────┘
     └───────────────────────┘
```

### 6.1 State 1: Monitoring Pasif (*Passive Surveillance*)
* Kamera merekam video pada 10 FPS 720p.
* Sistem menghitung nilai $FAI_t$ pada setiap frame secara real-time.
* Baseline aerator ($\mu_{\text{base}}, \sigma_{\text{base}}$) diperbarui secara adaptif.

### 6.2 State 2: Verifikasi Kuota Harian (*Quota Verification*)
* Ketika terdeteksi $FAI_t \ge 4,0$ selama minimal 5 frame berturut-turut ($0,5\text{ detik}$):
  $$\text{Sisa Kuota} = \text{Kuota Harian Petani} - \text{Total Pakan Dikeluarkan Hari Ini}$$
* **Jika Sisa Kuota $\le 0$ gram**: Sistem **TIDAK MEMICU SERVO**. Sistem mencatat log: *"Ikan lapar terdeteksi tetapi kuota harian habis. Mencegah overfeeding."* Notifikasi dikirimkan ke dashboard petani.
* **Jika Sisa Kuota $> 0$ gram**: Sistem beralih ke State 3.

### 6.3 State 3: Pemicuan Aktuator Servo PCA9685 (*Feeder Actuation*)
* Raspberry Pi mengirimkan perintah sinyal PWM I2C ke modul **PCA9685** (alamat default `0x40`):
  * **Sinyal PWM**: Frekuensi $50\text{ Hz}$ ($20\text{ ms}$ periode).
  * **Gerakan Buka**: Menggeser sudut servo dari $0^\circ$ ($1,0\text{ ms}$ pulse width) ke $90^\circ$ ($2,0\text{ ms}$ pulse width) untuk membuka katup hopper pakan.
  * **Durasi Buka**: Katup terbuka selama $\Delta t = 2,0\text{ detik}$ (terkalibrasi menjatuhkan $50\text{ gram}$ pelet ukuran pendederan $1\text{--}2\text{ mm}$).
  * **Gerakan Tutup**: Mengembalikan servo ke posisi $0^\circ$ (katup terkunci rapat).
* Sistem memperbarui catatan kuota:
  $$\text{Total Pakan Dikeluarkan} = \text{Total Pakan Dikeluarkan} + 50\text{ gram}$$

### 6.4 State 4: Jeda Pasca-Pakan (*Post-Feeding Cooldown & Ingestion Period*)
* Setelah pakan dijatuhkan, bibit lele akan menyambar pelet di permukaan air. Hal ini menyebabkan nilai $FAI$ melonjak sangat tinggi.
* **Sistem wajib masuk mode COOLDOWN selama $3\text{--}5\text{ menit}$**:
  * Selama masa cooldown, aktuator servo **dikunci total (*locked*)** dan tidak boleh terbuka lagi.
  * Hal ini memberikan waktu bagi bibit lele untuk mengonsumsi pelet yang sudah ada sampai habis dan mencegah penumpukan pelet yang tidak termakan di dasar kolam.
* Setelah masa cooldown selesai, sistem kembali ke State 1 untuk memantau apakah ikan masih lapar atau sudah tenang/kenyang.

---

## 📊 BAGIAN 7: RENCANA PENGUJIAN LAPANGAN & METRIK EVALUASI AKADEMIK (1 BULAN)

Untuk membuktikan keunggulan sistem pada naskah skripsi, pengujian lapangan dilakukan dengan membandingkan dua kolam pendederan lele selama **30 hari kalender**:
* **Kolam A (Perlakuan - Sistem Skripsi Mahasiswa)**: Pakan dikendalikan oleh kamera Raspberry Pi berbasis riak $FAI$ dan aktuator servo PCA9685 terikat kuota harian.
* **Kolam B (Kontrol - Konvensional Manual Petani)**: Pakan diberikan secara manual 3 kali sehari dengan jadwal tetap (jam 07.00, 13.00, 19.00) tanpa observasi riak.

### 7.1 Parameter Biologis & Budidaya yang Diukur

1. **Pertumbuhan Bobot Harian (*Average Daily Gain / ADG*)**:
   $$ADG = \frac{W_t - W_0}{t} \quad (\text{gram/hari})$$
2. **Rasio Konversi Pakan (*Feed Conversion Ratio / FCR*)**:
   $$FCR = \frac{\text{Total Bobot Pakan yang Diberikan (g)}}{\text{Pertambahan Total Biomassa Ikan (g)}}$$
   *(Target: Kolam A menghasilkan FCR lebih rendah/efisien dibanding Kolam B).*
3. **Tingkat Kelangsungan Hidup (*Survival Rate / SR*)**:
   $$SR = \frac{N_t}{N_0} \times 100\%$$
   *(Target: Kolam A memiliki SR lebih tinggi karena meminimalkan kanibalisme benih lele).*
4. **Efisiensi Penghematan Pakan (*Feed Saving Efficiency*)**:
   Menghitung persentase pakan yang berhasil dihemat dari alokasi kuota petani tanpa menurunkan laju pertumbuhan ikan.

### 7.2 Parameter Kinerja Computer Vision yang Diukur
* **Akurasi Deteksi Lapar (*Accuracy, Precision, Recall, F1-Score*)**:
  Membandingkan keputusan trigger sistem dengan pelabelan manual kebenaran lapangan (*ground truth*).
* **Tingkat Alarm Palsu (*False Positive Rate / FPR*)**:
  Memastikan letupan buih aerator dan pantulan sinar matahari menghasilkan alarm palsu $< 5\%$.
* **Latensi Pemrosesan Edge (*Processing Latency*)**:
  Memastikan satu frame 720p selesai diproses pada CPU Raspberry Pi 5 dalam waktu $< 80\text{ ms}$ (menjamin operasi real-time 10 FPS).

---

## 🏁 KESIMPULAN & PANDUAN IMPLEMENTASI PRAKTIK

1. **Kelengkapan Dokumen**: Dokumen ini telah menjawab secara tuntas seluruh pertanyaan mendasar dosen dan kebutuhan skripsimu, mulai dari karakteristik setup fisik jarak dekat (`image.png`), pemisahan matematis buih aerator, filter noise lingkungan tropis, rumus kuantifikasi $FAI$, hingga logika kendali aktuator servo PCA9685.
2. **Kesiapan Literatur**: 20 artikel ilmiah yang telah dihimpun di repositori sudah **lebih dari cukup** dan sangat solid untuk mempertahankan proposal dan naskah skripsi di hadapan dosen penguji.
3. **Langkah Konkret Berikutnya**:
   * Cetak dokumen PDF terlampir untuk dibaca, dicoret-coret, dan dipelajari secara mendalam.
   * Masukkan diagram alur logika FSM dan rumus matematis $FAI$ ini ke dalam naskah **Bab 3 (Metodologi)**.
   * Lakukan uji coba konektivitas dan putaran sudut servo PCA9685 menggunakan Raspberry Pi 5 di meja praktikum.

# Rancangan Metodologi Komparasi: Computer Vision Konvensional vs. Lightweight Deep Learning
**Judul Penelitian:** Sistem Pemberian Pakan Adaptif Berbasis Analisis Komparatif Deteksi Riak Aktivitas Permukaan Bibit Ikan Lele (*Clarias sp.*) Menggunakan Computer Vision Konvensional dan Lightweight Deep Learning pada Kolam Luar Ruangan  
**Mahasiswa:** Khoirotun Nisa' (NIM: 2341720057)  
**Dosen Pembimbing:** Dr. Ulla Delfana Rosiani, ST., MT.  
**Program Studi:** D4 Teknik Informatika, Jurusan Teknologi Informasi, Politeknik Negeri Malang  

---

## 1. Landasan Logika & Fenomena Fisik Kolam Lele (*Physics of the Problem*)

### 1.1 Karakteristik Air Kolam Pendederan Lele
1. **Kekeruhan Ekstrem (*High Turbidity - Green Water*):**  
   Pada budidaya pendederan benih lele (*Clarias sp.*) komersial, air kolam sengaja dikondisikan berwarna hijau kecokelatan pekat dengan kedalaman Secchi $\le 3\text{ cm}$ menggunakan inokulasi alga dan mikroba probiotik guna meredam penetrasi sinar matahari dan mencegah stres kanibalisme antarbenih.
2. **Ketiadaan Sinyal Visual Sub-Permukaan:**  
   Akibat kekeruhan ekstrem tersebut, tubuh individu bibit lele di bawah permukaan air **sama sekali tidak terlihat oleh kamera**. Metode pelacakan siluet tubuh ikan (*fish contour / multi-object tracking*) yang jamak digunakan di laboratorium air jernih dipastikan **gagal total**.
3. **Manifestasi Sinyal Rasa Lapar Lele:**  
   Bibit lele bersifat benthik (berdiam di dasar kolam). Saat lapar dan terstimulasi aroma pakan, lele bergerak melesat ke permukaan, menyambar butiran pelet, lalu seketika menyelam kembali. Pergerakan transien sub-detik ini ($0{,}3\text{--}0{,}6\text{ detik}$) memicu **riak gelombang turbulen dan cipratan air mikro (*surface ripples / feeding splashes*)** di permukaan air.

> [!IMPORTANT]
> **Prinsip Anti-Overclaim:**  
> Baik metode **Konvensional** maupun **Deep Learning** dalam penelitian ini **TIDAK MENDETEKSI TUBUH IKAN**, melainkan mendeteksi dan mengkuantifikasi **manifestasi riak cipratan air di permukaan (*Surface Water Ripples / Feeding Splashes*)** pada zona pemberian pakan (*feeding zone*).

---

## 2. Metode 1: Pendekatan Konvensional Deterministik (Baseline)

### 2.1 Alur Pemrosesan Citra
1. **Reduksi Derau Optik & Spasial:**
   * **Filter Polarisasi Sirkular (CPL):** Terpasang pada lensa kamera guna memblokir pantulan gelombang cahaya terpolarisasi permukaan air hingga $80\%$ secara pasif (*optical level*, tanpa beban CPU).
   * **Static ROI Masking:** Memotong $30\%$ area atas citra yang memuat dinding terpal kolam biru agar getaran terpal akibat hembusan angin tidak memicu deteksi palsu.
   * **Transformasi Ruang Warna HSV (Kanal $S$):** Mengonversi frame RGB ke HSV. Pantulan kilau matahari (*sun glint*) bersifat *specular highlight* dengan desaturasi tinggi mendekati putih ($S \approx 0$). Deteksi riak diprioritaskan pada kanal saturasi $S$ untuk membuang efek silau.
2. **Adaptive Three-Frame Differencing (TFD) + Bitwise AND:**
   Mengekstraksi gerak riak murni menggunakan 3 frame berurutan ($I_{t-1}, I_t, I_{t+1}$):
   $$\Delta I_1(x,y) = |I_t(x,y) - I_{t-1}(x,y)|$$
   $$\Delta I_2(x,y) = |I_{t+1}(x,y) - I_t(x,y)|$$
   $$B_1(x,y) = \begin{cases} 1, & \Delta I_1(x,y) > T_{\text{diff}} \\ 0, & \text{lainnya} \end{cases}, \quad B_2(x,y) = \begin{cases} 1, & \Delta I_2(x,y) > T_{\text{diff}} \\ 0, & \text{lainnya} \end{cases}$$
   $$M(x,y,t) = B_1(x,y,t) \land B_2(x,y,t)$$
   Operasi logika *bitwise AND* ($\land$) menjamin eliminasi bayangan semu (*ghosting artifacts*) yang biasa terjadi pada pengurangan dua-frame biasa.
3. **Welford Running Gaussian Baseline ($Z$-Score Anomaly):**
   Memodelkan riak normal kolam (akibat buih aerator atau hembusan angin sepoi) secara statistik rekursif:
   $$\mu_{\text{base}}(t) = \alpha \cdot A_t + (1 - \alpha) \cdot \mu_{\text{base}}(t-1)$$
   $$\sigma_{\text{base}}^2(t) = \alpha \cdot (A_t - \mu_{\text{base}}(t))^2 + (1 - \alpha) \cdot \sigma_{\text{base}}^2(t-1)$$
   $$Z_t = \frac{A_t - \mu_{\text{base}}(t)}{\sigma_{\text{base}}(t)}$$
   * Di mana $A_t = \sum M(x,y,t)$ adalah total piksel gerak aktif pada frame ke-$t$.
   * Jika $Z_t \ge 3{,}5$ bertahan selama $\ge 3$ frame berturut-turut ($0{,}3\text{ detik}$ pada 10 FPS), event dinyatakan sebagai **Riak Sambaran Makan Nyata**.
4. **Kuantifikasi Feeding Activity Index ($FAI$):**
   $$FAI_{\text{conv}}(t) = \frac{\sum_{(x,y) \in \text{ROI}} M(x,y,t)}{N_{\text{ROI}}} \times 100\%$$
5. **Finite State Machine (FSM) Pengendali Servo:**
   Logika FSM 5 status (`IDLE`, `FEEDING_BURST`, `MONITORING_RESPONSE`, `SATIATED`, `COOLDOWN`) yang mengendalikan putaran motor servo dispenser pelet dengan batas kuota pakan harian maksimal 5% biomassa ikan (SNI 01-6484.2-2000).

---

## 3. Metode 2: Pendekatan Lightweight Deep Learning

Untuk membandingkan performa secara menyeluruh, dirancang dua arsitektur Deep Learning:

### 3.1 Sub-Metode 2A: YOLOv8-nano Murni (Deteksi Objek Riak Spasial)
* **Tujuan:** Mendeteksi lokasi dan kuantitas kemunculan *bounding box* riak air (*water splash*) per frame.
* **Arsitektur:**
  * **Backbone:** Modified CSPDarknet53.
  * **Neck:** Path Aggregation Network (PANet) dengan C2f modules.
  * **Head:** Anchor-free decoupled head (klasifikasi dan regresi terpisah).
  * **Jumlah Parameter:** $\sim 3{,}2$ juta parameter (ukuran file model $\approx 6{,}3\text{ MB}$ FP32, $\approx 3{,}2\text{ MB}$ INT8).
* **Kelas Target:** 1 kelas tunggal: `ripple_splash`.
* **Formulasi Logika Nafsu Makan:**
  Pada setiap jendela waktu $\Delta T = 1{,}0\text{ detik}$ (10 frame):
  $$N_{\text{splash}} = \sum_{f=1}^{10} \sum_{i=1}^{K_f} \mathbb{I}(\text{conf}_i \ge 0{,}45 \land \text{IoU} \le 0{,}5)$$
  * $N_{\text{splash}} \ge 5\text{ box/detik} \to$ **Lapar / Agresif (Hungry)**
  * $2 \le N_{\text{splash}} < 5\text{ box/detik} \to$ **Makan Sedang (Moderate)**
  * $N_{\text{splash}} < 2\text{ box/detik} \to$ **Kenyang / Tenang (Satiated)**

---

### 3.2 Sub-Metode 2B: Arsitektur Hibrida Spatio-Temporal: YOLOv8n + LSTM
* **Rasional Ilmiah:** Riak cipratan bibit lele adalah fenomena dinamis transien ($0{,}3\text{--}0{,}6\text{ detik}$). Letupan satu gelembung aerator besar pada 1 frame dapat menyerupai riak lele secara visual, namun letupan aerator bersifat stasioner dan terisolasi. Oleh karena itu, penambahan modul temporal LSTM di atas ekstraksi spasial YOLO bertujuan membedakan **dinamika deret waktu riak makan lele vs derau aerator/angin**.
* **Tahap 1 (Spatial Feature Extraction via YOLOv8n):**
  Untuk setiap frame ke-$t$, YOLO mengekstrak vektor fitur gerak permukaan $v_t \in \mathbb{R}^5$:
  $$v_t = \Big[ N_t,\, \bar{A}_t,\, \sigma_A^2(t),\, \bar{C}_t,\, D_t \Big]$$
  * $N_t$: Jumlah bounding box riak terdeteksi pada frame $t$.
  * $\bar{A}_t$: Rata-rata luas area bounding box riak ($\text{pixel}^2$).
  * $\sigma_A^2(t)$: Varians luas bounding box (mengukur turbulensi ukuran cipratan).
  * $\bar{C}_t$: Rata-rata nilai confidence deteksi YOLO.
  * $D_t$: Dispersi spasial (jarak rata-rata antarpusat box riak terhadap titik pusat tebar pakan).
* **Tahap 2 (Temporal Sequence Modeling via LSTM):**
  * **Input Matriks:** Jendela waktu $W = 10\text{ frame}$ (durasi 1 detik pada 10 FPS):
    $$\mathbf{X}_t = \big[ v_{t-9},\, v_{t-8},\, \dots,\, v_t \big] \in \mathbb{R}^{10 \times 5}$$
  * **Arsitektur Jaringan LSTM:**
    * Input Layer: $10 \times 5$
    * Layer 1: Bidirectional LSTM (32 hidden units, output $10 \times 64$, Dropout 0.2)
    * Layer 2: LSTM (32 hidden units, output $32$, Dropout 0.2)
    * Fully Connected (Dense): 16 units (ReLU)
    * Output Layer: 3 units (Softmax)
* **Output Klasifikasi:** Probabilitas tingkat nafsu makan:
  $$\mathbf{y}_t = \text{Softmax}(\mathbf{W}_o \mathbf{h}_t + \mathbf{b}_o) = \big[ P(\text{Tenang}),\, P(\text{Sedang}),\, P(\text{Lapar}) \big]$$

---

### 3.3 Sub-Metode 2C: Arsitektur End-to-End Spatio-Temporal: MobileNetV3-Small + LSTM
Model MobileNetV3-Small + LSTM dirancang sebagai arsitektur pembanding *end-to-end action recognition* berbasis fitur visual laten tanpa memerlukan tahapan anotasi *bounding box* manual:
* **Rasional & Keunggulan Rekayasa:**  
  Berbeda dengan YOLO yang menuntut pelabelan koordinat kotak riak per-frame, MobileNetV3-Small memproses citra permukaan air secara holistik. Model ini belajar membedakan tekstur turbulensi air lapar vs pantulan sinar matahari langsung dari representasi fitur konvolusional tanpa terikat batasan geometri kotak.
* **Tahap 1 (Ekstraksi Fitur Spasial via MobileNetV3-Small):**  
  Setiap frame $I_t$ diubah ukurannya ke dimensi $224 \times 224 \times 3$. Backbone MobileNetV3-Small (menggunakan *Depthwise Separable Convolution*, aktivasi *Hard-Swish*, dan modul *Squeeze-and-Excitation*) memetakan citra menjadi vektor representasi fitur spasial 1D berdimensi 1024 melalui operasi *Global Average Pooling* (GAP):
  $$\mathbf{f}_t = \phi_{\text{MobileNet}}(I_t) \in \mathbb{R}^{1024}$$
  Dengan total parameter backbone hanya $\sim 1{,}53$ juta parameter, MobileNetV3-Small merupakan arsitektur konvolusi paling hemat daya untuk mikrokomputer *edge*.
* **Tahap 2 (Pemodelan Urutan Temporal via LSTM Cell):**  
  Rangkaian 10 vektor fitur spasial berurutan dihimpun membentuk matriks deret waktu $\mathbf{F}_t = [\mathbf{f}_{t-9}, \mathbf{f}_{t-8}, \dots, \mathbf{f}_t] \in \mathbb{R}^{10 \times 1024}$. Jaringan LSTM memproses dinamika temporal melalui persamaan gate formal:
  $$\mathbf{i}_\tau = \sigma(\mathbf{W}_{ii} \mathbf{f}_\tau + \mathbf{b}_{ii} + \mathbf{W}_{hi} \mathbf{h}_{\tau-1} + \mathbf{b}_{hi}) \quad \text{(Input Gate)}$$
  $$\mathbf{f}_\tau = \sigma(\mathbf{W}_{if} \mathbf{f}_\tau + \mathbf{b}_{if} + \mathbf{W}_{hf} \mathbf{h}_{\tau-1} + \mathbf{b}_{hf}) \quad \text{(Forget Gate)}$$
  $$\mathbf{c}_\tau = \mathbf{f}_\tau \odot \mathbf{c}_{\tau-1} + \mathbf{i}_\tau \odot \tanh(\mathbf{W}_{ig} \mathbf{f}_\tau + \mathbf{b}_{ig} + \mathbf{W}_{hg} \mathbf{h}_{\tau-1} + \mathbf{b}_{hg}) \quad \text{(Cell State)}$$
  $$\mathbf{h}_\tau = \sigma(\mathbf{W}_{io} \mathbf{f}_\tau + \mathbf{b}_{io} + \mathbf{W}_{ho} \mathbf{h}_{\tau-1} + \mathbf{b}_{ho}) \odot \tanh(\mathbf{c}_\tau) \quad \text{(Hidden State)}$$
  Di mana hidden state terakhir $\mathbf{h}_t \in \mathbb{R}^{64}$ diteruskan ke layer Dense (32 units, ReLU) dengan Dropout 0.3 dan layer klasifikasi Softmax untuk menghasilkan prediksi status nafsu makan lele.
* **Karakteristik Komputasi Edge:**  
  Ukuran file model MobileNetV3-LSTM terkuantisasi INT8 hanya berkisar $\approx 2{,}1\text{ MB}$ (lebih ringkas dibandingkan YOLOv8n yang mencapai $\approx 3{,}2\text{ MB}$), dengan estimasi latensi inferensi sub-detik pada Raspberry Pi 5.

---

## 4. Pipeline Dataset & Anotasi Ground Truth

### 4.1 Sumber Data Riil
Data diekstraksi langsung dari rekaman video MP4 (resolusi $1280 \times 720$, 10 FPS) yang dikumpulkan oleh sistem kamera overhead Raspberry Pi di kolam terpal mitra pendederan lele.

### 4.2 Protokol Sampling Dataset
Dataset disusun mencakup 3 kondisi lingkungan dan 3 kondisi perilaku ikan:
1. **Kondisi Lingkungan (Variasi Pencahayaan & Cuaca):**
   * *Morning Soft Light* (Pagi hari: 07.00 - 09.30 WIB)
   * *Midday Direct Sunlight & Glint* (Siang terik: 11.00 - 13.30 WIB)
   * *Afternoon Cloudy / Breeze* (Sore berangin / mendung: 15.00 - 16.30 WIB)
2. **Kondisi Perilaku Ikan:**
   * *Pre-feeding / Starving:* Ikan lapar sebelum pakan disebar.
   * *Active Feeding Burst:* Puncak sambaran pelet pakan (durasi 1 - 3 menit pertama).
   * *Post-feeding / Satiated:* Ikan kenyang, pakan mulai diabaikan, permukaan kembali tenang.

### 4.3 Spesifikasi Anotasi (*Annotation Standard*)
* **Untuk Model YOLO (Deteksi Box):**
  * Sebanyak 1.500 frame terpilih dianotasi bounding box kelas `ripple_splash` menggunakan CVAT / Roboflow.
  * Pembagian dataset: 70% Training (1.050 frame), 15% Validation (225 frame), 15% Testing (225 frame).
* **Untuk Model LSTM & Evaluasi Akhir (Klasifikasi Tingkat Nafsu Makan):**
  * Sebanyak 600 klip video berdurasi 1 detik (10 frame) dianotasi menjadi 3 kelas: `Lapar`, `Sedang`, `Kenyang`.
  * Anotasi divalidasi oleh 3 *observer* independen dengan uji konsistensi Cohen's Kappa ($\kappa \ge 0{,}85$).

---

## 5. Optimasi Edge Computing untuk Raspberry Pi 5

| Komponen Teknis | Spesifikasi Implementasi |
| :--- | :--- |
| **Lingkungan Training** | Workstation GPU / Google Colab (PyTorch, Ultralytics YOLOv8, CUDA 12). |
| **Format Model Edge** | TensorFlow Lite (TFLite) INT8 Quantization & ONNX Runtime. |
| **Akselerasi CPU Edge** | Pustaka XNNPACK teroptimasi untuk arsitektur ARM Neon SIMD (Quad-Core Cortex-A76 @ 2.4 GHz). |
| **Pipeline Threading** | Asynchronous Decoupled Threading: Thread 1 untuk Camera Capture (10 FPS), Thread 2 untuk Inference / TFD, Thread 3 untuk FSM Servo & Logging. |

---

## 6. Protokol Pengujian & Matriks Komparasi Ilmiah

Pengujian dilakukan secara berdampingan (*head-to-head*) memproses **dataset uji video yang sama persis** (15 klip video pengujian durasi 3 menit = 45 menit / 27.000 frame).

### 6.1 Matriks Evaluasi Komparatif

| Dimensi Pengujian | Parameter / Metrik Kuantitatif | Metode Konvensional (*TFD + HSV + Baseline*) | Metode DL 1 (*YOLOv8n Murni*) | Metode DL 2 (*YOLOv8n + LSTM*) | Metode DL 3 (*MobileNetV3 + LSTM*) |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **1. Kinerja Deteksi Nafsu Makan** | *Accuracy* (%) | Diuji | Diuji | Diuji | Diuji |
| | *Precision* (%) | Diuji | Diuji | Diuji | Diuji |
| | *Recall / Sensitivity* (%) | Diuji | Diuji | Diuji | Diuji |
| | *F1-Score* (%) | Diuji | Diuji | Diuji | Diuji |
| | *Confusion Matrix* (3 Kelas) | 3x3 Matrix | 3x3 Matrix | 3x3 Matrix | 3x3 Matrix |
| **2. Ketahanan Derau Lingkungan** | *False Positive Rate* pada Terik Matahari (*Sun Glint*) | Diuji | Diuji | Diuji | Diuji |
| | *False Positive Rate* pada Riak Angin Luar | Diuji | Diuji | Diuji | Diuji |
| | *False Positive Rate* pada Buih Aerator Kontinu | Diuji | Diuji | Diuji | Diuji |
| **3. Beban Komputasi Edge (Raspi 5)** | *Inference Throughput* (FPS) | Target: $\ge 25$ | Target: $\ge 12$ | Target: $\ge 10$ | Target: $\ge 12$ |
| | *Inference Latency* (ms) | Target: $< 40$ | Target: $< 85$ | Target: $< 95$ | Target: $< 80$ |
| | Rata-rata CPU Usage (%) | Target: $< 30\%$ | Target: $< 65\%$ | Target: $< 75\%$ | Target: $< 70\%$ |
| | Rata-rata Suhu CPU (°C) | Target: $\le 55^\circ\text{C}$ | Target: $\le 68^\circ\text{C}$ | Target: $\le 72^\circ\text{C}$ | Target: $\le 70^\circ\text{C}$ |
| | Ukuran Model / Bobot (MB) | $0\text{ MB}$ (Algoritmik) | $\sim 3{,}2\text{ MB}$ | $\sim 3{,}8\text{ MB}$ | $\sim 3{,}5\text{ MB}$ |
| **4. Kebutuhan Rekayasa Data** | Kebutuhan Dataset Berlabel | **Nol** (*Unsupervised*) | 1.500 Box | 1.500 Box + Klip | 600 Klip |
| | Sensitivitas Perubahan Kolam | Kalibrasi Threshold | Rentan Domain Shift | Rentan Domain Shift | Rentan Domain Shift |

---

## 7. Pemetaan Literatur Ilmiah Bereputasi (Literature Grounding)

Seluruh rancangan metode di atas berakar langsung pada literatur ilmiah resmi di repositori riset Anda:
1. **Qian et al. (2025)** (*Discover Applied Sciences*): Menjadi rujukan utama penggunaan varian YOLOv8-nano untuk pemantauan pakan ikan secara *real-time*.
2. **Hu et al. (2026)** (*Scientific Reports / Nature*): Menjadi rujukan utama pentingnya integrasi modul temporal (LSTM) untuk mengklasifikasikan dinamika nafsu makan berbasis deret waktu.
3. **Dong et al. (2024)** (*PLOS ONE*): Menjadi rujukan pembagian 3 tingkat nafsu makan ikan (*None, Moderate, Aggressive*).
4. **Zhao et al. (2025)** (*Scientific Reports / Nature*): Menjadi rujukan eksperimen perilaku kenyang (*satiety experiments*) pada ikan budidaya.
5. **Al-Abri et al. (2025)** (*Artificial Intelligence Review*): Menjadi rujukan perbandingan kesenjangan beban komputasi model Deep Learning terhadap mikrokomputer berdaya rendah (*Edge AI*).
6. **Atoum et al. (2015)** & **Liu et al. (2014)** (*IEEE & Aquacultural Engineering*): Menjadi rujukan dasar formulasi energi selisih frame biner dan *Feeding Activity Index* (FAI).
7. **Li et al. (2020)** (*Aquaculture Elsevier*): Menjadi rujukan solusi optik filter CPL dan kanal saturasi HSV untuk mengatasi kilau pantulan matahari di kolam luar ruangan.
8. **Gisbert et al. (2021)** & **Kurdowi et al. (2025)**: Menjadi rujukan urgensi biologis kanibalisme benih lele (*Clarias sp.*) fase pendederan akibat kekurangan pakan.

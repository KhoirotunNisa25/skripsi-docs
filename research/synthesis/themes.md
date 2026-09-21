# Sintesis Tematik Literatur Ilmiah (Berdasarkan Penelusuran Consensus)

Dokumen ini memetakan sintesis tematik dari artikel-artikel ilmiah yang ditinjau dari penelusuran Consensus mengenai deteksi aktivitas dan perilaku makan ikan berbasis *computer vision* untuk kolam luar ruangan (*outdoor*).

---

## Tema 1: Klasifikasi Status Makan & Intensitas Nafsu Makan (*Feeding State & Appetite Classification*)
- **Fokus Utama**: Mengklasifikasikan kondisi ikan antara lapar (*hungry/active feeding*), mendekati kenyang, dan kenyang (*satiety*) secara non-kontak.
- **Metode & Model**:
  - Jaringan dua tahap (*lightweight two-stage network*): Pose detection + Graph Convolutional Network (GCN) oleh **Zhao et al. (2025)** dengan akurasi 98,1%.
  - Kerangka hibrida CNN + Vision Transformer (ViT) + LSTM (HVIT) oleh **Hu et al. (2026)** untuk menangkap dinamika temporal kelompok ikan (akurasi >98%).
  - Model deteksi objek real-time PM-YOLOv8 oleh **Qian et al. (2025)** dengan presisi 87,7% dan mAP-50 83,5% pada latensi 8,1 ms/frame.
- **Implikasi bagi Skripsi**: Menunjukkan bahwa inferensi status lapar memerlukan pemodelan temporal berurutan (*time-series / temporal variance*) dan tidak cukup hanya mengandalkan deteksi spasial satu frame terisolasi.

---

## Tema 2: Analisis Dinamika Permukaan Air, Riak, & Cipratan (*Ripple, Splash, & Surface Disturbance*)
- **Fokus Utama**: Memanfaatkan fenomena visual sekunder berupa riak air dan cipratan (*splashes*) saat ikan menyambar pakan atau bergerak aktif di permukaan, terutama pada perairan keruh.
- **Metode & Model**:
  - Analisis ukuran dan frekuensi gelombang air permukaan berbasis deep learning oleh **Hu et al. (2022)** pada kolam outdoor (akurasi 93,2%).
  - Kuantifikasi intensitas makan melalui deteksi cipratan air (*feeding splashes*) oleh **Wu et al. (2024)** (akurasi 98,22%).
- **Implikasi bagi Skripsi**: Ikan lele (*Clarias sp.*) hidup pada air kolam keruh dengan visibilitas bawah air rendah. Pendekatan deteksi berbasis distorsi hidrodinamika permukaan air (*surface disturbance & splashes*) sangat sesuai dan aplikatif dibanding pelacakan visual tubuh ikan di bawah air.

---

## Tema 3: Kuantifikasi Gerakan Spasial-Temporal & *Optical Flow*
- **Fokus Utama**: Mengukur magnitudo dan vektor pergerakan kawanan ikan tanpa perlu melacak identitas individual setiap ikan.
- **Metode & Model**:
  - *Dense Optical Flow* dan pengelompokan vektor histogram oleh **Fukae et al. (2023)** untuk mengklasifikasikan aktivitas makan vs tidak makan.
  - *Frame-pair motion encoding* berbasis *optical flow* (V-Value) dan EfficientFeedingNet oleh **Xiao et al. (2026)** untuk inferensi feeding state real-time (96,53% akurasi pada Jetson Orin NX, 143 FPS).
  - Estimasi kecepatan renang (*velocity estimation*) oleh **Alahmad et al. (2025)** untuk membedakan ikan lapar vs normal.
  - Pemodelan energi kinetik spasial-temporal oleh **Zhao et al. (2016)** dan **Wei et al. (2021)**.
- **Implikasi bagi Skripsi**: *Motion quantification* berbasis *optical flow* atau diferensiasi frame terbukti efektif untuk membentuk kurva time-series aktivitas pergerakan agregat.

---

## Tema 4: Kompensasi Gangguan Lingkungan Kolam Outdoor (*Anti-Noise & Baseline Modeling*)
- **Fokus Utama**: Menekan derau lingkungan seperti pergerakan air aerator, pantulan cahaya matahari/lampu, bayangan dinamis, dan kotoran/dedaunan.
- **Metode & Model**:
  - Penekanan gangguan bayangan bergerak (*anti-shadow disturbance*) oleh **Ni et al. (2024)** pada kolam outdoor.
  - Model *dual-stream autoencoder* (AMA-Net) oleh **Wang et al. (2023)** yang dilatih menggunakan data *baseline* aerasi murni tanpa ikan untuk mendeteksi anomali feeding melalui *reconstruction error*.
  - *Anisotropic spatial differential filtering* oleh **Zhou et al. (2020)** untuk menekan derau latar belakang berfrekuensi tinggi (mencapai SNR 14,84 dB).
- **Implikasi bagi Skripsi**: **Ini merupakan pilar terpenting skripsi Anda**. Pemodelan *baseline* aerator harus dilakukan terlebih dahulu agar sistem tidak menganggap osilasi air dari aerator sebagai aktivitas ikan lapar.

---

## Tema 5: Implementasi Berlatensi Rendah pada Perangkat *Edge* (*Raspberry Pi Deployment*)
- **Fokus Utama**: Mengoptimalkan arsitektur algoritma agar dapat berjalan lancar pada perangkat komputasi terjangkau di tepi kolam (*edge devices*).
- **Metode & Model**:
  - *Frame-pair motion encoding* berbiaya komputasi rendah oleh **Xiao et al. (2026)**.
  - *Temporal variance analysis* dan segmentasi semantik ringkas oleh **Kong et al. (2024)**.
  - Penggunaan Raspberry Pi / mikrokontroler untuk kontrol pemberian pakan otomatis oleh **Marliza & Aisuwarya (2021)** dan **Atoum et al. (2015)**.
- **Implikasi bagi Skripsi**: Mengingat kamera yang digunakan adalah Raspberry Pi (10 FPS), algoritma ekstraksi fitur gerak harus dirancang efisien (misal: *frame differencing* adaptif atau *sparse optical flow*) agar tidak mengalami bottleneck komputasi.

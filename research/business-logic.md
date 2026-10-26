# Logika Penelitian & Konsep Skripsi (Hasil Bimbingan Dosen)

## Judul Penelitian
**Sistem Pemberian Pakan Adaptif Berbasis Deteksi Riak Aktivitas Permukaan Bibit Ikan Lele (*Clarias sp.*) Menggunakan *Computer Vision* pada Kolam Luar Ruangan Ber-aerator**

## Objek Penelitian & Batasan Batas Sistem
- **Objek Penelitian**: **BIBIT IKAN LELE** (*fry / fingerlings*, fase pendederan).
- **Fokus Utama**: Mengamati aktivitas dan perubahan riak permukaan kolam dari posisi kamera *top-view / overhead* sebagai dasar penentuan waktu pemberian pakan.
- **Batasan Mutlak (System Boundaries)**:
  - **TIDAK berfokus pada kualitas air** (kualitas air adalah domain kolaborator terpisah / Varizky, dan hanya diperlakukan sebagai parameter lingkungan pendukung/keterbatasan, bukan variabel independen skripsi ini).
  - **TIDAK berfokus pada diagnosis kesehatan ikan**.
  - **TIDAK menggantikan kontrol petani sepenuhnya**. Jumlah kuota pakan harian mutlak ditentukan oleh petani.

---

## 1. Konsep Sistem Hasil Bimbingan: "Mengamati Riak → Menentukan Pakan Terkontrol"

Prinsip kerja sistem dirancang bukan berdasarkan jadwal buta (*timer* kaku "tiap jam pakan"):
1. **Kendali Kuota Harian di Tangan Petani**:
   - Petani menentukan kapasitas dan batas kuota pakan harian (misalnya: 1 kg pakan/hari berdasarkan estimasi biomassa bibit lele 3–5%).
   - Jumlah total pakan harian memiliki batas atas (*ceiling quota*) yang tidak boleh dilanggar oleh sistem.
2. **Pemberian Pakan Mengikuti Aktivitas Bibit Lele (*Activity-Driven Adaptive Sub-rationing*)**:
   - Kuota harian tersebut dibagi ke dalam porsi-porsi kecil (*sub-rations*, misal 50–100 gram).
   - Sistem visi komputer mengamati permukaan kolam. Ketika terdeteksi lonjakan riak/aktivitas yang mengindikasikan bibit lele berkumpul dan aktif di permukaan, sistem mendispensasikan satu porsi pakan.
   - Sistem dengan demikian "menuruti" ritme lapar/responsif bibit lele, namun pakan tetap berhenti jika kuota harian tercapai guna mencegah *overfeeding*.
3. **Tujuan Praktis**:
   - Meringankan pekerjaan fisik petani (tidak perlu memantau kolam terus-menerus).
   - Menghindari pemborosan pakan (*overfeeding*) yang merusak air kolam dan merugikan finansial petani.
   - Menghindari *underfeeding* yang memicu kanibalisme pada bibit lele.

---

## 2. Konteks Lingkungan Penelitian & Masalah Computer Vision

- **Lingkungan**: Kolam bibit lele *outdoor* (luar ruangan).
- **Keberadaan Aerator Mekanis**:
  - Kolam dilengkapi aerator yang aktif terus-menerus untuk menjaga suplai oksigen bibit lele.
  - Aerator menyebabkan permukaan air selalu bergejolak, menghasilkan riak, gelembung, dan buih konstan.
- **Tantangan Utama Computer Vision**:
  - *"Bagaimana membedakan gerakan/riak normal akibat aerator dengan perubahan aktivitas permukaan yang berkaitan dengan aktivitas bibit lele?"*
  - **Kondisi aerator adalah BASELINE NORMAL**. Sistem tidak boleh memakai aturan naïf: *"ada gerakan = ikan lapar"*.
  - Yang dideteksi adalah **deviasi/perubahan temporal** dari baseline aerator menuju peningkatan riak/cipratan bibit lele di permukaan.

---

## 3. Rencana Evaluasi Lapangan (Uji Komparasi 1 Bulan)

1. **Fase Observasi Awal (Baseline Study - 1 Minggu)**:
   - Pengambilan sampel video 10–15 menit setiap jam untuk memetakan karakteristik riak aerator, pola fluktuasi riak lele harian, serta kondisi pencahayaan luar ruangan (pagi, siang, petang, malam).
2. **Fase Pengujian Komparasi (1 Bulan)**:
   - **Kolam Perlakuan (Sistem Berbasis Aktivitas)**: Pakan diberikan secara adaptif berbasis riak kamera + batas kuota pakan petani.
   - **Kolam Kontrol (Pemberian Pakan Manual)**: Pakan diberikan manual sesuai kebiasaan petani tanpa alat.
3. **Parameter Evaluasi Terukur di Lapangan**:
   - Pertumbuhan bibit (bobot rata-rata / *mean weight gain*).
   - Pertambahan panjang (*length gain*).
   - Tingkat kelangsungan hidup (*Survival Rate* / SR).
   - Total kuota pakan yang dikonsumsi (kg).
   - Rasio Konversi Pakan (*Feed Conversion Ratio* / FCR).
   - Frekuensi dan efisiensi waktu pemberian pakan.

---

## 4. Dimensi Studi Komparasi Algoritma: Konvensional vs. Lightweight Deep Learning

Untuk memberikan kontribusi ilmiah yang kuat dan menjawab pertanyaan dewan penguji mengenai keunggulan model modern, penelitian ini merancang dan membandingkan dua paradigma pemrosesan citra secara *head-to-head*:

1. **Metode Konvensional (Baseline Deterministik)**:
   - *Adaptive Three-Frame Differencing* (TFD) + operasi logika *bitwise AND*.
   - Filter optik polarisasi CPL dan transformasi ruang warna HSV (kanal saturasi $S$) untuk reduksi kilau matahari (*sun glint*).
   - *Welford Running Gaussian Baseline* ($Z$-score anomaly) untuk mengisolasi deviasi riak lele dari buih aerator kontinu.
   - Formulasi *Feeding Activity Index* ($FAI$) yang diintegrasikan ke *Finite State Machine* (FSM).
2. **Metode Lightweight Deep Learning (Probabilistik Spatio-Temporal)**:
   - **YOLOv8-nano Murni**: Deteksi *bounding box* cipratan riak air (`ripple_splash`) per-frame.
   - **Hibrida YOLOv8-nano + LSTM**: YOLO mengekstrak vektor fitur gerak permukaan ($N_{\text{splash}}$, luas rata-rata, varians luas, confidence, dispersi spasial), lalu diteruskan ke jaringan Bi-LSTM 2 layer untuk memodelkan dinamika deret waktu 10-frame (1 detik) menjadi klasifikasi 3 tingkat nafsu makan (*Lapar, Sedang, Kenyang*).
   - **MobileNetV3-Small + LSTM**: Model pembanding *end-to-end video action recognition*.
3. **Parameter Komparasi Algoritma Terukur**:
   - Akurasi klasifikasi (Accuracy, Precision, Recall, F1-Score, Confusion Matrix 3x3).
   - Ketahanan derau lingkungan (*False Positive Rate* akibat silau matahari, angin, dan aerator).
   - Efisiensi komputasi pada Raspberry Pi 5 (Throughput FPS, Latensi ms, CPU Usage %, Suhu CPU °C, Memory Footprint MB).
   - Efisiensi data latih (*Data Engineering Feasibility*).



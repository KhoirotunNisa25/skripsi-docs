# Kebutuhan Penelitian (*Research Requirements*)

## Judul Penelitian
**Sistem Pemberian Pakan Adaptif Berbasis Deteksi Riak Aktivitas Permukaan Bibit Ikan Lele (*Clarias sp.*) Menggunakan *Computer Vision* pada Kolam Luar Ruangan Ber-aerator**

---

## Pertanyaan Penelitian (*Research Questions*)

- **RQ1**: Bagaimana memodelkan kondisi *baseline* pergerakan air kolam luar ruangan ber-aerator secara objektif agar perubahan aktivitas/riak bibit lele dapat dibedakan dari gejolak konstan aerator?
- **RQ2**: Bagaimana mengekstraksi dan mengklasifikasikan fitur temporal riak permukaan (seperti *frame differencing*, *optical flow*, *motion intensity*, atau model temporal/LSTM) yang mampu mendeteksi lonjakan aktivitas makan bibit lele yang berlangsung singkat (3–6 frame @ 10 FPS)?
- **RQ3**: Bagaimana merancang mekanisme logika kendali pemberian pakan yang mengintegrasikan batas kuota harian yang ditetapkan petani dengan dispensasi sub-porsi adaptif berbasis sinyal aktivitas visual bibit lele?
- **RQ4**: Bagaimana perbedaan performa budidaya (pertumbuhan bobot, pertambahan panjang, *Survival Rate*, konsumsi pakan total, dan FCR) antara kolam bibit lele dengan sistem pemberian pakan adaptif berbasis aktivitas dibandingkan dengan kolam pemberian pakan manual konvensional selama periode evaluasi 1 bulan?

---

## Kebutuhan Sistem & Metodologi

### 1. Kebutuhan Data & Citra
- **Objek**: Bibit Ikan Lele (*Clarias sp.*), fase pendederan (benih/fingerlings).
- **Sumber Video**: Kamera Raspberry Pi posisi *overhead/top-view* (sudut $90^\circ$ tegak lurus atau sedikit miring) di atas permukaan kolam luar ruangan.
- **Frame Rate**: 10 FPS (analisis temporal rapat karena cipratan/riak bibit berlangsung cepat, 0,3–0,6 detik).
- **Lingkungan**: Kolam luar ruangan dengan aerator kontinu, pencahayaan alami (pagi, siang, petang, malam dengan lampu penerang).
- **Fase Pengumpulan Data**:
  - *Tahap 1 (Observasi Awal / 1 Minggu)*: Sampel video 10–15 menit tiap jam untuk membangun profil variabilitas baseline aerator dan ritme alami riak makan.
  - *Tahap 2 (Implementasi & Evaluasi / 1 Bulan)*: Pengujian sistem pada kolam perlakuan vs kolam manual.

### 2. Kebutuhan Algoritma & Pemrosesan
- **Penyaringan Noise Visual**: Penanganan pantulan sinar matahari (*specular highlights*), bayangan angin, daun melayang, dan buih aerator.
- **Pemodelan Baseline Dinamis**: Pemodelan energi kinetik / varians temporal gelembung aerator sebagai ambang batas dinamis (*adaptive threshold*).
- **Ekstraksi Fitur & Pemodelan Temporal**:
  - Analisis komparatif: *Frame differencing*, *Optical flow* (agregat), *Motion intensity*, *Background subtraction*, dan model temporal (LSTM / GRU / 1D-CNN) untuk menangkap dependensi sekuensial.
- **Logika Kontrol Aktuator Pakan**:
  - Kuota harian maksimum ($Q_{\max}$, misal 1 kg/hari) ditentukan oleh petani.
  - Sistem hanya memicu dispensasi porsi kecil ($q_i \approx 50\text{--}100\text{ g}$) jika terdeteksi lonjakan riak di atas baseline dan $\sum q_i < Q_{\max}$.

---

## Dimensi & Metrik Evaluasi Kinerja

1. **Metrik Computer Vision**:
   - Akurasi, Presisi, Recall, dan F1-Score deteksi event aktivitas riak bibit lele.
   - *False Positive Rate* (FPR) terhadap gejolak aerator murni dan pantulan cahaya.
   - Latensi inferensi pada perangkat *edge* (Raspberry Pi).
2. **Metrik Budidaya Lapangan (Uji 1 Bulan vs Manual)**:
   - Pertumbuhan bobot mutlak (*Mean Weight Gain*) dan Laju Pertumbuhan Spesifik (*Specific Growth Rate* / SGR).
   - Pertambahan panjang tubuh (*Length Gain*).
   - Tingkat Kelangsungan Hidup (*Survival Rate* / SR).
   - Rasio Konversi Pakan (*Feed Conversion Ratio* / FCR).
   - Total efisiensi pakan dan kepraktisan operasional petani.

---

## Terakhir Diperbarui
2026-09-26 (Sesi 11 - Sinkronisasi Bimbingan Dosen)


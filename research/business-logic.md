# Logika Penelitian & Konsep Skripsi

## Judul Penelitian
**Deteksi Aktivitas Ikan Lele (*Clarias sp.*) sebagai Indikasi Lapar Berbasis *Computer Vision* pada Kolam Luar Ruangan Ber-aerator**

## Peneliti & Kolaborasi
- **Fokus Penelitian**: *Computer Vision*, Deteksi Perilaku & Aktivitas Permukaan Ikan Lele
- **Kolaborator**: Varizky (Fokus: Kualitas Air & *Water Exchange System*)
- **Sensor Pendukung**: pH, Suhu, TDS, Kekeruhan (*Turbidity*), dan Tinggi Air (saat ini pada *dashboard* terpisah)

---

## 1. Latar Belakang & Masalah Utama

Pemberian pakan pada budidaya ikan lele sering kali dilakukan secara terjadwal atau manual tanpa mempertimbangkan kondisi nafsu makan aktual ikan. Hal ini berisiko menyebabkan:
1. *Underfeeding* (pertumbuhan ikan terhambat).
2. *Overfeeding* (pemborosan biaya pakan hingga 60% dari operasional budidaya serta pembusukan sisa pakan yang menurunkan kualitas air kolam).

Oleh karena itu, diperlukan sistem deteksi kondisi lapar/tidak lapar berbasis visual (*computer vision*) non-invasif dari kamera *top-view/overhead* di atas permukaan kolam.

### Tantangan Utama: Aktivitas Normal Kolam (*Baseline Aerator*)
Pada kolam lele *outdoor*, permukaan air **tidak pernah benar-benar diam** karena aerator terus menyala menghasilkan gelembung udara dan pergerakan air konstan. Oleh karena itu, sistem **tidak dapat menggunakan asumsi sederhana bahwa "ada gerakan air = ikan lapar"**.

Pergerakan akibat aerator merupakan **kondisi baseline normal**. Sistem harus mampu:
1. Memodelkan karakteristik baseline pergerakan air akibat aerator.
2. Mendeteksi deviasi/perubahan aktivitas visual yang menyimpang dari baseline.
3. Memfilter gangguan visual (*visual noise*) seperti pantulan sinar matahari (pagi), pantulan lampu (malam), daun mengapung, dan riak akibat burung.

---

## 2. Alur Logika Konseptual Deteksi (*Pipeline*)

```text
Kondisi Normal Kolam (Aerator Menyala)
  ↓
Pemodelan Karakteristik Baseline (Gerakan Air Konstan)
  ↓
Terjadi Perubahan Aktivitas Permukaan Air
  ↓
Ekstraksi Fitur Gerakan (Frame Differencing / Dense Optical Flow / Temporal Variance)
  ↓
Penyaringan Noise Visual (Pantulan Cahaya, Gelembung Aerator, Daun, Burung)
  ↓
Identifikasi Kandidat Sinyal Perilaku Ikan (Candidate Feeding Signal / Splashes / Riak)
  ↓
Estimasi Tingkat Lapar vs Tidak Lapar (Aktivitas Lapar vs Normal / Stres)
  ↓
Rekomendasi / Keputusan Pemberian Pakan Otomatis
```

---

## 3. Data Awal & Observasi Lapangan

- **Setup Kamera**: Kamera Raspberry Pi diposisikan *top-view/overhead* merekam pada **10 FPS**.
- **Dataset Awal**: 9 sesi rekaman valid dari 13 sesi terjadwal (periode 15–17 September 2026):
  - Sesi Pagi (~05.30–07.30, dekat waktu pakan) -> Persentase aktivitas ~11,8%.
  - Sesi Siang (~10.00–13.00, di luar waktu pakan) -> Persentase aktivitas ~0,95%.
  - Sesi Malam (~18.00 dekat waktu pakan, ~22.00/01.00 luar waktu pakan) -> Persentase aktivitas ~0,45%.
- **Event Terlabel Manual**: 151 event perubahan visual tercatat.
- **Karakteristik Temporal**: Event tercepat berlangsung sangat singkat, hanya **3–6 frame (0,3–0,6 detik)**, sehingga analisis membutuhkan resolusi temporal yang sangat rapat (*per-frame*).

---

## 4. Tujuan Penelitian

1. Membangun metode ekstraksi fitur gerak berbasis *computer vision* untuk memodelkan *baseline* pergerakan air kolam ber-aerator secara objektif.
2. Mengembangkan algoritma pemisahan antara dinamika riak ikan lele dengan *noise* visual lingkungan (gelembung aerator, pantulan cahaya, dedaunan).
3. Menganalisis korelasi temporal antara intensitas aktivitas permukaan ikan dengan waktu dan kondisi pemberian pakan guna mengestimasi status lapar.

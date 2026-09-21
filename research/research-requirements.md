# Kebutuhan Penelitian (*Research Requirements*)

## Judul Penelitian
**Deteksi Aktivitas Ikan Lele (*Clarias sp.*) sebagai Indikasi Lapar Berbasis *Computer Vision* pada Kolam Luar Ruangan Ber-aerator**

---

## Pertanyaan Penelitian (*Research Questions*)

- **RQ1**: Bagaimana memodelkan kondisi *baseline* pergerakan air kolam luar ruangan yang dipicu oleh aerator agar deviasi aktivitas ikan dapat dideteksi secara objektif menggunakan metode *computer vision* (seperti *frame differencing* atau *optical flow*)?
- **RQ2**: Bagaimana membedakan riak atau *splashes* pergerakan ikan lele dari gangguan visual (*visual noise*) lingkungan seperti gelembung aerator, pantulan sinar matahari/lampu, dan dedaunan?
- **RQ3**: Sejauh mana skor intensitas aktivitas permukaan berkorelasi secara konsisten dengan siklus waktu pemberian pakan (kondisi lapar vs kenyang) pada interval sampling temporal tinggi (per-frame / 10 FPS)?
- **RQ4**: Bagaimana merumuskan model klasifikasi / estimasi status lapar yang andal sebagai dasar pengambilan keputusan pada sistem pakan otomatis?

---

## Kebutuhan Sistem & Metodologi

### 1. Kebutuhan Data & Citra
- Sumber Video: Kamera Raspberry Pi posisi *overhead/top-view* di atas kolam outdoor.
- Frame Rate: 10 FPS (membutuhkan analisis per-frame karena durasi event ikan sangat singkat, 3–6 frame).
- Kondisi Pencahayaan: Pagi (matahari terbit/glare), Siang (intensitas tinggi), Malam (pencahayaan lampu buatan).
- Durasi Observasi Lanjutan: Minimal 1 minggu data rekaman stabil sebelum finalisasi dataset.

### 2. Kebutuhan Algoritma & Pemrosesan
- **Prapemrosesan**: Pengurangan pantulan cahaya (*anti-shadow / anti-reflection filtering*), normalisasi kontras.
- **Ekstraksi Fitur Gerak**: *Dense Optical Flow* (Farneback/Lucas-Kanade), *Background Subtraction* (MOG2/KNN), atau *Frame Differencing*.
- **Pemodelan Baseline**: Distribusi energi kinetik rata-rata (*baseline kinetic energy*) gelembung aerator.
- **Deteksi Event Singkat**: Analisis varians temporal dan ambang batas dinamis (*adaptive thresholding*).

---

## Dimensi & Metrik Evaluasi Kinerja
1. **Presisi & Recall Deteksi Event**: Kemampuan mendeteksi event pergerakan ikan tanpa salah mendeteksi gelembung/pantulan (Precision, Recall, F1-Score).
2. **Robustness terhadap Noise**: Rasio *false alarm* pada kondisi tanpa ikan (hanya aerator menyala dan gangguan cahaya).
3. **Korelasi Temporal dengan Waktu Pakan**: Korelasi statistik antara intensitas gerak terdeteksi dengan interval pra-pakan vs pasca-pakan.
4. **Efisiensi Komputasi (FPS / Latensi)**: Kemampuan inferensi mendekati *real-time* pada perangkat *edge* (Raspberry Pi/Jetson).

---

## Terakhir Diperbarui
2026-09-21

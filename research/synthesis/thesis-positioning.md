# Posisi Penelitian (*Thesis Positioning*)

Dokumen ini memetakan posisi skripsi ini relatif terhadap lanskap penelitian ilmiah terdahulu yang diekstrak dari penelusuran Consensus.

---

## 1. Matriks Pemosisian Terhadap State-of-the-Art

| Dimensi Penelitian | Penelitian Terdahulu (*State-of-the-Art*) | Pendekatan Penelitian Skripsi Ini |
|---|---|---|
| **Lingkungan Uji** | Dominan tangki RAS *indoor* / laboratorium dengan air jernih dan cahaya buatan stabil (Hu et al. 2026; Zhao et al. 2025; Ubiña et al. 2021). | **Kolam luar ruangan (*outdoor*) nyata** dengan air keruh, fluktuasi sinar matahari (pagi/siang/malam), dan aerator aktif. |
| **Kondisi Permukaan Air** | Mengasumsikan permukaan air relatif tenang (*zero-baseline motion*) saat ikan diam (Wu et al. 2024; Fukae et al. 2023). | **Permukaan air bergolak konstan akibat aerator mekanis**. Sistem terlebih dahulu memodelkan *baseline* pergerakan air aerator. |
| **Objek Deteksi Visual** | Deteksi tubuh fisik ikan secara langsung di bawah air menggunakan *bounding box* YOLO / pose (Qian et al. 2025; Zhao et al. 2025). | **Deteksi riak hidrodinamika & perubahan visual permukaan air** (*top-view*), cocok untuk ikan lele yang sering berada di bawah air keruh. |
| **Resolusi Temporal** | Agregasi interval waktu longgar (5–10 detik) atau downsampling frame (Atoum et al. 2015; Cui et al. 2024). | **Analisis per-frame (10 FPS)** untuk menangkap event sentakan singkat ikan (3–6 frame / 0,3–0,6 detik). |
| **Platform Komputasi** | Membutuhkan GPU berperforma tinggi (workstation / cloud) untuk ViT dan 3D-CNN (Hu et al. 2026; Ubiña et al. 2021). | **Berorientasi pada perangkat *edge* terjangkau (Raspberry Pi)** dengan metode ekstraksi gerak berlatensi rendah. |

---

## 2. Kebaruan & Kontribusi Penelitian (*Novelty & Contribution*)

1. **Pemodelan Baseline Dinamis untuk Kolam Ber-aerator**:
   Merumuskan algoritma pembentukan *baseline* visual yang mampu membedakan osilasi konstan gelembung aerator dari deviasi pergerakan ikan lele, memecahkan masalah *false alarm* pada kolam beraerator aktif.

2. **Deteksi Perilaku Ikan Lele pada Resolusi Temporal 10 FPS**:
   Mengembangkan ekstraksi fitur gerak berbasis *frame differencing / optical flow* yang responsif terhadap event singkat ikan lele berdurasi sub-detik (0,3–0,6 detik) tanpa mengabaikan batas kemampuan komputasi perangkat mikrokomputer Raspberry Pi.

3. **Validasi Korelasi Empiris Aktivitas Permukaan vs Waktu Pakan**:
   Menyediakan analisis data empiris terstruktur mengenai korelasi frekuensi dan intensitas riak permukaan dengan jadwal lapar/kenyang ikan lele pada siklus pagi, siang, dan malam hari.

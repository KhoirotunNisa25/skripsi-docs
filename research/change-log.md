# Catatan Perubahan (*Change Log*)

## Log Perubahan Dokumen Riset

### 2026-09-21 (Sesi 3)
- **Perubahan**:
  - Penapisan berkas `result 2.csv` (20 artikel mutakhir Consensus 2022–2026).
  - Melakukan audit menyeluruh terhadap keotentikan berkas PDF di `articles/pdf/`. Menemukan berkas anomali `[14]` (ternyata naskah non-akuakultur Massimo Cacciari 2005 dari JSTOR) dan langsung menghapusnya.
  - Mengunduh dan memverifikasi 6 artikel mutakhir (2023–2025) berkualitas tinggi melalui endpoint resmi Open Access tanpa live browser berat:
    - `[14]` Dong et al. (2024) - PLOS ONE (Three-stream network, 24 hal.)
    - `[15]` Zhang et al. (2024) - Frontiers in Marine Science (RUSNet adaptive optical flow, 14 hal.)
    - `[16]` Aris et al. (2023) - IAES IJ-AI (Background subtraction & GMM dynamic water waves, 12 hal.)
    - `[17]` Kamal et al. (2025) - Techno Agriculturae (Automated feed management for catfish, 11 hal.)
    - `[18]` Yang et al. (2025) - Journal of Big Data and Computing (State-of-the-Art CV fish feeding 2025, 9 hal.)
    - `[19]` Vijayalakshmi & Sasithradevi (2025) - Scientific Reports (AquaYOLO outdoor pond, 12 hal.)
  - Memperbarui katalog `articles/pdf/README.md`, `latex/references.bib`, dan `latex/tables/article-comparison.tex` (dengan `longtable` multi-halaman).
  - Kompilasi ulang dokumen LaTeX menghasilkan `output/main.pdf` (14 halaman) dengan status **0 error**.
  - Menyiapkan git remote ke `https://github.com/KhoirotunNisa25/skripsi-imoet.git` dan melakukan commit.
- **Alasan**: Permintaan pengguna untuk menambahkan artikel dari pencarian terbaru `result 2.csv`, mengutamakan publikasi $\le 5$ tahun terakhir (2022–2026), mengaudit isi PDF, dan melakukan commit ke repositori GitHub tujuan.
- **Dampak**: Total artikel ilmiah PDF yang tersimpan bertambah menjadi 19 artikel terverifikasi dengan komposisi $>63\%$ terbit pada rentang 2023–2026.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 2)
- **Perubahan**: Integrasi topik skripsi baru pengguna ("Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar Berbasis Computer Vision") dari `conteks.md`, penapisan 100 entri `consensus result.csv`, pengunduhan 14 artikel ilmiah teks lengkap (*full-text PDF*) ke `articles/pdf/`, penataan katalog pada `articles/pdf/README.md`, serta sinkronisasi `business-logic.md`, `research-requirements.md`, dan `search-log.md`.
- **Alasan**: Pengguna memberikan rincian konteks penelitian kolam lele outdoor dengan aerator dan hasil pencarian Consensus untuk mulai membangun studi literatur skripsi baru.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 1)
- **Perubahan**: Reset repositori dan pembersihan total dari data skripsi teman (Git reset, pembersihan artikel PDF lama, pembersihan konsep lead generation, dan pembersihan naskah LaTeX).
- **Alasan**: Inisialisasi awal repositori bersih untuk topik baru pengguna.
- **Status**: Selesai (*Completed*)

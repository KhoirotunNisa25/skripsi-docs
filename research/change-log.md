# Catatan Perubahan (*Change Log*)

## Log Perubahan Dokumen Riset

### 2026-09-21 (Sesi 8)
- **Perubahan**:
  - **Fokus Ketat pada Literatur Terunduh (9 Berkas PDF Fisik)**:
    - Menghilangkan pemaksaan 22 artikel referensi; membatasi dokumen hanya mengacu pada **9 artikel ilmiah yang berkas fisik Full-Text PDF-nya benar-benar telah diunduh secara lokal** di `articles/artikel bibit lele/`.
    - Melakukan penomoran ulang berkas PDF di folder `articles/artikel bibit lele/` secara teratur dari `[01]` hingga `[09]`:
      1. `[01]` Gisbert et al. (2021) - *Reviews in Aquaculture*
      2. `[02]` Kurdowi et al. (2025) - *Jurnal Perikanan Unram*
      3. `[03]` Afia et al. (2020) - *Sumerianz J. of Biotech*
      4. `[04]` Pranat et al. (2025) - *Jurnal Perikanan Unram*
      5. `[05]` Essien et al. (2024) - *Acta Nat. Sci.*
      6. `[06]` Jibrin et al. (2024) - *Int. J. Fish. Aquat. Stud.*
      7. `[07]` Uche et al. (2023) - *Agrobiological Records*
      8. `[08]` Srivastava et al. (2012) - *J. Aquac. Res. Dev.*
      9. `[09]` Pelu & Liubana (2025) - *Jurnal Akuakultur Sungai dan Danau*
    - Menyinkronkan ulang seluruh naskah agar hanya menyitir ke-9 artikel terunduh ini:
      - `articles/artikel bibit lele/STANDAR_BIBIT_DAN_PAKAN_LELE.md` (9 dari 9 disitir dan ada di Daftar Pustaka).
      - `research/synthesis/standar-bibit-dan-pakan-lele.md`
      - `articles/artikel bibit lele/README.md`
      - `latex/bibit-lele-references.bib`
      - `latex/laporan-standar-bibit-dan-pendederan.tex`
  - **Pembersihan Berkas PDF Ganda di `output/`**:
    - Menghapus berkas ganda `output/laporan-standar-bibit-dan-pendederan.pdf` dan berkas *auxiliary*-nya.
    - Mengompilasi naskah LaTeX secara langsung menghasilkan **1 berkas PDF utama tunggal**:
      - `output/Standar_Bibit_dan_Pendederan_Lele.pdf` (5 halaman, 0 error, tata letak tabel rapi).
- **Alasan**: Permintaan pengguna untuk tidak memaksakan 22 artikel dan hanya menggunakan artikel yang sudah diunduh secara fisik, serta klarifikasi dan pembersihan file PDF output yang ganda.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 7)
- **Perubahan**:
  - **Pembersihan & Standardisasi Direktori Literatur (`articles/`)**:
    - Menghapus semua folder duplikat, file PDF tersebar di `articles/pdf/`, serta Windows junction link yang membuat pengguna bingung (`articles/artikel-bibit-lele`, `articles/artikel-computer-vision`, `articles/pdf/`).
    - Menstandarkan `articles/` menjadi tepat **2 folder bersih**:
      1. `articles/artikel computer vision/` (berisi 19 Full-Text PDF Computer Vision + `README.md`).
      2. `articles/artikel bibit lele/` (berisi Full-Text PDF bibit lele, `STANDAR_BIBIT_DAN_PAKAN_LELE.md`, dan `README.md`).
  - **Integrasi Informasi Pendederan Lele (`pedederean.csv` & `pedederan.pdf`)**:
    - Mengekstrak data tahapan budidaya operasional di Indonesia dan membedakannya secara tegas dengan klasifikasi ontogenetik/fase biologis.
    - Menambahkan Bab 3: *Integrasi Sistem Pendederan Operasional (Pendederan I, II, dan III) vs Fase Biologis* pada:
      - `research/synthesis/standar-bibit-dan-pakan-lele.md`
      - `articles/artikel bibit lele/STANDAR_BIBIT_DAN_PAKAN_LELE.md`
    - Rincian parameter pendederan:
      - **Pendederan I (14–21 hari)**: Benih 2–3 cm (umur 10–14 hari); padanan Late Fry $\to$ Fingerling Awal; pakan beralih dari cacing sutra ke pelet mikro 0,5 mm (protein 35–40%).
      - **Pendederan II (21–28 hari)**: Benih 5–7 cm (bobot 1,65–2,55 g); padanan Fingerling Pertengahan; fase paling rawan kanibalisme; ransum harian 5–10% biomassa (optimum 5%), frekuensi 3–4x sehari, wajib sortasi/grading tiap 7–10 hari.
      - **Pendederan III (28–35 hari)**: Benih >7–8 cm (>3,8 g hingga 5–10 g); padanan Fingerling Akhir / Juvenil; pelet 1–2 mm; dosis ransum diturunkan ke 2–3% biomassa/hari; persiapan kolam pembesaran akhir.
    - Menambahkan parameter kualitas air pendederan berdasarkan studi Pelu & Liubana (2025) di BBI Teun (suhu 26–30°C dengan aerasi konstan, pH 6,5–8,5, DO $\ge 5$ mg/L) dan persiapan kolam pendederan Sadiana & Rahmanto (2021).
    - Memperbarui `latex/bibit-lele-references.bib` dan `articles/artikel bibit lele/README.md` dengan sitasi Pelu & Liubana (2025) dan Sadiana & Rahmanto (2021).
  - **Penyusunan & Kompilasi Laporan PDF di `output/`**:
    - Membuat naskah LaTeX `latex/laporan-standar-bibit-dan-pendederan.tex` lengkap dengan metadata mahasiswa (Khoirotun Nisa', NIM: 2341720057, Dosen Pembimbing: Dr. Ulla Delfana Rosiani, ST., MT.).
    - Mengompilasi naskah menjadi berkas PDF berkualitas tinggi tanpa overflow:
      - `output/laporan-standar-bibit-dan-pendederan.pdf` (5 halaman, 0 error).
      - `output/Standar_Bibit_dan_Pendederan_Lele.pdf` (salinan nama intuitif).
- **Alasan**: Permintaan pengguna untuk menambahkan data dari `pedederean.csv` dan `pedederan.pdf` ke informasi bibit lele serta menghasilkan output berkas PDF.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 6)
- **Perubahan**:
  - **Fokus Domain Bibit Lele (*Catfish Fry & Fingerlings*)**:
    - Memproses data literatur konsensus dari `bibit lele.csv` dan laporan `bibit lele consensus.pdf` (20 entri artikel ilmiah).
    - Melakukan restrukturisasi dan pengelompokan direktori artikel ilmiah di `articles/`:
      - Direktori `articles/artikel-computer-vision/` (menampung 19 artikel Full-Text PDF domain Visi Komputer & Analisis Gerakan).
      - Direktori `articles/artikel-bibit-lele/` (menampung artikel ilmiah domain Biologi Pembenihan, Nutrisi & Manajemen Pakan Bibit Lele).
      - Menambahkan junction folder Windows `articles/artikel computer vision` dan `articles/artikel bibit lele` untuk kenyamanan navigasi tanpa duplikasi ruang disk.
    - Mengunduh berkas fisik Full-Text PDF artikel bibit lele yang berstatus Open Access (`[01] Gisbert et al. 2021`, `[02] Kurdowi et al. 2025`, `[03] Afia et al. 2020`, `[06] Pranat et al. 2025`, `[08] Essien et al. 2024`, `[11] Jibrin et al. 2024`, `[20] Srivastava et al. 2012`) ke `articles/artikel-bibit-lele/`.
  - **Penyusunan Dokumen Sintesis Standar Bibit & Manajemen Pakan**:
    - Membuat naskah panduan akademik komprehensif `research/synthesis/standar-bibit-dan-pakan-lele.md` yang memuat:
      1. Klasifikasi 5 fase perkembangan bibit lele (*Sac-fry* D0–D3, *Early fry* D4–D7, *Late fry/Transisi* D8–D12, *Fingerling* D13–D30, *Juvenil* >D30).
      2. Standar baku kualitas air kolam benih (suhu 28–31°C, pH 6,5–8,0, DO $\ge 5,0$ mg/L, densitas tebar 500–700 ekor/m³).
      3. Kebutuhan nutrisi pakan alami (Cacing sutra *Tubifex sp.*, *Artemia*, *Daphnia*) dan pelet mikro protein tinggi (35–42% CP).
      4. Standar takaran pakan harian (*Feeding Rate*): Rekomendasi optimum 5% bobot tubuh/hari pada fase fingerling untuk keseimbangan laju pertumbuhan dan efisiensi FCR, serta penurunan bertahap ke 2–2,5% pada fase juvenil.
      5. Frekuensi pakan (3–4 kali/hari) dan metode sebar merata (*broadcast feeding*) di seluruh permukaan kolam untuk mencegah dominasi spasial dan kanibalisme.
      6. Integrasi langsung dengan sistem visi komputer pada Raspberry Pi (pemicuan kuota pakan otomatis berbasis deteksi lonjakan aktivitas kinetik menyambar pakan).
      7. Daftar Pustaka lengkap 20 artikel referensi standar APA dengan DOI aktif.
  - **Katalog & Berkas Sitasi**:
    - Menyusun `articles/artikel-bibit-lele/README.md` (katalog 20 artikel dan pengelompokan tematik).
    - Menyusun `articles/README.md` sebagai master index navigasi seluruh literatur.
    - Menghasilkan berkas BibTeX `latex/bibit-lele-references.bib` berisi 20 entri sitasi terverifikasi.
- **Alasan**: Permintaan pengguna untuk pemfokusan objek penelitian pada fase bibit lele, pengunduhan referensi pendukung dari Consensus, pengelompokan folder artikel, dan pembuatan dokumen standar benih & takaran pakan beserta sitasi dan dafpus.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 5)
- **Perubahan**:
  - **Audit Integritas Sitasi & Penghapusan Halusinasi AI**:
    - Memverifikasi secara langsung berkas fisik PDF `articles/pdf/[01]` (Qian et al., *Discover Applied Sciences* 2026, DOI: 10.1007/s42452-025-08043-5) dan `articles/pdf/[19]` (Vijayalakshmi & Sasithradevi, *Scientific Reports* 2025, DOI: 10.1038/s41598-025-89611-y).
    - Menghapus klaim angka ekstrapolasi/halusinasi AI sebelumnya: menghapus klaim "latensi 68 ms di Raspberry Pi" pada Qian et al. (paper aslinya hanya menguji di GPU 8,1 ms dan menyebut edge deployment sebagai *future work*), serta mengoreksi klaim AquaYOLO menjadi metrik asli paper (Precision 0,889, Recall 0,848, mAP@50 0,909 pada dataset DePondFi tanpa klaim fiktif ketahanan silau/daun).
    - Menghapus seluruh klaim angka performa spekulatif yang belum pernah diuji secara empiris di lab/lapangan (seperti latensi <25 ms, throughput $\ge 10$ FPS, memori <60 MB) dari naskah LaTeX dan dokumen sintesis.
  - **Perampingan Dokumen Sesuai Permintaan Nyata Dosen Pembimbing (Bu Ulla)**:
    - Merombak total `research/synthesis/literature-review-report.md` dari gaya pseudo-tesis yang *over-scoped* menjadi laporan studi literatur yang proporsional, jujur (*humble*), dan fokus pada 4 bagian konkret:
      1. Tabel 19 artikel terverifikasi (Judul, Penulis, Tahun, Jurnal/Konferensi, Link/DOI).
      2. Ringkasan 3–5 kalimat per artikel (100% fakta murni dari teks paper asli tanpa bumbu).
      3. Insight kasar & pola bacaan (metode konvensional vs deep learning, kondisi riil kolam luar ruangan & aerator kontinu, kendala komputasi edge).
      4. Arah metode tentatif untuk dicoba (bukan klaim rekomendasi mutlak).
      5. Daftar Pustaka lengkap 19 referensi standar IEEE.
  - **Sinkronisasi Naskah LaTeX & Tabel**:
    - Memperbarui `latex/tables/article-comparison.tex`, `latex/sections/03-literature-review.tex`, `latex/sections/06-positioning.tex`, dan `latex/sections/07-conclusion.tex`.
    - Kompilasi ulang `output/main.pdf` (27 halaman, 0 error).
- **Alasan**: Umpan balik kritis dan tepat dari pengguna mengenai bahaya sitasi bermasalah, integritas akademik, dan penyelarasan dengan lingkup tugas riil Bu Ulla.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 4)
- **Perubahan**:
  - Menyusun dokumen studi literatur komprehensif 8 bagian sesuai format penugasan Bu Ulla dan hasil brainstorming pengguna di `research/synthesis/literature-review-report.md`.
  - Mengintegrasikan analisis perbandingan mendalam 4 kelompok metode deteksi gerakan (*Frame Differencing*, *Optical Flow*, *GMM Background Subtraction*, dan *Deep Learning*) ke dalam `research/synthesis/comparison.md` dan tabel LaTeX `latex/tables/method-comparison.tex`.
  - Mengembangkan seluruh bab naskah LaTeX Polinema:
    - `latex/main.tex`: Halaman judul resmi Polinema, data mahasiswa (Khoirotun Nisa), dosen pembimbing (Siti Nurul Hidayah, S.Kom., M.Kom. / Bu Ulla), dan abstrak formal.
    - `latex/sections/01-introduction.tex`: Latar belakang komprehensif kolam lele outdoor, over/underfeeding, 4 kendala teknis (aerator kontinu, event 3--6 frame @ 10 FPS, Raspberry Pi edge, telemetri numerik), rumusan masalah, tujuan, dan manfaat.
    - `latex/sections/02-background.tex`: Landasan teori lengkap biologi lele, formulasi matematika *frame differencing*, *optical flow*, GMM, dan arsitektur komputasi Raspberry Pi.
    - `latex/sections/03-literature-review.tex`: Strategi penelusuran basis data, taksonomi query Boolean, dan ulasan mendalam 8 artikel kunci.
    - `latex/sections/04-comparison.tex`: Analisis naratif tabel perbandingan 19 artikel dan tabel perbandingan 4 metode deteksi gerak.
    - `latex/sections/05-research-gap.tex`: Formulasi tiga kesenjangan penelitian berbasis bukti (*Continuous Aeration Baseline Gap*, *Edge Sub-Second Latency Gap*, *Low-Cost Outdoor Monitoring Gap*).
    - `latex/sections/06-positioning.tex`: Posisi penelitian terhadap literatur global dan 3 poin kebaruan penelitian (*research novelty*).
    - `latex/sections/07-conclusion.tex`: Kesimpulan sintesis dan rekomendasi metode utama (*Adaptive Temporal Variance Subtraction*) serta metode alternatif (*Quantized YOLOv8n + FSM*).
  - Berhasil mengompilasi naskah proposal/studi literatur lengkap ke `output/main.pdf` (**25 halaman, 0 error, 0 undefined reference**).
- **Alasan**: Permintaan penugasan studi literatur dari Bu Ulla dengan format 8 bagian yang disesuaikan secara presisi dengan kondisi riil kolam lele ber-aerator.
- **Dampak**: Dokumen siap diserahkan/dikonsultasikan kepada dosen pembimbing.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 3)
- **Perubahan**: Penapisan `result 2.csv`, audit integritas berkas PDF (penghapusan berkas salah Massimo Cacciari 2005), pengunduhan 6 artikel Open Access mutakhir 2023--2025, pembaruan katalog 19 artikel terverifikasi, dan inisialisasi Git commit.
- **Alasan**: Pembaruan literatur fokus 5 tahun terakhir (2022–2026).
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 2)
- **Perubahan**: Integrasi topik skripsi baru pengguna ("Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar Berbasis Computer Vision") dari `conteks.md`, penapisan 100 entri `consensus result.csv`, pengunduhan 14 artikel ilmiah teks lengkap (*full-text PDF*) ke `articles/pdf/`.
- **Status**: Selesai (*Completed*)

---

### 2026-09-21 (Sesi 1)
- **Perubahan**: Reset repositori dan pembersihan total dari data skripsi teman.
- **Status**: Selesai (*Completed*)

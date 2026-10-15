# 📂 Direktori Berkas Luaran (*Output Directory*)

Dokumen ini memetakan seluruh berkas luaran PDF dan file pembantu hasil kompilasi LaTeX yang telah dikelompokkan secara rapi ke dalam subdirektori masing-masing:

```
output/
├── skripsi-proposal/          <-- Naskah Utama Proposal Skripsi
│   └── main.pdf               (25 halaman, format resmi Polinema)
│
├── studi-literatur/           <-- Dokumen Laporan Studi Literatur
│   └── Laporan_Studi_Literatur_Khoirotun_Nisa.pdf (Laporan penugasan Bu Ulla)
│
├── standar-bibit-lele/        <-- Panduan Standar Bibit & Manajemen Pakan
│   └── Standar_Bibit_dan_Pendederan_Lele.pdf (Standar pendederan benih lele)
│
├── analisis-pakan-dan-cv/     <-- Laporan Hasil Bimbingan Dosen Terbaru
│   └── laporan-analisis-pakan-dan-cv.pdf (Analisis Pakan Dibatasi vs Loss & 25 Parameter CV)
│
└── rp-rq-ro/                  <-- Matriks Penelitian RP - RQ - RO Kolam Tenang
    └── matriks-rp-rq-ro.pdf   (2 halaman landscape, tabel formal tanpa aerator)
```

---

## 📑 1. Proposal Skripsi Utama (*Skripsi Proposal*)
- **Jalur Folder**: [`output/skripsi-proposal/`](file:///e:/SKRIPSI/sekeripsi/output/skripsi-proposal/)
- **Berkas PDF**: [`output/skripsi-proposal/main.pdf`](file:///e:/SKRIPSI/sekeripsi/output/skripsi-proposal/main.pdf)
- **Sumber LaTeX**: [`latex/main.tex`](file:///e:/SKRIPSI/sekeripsi/latex/main.tex)
- **Deskripsi**: Naskah lengkap proposal skripsi *"Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar Berbasis Computer Vision pada Kolam Luar Ruangan Ber-aerator"* (Bab 1 s.d. Bab 7, tabel perbandingan 19 artikel, perbandingan 4 metode deteksi gerakan, formulasi 3 research gap, dan positioning penelitian).

---

## 📑 2. Laporan Studi Literatur (*Studi Literatur*)
- **Jalur Folder**: [`output/studi-literatur/`](file:///e:/SKRIPSI/sekeripsi/output/studi-literatur/)
- **Berkas PDF**: [`output/studi-literatur/Laporan_Studi_Literatur_Khoirotun_Nisa.pdf`](file:///e:/SKRIPSI/sekeripsi/output/studi-literatur/Laporan_Studi_Literatur_Khoirotun_Nisa.pdf)
- **Sumber LaTeX**: [`latex/laporan-tugas-bu-ulla.tex`](file:///e:/SKRIPSI/sekeripsi/latex/laporan-tugas-bu-ulla.tex)
- **Deskripsi**: Laporan terstruktur 8 bagian yang merangkum telaah literatur 19 artikel ilmiah terverifikasi untuk diserahkan/dikonsultasikan kepada dosen pembimbing (Dr. Ulla Delfana Rosiani, ST., MT.).

---

## 📑 3. Standar Bibit & Pendederan Lele (*Standar Bibit Lele*)
- **Jalur Folder**: [`output/standar-bibit-lele/`](file:///e:/SKRIPSI/sekeripsi/output/standar-bibit-lele/)
- **Berkas PDF**: [`output/standar-bibit-lele/Standar_Bibit_dan_Pendederan_Lele.pdf`](file:///e:/SKRIPSI/sekeripsi/output/standar-bibit-lele/Standar_Bibit_dan_Pendederan_Lele.pdf)
- **Sumber LaTeX**: [`latex/laporan-standar-bibit-dan-pendederan.tex`](file:///e:/SKRIPSI/sekeripsi/latex/laporan-standar-bibit-dan-pendederan.tex)
- **Deskripsi**: Laporan standar biologi perkembangan benih lele (*Clarias gariepinus*), parameter kualitas air pendederan (BBI Teun), kebutuhan pakan alami vs pelet mikro protein tinggi, dan takaran pakan harian berdasarkan 9 literatur fisik lokal.

---

## 📑 4. Laporan Analisis Pakan & Riset Computer Vision 25 Parameter (*Analisis Pakan & CV*)
- **Jalur Folder**: [`output/analisis-pakan-dan-cv/`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/analisis-pakan-dan-cv/)
- **Berkas PDF**: [`output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf)
- **Sumber LaTeX**: [`latex/laporan-analisis-pakan-dan-cv.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/laporan-analisis-pakan-dan-cv.tex)
- **Deskripsi**: Laporan akademik resmi hasil bimbingan dosen (4 halaman) yang mencakup:
  1. Penegasan konsep skripsi hasil bimbingan (kuota petani terbagi adaptif berbasis riak bibit lele, baseline aerator, evaluasi 1 bulan vs manual, tanpa kualitas air/kesehatan).
  2. Output 1: Analisis kebiasaan bibit lele dan respon pakan (dibatasi 5% vs loss ad libitum, FCR, amonia toksik, compensatory growth).
  3. Output 2: Riset mendalam computer vision dengan tabel komparasi 25 parameter rigid (Hu et al. 2026 vs Wu et al. 2024 vs kondisi skripsi), karakteristik metode visual, dan formulasi teknis model temporal LSTM (input 1D, windowing, target biner, Z-score baseline aerator).

---

## 📑 5. Kajian Lengkap Metodologi CV, Noise Aerator & Kendali Servo Feeder (*Kajian Lengkap CV Lele*)
- **Jalur Folder**: [`output/kajian-lengkap-cv-lele/`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/kajian-lengkap-cv-lele/)
- **Berkas PDF Siap Cetak**: [`output/kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf)
- **Dokumen Sintesis Markdown**: [`research/synthesis/kajian-lengkap-metodologi-cv-dan-noise-kolam.md`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/research/synthesis/kajian-lengkap-metodologi-cv-dan-noise-kolam.md)
- **Sumber LaTeX**: [`latex/kajian-lengkap-metodologi-cv-dan-noise-kolam.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/kajian-lengkap-metodologi-cv-dan-noise-kolam.tex)
- **Deskripsi**: Dokumen kajian akademik dan metodologi komprehensif (7 halaman siap cetak) yang mengintegrasikan:
  1. Analisis visual optik setup riil kamera jarak dekat ($h \approx 30\text{--}50\text{ cm}$) di atas kolam terpal ber-aerator berdasarkan citra aktual `image.png`.
  2. Sintesis kritis seluruh 20 artikel CV global dengan Tabel Master 20 artikel dan formulasi 4 *research gap* berbasis bukti.
  3. Formulasi matematis pemisahan riak makan bibit lele vs derau aerator kontinu via *Welford Running Gaussian Baseline* dan deteksi anomali $Z$-score terverifikasi temporal.
  4. Strategi reduksi derau luar ruangan (pantulan silau matahari via HSV/CLAHE + filter optik polarisasi CPL, daun melayang via arah vektor, bayangan burung via batas luas kontur maksimum).
  5. Kuantifikasi perubahan piksel (*Three-Frame Differencing*) menjadi skor kuantitatif *Feeding Activity Index* ($FAI$) beserta matriks keputusan.
  6. Desain sistem kontrol aktuator servo PCA9685 berbasis *Finite State Machine* (FSM) yang taat batasan kuota harian petani (*daily quota budgeting*) dan jeda *cooldown* 3--5 menit.
  7. Rancangan pengujian lapangan 1 bulan dan parameter evaluasi biologis (ADG, FCR, SR, Feed Saving) serta metrik visi komputer edge.

---

## 📑 6. Matriks Perumusan Penelitian RP, RQ, dan RO Kolam Tenang (*RP-RQ-RO*)
- **Jalur Folder**: [`output/rp-rq-ro/`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/rp-rq-ro/)
- **Berkas PDF Siap Cetak**: [`output/rp-rq-ro/matriks-rp-rq-ro.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/rp-rq-ro/matriks-rp-rq-ro.pdf) (salinan di root: [`matriks-rp-rq-ro-kolam-tenang.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/matriks-rp-rq-ro-kolam-tenang.pdf))
- **Sumber LaTeX**: [`latex/matriks-rp-rq-ro.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/matriks-rp-rq-ro.tex)
- **Deskripsi**: Dokumen matriks perumusan penelitian skripsi formal (2 halaman A4 landscape siap cetak) untuk konteks **kolam luar ruangan tenang tanpa aerator**:
  1. **Halaman 1 (Tabel Matriks Formal)**: Kolom 1 Research Problem (RP) di-merge penuh secara vertikal mencakup seluruh baris 4 Research Questions (RQ1–RQ4) dan 4 Research Objectives (RO1–RO4) tanpa menyinggung aerator.
  2. **Halaman 2 (Konstruk Metodologis & Batasan)**: Pemetaan metodologi dan metrik terukur (Recall, FPR, F1, latensi edge, signifikansi statistik $p < 0,05$, FCR, SR) serta batasan mutlak sistem (*system boundaries*) dan prinsip logika pakan adaptif terkendali kuota petani (*daily quota budgeting*).



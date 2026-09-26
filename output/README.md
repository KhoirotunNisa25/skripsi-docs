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
└── analisis-pakan-dan-cv/     <-- Laporan Hasil Bimbingan Dosen Terbaru
    └── laporan-analisis-pakan-dan-cv.pdf (Analisis Pakan Dibatasi vs Loss & 25 Parameter CV)
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
- **Jalur Folder**: [`output/analisis-pakan-dan-cv/`](file:///e:/SKRIPSI/sekeripsi/output/analisis-pakan-dan-cv/)
- **Berkas PDF**: [`output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf`](file:///e:/SKRIPSI/sekeripsi/output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf)
- **Sumber LaTeX**: [`latex/laporan-analisis-pakan-dan-cv.tex`](file:///e:/SKRIPSI/sekeripsi/latex/laporan-analisis-pakan-dan-cv.tex)
- **Deskripsi**: Laporan akademik resmi hasil bimbingan dosen (4 halaman) yang mencakup:
  1. Penegasan konsep skripsi hasil bimbingan (kuota petani terbagi adaptif berbasis riak bibit lele, baseline aerator, evaluasi 1 bulan vs manual, tanpa kualitas air/kesehatan).
  2. Output 1: Analisis kebiasaan bibit lele dan respon pakan (dibatasi 5% vs loss ad libitum, FCR, amonia toksik, compensatory growth).
  3. Output 2: Riset mendalam computer vision dengan tabel komparasi 25 parameter rigid (Hu et al. 2026 vs Wu et al. 2024 vs kondisi skripsi), karakteristik metode visual, dan formulasi teknis model temporal LSTM (input 1D, windowing, target biner, Z-score baseline aerator).


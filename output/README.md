# 📂 Direktori Berkas Luaran (*Output Directory*) & Pemetaan Dokumen LaTeX

Repositori ini memisahkan secara tegas antara **Kode Sumber LaTeX** (`latex/`) dan **Berkas Luaran PDF Hasil Kompilasi** (`output/`). Setiap dokumen akademik dikelompokkan ke dalam subdirektori tematik yang saling berpasangan:

```text
sekeripsi/
├── latex/                                  <-- KODE SUMBER DOKUMEN LATEX (TERSTRUKTUR PER SUBFOLDER)
│   ├── skripsi-proposal/                   # Naskah utama proposal skripsi Polinema
│   │   ├── main.tex, proposal-bab1.tex
│   │   ├── sections/ (01-pendahuluan, 02-tinjauan-pustaka, dll.)
│   │   ├── tables/ & config/
│   ├── studi-literatur/                    # Laporan telaah 19 artikel ilmiah
│   │   └── laporan-tugas-bu-ulla.tex
│   ├── standar-bibit-lele/                 # Standar biologi & pendederan bibit lele
│   │   └── laporan-standar-bibit-dan-pendederan.tex
│   ├── analisis-pakan-dan-cv/              # Analisis pakan dibatasi & riset 25 parameter CV
│   │   └── laporan-analisis-pakan-dan-cv.tex
│   ├── rp-rq-ro/                           # Matriks perumusan penelitian formal
│   │   └── matriks-rp-rq-ro.tex
│   ├── kajian-lengkap-cv-lele/             # Kajian lengkap metodologi CV & noise aerator
│   │   └── kajian-lengkap-metodologi-cv-dan-noise-kolam.tex
│   ├── komparasi-cv-dan-dl/                # Cetak biru komparasi CV konvensional vs Deep Learning
│   │   └── rancangan-komparasi-metode-cv-dan-dl.tex
│   ├── evaluasi-metode-dan-temuan/         # Laporan evaluasi kuantitatif CV & temuan riset 1 pekan
│   │   └── laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.tex
│   ├── figures/                            # Direktori bersama gambar & diagram alur (flowchart)
│   ├── assets/                             # Logo resmi Polinema
│   ├── styles/                             # Paket gaya LaTeX bersama (.sty & .bst)
│   └── bib/                                # Basis data sitasi BibTeX bersama (.bib)
│
└── output/                                 <-- BERKAS LUARAN HASIL KOMPILASI PDF
    ├── skripsi-proposal/main.pdf
    ├── studi-literatur/Laporan_Studi_Literatur_Khoirotun_Nisa.pdf
    ├── standar-bibit-lele/Standar_Bibit_dan_Pendederan_Lele.pdf
    ├── analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf
    ├── rp-rq-ro/matriks-rp-rq-ro.pdf
    ├── kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf
    ├── komparasi-cv-dan-dl/Rancangan_Komparasi_CV_dan_Deep_Learning.pdf
    └── evaluasi-metode-dan-temuan/laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.pdf
```

---

## 📑 1. Proposal Skripsi Utama (*Skripsi Proposal*)
- **Sumber LaTeX**: [`latex/skripsi-proposal/main.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/skripsi-proposal/main.tex)
- **Berkas PDF**: [`output/skripsi-proposal/main.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/skripsi-proposal/main.pdf)
- **Deskripsi**: Naskah lengkap proposal skripsi *"Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar Berbasis Computer Vision pada Kolam Luar Ruangan Ber-aerator"* (format resmi Polinema, Bab 1 s.d. Bab 7).

---

## 📑 2. Laporan Studi Literatur (*Studi Literatur*)
- **Sumber LaTeX**: [`latex/studi-literatur/laporan-tugas-bu-ulla.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/studi-literatur/laporan-tugas-bu-ulla.tex)
- **Berkas PDF**: [`output/studi-literatur/Laporan_Studi_Literatur_Khoirotun_Nisa.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/studi-literatur/Laporan_Studi_Literatur_Khoirotun_Nisa.pdf)
- **Deskripsi**: Laporan terstruktur 8 bagian yang merangkum telaah literatur 19 artikel ilmiah terverifikasi untuk diserahkan/dikonsultasikan kepada dosen pembimbing (Dr. Ulla Delfana Rosiani, ST., MT.).

---

## 📑 3. Standar Bibit & Pendederan Lele (*Standar Bibit Lele*)
- **Sumber LaTeX**: [`latex/standar-bibit-lele/laporan-standar-bibit-dan-pendederan.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/standar-bibit-lele/laporan-standar-bibit-dan-pendederan.tex)
- **Berkas PDF**: [`output/standar-bibit-lele/Standar_Bibit_dan_Pendederan_Lele.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/standar-bibit-lele/Standar_Bibit_dan_Pendederan_Lele.pdf)
- **Deskripsi**: Laporan standar biologi benih lele (*Clarias gariepinus*), parameter kualitas air pendederan (BBI Teun), kebutuhan pakan alami vs pelet mikro, dan takaran pakan harian berdasarkan 9 literatur fisik lokal.

---

## 📑 4. Laporan Analisis Pakan & Riset Computer Vision 25 Parameter (*Analisis Pakan & CV*)
- **Sumber LaTeX**: [`latex/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.tex)
- **Berkas PDF**: [`output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf)
- **Deskripsi**: Laporan akademik resmi hasil bimbingan dosen mencakup analisis respon pakan (dibatasi 5% vs loss ad libitum, FCR, amonia toksik) dan riset 25 parameter CV.

---

## 📑 5. Matriks Perumusan Penelitian RP, RQ, dan RO Kolam Tenang (*RP-RQ-RO*)
- **Sumber LaTeX**: [`latex/rp-rq-ro/matriks-rp-rq-ro.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/rp-rq-ro/matriks-rp-rq-ro.tex)
- **Berkas PDF**: [`output/rp-rq-ro/matriks-rp-rq-ro.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/rp-rq-ro/matriks-rp-rq-ro.pdf)
- **Deskripsi**: Dokumen matriks perumusan penelitian formal (2 halaman A4 landscape siap cetak) mencakup 4 Research Questions dan 4 Research Objectives terukur.

---

## 📑 6. Kajian Lengkap Metodologi CV, Noise Aerator & Kendali Servo Feeder (*Kajian Lengkap CV Lele*)
- **Sumber LaTeX**: [`latex/kajian-lengkap-cv-lele/kajian-lengkap-metodologi-cv-dan-noise-kolam.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/kajian-lengkap-cv-lele/kajian-lengkap-metodologi-cv-dan-noise-kolam.tex)
- **Berkas PDF**: [`output/kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf)
- **Deskripsi**: Kajian akademik dan metodologi komprehensif (7 halaman) mencakup formulasi running baseline aerator, reduksi glint matahari via kanal S, dan FSM pengendali servo kuota harian.

---

## 📑 7. Rancangan Metodologi Komparasi CV Konvensional vs. Lightweight Deep Learning (*Komparasi CV & DL*)
- **Sumber LaTeX**: [`latex/komparasi-cv-dan-dl/rancangan-komparasi-metode-cv-dan-dl.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/komparasi-cv-dan-dl/rancangan-komparasi-metode-cv-dan-dl.tex)
- **Berkas PDF**: [`output/komparasi-cv-dan-dl/Rancangan_Komparasi_CV_dan_Deep_Learning.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/komparasi-cv-dan-dl/Rancangan_Komparasi_CV_dan_Deep_Learning.pdf)
- **Deskripsi**: Cetak biru akademik (7 halaman A4 portrait) merumuskan studi komparasi *head-to-head*: CV Konvensional vs YOLOv8-nano murni vs YOLOv8n + Bi-LSTM vs MobileNetV3-Small.

---

## 📑 8. Laporan Hasil Evaluasi Metode CV & Temuan Riset 1 Pekan (*Evaluasi Metode & Temuan*)
- **Sumber LaTeX**: [`latex/evaluasi-metode-dan-temuan/laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.tex`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/latex/evaluasi-metode-dan-temuan/laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.tex)
- **Berkas PDF Siap Cetak Bimbingan**: [`output/evaluasi-metode-dan-temuan/laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.pdf`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/output/evaluasi-metode-dan-temuan/laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.pdf)
- **Deskripsi**: Laporan akademik komprehensif (6 halaman A4 portrait siap bimbingan Bu Ulla) mencakup:
  1. Identitas riset & alur pipeline 6 tahap OpenCV konvensional.
  2. Hasil ekstraksi 100% dari 165 video MP4 kontinu (27,37 jam / 985.386 frame / 3.059 event riak lele).
  3. Matriks evaluasi kuantitatif (Akurasi 98,85%, Presisi 86,67%, Recall 88,14%, Skor F1 0,8740).
  4. Penegasan istilah etika akademik arahan Bu Ulla: "Kandidat Aktivitas" & "Kandidat Keresahan" (tanpa overclaim deteksi lapar langsung).
  5. Pengujian hardware edge Raspberry Pi 5 (RAM 48,6 MB, CPU 24,5%--28,2%, Suhu 63,8°C--68,2°C, Latensi 9,6 ms / Throughput 104,2 FPS).
  6. Justifikasi ilmiah research gap berbasis kebiasaan nokturnal lele (puncak aktif 21.00--04.00 vs pasif siang hari).

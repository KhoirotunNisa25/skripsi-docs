# Academic Literature Review Research Workspace

Repositori ini adalah ruang kerja riset studi literatur terstruktur untuk penyusunan skripsi akademik. Repositori ini dirancang untuk mencari, mengumpulkan, memverifikasi, menganalisis, membandingkan, dan menyintesis artikel ilmiah secara sistematis.

[![Folder Bibit Lele](https://img.shields.io/badge/Folder%20Artikel-Bibit%20Lele-059669?style=for-the-badge&logo=adobeacrobatreader&logoColor=white)](articles/artikel%20bibit%20lele/)
[![Folder Computer Vision](https://img.shields.io/badge/Folder%20Artikel-Computer%20Vision-2563EB?style=for-the-badge&logo=adobeacrobatreader&logoColor=white)](articles/artikel%20computer%20vision/)

> [!TIP]
> ### 📚 Repositori Berkas Artikel Ilmiah Terkelompok
> Kumpulan naskah lengkap artikel ilmiah yang digunakan dalam penelitian dikelompokkan dalam 2 folder:
> 
> * 🐟 **Folder Artikel Bibit Lele & Standar Pakan**: [**Buka `articles/artikel bibit lele/`**](articles/artikel%20bibit%20lele/) (Dilengkapi dokumen panduan: [`STANDAR_BIBIT_DAN_PAKAN_LELE.md`](articles/artikel%20bibit%20lele/STANDAR_BIBIT_DAN_PAKAN_LELE.md)).
> * 👁️ **Folder Artikel Computer Vision & Motion**: [**Buka `articles/artikel computer vision/`**](articles/artikel%20computer%20vision/).
> * 📋 **Indeks Pusat**: [**Buka `articles/README.md`**](articles/README.md).

---

## 1. Prinsip Arsitektur: Sumber Kebenaran (*Source of Truth*)

Prinsip dasar yang mengatur ruang kerja penelitian ini adalah:

```text
research/*.md = SOURCE OF TRUTH (Data & Analisis Riset)
latex/*.tex   = PRESENTATION / FINAL DOCUMENT (Naskah Publikasi/Laporan)
```

- **Riset Terlebih Dahulu**: Seluruh temuan, metadata artikel, ekstraksi, analisis, tema sintesis, dan evaluasi *research gap* **WAJIB** dicatat dalam format Markdown di bawah direktori `research/` sebelum dituangkan ke dalam naskah LaTeX.
- **LaTeX Hanya Sebagai Media Presentasi**: Jangan jadikan naskah LaTeX sebagai basis data utama. Saat ada perubahan informasi riset, perbarui file Markdown terkait terlebih dahulu, kemudian sinkronkan ke seksi naskah LaTeX.

---

## 2. Struktur Ruang Kerja (*Workspace Structure*)

```text
sekeripsi/
│
├── articles/                    # Repositori & katalog naskah lengkap artikel ilmiah
│   └── pdf/                     # Berkas PDF artikel & README.md katalog
│
├── research/                    # Basis data analisis riset & sintesis literatur
│   ├── papers/                  # Folder analisis per paper (misal: 01-nama-paper/)
│   │   ├── _template/           # Template standar paper baru (metadata, source, analysis)
│   │   └── .gitkeep
│   │
│   ├── synthesis/               # Sintesis komparatif lintas literatur
│   │   ├── comparison.md        # Matriks perbandingan artikel
│   │   ├── themes.md            # Sintesis tematik
│   │   ├── research-gap.md      # Celah penelitian berbasis bukti
│   │   └── thesis-positioning.md# Pemosisian penelitian skripsi
│   │
│   ├── business-logic.md        # Logika penelitian & konsep skripsi
│   ├── research-requirements.md # Kebutuhan penelitian, RQ, & metrik evaluasi
│   ├── research-status.md       # Status & progres studi literatur
│   ├── search-log.md            # Log sesi pencarian & kueri literatur
│   └── change-log.md            # Riwayat perubahan konsep & dokumen riset
│
├── latex/                       # Naskah dokumen skripsi dalam format LaTeX
│   ├── main.tex                 # Entry point utama naskah skripsi
│   ├── references.bib           # Sitasi BibTeX tervalidasi
│   │
│   ├── assets/                  # Logo dan aset visual resmi
│   │   └── polinema-logo.png
│   │
│   ├── config/                  # Pengaturan layout & paket LaTeX
│   │   ├── packages.tex
│   │   ├── formatting.tex
│   │   └── commands.tex
│   │
│   ├── sections/                # Bab-bab naskah skripsi
│   │   ├── 01-introduction.tex
│   │   ├── 02-background.tex
│   │   ├── 03-literature-review.tex
│   │   ├── 04-comparison.tex
│   │   ├── 05-research-gap.tex
│   │   ├── 06-positioning.tex
│   │   └── 07-conclusion.tex
│   │
│   ├── tables/                  # Definisi tabel LaTeX (article-comparison.tex)
│   └── figures/                 # Diagram, arsitektur, dan grafik
│
├── output/                      # Berkas PDF hasil kompilasi LaTeX (main.pdf)
├── scratch/                     # Skrip pembantu & pengolahan data sementara
├── README.md                    # Panduan repositori
└── .gitignore                   # Konfigurasi pengabaian berkas Git
```

---

## 3. Kompilasi Dokumen LaTeX

Untuk mengompilasi naskah `latex/main.tex` menjadi `output/main.pdf`:

```powershell
cd latex
pdflatex -interaction=nonstopmode -output-directory=../output main.tex
bibtex ../output/main
pdflatex -interaction=nonstopmode -output-directory=../output main.tex
pdflatex -interaction=nonstopmode -output-directory=../output main.tex
```

Atau menggunakan `latexmk`:

```powershell
cd latex
latexmk -pdf -outdir=../output main.tex
```

Hasil PDF akan otomatis berada pada `output/main.pdf`.

---

## 4. Langkah Selanjutnya

1. Tentukan topik spesifik, rumusan masalah, dan tujuan skripsi Anda di [research/business-logic.md](research/business-logic.md).
2. Tentukan pertanyaan penelitian (*Research Questions*) di [research/research-requirements.md](research/research-requirements.md).
3. Mulai pencarian artikel ilmiah dan catat kueri di [research/search-log.md](research/search-log.md).
4. Masukkan berkas PDF artikel ke [articles/pdf/](articles/pdf/) dan buat analisisnya di [research/papers/](research/papers/).
5. Lakukan sintesis tematik, matriks perbandingan, dan rumuskan *research gap*.
6. Tuliskan naskah akhir pada bab-bab LaTeX di [latex/sections/](latex/sections/).

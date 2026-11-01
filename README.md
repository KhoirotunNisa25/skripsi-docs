# 📚 Skripsi Docs: Dokumentasi Akademik & Naskah Proposal/Skripsi

Repositori ini memuat seluruh naskah akademik (LaTeX), tinjauan pustaka terstruktur, sintesis matriks SOTA, analisis *research gap*, dan dokumentasi bimbingan penelitian skripsi:

> **"Sistem Pemberian Pakan Adaptif Berbasis Deteksi Riak Aktivitas Permukaan Bibit Ikan Lele (*Clarias sp.*) Menggunakan *Computer Vision* pada Kolam Luar Ruangan Ber-aerator"**  
> **Peneliti**: Khoirotun Nisa' (NIM: 2341720057)  
> **Dosen Pembimbing**: Dr. Ulla Delfana Rosiani, ST., MT.  
> **Program Studi**: Sarjana Terapan Teknik Informatika, Politeknik Negeri Malang  
> **Repositori Source Code & Engine**: [github.com/KhoirotunNisa25/skripsi-engine](https://github.com/KhoirotunNisa25/skripsi-engine)

---

## 🏗️ Struktur Ruang Kerja (*Workspace Structure*)

```text
skripsi-docs/
├── latex/                               # Berkas sumber naskah LaTeX standar Polinema
│   ├── proposal-bab1.tex                # Entry point kompilasi Draf Bab 1 & Daftar Pustaka
│   ├── matriks-rp-rq-ro.tex             # Matriks formal RP-RQ-RO standar Bu Ulla (Landscape)
│   ├── rancangan-komparasi-metode-cv-dan-dl.tex # Naskah komparasi CV vs Lightweight DL
│   ├── sections/                        # Sub-bab narasi (01-introduction, dll.)
│   ├── figures/                         # Diagram alur sistem & montase visual resmi
│   └── references.bib                   # Pustaka BibTeX tervalidasi APA 7th lengkap DOI
├── research/                            # Sumber kebenaran (Source of Truth) riset
│   ├── panduan-penulisan-proposal-skripsi.md # Buku panduan resmi penulisan proposal Polinema
│   ├── business-logic.md                # Logika riset, batasan kolam, & kendali kuota pakan
│   ├── rancangan-komparasi-metode-cv-dan-dl.md # Desain eksperimen TFD vs Lightweight DL
│   ├── observasi_awal/                  # Ground truth manual 151 event observasi awal 3 hari
│   └── change-log.md                    # Catatan perubahan berkala setiap sesi riset
├── articles/                            # Katalog naskah lengkap artikel ilmiah bereputasi
│   ├── artikel computer vision/         # 20 PDF artikel visi komputer & perilaku makan ikan
│   ├── artikel bibit lele/              # 14 PDF artikel standar pendederan lele & pakan
│   └── searches/                        # CSV hasil pencarian Consensus & literatur
├── output/                              # Berkas PDF hasil kompilasi LaTeX siap cetak/bimbingan
├── Proposal_Bab1_Khoirotun_Nisa.pdf     # Berkas PDF Draf Bab 1 siap bimbingan (10 Halaman)
└── matriks-rp-rq-ro-kolam-tenang.pdf    # Berkas PDF Matriks RP-RQ-RO siap bimbingan (2 Halaman)
```

---

## 🔗 Hubungan Antar-Repositori

| Repositori | URL GitHub | Peran & Isi Utama |
| :--- | :--- | :--- |
| **`skripsi-docs`** (Repo ini) | [github.com/KhoirotunNisa25/skripsi-docs](https://github.com/KhoirotunNisa25/skripsi-docs) | Naskah LaTeX Bab 1–5, sintesis artikel ilmiah, panduan Bu Ulla, dan berkas PDF bimbingan. |
| **`skripsi-engine`** | [github.com/KhoirotunNisa25/skripsi-engine](https://github.com/KhoirotunNisa25/skripsi-engine) | Source code deteksi riak, batch extractor 165 video, server Flask Raspberry Pi 5, dan hasil CSV/grafik. |

---

## 🛠️ Kompilasi Naskah LaTeX

Kompilasi naskah proposal Bab 1:
```bash
cd latex
pdflatex proposal-bab1.tex
bibtex proposal-bab1
pdflatex proposal-bab1.tex
pdflatex proposal-bab1.tex
```
Hasil kompilasi akan menghasilkan PDF bersih siap bimbingan di direktori `output/`.

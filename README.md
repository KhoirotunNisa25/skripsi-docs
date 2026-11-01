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
├── latex/                               # Berkas sumber naskah LaTeX (terstruktur per subfolder):
│   ├── skripsi-proposal/                # Naskah utama proposal skripsi Polinema (main.tex, proposal-bab1.tex, sections/)
│   ├── studi-literatur/                 # Laporan telaah 19 artikel ilmiah (laporan-tugas-bu-ulla.tex)
│   ├── standar-bibit-lele/              # Standar biologi & pendederan benih lele (laporan-standar-bibit-dan-pendederan.tex)
│   ├── analisis-pakan-dan-cv/           # Analisis pakan dibatasi & riset 25 parameter CV (laporan-analisis-pakan-dan-cv.tex)
│   ├── rp-rq-ro/                        # Matriks perumusan penelitian formal (matriks-rp-rq-ro.tex)
│   ├── kajian-lengkap-cv-lele/          # Kajian lengkap metodologi CV & noise aerator (kajian-lengkap-metodologi-cv-dan-noise-kolam.tex)
│   ├── komparasi-cv-dan-dl/             # Cetak biru komparasi CV konvensional vs Deep Learning (rancangan-komparasi-metode-cv-dan-dl.tex)
│   ├── evaluasi-metode-dan-temuan/      # Laporan evaluasi kuantitatif CV & temuan riset 1 pekan (laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.tex)
│   ├── figures/                         # Diagram alur sistem, montase visual, & grafik riset bersama
│   ├── assets/                          # Logo resmi Polinema
│   ├── styles/                          # Paket gaya LaTeX bersama (.sty & .bst)
│   └── bib/                             # Basis data sitasi BibTeX bersama (references.bib)
├── output/                              # Berkas PDF hasil kompilasi LaTeX siap cetak/bimbingan:
│   ├── skripsi-proposal/main.pdf
│   ├── studi-literatur/Laporan_Studi_Literatur_Khoirotun_Nisa.pdf
│   ├── standar-bibit-lele/Standar_Bibit_dan_Pendederan_Lele.pdf
│   ├── analisis-pakan-dan-cv/laporan-analisis-pakan-dan-cv.pdf
│   ├── rp-rq-ro/matriks-rp-rq-ro.pdf
│   ├── kajian-lengkap-cv-lele/Kajian_Lengkap_CV_Bibit_Lele_dan_Noise_Aerator.pdf
│   ├── komparasi-cv-dan-dl/Rancangan_Komparasi_CV_dan_Deep_Learning.pdf
│   └── evaluasi-metode-dan-temuan/laporan-hasil-evaluasi-metode-cv-dan-temuan-riset.pdf
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

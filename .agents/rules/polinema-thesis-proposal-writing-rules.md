---
trigger: model_decision
description: Digunakan saat menyusun, merevisi, atau memvalidasi draf naskah proposal skripsi (Bab 1, Bab 2, Bab 3, dan naskah LaTeX) sesuai standar resmi D4 Teknik Informatika JTI Polinema yang diampu oleh Dr. Ulla Delfana Rosiani, ST., MT.
---

# Aturan Penulisan Proposal Skripsi D4 Teknik Informatika JTI Polinema
**Dosen Pembimbing**: Dr. Ulla Delfana Rosiani, ST., MT.  
**Referensi Induk**: [`research/panduan-penulisan-proposal-skripsi.md`](file:///run/media/nisaak/New%20Volume/SKRIPSI/sekeripsi/research/panduan-penulisan-proposal-skripsi.md)

---

## 1. Aturan Kalimat Judul (Materi MT1)
1. **3 Komponen Wajib**: Objek Penelitian (*Benih ikan lele*), Tujuan (*Sistem pakan adaptif*), Metode Utama (*Three-frame differencing*).
2. **Batasan Panjang**: Maksimal **$< 20$ kata**.
3. **Larangan**: Dilarang mencantumkan library pendukung sepele (misal: "Python OpenCV Tkinter"), dilarang istilah umum tanpa metode (misal: "Berbasis AI").

---

## 2. Aturan Bab 1: Pendahuluan (Materi MT2 & M3)
1. **Sub-Bab Baku**:
   - `1.1` Latar Belakang
   - `1.2` Rumusan Masalah
   - `1.3` Batasan Masalah
   - `1.4` Tujuan Penelitian
   - `1.5` Sistematika Penulisan
2. **Pola Narasi Latar Belakang (OMKKMasaSolTu)**:
   - **O**: Objek & urgensi lapangan (mortalitas bibit lele 2--12 cm (Pendederan I--IV) akibat kanibalisme & pembusukan amonia).
   - **M**: Metode terkini di literatur (feeder timer & model DL akuakultur).
   - **KK**: Kelebihan & kelemahan metode (DL akurat di lab jernih tapi gagal pada kolam keruh pendederan lele $\le 3$ cm & boros komputasi).
   - **Masa / RP**: Masalah inti penelitian (*Research Problem*). **WAJIB ditulis eksplisit di akhir latar belakang**.
   - **Sol**: Solusi usulan (*Adaptive Three-Frame Differencing + Bitwise AND* + HSV S-channel + FAI + FSM servo).
   - **Tu**: Rangkuman tujuan penelitian.
3. **Kaidah RP $\to$ RQ $\to$ RO (Konsisten 1-ke-1)**:
   - RQ terdiri dari 2--4 pertanyaan spesifik menggunakan kata tanya *"Bagaimana"* atau *"Apa"*.
   - Setiap butir RQ dijawab oleh RO secara berurutan menggunakan kata kerja operasional (*mengembangkan, merancang, menguji, menganalisis*).
4. **Standar Sitasi Bab 1**: Minimal $\ge 8$ referensi mutakhir (5 tahun terakhir 2020--2025), format APA 7th, kombinasi data lokal (KKP/SNI) dan jurnal global bereputasi.

---

## 3. Aturan Bab 2: Landasan Teori & SOTA (Materi MT3 & M5)
1. **Sub-Bab Baku**:
   - `2.1` Landasan Teori (Umum ke Khusus, sertakan formula matematika formal Gonzalez & Woods, hindari kamus definisi).
   - `2.2` Penelitian Terdahulu / State of the Art (SOTA).
2. **Tabel Perbandingan SOTA Wajib**:
   - Kolom: *No*, *Peneliti & Tahun*, *Metode*, *Objek / Dataset*, *Hasil Utama*, *Keterbatasan / GAP*.
   - Minimal 5 rujukan (campuran nasional & internasional).
3. **Penegasan Akhir Bab 2**:
   - *Research Gap*: Kesenjangan literatur yang belum terselesaikan.
   - *Novelty*: Unsur kebaruan algoritma/pendekatan.
   - *Knowledge Contribution*: Kontribusi perbaikan metode (*method improvement*).

---

## 4. Aturan Bab 3: Metodologi Penelitian (Materi MT4 & M7)
1. **Sub-Bab Baku (3.1 s.d. 3.7)**:
   - `3.1` Waktu dan Tempat Penelitian (Lab IVSS Polinema & kolam mitra).
   - `3.2` Data dan Sumber Data (Karakteristik video riak bibit lele, durasi, pencahayaan, resolusi).
   - `3.3` Tahapan Penelitian / Alur Metodologi (Diagram alir *flowchart* menyeluruh).
   - `3.4` Metode Pengumpulan Data.
   - `3.5` Metode Pengolahan Data / Implementasi Algoritma.
   - `3.6` Metode Pengujian dan Evaluasi (Confusion matrix, akurasi, presisi, recall, F1, FPS, latensi, kriteria keberhasilan).
   - `3.7` Perangkat dan Tools Penelitian (Tabel Hardware & Software).
2. **Kriteria Keberhasilan Terukur**: Wajib dinyatakan secara kuantitatif (misal: akurasi deteksi riak $\ge 85\%$, kecepatan $\ge 10$ FPS pada Raspberry Pi).

---

## 5. Aturan Etika Akademik & AI Ethics (Materi M12 & M13)
1. Bebas fabrikasi, falsifikasi data, dan plagiarisme.
2. Jika menggunakan bantuan AI generatif untuk perbaikan tata bahasa atau penataan struktur naskah, **WAJIB mencantumkan pernyataan resmi**:
   > *"Penulis menyatakan bahwa dalam proses penyusunan naskah proposal skripsi ini, penulis menggunakan bantuan alat kecerdasan buatan untuk perbaikan tata bahasa, penataan struktur kalimat, dan kejelasan narasi akademis tanpa mengubah substansi ilmiah. Seluruh data literatur, formulasi matematis, metodologi, dan analisis merupakan gagasan dan tanggung jawab penulis sepenuhnya."*

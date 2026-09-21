# Log Pencarian Literatur (*Search Log*)

## Sesi Pencarian 1: Penelusuran Consensus AI Awal
### Metadata Sesi
- **Tanggal**: 2026-09-21
- **Topik Pencarian**: Deteksi Aktivitas dan Perilaku Makan Ikan dalam Akuakultur (*Fish Feeding Behavior, Appetite Assessment, & Computer Vision*)
- **Basis Data**: Consensus AI Academic Search Engine
- **Tautan Pencarian**: [Consensus Search: deteksi-aktivitas-makan-ikan](https://consensus.app/search/deteksi-aktivitas-makan-ikan/dOJjbVUuQh2V0wlidgQ_gQ/?utm_source=share&utm_medium=clipboard)
- **Berkas Ekspor**: [consensus result.csv](file:///e:/SKRIPSI/sekeripsi/consensus%20result.csv) (100 entri artikel)

---

## Sesi Pencarian 2: Penelusuran Consensus AI Terfokus (2022–2026)
### Metadata Sesi
- **Tanggal**: 2026-09-21
- **Topik Pencarian**: Deteksi Aktivitas Makan Ikan Mutakhir (Fokus 5 Tahun Terakhir: 2022–2026)
- **Basis Data**: Consensus AI Academic Search Engine
- **Tautan Pencarian**: [Consensus Search 2: deteksi-aktivitas-makan-ikan](https://consensus.app/search/deteksi-aktivitas-makan-ikan/dfvgxlS3TbqKYpgzVnIf6Q/?utm_source=share&utm_medium=clipboard)
- **Berkas Ekspor**: [result 2.csv](file:///e:/SKRIPSI/sekeripsi/result%202.csv) (20 entri artikel mutakhir 2022–2026)

---

### Audit Kualitas & Integritas Berkas PDF (Quality Check)
1. **Pemeriksaan Isi Berkas Sebelumnya**:
   - Seluruh 14 berkas awal diuji menggunakan parser `pypdf`.
   - **Temuan Anomali**: Berkas `[14]` lama (*Wei et al. 2021*) ternyata berisi naskah sastra Portugis dari JSTOR (*"NOMES DE LUGAR: CONFIM"* oleh Massimo Cacciari, 2005) akibat ketidaksesuaian tautan mirror.
   - **Tindakan Koreksi**: Berkas anomali tersebut langsung **dihapus** dan digantikan oleh artikel-artikel mutakhir (2023–2025) yang diverifikasi 100% otentik.
2. **Pengunduhan & Verifikasi Batch 2 (Tanpa Live Browser)**:
   - Dilakukan pemindaian endpoint Open Access langsung (PLOS ONE, Frontiers in Marine Science, IAES IJ-AI, Nature Scientific Reports, STEMM Press JBDC, dan ADRA).
   - Berhasil mengunduh dan memverifikasi 6 artikel baru:
     1. `Dong et al. (2024)` - *PLOS ONE* (Three-stream network, 24 halaman)
     2. `Zhang et al. (2024)` - *Frontiers in Marine Science* (RUSNet adaptive optical flow, 14 halaman)
     3. `Aris et al. (2023)` - *IAES IJ-AI* (Background subtraction & GMM dynamic, 12 halaman)
     4. `Kamal et al. (2025)` - *Techno Agriculturae* (Otomasi pakan lele intensif via akustik, 11 halaman)
     5. `Yang et al. (2025)` - *Journal of Big Data and Computing* (State-of-the-Art CV fish feeding 2025, 9 halaman)
     6. `Vijayalakshmi & Sasithradevi (2025)` - *Scientific Reports* (AquaYOLO outdoor pond, 12 halaman)
   - **Catatan Khusus**: Kamal et al. (2025) spesifik meneliti lele (*Clarias gariepinus*) pada budidaya densitas tinggi, namun menggunakan sensor akustik (suara kunyahan) alih-alih visi komputer. Tetap disertakan sebagai rujukan komparatif antar-modalitas.

---

### Ringkasan Status Koleksi Artikel
- **Total Artikel Terverifikasi**: 19 artikel Full-Text PDF.
- **Distribusi Tahun**: 12 artikel terbit pada periode mutakhir (**2023–2026**), dan 7 artikel fondasional klasik (**2014–2021**).
- **Penyimpanan**: Direktori [articles/pdf/](file:///e:/SKRIPSI/sekeripsi/articles/pdf/) (`[01]` s.d. `[19]`).
- **Katalog Lengkap**: [articles/pdf/README.md](file:///e:/SKRIPSI/sekeripsi/articles/pdf/README.md).

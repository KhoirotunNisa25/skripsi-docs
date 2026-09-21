# Analisis Gap Penelitian (*Research Gap*) Berbasis Bukti Literatur

## Gambaran Umum

Berdasarkan sintesis sistematis terhadap literatur ilmiah yang ditinjau melalui Consensus, ditemukan bahwa mayoritas penelitian terdahulu mengenai *computer vision* untuk pemantauan makan ikan dilakukan pada:
1. **Sistem Sirkulasi Akuakultur Tertutup (RAS) / Indoor Laboratorium** dengan air jernih, pencahayaan terkontrol, dan kondisi permukaan air yang tenang tanpa aerasi turbulen.
2. **Kondisi Perairan Tenang (*Calm Water Assumption*)**, di mana pemodelan latar belakang (*background subtraction*) mengasumsikan bahwa pergerakan air di permukaan kolam mendekati nol ($\approx 0$) ketika ikan tidak aktif.

---

## Gap Penelitian Berbasis Bukti Literatur (*Evidence-Based Research Gaps*)

### Gap 1: Celah Pemodelan *Moving Background* pada Kolam Luar Ruangan Ber-aerator Aktif (*The Continuous Aeration Baseline Gap*)
- **Kategori**: Gap Metodologis & Kondisi Lingkungan Nyata (*Realistic Operational Gap*)
- **Bukti dari Literatur**:
  - Studi pemantauan makan ikan (Hu et al. 2026; Zhao et al. 2025; Liu et al. 2014; Ubiña et al. 2021) berfokus pada tangki indoor atau RAS dengan air tenang dan latar belakang statis.
  - Model analisis riak/splash (Wu et al. 2024; Hu et al. 2022) mengasumsikan bahwa setiap riak air yang muncul adalah hasil interaksi makan ikan, karena tidak adanya aerator gelembung mekanis konstan di area observasi.
- **Aspek yang Belum Terjawab**: Bagaimana memodelkan kondisi *baseline* pergerakan air kolam luar ruangan (*outdoor*) yang dipicu oleh aerator mekanis yang menyala terus-menerus, sehingga sistem mampu memisahkan osilasi periodik gelembung aerator dari deviasi pergerakan ikan lele yang sebenarnya.
- **Signifikansi bagi Skripsi**: Menjawab gap ini menjadi kunci keberhasilan deteksi otomatis di kolam nyata pembudidaya lele, di mana aerator tidak boleh dimatikan karena berkaitan dengan pasokan oksigen terlarut (*dissolved oxygen*).

---

### Gap 2: Penanganan Derau Visual Lingkungan Dinamis Luar Ruangan (*Outdoor Visual Noise Robustness Gap*)
- **Kategori**: Gap Robustness & Pemfilteran Noise
- **Bukti dari Literatur**:
  - Sebagian besar model berbasis *deep learning* (YOLO / CNN) mengalami penurunan presisi drastis ketika dihadapkan pada pantulan cahaya matahari (*sun glare*), pantulan lampu malam hari, dan bayangan dinamis (Ni et al. 2024; Qian et al. 2025).
  - Pada kolam lele terbuka (*outdoor*), terdapat gangguan eksternal acak seperti dedaunan yang jatuh mengapung dan burung yang menyentuh air, memicu *false positive*.
- **Aspek yang Belum Terjawab**: Metode penyaringan derau (*noise suppression*) yang ringan namun adaptif terhadap perubahan iluminasi ekstrem (pagi matahari terbit vs siang terik vs malam lampu buatan) pada kolam ikan lele.
- **Solusi yang Diajukan Skripsi**: Mengintegrasikan normalisasi pencahayaan, deteksi wilayah ROI aerator, dan filter morfologis untuk mengeliminasi distorsi cahaya sebelum evaluasi skor pergerakan.

---

### Gap 3: Resolusi Temporal Ekstrem untuk Karakteristik Event Singkat (*High-Temporal Resolution for Brief Fish Events*)
- **Kategori**: Gap Resolusi Temporal
- **Bukti dari Literatur**:
  - Banyak metode terdahulu menggunakan interval sampling temporal longgar (misal: 10–30 frame sekali atau window agregasi 5–10 detik) untuk menghemat komputasi (Cui et al. 2024).
  - **Temuan Awal Observasi Lapangan Skripsi**: Event kemunculan atau sentakan aktivitas ikan lele ke permukaan berlangsung sangat singkat, hanya **3–6 frame (0,3–0,6 detik pada 10 FPS)**.
- **Aspek yang Belum Terjawab**: Bagaimana mengekstraksi dan mendeteksi event pergerakan ultra-singkat tersebut secara *per-frame* tanpa membebani kapasitas komputasi perangkat *edge* (Raspberry Pi).
- **Solusi yang Diajukan Skripsi**: Menerapkan *frame differencing* adaptif atau *frame-pair motion encoding* yang ringan secara komputasional pada resolusi temporal tinggi (10 FPS per-frame).

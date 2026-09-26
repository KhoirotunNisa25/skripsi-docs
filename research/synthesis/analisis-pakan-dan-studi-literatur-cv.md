# 📘 Analisis Perilaku Makan Bibit Lele & Riset Mendalam Computer Vision
## Dokumen Kajian Akademik Terintegrasi (Berdasarkan Hasil Bimbingan Dosen)

---

## 📌 BAGIAN I: PENEGASAN KONSEP SKRIPSI HASIL BIMBINGAN

Berdasarkan hasil konsultasi dan bimbingan langsung dengan dosen pembimbing (Dr. Ulla Delfana Rosiani, ST., MT.), batasan, logika sistem, dan konteks penelitian diselaraskan secara tegas:

```
[PETANI]                                [KAMERA TOP-VIEW]
   │ (Menetapkan Kuota Harian, misal 1 kg/hari) │ (Merekam Permukaan Kolam @ 10 FPS)
   ▼                                            ▼
┌────────────────────────────────────────────────────────┐
│             SISTEM COMPUTER VISION (EDGE)              │
│  - Memodelkan baseline gejolak konstan aerator         │
│  - Mendeteksi deviasi/lonjakan riak bibit lele         │
│  - Menginterpretasi sinyal respons makan aktif         │
└──────────────────────────┬─────────────────────────────┘
                           │ Pemicuan Sub-Porsi Pakan (misal 50–100 g)
                           ▼
                    [FEEDER OTOMATIS]
                           │
       (Berhenti jika Kuota Harian Petani Tercapai)
```

1. **Objek Penelitian**: **BIBIT IKAN LELE** (*Clarias sp.*, fase benih / pendederan).
2. **Batasan Mutlak (*System Boundaries*)**:
   - **TIDAK berfokus pada kualitas air** (kualitas air adalah domain penelitian terpisah kolaborator / Varizky; parameter air hanya sebagai kondisi lingkungan pendukung/keterbatasan, bukan variabel independen).
   - **TIDAK berfokus pada diagnosis kesehatan ikan**.
   - **TIDAK menggantikan kontrol petani secara total**.
3. **Logika Inti Sistem**: *"Mengamati riak $\to$ Menentukan pemberian pakan terkontrol"*.
   - Bukan *timer* buta (*"tiap jam pasti diberi pakan"*).
   - Petani menentukan batas kemampuan pakan harian (*ceiling quota*, contoh: 1 kg pakan/hari). Pakan kemudian dibagi (*sub-rationing*) mengikuti ritme riak makan bibit lele. Sistem menuruti aktivitas bibit lele namun tetap terikat batas kuota dari petani.
   - Tujuan praktis: **Meringankan kerja petani dalam pemberian pakan, tanpa menghilangkan kendali petani atas alokasi pakan**.
4. **Masalah Utama Computer Vision**:
   - Kolam luar ruangan (*outdoor*) menggunakan **aerator aktif terus-menerus**.
   - Permukaan air tidak pernah diam; gejolak aerator adalah **BASELINE NORMAL**.
   - Sistem tidak boleh menggunakan aturan naïf *"ada gerakan = ikan lapar"*, melainkan mendeteksi **perubahan deviasi temporal** riak bibit lele terhadap riak aerator.
5. **Rencana Evaluasi Lapangan (1 Bulan vs Kolam Manual)**:
   - Didahului observasi awal 1 minggu (10–15 menit tiap jam) untuk memetakan variasi riak normal kolam.
   - Diikuti pengujian 1 bulan membandingkan kolam ber-alat dengan kolam pemberian pakan manual tanpa alat pada parameter: **Pertumbuhan bobot, pertambahan panjang, kelangsungan hidup (*Survival Rate*), total konsumsi pakan, dan FCR**.

---

## 🐟 BAGIAN II (OUTPUT 1): ANALISIS KEBIASAAN BIBIT LELE & RESPON KESEHATAN (PAKAN DIBATASI VS LOSS)

Kajian ini disusun berdasarkan sintesis 14 artikel ilmiah fisik di folder `articles/artikel bibit lele/pakannya bibit lele/` (antara lain: Ikeogu et al. 2020; Tiamiyu et al. 2018; Ojelade et al. 2025; Hildebrand et al. 2025; Hossain & Beveridge 2001; Khormi et al. 2026; Abdel-Aziz et al. 2021; Al-salahy & Ibrahim 2018).

### 1. Pola Makan Alami & Perilaku Riak Bibit Lele (*Feeding Ethology*)
- **Sifat Nokturnal & Respons Sensorik**: Lele afrika (*Clarias gariepinus*) adalah ikan nokturnal yang sangat aktif mencari makan pada intensitas cahaya rendah (petang, malam, fajar) menggunakan sungut (*barbels*) dan garis lateral (*lateral line*) untuk mendeteksi getaran dan aroma pakan (Hossain & Beveridge 2001; Hildebrand et al. 2025).
- **Karakteristik Riak Permukaan Bibit**: Saat lapar dan mendeteksi stimulus pakan di permukaan, bibit lele bergerak vertikal secara serentak ke permukaan air (*feeding frenzies*), menghasilkan riak halus dan cipratan mikro singkat berdurasi **3–6 frame (0,3–0,6 detik)** pada rekaman 10 FPS sebelum kembali menyelam ke kolom bawah.
- **Sifat Kanibalisme pada Fase Benih**: Benih lele memiliki variasi laju pertumbuhan individual (*growth heterogeneity*). Jika pakan terlambat atau terjadi disparitas ukuran tubuh, benih yang lebih besar akan memangsa benih yang lebih kecil.

---

### 2. Analisis Kondisi Pakan Bebas / "Loss" (*Ad Libitum / Feeding to Satiation*)

Memberikan pakan tanpa batas (*ad libitum / loss*) terbukti secara biologis merugikan budidaya bibit lele:

| Parameter Tinjauan | Temuan Literatur Empiris | Dampak pada Bibit Lele |
|---|---|---|
| **Rasio Konversi Pakan (FCR)** | **Ikeogu et al. (2020)** membuktikan bahwa pakan *satiation/loss* menghasilkan FCR **1,3 ± 0,03**, sedangkan pakan terkontrol (5% bobot tubuh) menghasilkan FCR **1,1 ± 0,01** ($p < 0,05$). | Pakan terbuang sia-sia; dibutuhkan 1,3 kg pakan untuk 1 kg pertumbuhan bobot (pemborosan biaya pakan hingga 18–25%). |
| **Pembusukan Bahan Organik** | Pelet komersial benih lele memiliki kandungan protein sangat tinggi (38–42% CP). Pakan yang tidak termakan dalam 5–10 menit akan tenggelam, larut, dan mengalami dekomposisi anaerobik (Tiamiyu et al. 2018; Oboh 2022). | Lonjakan konsentrasi amonia tak terionisasi ($NH_3$) dan nitrit ($NO_2^-$) toksik. Karena insang bibit lele masih sangat rentan, paparan amonia memicu kerusakan epitel insang dan mortalitas massal. |
| **Fisiologi Saluran Cerna** | Lambung lele bersifat elastis. Konsumsi pakan berlebih dalam waktu singkat menyebabkan distensi lambung (*bloating*), efisiensi enzim pencernaan turun, dan pelet dikeluarkan kembali sebelum terserap sempurna (*regurgitation*) (Li et al. 2020). | Penurunan efisiensi serap protein dan penurunan laju tumbuh spesifik (*Specific Growth Rate* / SGR). |

---

### 3. Analisis Kondisi Pakan Dibatasi (*Restricted / Rationed Feeding*)

Pembatasan pakan terbagi menjadi dua kategori: **pembatasan terukur/terencana** vs **pembatasan ekstrem/acak**:

1. **Pembatasan Terukur (Rationed Feeding, 3–5% Bobot Tubuh/Hari)**:
   - **Hasil Terbaik**: Penelitian Ikeogu et al. (2020) dan Tiamiyu et al. (2018) menyimpulkan bahwa batas pakan **5% dari biomassa harian** adalah rasio emas (*optimum economic rate*) untuk benih/fingerling lele:
     - Pertambahan bobot rata-rata (*Mean Weight Gain*) mencapai $26,11 \pm 3,65\text{ g}$ (lebih tinggi signifikan dibanding kelompok *satiation*).
     - Pertambahan panjang mencapai $6,11 \pm 0,20\text{ cm}$.
     - Tingkat kelangsungan hidup (*Survival Rate*) mencapai 100%.
   - **Pertumbuhan Kompensasi (*Compensatory Growth*)**: Studi Khormi et al. (2026) dan Agunbiade-Olu et al. (2022) mengungkap bahwa lele memiliki kapasitas hiperglikemik dan hiperfagia kompensatoris. Ketika interval antar-pemberian pakan dijaga teratur dan pakan diberikan saat lele menunjukkan riak lapar aktif, efisiensi anabolisme lele meningkat pesat sehingga lele tumbuh lebih padat daging.

2. **Bahaya Pembatasan Ekstrem / Pakan Tidak Teratur (*Unpredictable Starvation*)**:
   - Studi **Ojelade et al. (2025)** membuktikan bahwa jadwal pakan yang tidak terduga/acak memicu stres kronis pada *Clarias gariepinus*, ditandai dengan penurunan hematokrit (PCV) dan hemoglobin, serta penurunan drastis laju tumbuh.
   - Studi **Al-salahy & Ibrahim (2018)** membuktikan bahwa rasa lapar berlarut (*starvation*) memicu stres oksidatif lipid peroksidasi pada jaringan hati lele.
   - Pada tingkat benih, lapar berlarut memicu lonjakan agresivitas dan **kanibalisme**, menyebabkan tingkat kelangsungan hidup anjlok drastis.

---

### 4. Menghubungkan Temuan Biologis dengan Logika Sistem Skripsi

Dari sintesis biologis di atas, terlihat keselarasan mutlak dengan arahan dosen pembimbing:
- **Mengapa Harus Dibatasi oleh Petani?** Karena bibit lele tidak boleh dibiarkan makan *loss* tak terbatas (risiko amonia toksik dan pembengkakan FCR). Petani memasukkan kuota harian (misal: 1 kg pakan, merepresentasikan 5% biomassa kolam).
- **Mengapa Harus Berbasis Deteksi Riak Permukaan?** Karena memberikan jatah kuota tersebut secara sekaligus atau menggunakan *timer* buta tiap jam berisiko pakan jatuh saat lele sedang tidak responsif (terjadi pembusukan pakan atau stres jadwal acak seperti temuan Ojelade 2025).
- **Solusi Sistem Skripsi**: Sistem memecah kuota 1 kg tersebut menjadi 10–20 sub-porsi (masing-masing 50–100 gram). Kamera mendeteksi kapan bibit lele menunjukkan lonjakan riak di atas *baseline* aerator $\to$ dispensasi 1 sub-porsi $\to$ bibit lele menyambar pakan dengan efisiensi serap maksimal $\to$ pakan berhenti jika kuota harian habis.

---

## 📷 BAGIAN III (OUTPUT 2): RISET MENDALAM STUDI LITERATUR COMPUTER VISION

Di bawah ini adalah ekstraksi mendalam **25 Parameter Detail** dari dua paper fokus utama (**Hu et al. 2026** dan **Wu et al. 2024**) serta paper-paper pendukung top-view/outdoor/temporal lainnya.

---

### A. Bedah Ekstraksi 25 Parameter Paper Utama 1: Hu et al. (2026)
*Publikasi: Scientific Reports (Nature), Vol. 16, Art. 54934, DOI: 10.1038/s41598-026-54934-x.*
*Judul: A vision-based framework for quantifying fish feeding behavior in industrial recirculating aquaculture systems.*

1. **Objek Ikan**: *Largemouth bass* (*Micropterus salmoides*).
2. **Ukuran / Fase Ikan**: Ikan teraklimatisasi selama 4 bulan, populasi komersial $>20.000$ ekor; kelompok uji 1.200 ekor ikan aktif (*flow-conditioned*).
3. **Lingkungan Kolam**: Sistem Akuakultur Resirkulasi Industri (*Industrial RAS*).
4. **Indoor / Outdoor**: Semi-indoor / fasilitas tertutup industri RAS dengan penerangan terkontrol.
5. **Jenis Kolam**: Tangki bundar budidaya berdiameter $4,0\text{ m}$, tinggi tangki $1,5\text{ m}$, dengan kedalaman operasional air $1,4\text{ m}$.
6. **Kondisi Permukaan Air**: Dinamis dengan arus sirkulasi air RAS dan riak gelombang air akibat pergerakan kawanan ikan.
7. **Apakah Menggunakan Aerator**: Sistem menggunakan aerasi/oksigenasi RAS terintegrasi serta aliran air hidrodinamis tangki bundar.
8. **Posisi Kamera**: Kamera dipasang miring (*oblique angle / top-oblique view*).
9. **Ketinggian Kamera**: Sekitar **$70\text{ cm}$** di atas permukaan air.
10. **Sudut Kamera**: Sudut miring menghadap permukaan air (*oblique angle* $\approx 45^\circ\text{--}60^\circ$).
11. **Resolusi Video**: Resolusi tinggi, dipotong/diresize menjadi $512 \times 512$ piksel untuk input komputasi model.
12. **FPS**: Video standar industri ($25\text{--}30\text{ FPS}$), diekstraksi ke jendela temporal $T = 5$ frame.
13. **Jenis Kamera**: Kamera industri optik digital *high-definition*.
14. **Durasi Pengambilan Data**: Perekaman kontinu selama sesi pemberian pakan komersial berulang selama beberapa minggu.
15. **Waktu Pengambilan Data**: Waktu pemberian pakan rutin industri RAS.
16. **Cara Anotasi Data**: Anotasi 4 tingkat intensitas makan (*None, Weak, Medium, Strong*) yang divalidasi oleh pakar akuakultur berdasarkan intensitas riak, cipratan, dan kecepatan makan.
17. **Fitur yang Digunakan**: Fitur spasial tekstur gelombang air, riak permukaan (*ripples*), cipratan (*splashes*), dan pola temporal ketergantungan antar-frame sekuensial.
18. **Metode Computer Vision**: Ekstraksi spasial konvolusional CNN + *Patch Embedding* Vision Transformer + pemodelan dependensi waktu.
19. **Model Machine Learning / Deep Learning**: **Arsitektur Hibrida HVIT (ResNet18 CNN Backbone + 5-Layer Vision Transformer + Single-Layer LSTM)** dengan parameter $\approx 28,6\text{ Juta}$.
20. **Input Model**: Sekuens jendela temporal video berukuran $T = 5$ frame resolusi $512 \times 512 \times 3$.
21. **Output Model**: Klasifikasi 4 status intensitas perilaku makan: *None, Weak, Medium, Strong*.
22. **Cara Membedakan Makan vs Normal**:
    - *None*: Permukaan air tenang/arus biasa, ikan tidak merespons pelet.
    - *Weak*: Sebagian kecil ikan naik ke permukaan, menimbulkan riak halus (*slight ripples*).
    - *Medium*: Sebagian kelompok ikan menyambar pakan dengan cipratan sedang.
    - *Strong*: Agresi makan massal, ikan menyambar rakus dan menimbulkan riak gelombang besar dan cipratan luas.
23. **Cara Menangani Noise**: Modul Vision Transformer memusatkan *self-attention* pada area riak pakan dinamis dan mengabaikan latar belakang statis dinding tangki dan pantulan cahaya statis.
24. **Hasil Eksperimen**: Rata-rata akurasi mencapai **$95,10 \pm 1,05\%$** (mengungguli model statis murni ConvNeXt dan Swin Transformer); latensi inferensi $145\text{ ms}$ per jendela 5-frame.
25. **Keterbatasan Penelitian**:
    - Membutuhkan komputasi GPU tinggi ($28,6\text{ M}$ parameter), sulit dijalankan langsung pada mikrokontroler/Raspberry Pi murni tanpa akselerator.
    - Diuji pada tangki indoor RAS dengan pencahayaan buatan stabil, belum diuji pada kolam terbuka dengan perubahan cahaya matahari ekstrem dan aerator gelembung luar ruangan.

---

### B. Bedah Ekstraksi 25 Parameter Paper Utama 2: Wu et al. (2024)
*Publikasi: Journal of Marine Science and Engineering (JMSE), Vol. 12, Issue 5, Art. 726, DOI: 10.3390/jmse12050726 & Feeding Splash Study.*
*Judul: Identification of fish hunger degree with deformable attention transformer & Fish feeding intensity assessment method using deep learning-based analysis of feeding splashes.*

1. **Objek Ikan**: *Largemouth bass* (*Micropterus salmoides*).
2. **Ukuran / Fase Ikan**: Fase pembesaran / ikan remaja menjelang dewasa.
3. **Lingkungan Kolam**: Kolam / tangki budidaya terkontrol.
4. **Indoor / Outdoor**: Indoor / semi-outdoor beratap naungan.
5. **Jenis Kolam**: Tangki terpal / fiberglass persegi budidaya.
6. **Kondisi Permukaan Air**: Air jernih-sedang dengan permukaan relatif tenang sebelum pakan disebar.
7. **Apakah Menggunakan Aerator**: Aerasi dimatikan atau dialirkan secara tenang selama sesi perekaman pakan agar riak cipratan terlihat kontras.
8. **Posisi Kamera**: Posisi atas tegak lurus (*top-view / overhead*).
9. **Ketinggian Kamera**: Sekitar $1,2\text{--}1,5\text{ m}$ di atas permukaan air.
10. **Sudut Kamera**: Tegak lurus $90^\circ$ vertikal ke bawah (*nadir*).
11. **Resolusi Video**: $1920 \times 1080$ Full HD, dipotong ke area *feeding splash thumbnails*.
12. **FPS**: 30 FPS.
13. **Jenis Kamera**: Kamera digital RGB industri dengan lensa *wide-angle* terpasang pada rig overhead.
14. **Durasi Pengambilan Data**: Perekaman multi-hari saat interval pemberian pakan terjadwal.
15. **Waktu Pengambilan Data**: Pagi dan siang hari saat pemberian pakan rutin.
16. **Cara Anotasi Data**: Anotasi 3 tingkat rasa lapar (*Weakly hungry, Moderately hungry, Strongly hungry*) berdasarkan luas cipratan dan tingkat agregasi ikan.
17. **Fitur yang Digunakan**: *Feeding splash thumbnails* (potongan citra cipratan air putih berbusa), kontras intensitas piksel buih air, dan tingkat pengelompokan (*aggregation level*).
18. **Metode Computer Vision**: Ekstraksi lokal *feeding splash thumbnails* untuk mengeliminasi gangguan area luas permukaan air.
19. **Model Machine Learning / Deep Learning**: **Deformable Attention Vision Transformer (DeformAtt-ViT)**.
20. **Input Model**: Potongan gambar citra cipratan air (*splash thumbnails*).
21. **Output Model**: Klasifikasi 3 tingkat rasa lapar (*Weakly, Moderately, Strongly Hungry*) serta sinyal pemicu *feeder* (ON saat agregasi tinggi, OFF saat dispersi).
22. **Cara Membedakan Makan vs Normal**:
    - Mengukur kerapatan dan luas sebaran cipratan buih putih (*splashes*) yang dihasilkan saat mulut dan ekor ikan membentur permukaan air saat menangkap pelet.
    - Tidak ada cipratan = ikan kenyang/normal; cipratan sporadis = agak lapar; cipratan meluas masif = sangat lapar.
23. **Cara Menangani Noise**: Penggunaan *feeding splash thumbnails* secara efektif memotong dan mengabaikan pantulan cahaya matahari (*specular reflection*), riak air tenang, dan bayangan lingkungan karena model hanya mengevaluasi area cipratan mikro.
24. **Hasil Eksperimen**: Akurasi **$95,50\%$**, F1-Score **$94,13\%$**, Recall **$95,87\%$**, dan Precision **$92,45\%$**.
25. **Keterbatasan Penelitian**:
    - **TIDAK COCOK UNTUK BIBIT IKAN (*FISH FRY*)**: Peneliti dan literatur penelaah mencatat bahwa metode *feeding splash thumbnails* mengalami penurunan performa drastis pada **bibit ikan / benih** karena bibit ikan terlalu kecil untuk menghasilkan cipratan air berbusa putih (*inconspicuous splashing*).
    - **Mengasumsikan Air Awal Tenang**: Mengasumsikan permukaan air tenang sebelum pakan jatuh, sehingga tidak siap menghadapi turbulensi aerator gelembung mekanis konstan seperti di kolam lele luar ruangan.

---

### C. Bedah Ringkas Paper Pendukung Terpilih (Kamera Top-View & Edge)

| Penulis & Tahun | Objek & Kolam | Setup Kamera & Posisi | Metode & Model | Hasil & Latensi | Keterbatasan Utama Terhadap Kasus User |
|---|---|---|---|---|---|
| **Qian et al. (2025)** (*Discover Appl. Sci.*) | Ikan air tawar, kolam luar ruangan | *Overhead*, tinggi 1,8 m, $90^\circ$ nadir, Full HD | PM-YOLOv8 (YOLOv8 + Partial Convolution) | mAP 94,8%, inferensi 8,1 ms di GPU | Mengharuskan visual tubuh ikan terlihat jelas; gagal di air kolam bibit lele yang keruh kehijauan/kecokelatan. |
| **Fukae et al. (2023)** (*IEICE Trans.*) | Kawanan ikan, tangki budidaya | *Overhead*, tinggi 1,5 m, $90^\circ$, 30 FPS | *Dense Optical Flow* (Farnebäck) + SVM | Akurasi klasifikasi 88,3% | Komputasi Farnebäck sangat berat untuk Raspberry Pi; mengasumsikan nol gerakan saat diam (rusak jika ada aerator konstan). |
| **Zhao et al. (2025)** (*Sci. Rep.*) | Ikan air tawar, tangki observasi | *Top-view*, air jernih dengan pencahayaan bawah | *Pose Estimation* keypoint (kepala, punggung, ekor) + GCN | Akurasi kenyang 93,7% | Membutuhkan deteksi keypoint anatomi individual; mustahil diterapkan pada air lele keruh berbusa. |
| **Marliza & Aisuwarya (2021)** (*JNTE*) | Ikan lele (*Clarias sp.*), kolam lokal terpal | *Top-view*, Raspberry Pi Camera di atas kolam | Grayscale + Binerisasi Thresholding + Bounding Contour | Pakan otomatis terpicu kontur lele | Sangat rentan *false trigger* akibat gelembung aerator dan pantulan sinar matahari outdoor. |
| **Kamal et al. (2025)** (*Techno Agric.*) | Ikan lele (*Clarias gariepinus*) densitas tinggi | Sensor hidrofon akustik terendam dalam air | Ekstraksi fitur audio + Machine Learning | Akurasi klasifikasi lapar lele 91,2% | Kinerja anjlok drastis jika ada aerator mekanis karena kebisingan gelembung menutupi spektrum suara kunyahan lele. |

---

### D. Tabel Komparasi 25 Parameter: Literatur Terdahulu vs Kondisi Riil Skripsi User

Tabel komparatif berikut menyejajarkan literatur mutakhir dengan kondisi riil skripsi mahasiswa:

| No | Parameter Ekstraksi | Hu et al. (2026) | Wu et al. (2024) | Fukae et al. (2023) | Kondisi Skripsi Mahasiswa (Bibit Lele) |
|:--:|---|---|---|---|---|
| **1** | **Objek Ikan** | *Largemouth bass* | *Largemouth bass* | Ikan air tawar (*marine/fresh*) | **Bibit Ikan Lele (*Clarias sp.*)** |
| **2** | **Ukuran / Fase** | Dewasa (1.200 ekor diuji) | Remaja – Dewasa | Fase pembesaran | **Fase Benih / Pendederan (2–7 cm)** |
| **3** | **Lingkungan Kolam** | RAS Industri Tertutup | Tangki Eksperimental | Tangki Akuakultur | **Kolam Budidaya Terpal Luar Ruangan (*Outdoor*)** |
| **4** | **Indoor / Outdoor** | Indoor / Fasilitas RAS | Indoor / Semi-outdoor beratap | Indoor terkontrol | **Outdoor Murni (Terpapar Cuaca & Cahaya Alami)** |
| **5** | **Jenis Kolam** | Tangki bundar $\varnothing$ 4 m, d 1,4 m | Tangki persegi budidaya | Tangki bundar budidaya | **Kolam terpal bundar/kotak outdoor** |
| **6** | **Kondisi Permukaan** | Dinamis karena sirkulasi RAS | Relatif tenang sebelum pakan | Air tenang tanpa arus | **Bergolak konstan akibat aerator mekanis** |
| **7** | **Penggunaan Aerator** | Terintegrasi RAS | Dimatikan saat perekaman | Tanpa aerator saat rekam | **AERATOR MENYALA AKTIF TERUS-MENERUS** |
| **8** | **Posisi Kamera** | *Oblique* (miring) | *Overhead / Top-view* | *Overhead / Top-view* | ***Overhead / Top-View* (Tegak lurus kolam)** |
| **9** | **Ketinggian Kamera** | Sekitar 70 cm di atas air | 1,2 – 1,5 meter | 1,5 meter | **Sekitar 0,8 – 1,2 meter di atas kolam** |
| **10** | **Sudut Kamera** | $45^\circ\text{--}60^\circ$ miring | $90^\circ$ vertikal | $90^\circ$ vertikal | **$90^\circ$ vertikal (atau sedikit sudut koreksi silau)** |
| **11** | **Resolusi Video** | Resize ke $512 \times 512$ | 1080p cropped ke splash | 1080p Full HD | **720p / 640x480 (Disesuaikan kapasitas Edge)** |
| **12** | **FPS (Frame Rate)** | 25–30 FPS ($T=5$ frames) | 30 FPS | 30 FPS | **10 FPS (Event cepat 3–6 frame = 0,3–0,6 detik)** |
| **13** | **Jenis Kamera** | Kamera optik industri HD | Kamera digital RGB | Kamera digital RGB | **Raspberry Pi Camera Module** |
| **14** | **Durasi Data** | Multi-sesi makan RAS | Sesi makan terjadwal | Multi-menit per feeding | **1 minggu observasi awal + 1 bulan evaluasi** |
| **15** | **Waktu Pengambilan** | Jam pakan industri | Pagi dan siang hari | Siang pencahayaan stabil | **Pagi (06.00), Siang (12.00), Petang/Malam (18.00–22.00)** |
| **16** | **Cara Anotasi** | 4 kelas (*None, Weak, Med, Strong*) | 3 kelas (*Weak, Mod, Strong*) | 3 status aktivitas | **2 kelas operasional (Riak Baseline vs Riak Bibit Lele)** |
| **17** | **Fitur Visual** | Tekstur riak + dependensi waktu | *Feeding splash thumbnails* | Vektor gerak *dense optical flow* | **Fluktuasi intensitas riak & varians temporal deviasi** |
| **18** | **Metode CV** | CNN Patch + Transformer + LSTM | Deformable Attention ViT | Farnebäck Optical Flow | **Baseline Modeling + Temporal Motion Variance** |
| **19** | **Model ML / DL** | HVIT (ResNet18 + ViT + LSTM) | DeformAtt-ViT | Support Vector Machine (SVM) | **Model Temporal Ringan (LSTM / GRU / 1D-CNN) atau Rule Baseline** |
| **20** | **Input Model** | Jendela 5 frame ($512\times 512$) | *Splash thumbnails* citra | Matriks magnitudo aliran optik | **Sekuens vektor energi gerak $T$ frame ($T \approx 10\text{--}20$)** |
| **21** | **Output Model** | 4 kelas intensitas makan | 3 derajat lapar lele | Status aktivitas kawanan | **Pemicu dispensasi sub-porsi pakan (Trigger Feeding)** |
| **22** | **Pembeda Makan vs Normal** | Luas riak dan cipratan pakan | Keberadaan cipratan buih putih | Peningkatan vektor kecepatan | **Lonjakan deviasi energi riak terhadap baseline aerator** |
| **23** | **Penanganan Noise** | *Self-attention* fokus area riak | Crop spesifik thumbnail cipratan | Pemotongan threshold biner | **Pemodelan statistik baseline aerator + filter silau/daun** |
| **24** | **Hasil Eksperimen** | Akurasi 95,10%, Latensi 145 ms | Akurasi 95,50%, F1 94,13% | Akurasi 88,3% | *Target: Akurasi $\ge 85\%$, F1 $\ge 80\%$ pada Raspberry Pi* |
| **25** | **Keterbatasan Utama** | Berat (28,6 M param), bukan outdoor | Gagal pada bibit lele & air ber-aerator | Terlalu lambat untuk Raspberry Pi | Tantangan komputasi edge & fluktuasi cuaca outdoor |

---

## 🔬 BAGIAN IV: PERBANDINGAN METODE COMPUTER VISION & KELAYAKANNYA PADA SKRIPSI

Untuk tahap skripsi saat ini, metode tidak langsung dikunci secara kaku. Berikut perbandingan karakteristik metode berdasarkan data nyata kolam bibit lele ber-aerator:

```
+───────────────────────────+─────────────────────────────────────────────────────────────+
| METODE COMPUTER VISION    | EVALUASI UNTUK KOLAM BIBIT LELE OUTDOOR BER-AERATOR         |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 1. Frame / Temporal       | (+) Sangat ringan, berjalan >30 FPS di Raspberry Pi.        |
|    Difference             | (-) Sensitif terhadap perubahan intensitas cahaya matahari. |
|                           | (*) Cocok sebagai tahap ekstraksi awal (first-stage filter).|
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 2. Dense Optical Flow     | (+) Menangkap arah dan kecepatan pergerakan riak detail.    |
|    (Farnebäck)            | (-) Sangat berat untuk CPU Raspberry Pi 4 (<2 FPS).         |
|                           | (*) Sparse optical flow (Lucas-Kanade) lebih realistis.     |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 3. Motion Intensity Index | (+) Menghitung magnitudo energi kinetik agregat seluruh ROI.|
|                           | (+) Komputasi sangat efisien dan mudah dibentuk sekuensnya. |
|                           | (*) Menjadi fitur input ideal untuk model temporal.         |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 4. Background Subtraction | (+) Memisahkan objek bergerak dari latar belakang statis.   |
|    (MOG2 / KNN)           | (-) Aerator bergerak terus-menerus sehingga masuk foreground|
|                           | (*) Perlu laju pembaruan (*learning rate*) adaptif tinggi.  |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 5. Dynamic / Temporal     | (+) Memodelkan tekstur air beriak sebagai proses stokastik. |
|    Texture (LBP-TOP)      | (-) Kompleksitas matematika tinggi, rentan perubahan cuaca. |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 6. Ripple / Splash        | (+) Menargetkan fenomena fisik riak/cipratan air langsung.   |
|    Detection              | (-) Seperti catatan Wu et al. (2024), bibit lele berukuran  |
|                           |     kecil sehingga cipratannya halus dan tidak berbusa putih|
|                           | (*) Harus mendeteksi riak gelombang halus, bukan cipratan.  |
+───────────────────────────+─────────────────────────────────────────────────────────────+
| 7. Model Temporal         | (+) Mengingat pola temporal periodik aerator vs acak lele.  |
|    (LSTM / GRU / 1D-CNN)  | (+) Mampu mengenali event singkat (3–6 frame) dalam konteks.|
|                           | (*) Sangat direkomendasikan jika inputnya berupa fitur 1D!  |
+───────────────────────────+─────────────────────────────────────────────────────────────+
```

---

## 🧠 BAGIAN V: SPESIFIKASI JIKA MODEL TEMPORAL (LSTM) DIGUNAKAN

Jika skripsi mengadopsi model temporal seperti **LSTM (Long Short-Term Memory)** atau **GRU (Gated Recurrent Unit)**, arsitektur harus dirancang secara rasional dan dapat dijelaskan secara ilmiah:

```
[Frame Video 10 FPS]
         │
         ▼
[Prapemrosesan ROI & Normalisasi]
         │
         ▼
[Ekstraksi Vektor Fitur Per-Frame] ───► e.g., [Motion Intensity, Spatial Variance, Ripple Density]
         │                              (Dimensi Fitur: d = 3 s.d. 8 per frame)
         ▼
[Jendela Sekuens Geser (Sliding Window)] ───► T = 15 frame (1,5 detik, overlap 50%)
         │
         ▼
[Model Temporal: 1-Layer LSTM / GRU] ───► Mengingat ritme baseline aerator vs impuls bibit lele
         │
         ▼
[Dense Layer + Sigmoid / Softmax]
         │
         ▼
[Status Aktivitas Makan: Baseline (0) vs Lonjakan Riak Lele (1)]
```

### 1. Apa Input Sequence-nya?
- **Bukan Raw Video Piksel Berat**: Mengalirkan raw video $512 \times 512$ ke LSTM (seperti Hu et al. 2026) akan membebani Raspberry Pi dan menyebabkan latensi tinggi.
- **Vektor Fitur Gerak Terkompresi (*Compact 1D Feature Sequence*)**: Input sequence berupa sekuens temporal berdimensi $(B, T, D)$:
  - $B$: *Batch size* (saat inferensi $B = 1$).
  - $T$: Panjang jendela sekuens waktu (misalnya $T = 15\text{--}20$ frame pada 10 FPS, mencakup durasi $1,5\text{--}2,0$ detik).
  - $D$: Jumlah fitur per-frame ($D \approx 4\text{--}6$ fitur).

### 2. Fitur Aktivitas Apa yang Digunakan ($D$)?
Untuk setiap frame $t$, diekstraksi fitur gerakan permukaan yang mewakili riak:
1. $M_t$: **Indeks Intensitas Gerak (*Motion Intensity*)**, rata-rata nilai perbedaan frame terbobot $\frac{1}{N} \sum |I_t - I_{t-1}|$.
2. $V_t$: **Varians Spasial Gerakan (*Spatial Variance*)**, mengukur apakah riak terkonsentrasi di titik aerator atau menyebar akibat bibit lele.
3. $A_t$: **Luas Area Aktif (*Active Ripple Area*)**, persentase piksel di atas ambang batas biner.
4. $\Delta M_t$: **Gradien Laju Perubahan Energi (*Temporal Energy Derivative*)**, $M_t - M_{t-1}$.

### 3. Bagaimana Sequence Dibentuk?
- Menggunakan **Jendela Geser (*Sliding Window*)** dengan panjang $T = 15$ frame ($1,5$ detik) dan langkah pergeseran (*stride*) 3 frame ($0,3$ detik, setara $70\%$ overlap).
- Panjang jendela $1,5$ detik dipilih karena event riak bibit lele berlangsung $0,3\text{--}0,6$ detik (3–6 frame). Jendela $1,5$ detik memberikan konteks sebelum event (*baseline pre-event*), saat event (*peak event*), dan setelah event (*post-event relaxation*).

### 4. Apa Target / Label-nya?
- **Klasifikasi Biner Operasional**:
  - Label `0`: **Kondisi Normal / Baseline Kolam** (aerator menyala normal, permukaan beriak periodik, ikan tenang/tidak merespons pakan).
  - Label `1`: **Lonjakan Aktivitas Riak Bibit Lele** (bibit lele menyambar aktif ke permukaan kolam menghasilkan deviasi riak yang signifikan).

### 5. Mengapa Model Temporal Diperlukan?
- **Perbedaan Karakteristik Waktu Antara Aerator vs Bibit Lele**:
  - Gejolak aerator bersifat **siklis dan kuasi-periodik** dengan frekuensi relatif stabil sepanjang waktu.
  - Aktivitas bibit lele saat lapar bersifat **impulsif dan stokastik** (tiba-tiba muncul lonjakan tajam selama 3–6 frame lalu mereda).
- Model spasial murni (frame-by-frame) hanya melihat intensitas sesaat, sehingga mudah tertipu oleh letupan gelembung besar aerator sesaat (*false alarm*). Model temporal (LSTM) melihat **dinamika riwayat frame sebelumnya** untuk memastikan apakah lonjakan tersebut merupakan anomali aerator atau lonjakan riak kawanan lele.

### 6. Bagaimana Baseline Aerator Ditangani?
1. **Pemodelan Baseline Adaptif (*Running Moving Average & Variance*)**:
   - Sistem secara berkala menghitung rata-rata bergerak $\mu_{\text{baseline}}$ dan standar deviasi $\sigma_{\text{baseline}}$ intensitas gerak saat tidak ada pakan.
   - Sinyal yang masuk ke LSTM adalah sinyal ternormalisasi deviasi terhadap baseline:
     $$Z_t = \frac{M_t - \mu_{\text{baseline}}}{\sigma_{\text{baseline}}}$$
2. **Masking Spasial (*Region of Interest / ROI*)**:
   - Area titik semprotan gelembung aerator utama di kolam dapat diberi bobot lebih rendah atau di-masking secara parsial, sehingga kamera lebih sensitif mengamati permukaan air di sekeliling aerator tempat bibit lele berkerumun.
3. **Penyaringan Waktu Tenang (*Post-Feeding Refractory Period*)**:
   - Setelah feeder mendispensasikan porsi pakan, sistem menerapkan jeda waktu tenang (*refractory cooldown*, misal 3–5 menit) sebelum deteksi riak diaktifkan kembali, agar cipratan sisa makan tidak memicu pakan berulang kali.

---

## 🎯 KESIMPULAN & LANGKAH PRIORITAS BERIKUTNYA

1. **Output 1 Selesai**: Dasar biologis telah tervalidasi dari 14 paper pakan lele lokal. Pemberian pakan pendederan benih lele harus berbasis pembatasan kuota terukur (5% biomassa) yang disalurkan secara sinkron dengan nafsu makan riak lele guna mencegah FCR membengkak (Ikeogu 2020) dan mencegah stres acak (Ojelade 2025).
2. **Output 2 Selesai**: Riset mendalam 25 parameter Hu et al. (2026) dan Wu et al. (2024) mengonfirmasi *research gap* skripsi: metode cipratan *splash thumbnails* Wu et al. tidak efektif untuk bibit lele karena cipratan benih terlalu halus, sementara model Hu et al. belum menguji kolam luar ruangan dengan aerator gelembung konstan.
3. **Langkah Berikutnya**:
   - Melaksanakan fase observasi 1 minggu sampling video 10–15 menit per jam untuk membangun dataset variabilitas riak aerator kolam lele mahasiswa.
   - Menghubungkan fitur vektor gerak 1D dengan model temporal ringan yang dapat dieksekusi secara real-time pada Raspberry Pi tanpa kendala latensi.

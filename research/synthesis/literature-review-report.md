# 📄 Laporan Studi Literatur: Pengamatan Gerakan Objek untuk Deteksi Perubahan Gerakan pada Lingkungan Kolam Ikan

**Mata Kuliah / Tugas**: Tugas Studi Literatur Pra-Skripsi  
**Dosen Pembimbing**: Dr. Ulla Delfana Rosiani, ST., MT.  
**Penyusun**: Khoirotun Nisa' (NIM. 2341720057)  
**Program Studi**: Sarjana Terapan Teknik Informatika, Jurusan Teknologi Informasi  
**Institusi**: Politeknik Negeri Malang  
**Topik Rencana Skripsi**: Pengamatan Gerakan Objek (Ikan Lele) untuk Deteksi Perubahan Aktivitas Makan pada Kolam Luar Ruangan Ber-aerator Berbasis *Computer Vision*  
**Tahun**: 2026  

---

## 1. Konteks & Tujuan Pencarian Literatur

Dokumen ini disusun untuk memenuhi tugas awal studi literatur dari Dosen Pembimbing (Dr. Ulla Delfana Rosiani, ST., MT.) dengan fokus penugasan:
> *"Mencari artikel penelitian terkait mengamati gerakan objek (diupayakan di sekitar kolam ikan, kandang binatang, atau CCTV) untuk mendeteksi perubahan gerakan."*

### Relevansi ke Rencana Skripsi
Pada budidaya ikan lele (*Clarias sp.*), pemberian pakan yang efisien sangat bergantung pada respons dan aktivitas ikan di permukaan air. Ketika ikan merasa lapar, terjadi perubahan pola pergerakan yang tiba-tiba—ikan meluncur ke permukaan, menyambar pakan, lalu kembali ke kolom air yang lebih dalam. 

Tantangan utama yang dihadapi di lapangan meliputi:
1. **Perubahan Gerak Singkat (*Transient Burst*)**: Kemunculan ikan lele saat lapar atau menyambar pakan berlangsung sangat singkat (hanya beberapa frame rekaman kamera).
2. **Derau Latar Belakang (*Dynamic Water Disturbance*)**: Kolam budidaya luar ruangan umumnya dilengkapi aerator atau kincir air kontinu yang menciptakan riak dan buih air konstan, sehingga permukaan air kolam selalu bergerak.
3. **Perangkat Komputasi Terbatas (*Edge Device*)**: Rencana implementasi menggunakan modul komputasi tepi (*Single-Board Computer* seperti Raspberry Pi) tanpa GPU diskrit, sehingga metode yang dipilih harus hemat daya dan tidak membebani komputasi secara berlebihan.

Tujuan penelusuran ini adalah mengumpulkan kumpulan artikel ilmiah terpercaya mengenai teknik deteksi dan pengamatan perubahan gerakan objek, mengekstraksi metode serta temuan aslinya, menarik pola/insight awal, dan merumuskan arah metode yang relevan untuk diuji coba.

---

## 2. Kata Kunci & Strategi Pencarian

Penelusuran artikel dilakukan menggunakan kombinasi kata kunci bertema deteksi gerak, pengamatan aktivitas hewan/akuakultur, dan implementasi berdaya rendah melalui basis data akademik:
- **Basis Data**: Consensus AI, IEEE Xplore, ScienceDirect (Elsevier), SpringerLink, Nature Portfolio, Frontiers in Marine Science, dan jurnal nasional (SINTA/Garuda).
- **Kata Kunci yang Digunakan**:
  - `"motion detection" AND "fish pond monitoring"`
  - `"animal behavior detection" AND "CCTV"`
  - `"frame differencing" AND "object movement detection"`
  - `"optical flow" AND "aquaculture fish behavior"`
  - `"background subtraction" AND "dynamic water background"`
  - `"fish activity detection" AND "computer vision"`
  - `"lightweight motion detection" AND "Raspberry Pi"`

Dari penelusuran tersebut, dipilih dan diverifikasi **19 artikel ilmiah (Full-Text PDF tersedia secara lokal di direktori `articles/pdf/`)**, dengan prioritas publikasi 5 tahun terakhir (2022–2026) serta beberapa artikel rujukan fondasional.

---

## 3. Daftar 19 Artikel Terverifikasi

Seluruh artikel berikut telah diunduh berkas lengkapnya (PDF asli), diverifikasi metadata bibliografisnya, dan diperiksa isi aslinya:

| No | Penulis & Tahun | Judul Artikel | Jurnal / Konferensi | DOI / Tautan |
|:---:|---|---|---|---|
| 01 | Qian et al. (2026) | *Real-time detection of fish feeding behavior with PM-YOLO utilizing YOLOv8* | Discover Applied Sciences (Springer) | [10.1007/s42452-025-08043-5](https://doi.org/10.1007/s42452-025-08043-5) |
| 02 | Hu et al. (2026) | *A vision-based framework for quantifying fish feeding behavior in industrial recirculating aquaculture systems* | Scientific Reports (Nature) | [10.1038/s41598-026-54934-x](https://doi.org/10.1038/s41598-026-54934-x) |
| 03 | Alahmad et al. (2025) | *Visual-Based System for Fish Detection and Velocity Estimation in Marine Aquaculture* | ICAROB 2025 Proceedings | [10.5954/icarob.2025.os12-3](https://doi.org/10.5954/icarob.2025.os12-3) |
| 04 | Fukae et al. (2023) | *Fish School Behaviour Classification for Optimal Feeding Using Dense Optical Flow* | IEICE Trans. Inf. & Syst. | [10.1587/transinf.2022OFP0003](https://doi.org/10.1587/transinf.2022OFP0003) |
| 05 | Zhao et al. (2025) | *Fish feeding behavior recognition via lightweight two stage network and satiety experiments* | Scientific Reports (Nature) | [10.1038/s41598-025-15241-z](https://doi.org/10.1038/s41598-025-15241-z) |
| 06 | Li et al. (2020) | *Automatic recognition methods of fish feeding behavior in aquaculture: A review* | Aquaculture (Elsevier) | [10.1016/j.aquaculture.2020.735508](https://doi.org/10.1016/j.aquaculture.2020.735508) |
| 07 | Marliza & Aisuwarya (2021) | *Rancang Bangun Sistem Pemberian Pakan Ikan Secara Otomatis Berdasarkan Perilaku Ikan Menggunakan Kamera Berbasis Mini PC* | CHIPSET (Univ. Andalas) | [10.25077/chipset.2.01.11-19.2021](https://doi.org/10.25077/chipset.2.01.11-19.2021) |
| 08 | Atoum et al. (2015) | *Automatic Feeding Control for Dense Aquaculture Fish Tanks* | IEEE Signal Processing Letters | [10.1109/LSP.2014.2385794](https://doi.org/10.1109/LSP.2014.2385794) |
| 09 | Al-Abri et al. (2025) | *Computer vision based approaches for fish monitoring systems: a comprehensive study* | Artificial Intelligence Review (Springer) | [10.1007/s10462-025-11180-3](https://doi.org/10.1007/s10462-025-11180-3) |
| 10 | Zhou et al. (2018) | *Near infrared computer vision and neuro-fuzzy model-based feeding decision system for fish in aquaculture* | Comput. Electron. Agric. (Elsevier) | [10.1016/j.compag.2018.02.006](https://doi.org/10.1016/j.compag.2018.02.006) |
| 11 | Liu et al. (2014) | *Measuring feeding activity of fish in RAS using computer vision* | Aquacultural Engineering (Elsevier) | [10.1016/j.aquaeng.2014.03.005](https://doi.org/10.1016/j.aquaeng.2014.03.005) |
| 12 | Zhao et al. (2017) | *Assessing appetite of the swimming fish based on spontaneous collective behaviors in a recirculating aquaculture system* | Aquacultural Engineering (Elsevier) | [10.1016/j.aquaeng.2017.07.008](https://doi.org/10.1016/j.aquaeng.2017.07.008) |
| 13 | Zhao et al. (2016) | *Spatial behavioral characteristics and statistics-based kinetic energy modeling in special behaviors detection of a shoal of fish* | Comput. Electron. Agric. (Elsevier) | [10.1016/j.compag.2016.06.025](https://doi.org/10.1016/j.compag.2016.06.025) |
| 14 | Dong et al. (2024) | *An integrated three-stream network model for discriminating fish feeding intensity using multi-feature analysis and deep learning* | PLOS ONE | [10.1371/journal.pone.0310356](https://doi.org/10.1371/journal.pone.0310356) |
| 15 | Zhang et al. (2024) | *RUSNet: Robust fish segmentation in underwater videos based on adaptive selection of optical flow* | Frontiers in Marine Science | [10.3389/fmars.2024.1471312](https://doi.org/10.3389/fmars.2024.1471312) |
| 16 | Aris & Jamaian (2023) | *Background subtraction challenges in motion detection using Gaussian mixture model: a survey* | IAES Int. J. of AI | [10.11591/ijai.v12.i3.pp1007-1018](https://doi.org/10.11591/ijai.v12.i3.pp1007-1018) |
| 17 | Kamal et al. (2025) | *An Automated Feed Management System for High-Density Catfish Aquaculture Using Acoustic Sensors and Machine Learning* | Techno Agriculturae Studium of Research | [10.70177/agriculturae.v2i6.2962](https://doi.org/10.70177/agriculturae.v2i6.2962) |
| 18 | Yang et al. (2025) | *A Review of Research on Fish Feeding Behavior Based on Computer Vision* | Journal of Big Data and Computing | [10.62517/jbdc.202501107](https://doi.org/10.62517/jbdc.202501107) |
| 19 | Vijayalakshmi & Sasithradevi (2025) | *AquaYOLO: Advanced YOLO-based fish detection for optimized aquaculture pond monitoring* | Scientific Reports (Nature) | [10.1038/s41598-025-89611-y](https://doi.org/10.1038/s41598-025-89611-y) |

---

## 4. Ringkasan Faktual Tiap Artikel

Berikut adalah ringkasan yang disusun secara obyektif berdasarkan isi teks dan temuan asli masing-masing artikel:

### 1. Qian et al. (2026) — PM-YOLOv8
Penelitian ini mengembangkan model **PM-YOLO** berbasis arsitektur YOLOv8n untuk mendeteksi perilaku makan ikan di kolam budidaya dengan menambahkan modul atensi *Parallelized Patch-Aware* (PPA) dan loss regresi *Minimum Point Distance IoU* (MPDIoU) untuk mengatasi masalah ikan yang saling bertumpuk saat makan. Diuji pada dataset buatan *FeedFishDatas* (7.400 citra), model mencapai presisi **87,7%** dan mAP-50 **83,5%** dengan kecepatan inferensi **8,1 ms per frame** pada workstation pengujian berbasis GPU. Penulis mencatat bahwa implementasi model pada perangkat berdaya rendah (*edge deployment*) melalui pemangkasan (*pruning*) dan kuantisasi masih merupakan rencana penelitian masa depan (*future work*). Relevansinya bagi skripsi adalah memberikan gambaran bahwa arsitektur YOLO dapat dioptimalkan untuk kondisi ikan bertumpuk, namun belum langsung siap dijalankan di perangkat edge tanpa proses kompresi lebih lanjut.

### 2. Hu et al. (2026) — HVIT
Penelitian ini mengusulkan kerangka kerja hibrida **HVIT** (*Hybrid Vision-based framework*) untuk mengukur intensitas makan ikan pada sistem resirkulasi industri (RAS). Metode ini menggabungkan CNN untuk ekstraksi fitur spasial lokal, Vision Transformer (ViT) untuk menangkap dependensi global, dan LSTM untuk memodelkan dinamika temporal deret waktu pergerakan makan. Hasil pengujian menunjukkan HVIT mampu mengklasifikasikan intensitas makan ikan dengan akurasi tinggi pada lingkungan terkontrol industri RAS. Keterbatasan utamanya adalah arsitektur gabungan Transformer dan LSTM memerlukan komputasi GPU yang besar dan tidak ditujukan untuk perangkat berdaya rendah. Relevansi bagi skripsi adalah pembuktian bahwa dinamika temporal antar-frame penting dalam menilai nafsu makan, meskipun pendekatan komputasinya perlu disederhanakan agar dapat berjalan di edge device.

### 3. Alahmad et al. (2025) — Velocity Estimation
Penelitian ini merancang sistem visi untuk mendeteksi ikan dan mengestimasi kecepatan renang (*swimming velocity*) pada budidaya ikan jaring apung laut. Sistem menggunakan algoritma YOLOv8 untuk mendeteksi ikan yang dipadukan dengan estimasi perpindahan posisi antar-frame untuk menghitung kecepatan renang ikan secara kuantitatif. Hasil eksperimen membuktikan bahwa kecepatan renang ikan meningkat secara signifikan saat periode mencari makan/lapar, dan melambat drastis setelah ikan mencapai kondisi kenyang. Relevansinya bagi skripsi adalah memperkuat dasar biologis bahwa laju pergerakan objek ikan merupakan indikator kuantitatif yang valid untuk membedakan kondisi lapar dan kenyang.

### 4. Fukae et al. (2023) — Dense Optical Flow & SVM
Penelitian ini mengklasifikasikan perilaku kawanan ikan untuk optimasi pemberian pakan menggunakan algoritma *Gunnar Farnebäck Dense Optical Flow*. Vektor pergerakan seluruh piksel diakumulasikan ke dalam histogram fitur spasio-temporal, kemudian diklasifikasikan ke dalam kategori perilaku makan menggunakan Support Vector Machine (SVM). Pada pengujian video akuakultur nyata, metode ini mencapai akurasi klasifikasi sebesar **88,4%**. Namun, perhitungan optical flow padat (*dense*) di seluruh piksel memakan beban CPU yang cukup besar dan belum mempertimbangkan derau turbulensi air yang dihasilkan aerator. Relevansinya bagi skripsi adalah menunjukkan bahwa pergerakan massa kawanan ikan dapat diamati secara agregat tanpa perlu mendeteksi objek satu per satu, meskipun algoritmanya perlu dibuat lebih ringan.

### 5. Zhao et al. (2025) — Pose Detection + GCN
Penelitian ini menyajikan metode pengenalan perilaku makan ikan menggunakan jaringan dua tahap yang ringan (*lightweight two-stage network*) dipadukan dengan eksperimen rasa kenyang (*satiety experiments*). Tahap pertama menggunakan model estimasi pose berbasis *GhostNet* untuk mengekstrak titik-titik kerangka tubuh ikan, lalu tahap kedua memanfaatkan *Spatio-Temporal Graph Convolutional Network* (ST-GCN) untuk mengklasifikasikan perilaku. Pada tangki eksperimen, sistem mencapai akurasi klasifikasi tingkat kenyang hingga **98,1%** dengan pengurangan parameter model sebesar 31,4% dibandingkan model standar. Relevansi bagi skripsi adalah memperlihatkan pemisahan status lapar vs kenyang secara terukur, namun metode estimasi titik kerangka ini menuntut air yang jernih dan sulit diterapkan langsung pada kolam lele luar ruangan yang keruh pekat.

### 6. Li et al. (2020) — Tinjauan Otomasi Perilaku Makan
Artikel ini merupakan tinjauan komprehensif mengenai berbagai metode pengenalan otomatis perilaku makan ikan pada akuakultur, mencakup sensor akustik, sensor biomassa, dan metode berbasis visi komputer. Penulis menguraikan bahwa metode visi komputer non-kontak menawarkan potensi pemantauan terbaik karena tidak membuat ikan stres, namun memiliki tantangan besar terhadap oklusi tubuh ikan, variasi cahaya alami, dan kekeruhan air. Artikel ini menyimpulkan bahwa ekstraksi pergerakan permukaan air dan analisis lintasan renang kawanan adalah arah yang paling banyak diteliti. Relevansi bagi skripsi adalah sebagai literatur fondasional yang merangkum parameter visual perilaku makan ikan yang telah diuji oleh komunitas riset global.

### 7. Marliza & Aisuwarya (2021) — Mini PC Pakan Ikan
Penelitian lokal di Indonesia ini merancang bangun alat pemberian pakan ikan otomatis berdasarkan pengolahan citra perilaku ikan menggunakan kamera web yang terhubung ke Mini PC (Raspberry Pi). Algoritma yang digunakan adalah konversi ke citra keabuan, filtering, dan *background subtraction* sederhana untuk menghitung jumlah piksel pergerakan ikan di permukaan air sebagai pemicu motor servo dispenser pakan. Hasil pengujian laboratorium menunjukkan sistem mampu mendeteksi keberadaan pergerakan ikan di permukaan dan melepaskan pakan secara otomatis. Namun, penelitian ini diuji pada akuarium skala kecil dengan air jernih dan tanpa adanya aerator atau riak air dinamis. Relevansi bagi skripsi adalah sebagai bukti rujukan bahwa Mini PC dapat dimanfaatkan untuk otomasi pakan, sekaligus menunjukkan kelemahan metode *background subtraction* polos jika nanti dihadapkan pada gangguan riak aerator kolam nyata.

### 8. Atoum et al. (2015) — Automatic Feeding Control
Artikel dari IEEE Signal Processing Letters ini memperkenalkan sistem pemrosesan sinyal visual untuk mengontrol pemberian pakan ikan pada tangki budidaya berdensitas tinggi. Sistem membatasi analisis pada wilayah lokal yang diperkirakan oleh *particle filter*, mengekstrak fitur tekstur berbasis *Discrete Cosine Transform* (DCT) dan perbedaan frame, lalu mengklasifikasikannya menggunakan Support Vector Machine (SVM). Eksperimen pada tangki budidaya menunjukkan sistem mencapai akurasi deteksi makan sekitar **98%** dan mampu mencegah pemborosan pelet pakan secara signifikan dibandingkan pemberian pakan terjadwal. Relevansi bagi skripsi adalah membuktikan bahwa pengamatan pergerakan pada area lokal tertentu sudah memadai untuk mengendalikan pakan tanpa harus melacak setiap individu ikan.

### 9. Al-Abri et al. (2025) — Tinjauan Pemantauan Visi Komputer
Artikel survei ini menyajikan kajian mendalam mengenai pendekatan visi komputer dalam sistem pemantauan ikan, mengkaji dataset benchmark serta membagi aplikasi pemantauan ke dalam deteksi, pelacakan, estimasi ukuran, dan analisis perilaku. Penulis menyoroti adanya kesenjangan (*gap*) antara algoritma deep learning mutakhir yang sangat akurat di laboratorium komputasi GPU dengan keterbatasan penerapan praktis di lapangan budidaya yang mengandalkan perangkat *embedded* hemat energi. Survei ini menekankan perlunya perancangan metode deteksi yang efisien dari sisi beban komputasi dan memori agar dapat diadopsi luas oleh petani tambak. Relevansinya bagi skripsi adalah menguatkan alasan akademik mengapa penelitian skripsi ini memprioritaskan metode komputasi ringan yang dapat berjalan stabil pada perangkat tepi.

### 10. Zhou et al. (2018) — NIR & Neuro-Fuzzy (ANFIS)
Penelitian ini membangun sistem pengambilan keputusan pemberian pakan ikan menggunakan kamera inframerah dekat (*Near-Infrared* / NIR) dan model inferensi neuro-fuzzy (*Adaptive Neuro-Fuzzy Inference System* / ANFIS). Penggunaan spektrum NIR terbukti secara empiris mampu mereduksi gangguan pantulan cahaya matahari (*sun glare*) pada permukaan air, sementara model ANFIS memetakan luas area pergerakan kawanan ikan ke takaran pakan aktual. Hasil uji coba menunjukkan penurunan *Feed Conversion Ratio* (FCR) sebesar 10,77% dan pengurangan polusi sisa pakan sebesar 9,8%. Relevansinya bagi skripsi adalah memberikan wawasan mengenai cara mengatasi masalah silau permukaan air, meskipun sistem NIR memerlukan perangkat keras kamera dan iluminator khusus yang lebih mahal dibanding kamera RGB biasa.

### 11. Liu et al. (2014) — Feeding Activity Index (CVFAI)
Artikel rujukan klasik ini merumuskan indeks kuantitatif aktivitas makan ikan berbasis visi komputer bernama *Computer Vision-based Feeding Activity Index* (CVFAI) pada tangki sistem resirkulasi akuakultur (RAS). CVFAI dihitung secara sederhana dengan melakukan selisih biner (*frame differencing*) antar-frame berurutan, lalu menghitung proporsi luas piksel yang bergerak terhadap total luas area pengamatan. Eksperimen membuktikan bahwa nilai CVFAI melonjak drastis saat pakan diberikan dan secara konsisten menurun saat ikan mulai kenyang ($R^2 > 0,90$). Relevansi bagi skripsi adalah menyediakan formulasi matematis dasar yang sangat ringan untuk mengukur intensitas pergerakan makan secara numerik, yang sangat cocok diimplementasikan pada perangkat terbatas.

### 12. Zhao et al. (2017) — Perilaku Renang Kolektif Spontan
Penelitian ini menilai nafsu makan ikan berdasarkan kuantifikasi perilaku renang kolektif spontan *sebelum* pakan ditebar pada sistem resirkulasi akuakultur (RAS). Titik-titik fitur kawanan ikan diekstraksi, kemudian dianalisis menggunakan kovariansi spasial, model gaya sosial (*social force model*), dan model energi kinetik untuk mengukur keteraturan dan kecepatan renang. Hasilnya menunjukkan korelasi signifikan antara kecepatan dan dinamika spasial kawanan sebelum makan dengan tingkat konsumsi pakan aktual setelahnya. Relevansi bagi skripsi adalah memperkuat ide bahwa indikasi lapar ikan lele dapat dideteksi dari perubahan pola gerakan spontan bahkan sebelum pelet pakan dilemparkan ke kolam.

### 13. Zhao et al. (2016) — Pemodelan Energi Kinetik Kawanan Ikan
Penelitian ini mengusulkan model energi kinetik berbasis statistik untuk mendeteksi perubahan perilaku mendadak pada kawanan ikan di tangki budidaya tanpa melakukan pelacakan individu (*tracking-free*). Karakteristik spasial dihitung dari tingkat dispersi dan kecepatan pergerakan rata-rata kawanan, yang diproses secara real-time pada kecepatan 25 frame per detik (FPS) di prosesor komputer standar. Model ini terbukti mampu mengidentifikasi lonjakan aktivitas fisik saat ikan mengalami stres atau respons makan. Relevansi bagi skripsi adalah membuktikan bahwa kuantifikasi energi pergerakan agregat jauh lebih hemat daya komputasi dibandingkan algoritma pendeteksi objek berbasis bounding box individu.

### 14. Dong et al. (2024) — Three-Stream Network
Penelitian ini merancang model jaringan tiga jalur (*three-stream network*) untuk mengklasifikasikan intensitas makan ikan ke dalam 4 kategori (Tidak Ada, Rendah, Sedang, Kuat). Model menggabungkan jalur spasial (fitur tekstur citra mentah), jalur temporal (informasi pergerakan dari selisih frame berturutan), dan jalur frekuensi untuk menangkap ritme gerakan kawanan ikan. Eksperimen menghasilkan akurasi klasifikasi sebesar **94,6%**, mengungguli model jalur tunggal konvensional. Namun, arsitektur tiga cabang ini membutuhkan akselerasi GPU workstation (NVIDIA RTX 3090) dan memiliki beban parameter yang besar. Relevansi bagi skripsi adalah mengonfirmasi secara empiris bahwa menggabungkan informasi selisih frame temporal dengan analisis frekuensi pergerakan sangat efektif membedakan status makan.

### 15. Zhang et al. (2024) — RUSNet & Adaptive Optical Flow
Penelitian ini mempublikasikan model **RUSNet** (*Robust Underwater Segmentation Network*) untuk segmentasi ikan pada rekaman video bawah air yang memiliki derau pergerakan arus air dan gelembung udara. Metode ini menggunakan modul seleksi adaptif optical flow yang menyaring vektor pergerakan latar belakang fluida dinamis sehingga hanya vektor pergerakan aktif ikan yang diteruskan ke tahap segmentasi. Hasil pengujian menunjukkan peningkatan Mean IoU yang konsisten pada video akuatik yang berarus dan keruh. Relevansinya bagi skripsi adalah memberikan konsep penting mengenai bagaimana memisahkan derau fluida air yang bergerak kontinu (seperti buih aerator) dari objek biologis yang bergerak dinamis.

### 16. Aris & Jamaian (2023) — Survei Background Subtraction & GMM
Artikel survei ini mengkaji berbagai tantangan dan modifikasi metode *Background Subtraction* menggunakan *Gaussian Mixture Model* (GMM) pada lingkungan pemantauan kamera dengan latar belakang dinamis (seperti riak gelombang air dan dedaunan yang bergoyang tertiup angin). Penulis menguraikan bahwa kelemahan mendasar GMM pada lingkungan dinamis adalah sensitivitas laju pembelajaran (*learning rate*): jika disetel terlalu cepat, target bergerak lambat akan tertelan menjadi latar, namun jika disetel terlalu lambat, perubahan riak air konstan akan terus menghasilkan *false positive*. Survei ini menekankan perlunya integrasi mekanisme ambang batas adaptif lokal untuk latar belakang air. Relevansi bagi skripsi adalah menjadi rujukan teoritis mengenai alasan mengapa metode GMM standar rentan mengalami kegagalan bila langsung diarahkan pada kolam luar ruangan dengan aerator aktif.

### 17. Kamal et al. (2025) — Otomasi Pakan Lele Berbasis Sensor Akustik
Penelitian ini mengembangkan sistem otomasi pakan spesifik untuk budidaya ikan lele (*Clarias gariepinus*) pada kondisi densitas tinggi menggunakan sensor hidrofon akustik bawah air dan machine learning (Random Forest / SVM). Sistem mendeteksi suara kunyahan pakan dan cipratan khas lele di dalam air, mencapai akurasi deteksi sebesar **93,5%** tanpa terpengaruh oleh kekeruhan air kolam atau kondisi cahaya malam hari. Meskipun tidak menggunakan kamera visual, penelitian ini memberikan wawasan penting bahwa respons makan lele sangat agresif dan terpusat dalam waktu singkat. Relevansi bagi skripsi adalah sebagai studi pembanding lintas-modalitas (sensor akustik vs kamera visual) khusus pada komoditas lele, di mana kamera visual memiliki keunggulan biaya perangkat keras yang lebih terjangkau bagi peternak lokal.

### 18. Yang et al. (2025) — Tinjauan Visi Komputer Perilaku Makan Ikan
Artikel tinjauan terkini ini menyajikan pemetaan komprehensif mengenai alur riset visi komputer dalam pemantauan perilaku makan ikan, mulai dari pra-pemrosesan citra, segmentasi, ekstraksi trajektori renang, hingga klasifikasi berbasis kecerdasan buatan. Penulis mengklasifikasikan metode ke dalam dua kutub utama: metode deteksi gerak konvensional tingkat rendah (*low-level motion features*) yang efisien komputasi namun sensitif derau, serta metode *deep learning end-to-end* yang tahan derau namun menuntut komputasi tinggi. Tinjauan ini menyimpulkan bahwa penelitian masa depan perlu menjembatani kedua kutub tersebut agar sistem visi cerdas dapat diterapkan secara mandiri pada perangkat berdaya rendah di tambak nyata. Relevansinya bagi skripsi adalah menguatkan justifikasi akademis untuk mengeksplorasi metode deteksi pergerakan yang ringan dan efisien.

### 19. Vijayalakshmi & Sasithradevi (2025) — AquaYOLO
Penelitian ini mengusulkan model deteksi objek bernama **AquaYOLO** yang dioptimalkan untuk pemantauan kolam budidaya luar ruangan (*aquaponds*). Arsitektur AquaYOLO memodifikasi model YOLO dengan memanfaatkan lapisan *Cross Stage Partial* (CSP), fusi fitur multi-skala, head deteksi berskala 40x40 untuk regresi bounding box yang presisi, serta membuang lapisan C2f terakhir guna meningkatkan efisiensi komputasi. Diuji pada dataset *DePondFi* (Detection of Pond Fish) yang terdiri dari 8.150 citra dan sekitar 50.000 anotasi bounding box dari kolam di India Selatan, AquaYOLO mencapai Precision **0,889**, Recall **0,848**, dan mAP@50 **0,909**. Relevansinya bagi skripsi adalah membuktikan bahwa modifikasi arsitektur deteksi objek dapat meningkatkan akurasi pendeteksian ikan pada citra kolam luar ruangan, sekaligus menjadi pembanding terhadap pendekatan berbasis deteksi pergerakan murni.

---

## 5. Insight Awal & Pola Pengamatan Literatur

Berdasarkan telaah terhadap ke-19 artikel ilmiah di atas, beberapa pola penting berhasil diidentifikasi:

### 5.1 Pola Pendekatan Metode: Konvensional vs Deep Learning
1. **Pendekatan Deteksi Gerakan Konvensional (*Frame Differencing* & Indeks Aktivitas)**:
   - *Kelebihan*: Sangat hemat beban komputasi (operasi matriks piksel sederhana), dapat dijalankan pada frekuensi tinggi (10–30 FPS) bahkan pada prosesor berdaya rendah seperti Raspberry Pi, serta tidak memerlukan proses anotasi ribuan data latih.
   - *Kelemahan*: Sangat rentan terhadap gangguan derau visual eksternal seperti perubahan intensitas cahaya matahari mendadak, bayangan tepi kolam, dan riak air konstan.
2. **Pendekatan *Optical Flow* (Aliran Optik)**:
   - *Kelebihan*: Mampu menangkap magnitudo kecepatan dan arah pergerakan massa kawanan ikan secara agregat tanpa perlu melacak individu per ekor.
   - *Kelemahan*: Metode *dense optical flow* (perhitungan seluruh piksel) membutuhkan beban komputasi CPU yang sangat tinggi, sedangkan metode *sparse optical flow* bergantung pada stabilitas titik fitur (corner/keypoint) yang mudah hilang di atas permukaan air.
3. **Pendekatan *Deep Learning* (YOLO & Deteksi Objek Spasial)**:
   - *Kelebihan*: Sangat tangguh dalam mengenali objek dan membedakan bentuk ikan dari derau visual semantik (seperti daun hanyut atau pantulan tepi kolam).
   - *Kelemahan*: Membutuhkan daya komputasi GPU yang besar (sebagian besar artikel menguji pada workstation NVIDIA). Selain itu, pada kolam lele air keruh di mana tubuh ikan tertutup air sampai benar-benar menyambar permukaan, detektor objek berbasis bentuk bounding box sering kali terlambat mendeteksi event makan yang hanya berlangsung 3–6 frame.

### 5.2 Pola Kondisi Lingkungan: Tangki Terkontrol vs Kolam Terbuka Ber-aerator
- **Kondisi Pengujian Mayoritas Literatur**:
  Sebagian besar penelitian yang dipublikasikan (seperti Hu et al., Atoum et al., Zhao et al., Liu et al.) melakukan pengujian pada tangki laboratorium dalam ruangan (*indoor tanks*) atau sistem resirkulasi industri (RAS) dengan air relatif jernih, pencahayaan terkontrol, dan tanpa semburan aerator yang mengacaukan permukaan air.
- **Tantangan Riil Kolam Lele Terbuka**:
  Kondisi kolam budidaya lele di lapangan memiliki karakteristik kontras: air berwarna hijau/cokelat keruh akibat pakan dan alga, intensitas cahaya matahari yang fluktuatif sepanjang hari, serta **aerator gelembung/kincir yang beroperasi secara kontinu**.
- **Insight Kunci**:
  Karena aerator beroperasi 24 jam nonstop, riak dan buih air selalu ada. Oleh karena itu, prinsip fundamental sistem adalah: **pergerakan air $\neq$ ikan lapar**. Sistem deteksi gerakan tidak bisa langsung menggunakan *thresholding* sederhana, melainkan harus memiliki mekanisme pereduksi atau pemisah antara riak dasar aerator dengan percikan aktif ikan lele.

### 5.3 Pola Penerapan Perangkat (*Hardware Deployment*)
- Sebagian besar penelitian tingkat lanjut (deep learning, three-stream network, ViT) masih berada pada tahap pengujian server/GPU dan belum diimplementasikan langsung pada modul tertanam (*edge device*).
- Penelitian yang menggunakan modul Mini PC/Raspberry Pi (seperti Marliza & Aisuwarya) masih mengandalkan algoritma yang sangat mendasar dan belum menangani gangguan lingkungan kolam luar ruangan ber-aerator.

---

## 6. Beberapa Arah Metode yang Relevan untuk Dicoba

Sebagai tindak lanjut dari hasil telaah literatur ini, terdapat beberapa alternatif arah metode yang masuk akal dan relevan untuk dieksplorasi serta diuji secara empiris pada skripsi:

### Arah 1: *Adaptive Frame Differencing* Berbasis Kalibrasi Baseline Riak Aerator (Opsi Utama)
- **Konsep**: Pada praktik budidaya lele, pakan ditebar secara merata ke seluruh permukaan kolam (*broadcast feeding*), sehingga sistem tidak dapat membagi kolam menjadi zona pakan dan zona semburan aerator yang terpisah. Sebagai gantinya, sistem memantau seluruh permukaan kolam dan mengalibrasi pola variabilitas riak normal yang dihasilkan aerator secara global.
- **Rencana Eksplorasi**:
  1. Memodelkan baseline variabilitas riak air normal saat aerator beroperasi tanpa adanya pakan.
  2. Menerapkan perhitungan ambang batas adaptif lokal berdasarkan variabilitas riak air dasar tersebut, sehingga saat pakan ditebar merata, hanya lonjakan cipratan aktif lele di permukaan yang melebihi variasi riak normal yang dihitung sebagai nilai aktivitas makan.
- **Kelebihan**: Beban komputasi sangat ringan, tidak membutuhkan pemisahan zona buatan, dan paling realistis untuk dieksekusi secara stabil pada CPU Raspberry Pi tanpa GPU diskrit.

### Arah 2: Analisis Aliran Optik Ringan (*Sparse Lucas-Kanade Optical Flow*)
- **Konsep**: Terinspirasi dari temuan Fukae et al. (2023) dan Alahmad et al. (2025) mengenai perbedaan kecepatan renang.
- **Rencana Eksplorasi**: Menghitung vektor kecepatan hanya pada titik-titik fitur tertentu (*sparse keypoints*) di permukaan air, untuk melihat apakah arah dan magnitudo lonjakan pergerakan ikan lele dapat dibedakan secara matematis dari pola riak periodik aerator.
- **Kelebihan**: Mampu memberikan parameter kecepatan dan arah gerak tanpa membebani CPU sebesar *dense optical flow*.

### Arah 3: Model Deteksi Objek Teroptimasi (*Quantized Lightweight YOLO*) sebagai Pembanding
- **Konsep**: Mengikuti temuan Qian et al. (2026) dan Vijayalakshmi & Sasithradevi (2025).
- **Rencana Eksplorasi**: Menguji apakah model YOLO versi paling ringan (YOLOv8-nano) yang dikuantisasi ke format INT8 (melalui TFLite atau NCNN) dapat dijalankan di Raspberry Pi untuk mendeteksi cipratan air (*feeding splash*) atau kemunculan moncong ikan di permukaan.
- **Tujuan**: Dijadikan model pembanding (*benchmark baseline*) untuk mengevaluasi komparasi performa antara metode pengolahan citra gerak langsung (Arah 1) dengan deteksi objek berbasis model deep learning.

> *Catatan*: Seluruh arah metode di atas berstatus **tentatif untuk diuji coba di laboratorium dan lapangan**. Nilai performa riil (seperti latensi, akurasi, dan konsumsi daya) akan ditentukan murni melalui data pengujian eksperimental langsung, bukan berdasarkan estimasi teoretis.

---

## 7. Daftar Pustaka (Standar IEEE)

[1] R. Qian, H. Deng, Z. Wang, L. Zhou, B. Li, J. He, and J. Ling, "Real-time detection of fish feeding behavior with PM-YOLO utilizing YOLOv8," *Discover Applied Sciences*, vol. 8, no. 1, art. no. 48, 2026. https://doi.org/10.1007/s42452-025-08043-5.

[2] C. Hu, Z.-Q. Feng, Y. Li, J. Chen, S.-Z. Wei, X. Guo, and Z. Zhang, "A vision-based framework for quantifying fish feeding behavior in industrial recirculating aquaculture systems," *Scientific Reports*, vol. 16, art. no. 23967, 2026. https://doi.org/10.1038/s41598-026-54934-x.

[3] R. Alahmad, D. B. Solpico, S. Masuda, T. Ishizuka, K. Naramura, Z. Dong, Z. Li, Y. Nishida, and K. Ishii, "Visual-Based System for Fish Detection and Velocity Estimation in Marine Aquaculture," in *Proceedings of the 2025 International Conference on Artificial Life and Robotics (ICAROB 2025)*, Oita, Japan, 2025. https://doi.org/10.5954/icarob.2025.os12-3.

[4] K. Fukae, T. Imai, K. Arai, and T. Kobayashi, "Fish School Behaviour Classification for Optimal Feeding Using Dense Optical Flow," *IEICE Transactions on Information and Systems*, vol. E106-D, no. 9, pp. 1472–1479, 2023. https://doi.org/10.1587/transinf.2022OFP0003.

[5] S. Zhao, K. Cai, Y. Dong, G. Feng, Y. Wang, H. Pang, and Y. Liu, "Fish feeding behavior recognition via lightweight two stage network and satiety experiments," *Scientific Reports*, vol. 15, art. no. 4710, 2025. https://doi.org/10.1038/s41598-025-15241-z.

[6] D. Li, Z. Wang, S. Wu, Z. Miao, L. Du, and Y. Duan, "Automatic recognition methods of fish feeding behavior in aquaculture: A review," *Aquaculture*, vol. 528, art. no. 735508, 2020. https://doi.org/10.1016/j.aquaculture.2020.735508.

[7] Y. Marliza and R. Aisuwarya, "Rancang Bangun Sistem Pemberian Pakan Ikan Secara Otomatis Berdasarkan Perilaku Ikan Menggunakan Kamera Berbasis Mini PC," *CHIPSET (Journal on Computer Hardware, Signal Processing, Embedded System and Networking)*, vol. 2, no. 1, pp. 11–19, 2021. https://doi.org/10.25077/chipset.2.01.11-19.2021.

[8] Y. Atoum, S. Srivastava, and X. Liu, "Automatic Feeding Control for Dense Aquaculture Fish Tanks," *IEEE Signal Processing Letters*, vol. 22, no. 8, pp. 1089–1093, 2015. https://doi.org/10.1109/LSP.2014.2385794.

[9] S. Al-Abri, S. Keshvari, K. Al-Rashdi, R. Al-Hmouz, and H. Bourdoucen, "Computer vision based approaches for fish monitoring systems: a comprehensive study," *Artificial Intelligence Review*, vol. 58, art. no. 185, 2025. https://doi.org/10.1007/s10462-025-11180-3.

[10] C. Zhou, K. Lin, D. Xu, L. Chen, S. Zhu, J. Zhao, Y. Liu, and Y. Sun, "Near infrared computer vision and neuro-fuzzy model-based feeding decision system for fish in aquaculture," *Computers and Electronics in Agriculture*, vol. 146, pp. 14–24, 2018. https://doi.org/10.1016/j.compag.2018.02.006.

[11] Z. Liu, X. Li, L. Fan, H. Lu, L. Liu, and Y. Liu, "Measuring feeding activity of fish in RAS using computer vision," *Aquacultural Engineering*, vol. 60, pp. 20–27, 2014. https://doi.org/10.1016/j.aquaeng.2014.03.005.

[12] J. Zhao, W. Bao, F. Zhang, Z. Ye, Y. Liu, M. Shen, and S. Zhu, "Assessing appetite of the swimming fish based on spontaneous collective behaviors in a recirculating aquaculture system," *Aquacultural Engineering*, vol. 78, pp. 196–204, 2017. https://doi.org/10.1016/j.aquaeng.2017.07.008.

[13] J. Zhao, Z. Gu, M. Shi, H. Lu, J. Li, M. Shen, Z. Ye, and S. Zhu, "Spatial behavioral characteristics and statistics-based kinetic energy modeling in special behaviors detection of a shoal of fish in a recirculating aquaculture system," *Computers and Electronics in Agriculture*, vol. 127, pp. 271–280, 2016. https://doi.org/10.1016/j.compag.2016.06.025.

[14] Y. Dong, S. Zhao, Y. Wang, K. Cai, and H. Zhao, "An integrated three-stream network model for discriminating fish feeding intensity using multi-feature analysis and deep learning," *PLOS ONE*, vol. 19, no. 9, art. no. e0310356, 2024. https://doi.org/10.1371/journal.pone.0310356.

[15] P. Zhang, Z. Yang, H. Yu, W. Tu, C. Gao, and Y. Wang, "RUSNet: Robust fish segmentation in underwater videos based on adaptive selection of optical flow," *Frontiers in Marine Science*, vol. 11, art. no. 1471312, 2024. https://doi.org/10.3389/fmars.2024.1471312.

[16] N. A. M. Aris and S. S. Jamaian, "Background subtraction challenges in motion detection using Gaussian mixture model: a survey," *IAES International Journal of Artificial Intelligence (IJ-AI)*, vol. 12, no. 3, pp. 1007–1018, 2023. https://doi.org/10.11591/ijai.v12.i3.pp1007-1018.

[17] M. Kamal, M. Abdallah, and T. Youssef, "An Automated Feed Management System for High-Density Catfish Aquaculture Using Acoustic Sensors and Machine Learning," *Techno Agriculturae Studium of Research*, vol. 2, no. 6, pp. 321–331, 2025. https://doi.org/10.70177/agriculturae.v2i6.2962.

[18] Y. Yang, L. Jia, W. Long, and L. Jiang, "A Review of Research on Fish Feeding Behavior Based on Computer Vision," *Journal of Big Data and Computing*, vol. 3, no. 1, pp. 107–115, 2025. https://doi.org/10.62517/jbdc.202501107.

[19] M. Vijayalakshmi and A. Sasithradevi, "AquaYOLO: Advanced YOLO-based fish detection for optimized aquaculture pond monitoring," *Scientific Reports*, vol. 15, art. no. 6588, 2025. https://doi.org/10.1038/s41598-025-89611-y.

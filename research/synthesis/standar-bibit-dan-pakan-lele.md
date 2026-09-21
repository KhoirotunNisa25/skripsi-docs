# Standar Biologis Bibit Lele, Tahapan Pendederan Operasional, dan Manajemen Takaran Pakan Presisi
**Sintesis Literatur Ilmiah Terverifikasi untuk Sistem Deteksi Aktivitas Makan Berbasis Visi Komputer (*Edge AI*)**

---

## Ringkasan Eksekutif & Konteks Penelitian
* **Nama Peneliti / Mahasiswa**: Khoirotun Nisa' (NIM: 2341720057)
* **Dosen Pembimbing**: Dr. Ulla Delfana Rosiani, ST., MT.
* **Program Studi**: Sarjana Terapan Teknik Informatika, Jurusan Teknologi Informasi, Politeknik Negeri Malang (2026)
* **Fokus Riset**: Deteksi Aktivitas Gerak Ikan Lele sebagai Indikasi Tingkat Lapar Berbasis Visi Komputer pada *Edge Device* (Raspberry Pi)
* **Objek Amatan**: Bibit Ikan Lele (*Clarias spp.* / Lele Dumbo & Sangkuriang) pada Fase Benih & Pendederan Operasional
* **Sumber Data**: 9 Artikel Ilmiah Terverifikasi (Full-Text PDF Tersimpan Lokal di `articles/artikel bibit lele/`)

---

## 1. Pendahuluan & Urgensi Domain Bibit Lele

Dalam industri akuakultur air tawar, tahap pembenihan (*hatchery*) dan pendederan (*nursery*) ikan lele (*Clarias spp.*, khususnya *Clarias gariepinus* dan galur Sangkuriang) merupakan fase paling kritis (*critical bottleneck*) yang menentukan kelangsungan hidup populasi (Gisbert et al., 2021; Kurdowi et al., 2025). Berbeda dengan ikan lele dewasa pada kolam pembesaran akhir yang memiliki toleransi fisiologis tinggi, benih lele memiliki tingkat kerentanan ekstrem terhadap faktor mortalitas:

1. **Keterbatasan Enzimatis & Bukaan Mulut (*Mouth Gape*)**: Saluran pencernaan benih yang baru menyerap kantung telur (*yolk sac*) belum memiliki lambung fungsional dan enzim proteolitik lengkap, serta dibatasi bukaan mulut sempit (*mouth gape constraint*), sehingga mutlak memerlukan pakan alami hidup sebelum beralih ke pakan formulasi (Gisbert et al., 2021; Srivastava et al., 2012).
2. **Sifat Agresif & Kanibalisme Tinggi**: Disparitas ukuran (*size heterogeneity*) dan keterlambatan pemberian pakan memicu kanibalisme ganas di antara benih sejenis, yang dapat memusnahkan 30–60% populasi dalam hitungan hari jika manajemen pakan tidak terkontrol (Gisbert et al., 2021; Pelu & Liubana, 2025).
3. **Kerentanan terhadap Kualitas Air**: Pemberian pakan berlebih (*overfeeding*) pada kolam benih lele sangat fatal. Sisa pakan mikro berprotein tinggi (35–42%) sangat cepat membusuk di dasar kolam, menyebabkan deplesi oksigen terlarut (*Dissolved Oxygen* / DO < 3 mg/L) serta lonjakan amonia bebas ($NH_3$) yang mematikan benih (Afia et al., 2020; Jibrin et al., 2024; Kurdowi et al., 2025; Pelu & Liubana, 2025).

Oleh sebab itu, penerapan **sistem pemantauan aktivitas makan berbasis visi komputer (*computer vision*)** pada perangkat tepi (*edge device* Raspberry Pi) membutuhkan acuan standar biologis yang presisi. Dokumen ini menyajikan sintesis komprehensif mengenai **tahapan umur bibit lele, standar kualitas air, takaran pakan harian (% biomassa), frekuensi pemberian pakan, serta strategi mitigasi kanibalisme** berdasarkan 9 artikel ilmiah yang telah diunduh secara utuh.

---

## 2. Klasifikasi Fase Perkembangan Biologis Bibit Lele

Berdasarkan perkembangan ontogenetik, morfologi bukaan mulut (*mouth gape*), dan kesiapan saluran pencernaan, fase hidup awal bibit lele diklasifikasikan ke dalam 5 (lima) tahapan utama (Gisbert et al., 2021; Kurdowi et al., 2025; Srivastava et al., 2012):

### Tabel 1: Matriks Klasifikasi Fase Perkembangan Biologis Bibit Lele (*Ontogenetic Stages*)

| No | Fase Biologis | Rentang Umur | Panjang / Bobot | Karakteristik Morfologi & Bukaan Mulut | Kebutuhan & Jenis Pakan |
|:--:|---|:---:|:---:|---|---|
| **1** | **Larva / *Sac-Fry*** | D0 – D3 (0–3 hari pascatetas) | 0,5 – 0,7 cm | Cadangan kuning telur (*yolk sac*) aktif; saluran cerna belum terbuka sempurna; sirip belum berdiferensiasi. | **Nihil** (mengandalkan nutrisi endogen kuning telur) (Gisbert et al., 2021; Kurdowi et al., 2025). |
| **2** | **Early Fry** | D4 – D7 pascatetas | 0,8 – 1,5 cm | *Yolk sac* terserap habis; bukaan mulut kecil (*mouth gape constraint*); gerakan renang mulai aktif mencari makan. | Pakan alami mikro: Nauplii *Artemia*, cacing sutra halus (*Tubifex*), *ad libitum* 3–4x/hari (Pranat et al., 2025; Srivastava et al., 2012). |
| **3** | **Late Fry / Transisi** | D8 – D12 pascatetas | 1,5 – 3,0 cm | Saluran cerna mulai membentuk lambung fungsional; mampu menelan remah pakan halus; fase transisi (*weaning*). | Cacing sutra + pelet mikro awal (PF-500 / remah 0,5 mm) dibasahi air hangat (Srivastava et al., 2012; Kurdowi et al., 2025). |
| **4** | **Fingerling Awal** | D13 – D30 pascatetas | 5,0 – 7,0 cm (1 – 5 g) | Sirip punggung dan ekor sempurna; organ arborescent (pernapasan tambahan) aktif; gerakan menyambar permukaan sangat agresif saat lapar. | Pelet mikro terapung protein tinggi (35–42% CP); dosis 5% biomassa/hari (Afia et al., 2020; Jibrin et al., 2024; Essien et al., 2024). |
| **5** | **Juvenil Lanjut** | Umur >30 hari | 7,0 – 12,0 cm (>5 – 10 g) | Morfologi menyerupai lele dewasa; lambung dan enzim proteolitik sempurna; toleransi lingkungan meningkat. | Pelet komersial 1–2 mm (protein 30–35%); dosis diturunkan bertahap ke 2–3% biomassa/hari (Essien et al., 2024). |

---

## 3. Integrasi Sistem Pendederan Operasional (Pendederan I, II, dan III)

Dalam tata kelola budidaya di Indonesia, pembudidaya menerapkan istilah operasional **Pendederan I, II, dan III** yang merupakan segmentasi wadah dan waktu manajemen kolam (Pelu & Liubana, 2025; Kurdowi et al., 2025). Segmentasi ini bertujuan mengantisipasi heterogenitas pertumbuhan anak ikan yang sangat cepat dan memicu kanibalisme:

### Tabel 2: Korelasi Tahapan Pendederan Operasional terhadap Fase Biologis & Manajemen Kolam

| Tahap Pendederan | Durasi Pemeliharaan | Ukuran Awal Benih & Padanan Biologis | Target Ukuran Akhir | Manajemen Pakan & Risiko Kritis |
|---|:---:|---|---|---|
| **Pendederan I** | 14 – 21 hari | Benih 2–3 cm (umur 10–14 hari).<br>*Padanan: Late Fry $\to$ Fingerling Awal*. | 3–5 cm | Pakan beralih dari cacing sutra ke tepung/pelet mikro halus ($\pm 0,5$ mm, protein 35–40%). Pakan dibasahi air hangat untuk mencegah stres transisi (*weaning*) (Kurdowi et al., 2025; Srivastava et al., 2012). |
| **Pendederan II** | 21 – 28 hari | Benih 5–7 cm (bobot 1,65–2,55 g).<br>*Padanan: Fingerling Pertengahan*. | 7–8 cm (bobot 3,8–4,5 g) | **Fase paling rawan kanibalisme & predasi**. Pelet mikro terapung protein tinggi (35–42%). Ransum harian 5–10% biomassa (optimum 5%), frekuensi 3–4x sehari. **Sortir berkala (*grading*) wajib tiap 7–10 hari** (Pelu & Liubana, 2025; Afia et al., 2020). |
| **Pendederan III** | 28 – 35 hari | Benih 7–8 cm (bobot >3,8 g).<br>*Padanan: Fingerling Akhir / Juvenil*. | 9–12 cm (bobot >5–10 g) | Pelet komersial 1–2 mm. Dosis pakan diturunkan bertahap menjadi 2–3% biomassa per hari guna menjaga kualitas air. Persiapan masuk kolam pembesaran konsumsi akhir (Essien et al., 2024; Pelu & Liubana, 2025). |

---

## 4. Standar Baku Kualitas Air Pembenihan & Pendederan

Kualitas air kolam benih lele harus dikontrol ketat dengan aerasi konstan berdasarkan hasil observasi Balai Benih Ikan (BBI) Teun (Pelu & Liubana, 2025) dan BPPP Banyuwangi (Kurdowi et al., 2025):

### Tabel 3: Standar Baku Parameter Fisika-Kimia Air Kolam Benih & Pendederan Lele

| Parameter Kualitas Air | Rentang Toleransi | Nilai Rekomendasi Optimum | Dampak Fisiologis & Perilaku Benih | Rujukan Ilmiah |
|---|:---:|:---:|---|---|
| **Suhu Air ($^\circ$C)** | 26,0 – 32,0 | **26,0 – 30,0 $^\circ$C** | Suhu <26$^\circ$C menurunkan nafsu makan >40% dan memperlambat metabolisme; suhu >32$^\circ$C memicu stres termal dan konsumsi O$_2$ berlebih. | Pelu & Liubana (2025); Kurdowi et al. (2025) |
| **Derajat Keasaman (pH)** | 6,5 – 8,5 | **6,8 – 7,5** | pH <6,0 merusak lendir pelindung kulit dan epitel insang; pH >8,5 melipatgandakan fraksi toksik amonia tak-terionisasi ($NH_3$). | Pelu & Liubana (2025); Essien et al. (2024) |
| **Oksigen Terlarut (DO)** | $\ge 3,0$ mg/L | **$\ge 5,0$ mg/L** (Aerasi Konstan) | DO <3 mg/L menyebabkan benih *piping* (menggantung di permukaan mencari udara), mogok makan, dan memicu kematian massal larva. | Pelu & Liubana (2025); Kurdowi et al. (2025) |
| **Padat Tebar Larva** | 300 – 1.000 ekor/m³ | **500 – 700 ekor/m³** | Kepadatan berlebih (>800 ekor/m³) memicu perebutan pakan dan meningkatkan kontak agresi kanibalisme. | Kurdowi et al. (2025) |
| **Biosekuriti Kolam** | Rutin | **Garam + Daun Pepaya (2,5 L)** | Larutan garam (NaCl) dan ekstrak daun pepaya terbukti efektif mencegah infestasi jamur *Saprolegnia* dan infeksi bakteri benih. | Kurdowi et al. (2025) |

---

## 5. Standar Manajemen Takaran Pakan Presisi (*Feeding Management*)

### 5.1. Evaluasi Pakan Alami vs Pakan Formulasi pada Benih Awal
* **Cacing Sutra (*Tubifex sp.*)**: Pranat et al. (2025) membuktikan bahwa pakan alami cacing sutra mendukung pertumbuhan panjang mutlak terbaik pada benih lele (0,42 mm/minggu).
* **Nauplii *Artemia sp.***: Pranat et al. (2025) menunjukkan bahwa pemberian nauplii *Artemia sp.* mampu menjaga tingkat kelangsungan hidup (*survival rate*) benih lele hingga mencapai **98%**.
* **Transisi Bertahap (*Weaning*)**: Srivastava et al. (2012) membuktikan bahwa larva lele yang diberi pakan alami hidup nauplii *Artemia* selama 14–21 hari kemudian beralih bertahap ke pakan buatan formula mikro menghasilkan laju pertumbuhan spesifik (SGR) dan sintasan optimal.

### 5.2. Takaran Ransum Harian Berbasis Persentase Bobot Biomassa (% BW/Day)
Setelah memasuki fase *fingerling* (bobot >1–2 gram), pakan buatan komersial berprotein tinggi (35–42% CP) diberikan dengan persentase terukur:

1. **Afia, Kolawole, & David (2020)** meneliti variasi takaran pakan 3%, 5%, dan 7% bobot tubuh per hari (*body weight/day*) pada benih *Clarias gariepinus* (bobot awal 5,92 g) selama 99 hari:
   - Dosis **7% bw/day** mencatat bobot akhir tertinggi, namun **Feed Conversion Ratio (FCR)** terbaik dicapai pada perlakuan **3% bw/day**.
   - Berdasarkan kompromi biaya dan konversi nutrisi, Afia et al. (2020) merekomendasikan **5% bw/day sebagai takaran ransum optimum** benih lele.
2. **Jibrin et al. (2024)** menguji dosis 3%, 5%, 7%, dan 10% bobot tubuh pada benih *Clarias gariepinus*:
   - Efisiensi pakan (*Feed Efficiency Ratio* / FER) dan pemanfaatan protein (*Protein Efficiency Ratio* / PER) terbaik dicatatkan pada diet **3% dan 5% bw/day**.
   - Dosis di atas 7% menghasilkan pemborosan pakan dan penurunan efisiensi drastis, sehingga direkomendasikan batas pemberian pakan benih adalah **maksimal 5% biomassa**.
3. **Essien et al. (2024)** mengevaluasi benih lele berbobot 2,25 g dengan ransum standar **5% biomassa per hari** selama 10 minggu:
   - Pakan komersial kualitas prima (*Coppens*) mencatatkan kelulushidupan (*survival rate*) sebesar **100%** dengan bobot akhir 53,10 g.
4. **Pelu & Liubana (2025)** mencatat bahwa pada fase pendederan lele sangkuriang di BBI Teun, pembudidaya menerapkan ransum **5% hingga 10% dari total biomassa** yang dibagi dalam beberapa waktu makan per hari untuk mengimbangi laju metabolisme benih.

### 5.3. Frekuensi Pemberian Pakan Harian (*Feeding Frequency*)
* Pembagian ransum harian ke dalam **3 hingga 4 kali waktu makan per hari** menghasilkan pertumbuhan dan kelulushidupan yang optimal (Pelu & Liubana, 2025; Kurdowi et al., 2025).
* **Jadwal 4 Kali Sehari (Pendederan Intensif)**: Pagi (07.00 - 08.00 WIB), Siang (12.00 - 13.00 WIB), Sore (17.00 - 18.00 WIB), dan Malam (21.00 - 22.00 WIB).
* Survei unit pembenihan lele komersial oleh Uche et al. (2023) mengonfirmasi bahwa kepatuhan jadwal pemberian pakan harian teratur merupakan faktor utama pencegahan mortalitas larva dan heterogenitas ukuran benih lele.

### 5.4. Pola Sebar Pakan (*Broadcast Feeding*)
Pemberian pakan **wajib disebar merata ke seluruh permukaan kolam (*broadcast feeding*)** dan tidak boleh dikonsentrasikan hanya pada satu titik sudut:
* Memastikan seluruh individu benih memperoleh akses nutrisi secara setara.
* Mencegah benih dominan berukuran besar menguasai area tertentu yang memicu kanibalisme terhadap benih kecil.

---

## 6. Dinamika Perilaku Makan & Mitigasi Kanibalisme

Benih lele memiliki dua tipe kanibalisme (Gisbert et al., 2021):
1. **Tipe I (*Tail-Biting*)**: Benih menyerang dan menggigit sirip ekor sesamanya. Mengakibatkan luka fisik, infeksi bakteri/jamur sekunder, dan stres berkepanjangan.
2. **Tipe II (*Head-First Swallowing*)**: Benih berukuran besar menelan utuh benih yang lebih kecil mulai dari bagian kepala. Terjadi saat rasio panjang tubuh antaranak ikan melampaui 1,3 : 1.

**Prosedur Mitigasi Terpadu**:
* **Sortasi Ukuran (*Grading*) Rutin**: Wajib dilakukan setiap **7 hingga 10 hari sekali** pada tahap pendederan menggunakan saringan berpori seragam (Pelu & Liubana, 2025).
* **Ketepatan Waktu Pakan Otomatis**: Menghindari keterlambatan pemberian ransum pakan saat benih telah mencapai ambang batas lapar.

---

## 7. Integrasi Sistem Visi Komputer pada *Edge Device* (Raspberry Pi)

Penerapan kamera dan algoritma visi komputer pada Raspberry Pi menghubungkan standar biologis benih lele dengan pemberian pakan otomatis:

1. **Uji Nafsu Makan (*Sampling Batch*)**: Feeder menyebarkan sedikit pelet uji (~5% dari kuota ransum per sesi) secara merata di permukaan kolam.
2. **Kalkulasi Indeks Gerakan (*Motion Activity Index*)**: Kamera mendeteksi lonjakan pergerakan renang menyambar permukaan (*surface bursting*) menggunakan algoritma komputasi ringan (*frame differencing*).
3. **Pemberian Kuota Penuh**: Jika indeks gerakan melampaui ambang batas lapar ($T_{\text{lapar}}$), aktuator menyalurkan sisa kuota pakan (sesuai dosis standar 5% biomassa) (Afia et al., 2020; Jibrin et al., 2024).
4. **Penghentian Otomatis (*Anti-Overfeeding*)**: Begitu intensitas gerak ikan turun mendekati *baseline* tenang ($T_{\text{kenyang}}$), pemberian pakan segera dihentikan otomatis. Hal ini menjaga DO kolam tetap $\ge 5$ mg/L dan mencegah pembusukan pelet mikro (Kurdowi et al., 2025; Pelu & Liubana, 2025).

---

## 8. Daftar Pustaka Ilmiah Terverifikasi (9 Artikel Terunduh)

1. **Afia, O. E., Kolawole, D. O., & David, G. S. (2020).** Growth Response of *Clarias gariepinus* (North African Catfish) Under Varying Feeding Rates. *Sumerianz Journal of Biotechnology*, 3(11), 113–117. [https://doi.org/10.47752/sjb.311.113.117](https://doi.org/10.47752/sjb.311.113.117)
2. **Essien, E., Okon, A., Udoinyang, E., Abasubong, K., & Akinjogunla, V. (2024).** Comparative Assessment on the Growth Performance of the African Catfish, *Clarias gariepinus* Fingerlings Fed Two Commercial Feeds in Nigeria. *Acta Natura et Scientia*, 5(2), 324–332. [https://doi.org/10.61326/actanatsci.v5i2.324](https://doi.org/10.61326/actanatsci.v5i2.324)
3. **Gisbert, E., Luz, R. K., Fernández, I., Pradhan, P. K., Salhi, M., Mozanzadeh, M. T., Kumar, A., Kotzamanis, Y., Castro-Ruiz, D., Bessonart, M., & Darias, M. (2021).** Development, nutrition, and rearing practices of relevant catfish species (Siluriformes) at early stages. *Reviews in Aquaculture*, 13(4), 1807–1843. [https://doi.org/10.1111/raq.12586](https://doi.org/10.1111/raq.12586)
4. **Jibrin, H., Sakaba, A. A., Adeoye, R. L., O., E., Abdullahi, U. U., & Salawu, A. (2024).** Effect of feeding rate on growth and nutrients utilization of African catfish *Clarias gariepinus* (Burchell 1822) fingerlings fed with vital feed. *International Journal of Fisheries and Aquatic Studies*, 12(5), 24–30. [https://doi.org/10.22271/fish.2024.v12.i5b.2979](https://doi.org/10.22271/fish.2024.v12.i5b.2979)
5. **Kurdowi, S. A., Khumaidi, A., & Wafi, A. (2025).** TECHNIQUE FOR BREDDING CATFISH (*CLARIAS GARIEPINUS*) AT THE FISHERIES TRAINING AND EXTENSION CENTER (BPPPP) BANYUWANGI. *Jurnal Perikanan Unram*, 15(3), 1634–1643. [https://doi.org/10.29303/jp.v15i3.1634](https://doi.org/10.29303/jp.v15i3.1634)
6. **Pelu, A. M., & Liubana, D. V. (2025).** Pengaruh Kualitas Air Terhadap Tingkat Kelangsungan Hidup Ikan Lele Sangkuriang (*Clarias gariepinus*) pada Tahap Pendederan di Balai Benih Ikan (BBI) Teun. *Jurnal Akuakultur Sungai dan Danau*, 10(2), 287–294. [https://doi.org/10.35965/jasd.v10i2.7533](https://doi.org/10.35965/jasd.v10i2.7533)
7. **Pranat, G. V. Y., Heirina, A., Murtini, S., & Neksidin, N. (2025).** THE EFFECT OF DIFFERENT FEED TYPES ON THE SURVIVAL OF CATFISH FRY (*Clarias sp.*). *Jurnal Perikanan Unram*, 15(6), 1912–1920. [https://doi.org/10.29303/jp.v15i6.1912](https://doi.org/10.29303/jp.v15i6.1912)
8. **Srivastava, P. P., Raizada, S., Dayal, R., Chowdhary, S., Lakra, W. S., Yadav, A. K., Sharma, P., & Gupta, J. (2012).** Breeding and Larval Rearing of Asian Catfish, *Clarias batrachus* (Linnaeus, 1758) on Live and Artificial Feed. *Journal of Aquaculture Research and Development*, 3(4), 1000134. [https://doi.org/10.4172/2155-9546.1000134](https://doi.org/10.4172/2155-9546.1000134)
9. **Uche, C., et al. (2023).** Survey of Catfish Hatchery Knowledge and Practices in Obio-Akpor Local Government Area, Rivers State, Nigeria. *Agrobiological Records*, 11, 26–34. [https://doi.org/10.47278/journal.abr/2023.026](https://doi.org/10.47278/journal.abr/2023.026)

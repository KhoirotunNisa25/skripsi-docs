# Konteks Proyek Skripsi: Deteksi Aktivitas Ikan Lele sebagai Indikasi Lapar

Saya sedang mengembangkan skripsi tentang **deteksi kondisi lapar/tidak lapar pada ikan lele berdasarkan pola aktivitas atau gerakan ikan di permukaan kolam**, yang nantinya digunakan sebagai salah satu dasar dalam pengembangan sistem pemberian pakan otomatis. Fokus penelitian saya berada pada sisi *computer vision* dan deteksi perilaku ikan, sedangkan kolaborator saya, Varizky, berfokus pada kualitas air dan *water exchange system*.

## 1. Setup Penelitian

Objek penelitian berupa kolam lele outdoor yang menggunakan aerator. Kamera Raspberry Pi ditempatkan di atas kolam (*top-view/overhead*) untuk merekam kondisi permukaan air pada **10 FPS**.

Terdapat pula sensor pendukung seperti pH, suhu, TDS, kekeruhan, dan tinggi air. Saat ini data sensor masih ditampilkan pada dashboard terpisah dan belum disinkronkan dengan analisis video.

Data awal yang telah dikumpulkan terdiri dari **9 sesi rekaman valid dari 13 sesi yang dijadwalkan**, yang dilakukan selama 3 hari (15–17 September 2026), dengan variasi waktu:

* pagi, dekat waktu pemberian pakan (~05.30–07.30);
* siang, di luar waktu pakan (~10.00–13.00);
* malam, baik dekat waktu pakan (~18.00) maupun di luar waktu pakan (~22.00/01.00).

## 2. Tantangan Utama: Aktivitas Normal Kolam

Permasalahan utama penelitian adalah permukaan kolam **tidak pernah benar-benar diam** karena aerator terus menghasilkan gelembung dan pergerakan air.

Dengan demikian, sistem tidak dapat menggunakan logika sederhana:

> **Ada gerakan air → ikan lapar.**

Pergerakan akibat aerator harus dianggap sebagai **kondisi normal atau baseline**. Sistem perlu mempelajari karakteristik pergerakan tersebut terlebih dahulu, kemudian mendeteksi aktivitas yang menyimpang dari baseline.

Secara konseptual, alur deteksinya adalah:

**Kondisi normal kolam**
→ pergerakan air akibat aerator
→ **pembentukan baseline**
→ terjadi perubahan aktivitas
→ **analisis pola perubahan**
→ *fish activity / candidate feeding signal*
→ estimasi kondisi lapar/tidak lapar
→ keputusan pemberian pakan

Perubahan yang diamati dapat berupa ikan yang naik ke permukaan, peningkatan intensitas gerakan, gerakan mengejar sesuatu, riak yang muncul secara tiba-tiba, atau *splash*.

Namun, **perubahan aktivitas tidak secara otomatis berarti ikan lapar**. Aktivitas permukaan juga dapat dipengaruhi oleh kualitas air, stres, cahaya, kepadatan ikan, kondisi lingkungan, maupun gangguan eksternal. Oleh karena itu, hubungan:

**aktivitas permukaan → indikasi lapar → pemberian pakan**

masih harus dibuktikan berdasarkan data penelitian.

## 3. Metode Observasi Awal

Pada tahap awal, pelabelan masih dilakukan secara manual. Saya menonton setiap video dan mencatat kejadian ketika terdapat perubahan visual dari kondisi baseline kolam dengan aerator menyala.

Setiap kejadian dicatat dalam bentuk:

* rentang frame mulai–selesai;
* kategori aktivitas;
* intensitas subjektif.

Label awal yang digunakan adalah:

* **Kandidat Aktivitas** — perubahan/riak relatif kecil;
* **Kandidat Keresahan** — gelombang lebih besar atau indikasi ikan melompat.

Intensitas kemudian dikelompokkan menjadi **Rendah, Sedang, dan Tinggi**.

Dari 9 sesi rekaman tersebut, terdapat **151 event** yang berhasil dicatat.

## 4. Temuan Awal

Beberapa temuan awal dari observasi manual adalah:

1. **Durasi event sangat singkat.**
   Event tercepat hanya berlangsung sekitar **3–6 frame**, atau 0,3–0,6 detik pada 10 FPS. Ini menunjukkan bahwa interval sampling 10–15 frame yang sebelumnya diusulkan berpotensi melewatkan kejadian pendek. Untuk tahap berikutnya, analisis perlu dilakukan dengan resolusi temporal yang lebih rapat, bahkan mendekati *per-frame*.

2. **Aktivitas lebih banyak ditemukan pada sesi pagi dekat waktu pakan.**
   Persentase durasi aktivitas terhadap total durasi sesi sekitar **11,8% pada sesi pagi**, dibandingkan sekitar **0,95% pada siang hari** dan **0,45% pada malam hari di luar waktu pakan**.

3. **Kandidat keresahan hanya muncul pada sesi pagi dekat waktu pakan.**
   Kategori dengan intensitas lebih tinggi tersebut belum ditemukan pada sesi siang maupun malam. Hal ini dapat menjadi indikasi awal adanya hubungan antara aktivitas permukaan dan waktu pemberian pakan, tetapi **belum cukup untuk menyimpulkan bahwa aktivitas tersebut merupakan indikator lapar** karena jumlah dan durasi data masih terbatas.

4. **Terdapat gangguan visual (*visual noise*).**
   Beberapa kondisi dapat menghasilkan perubahan visual yang menyerupai aktivitas ikan, seperti pantulan cahaya matahari pada pagi hari, pantulan lampu pada malam hari, daun yang mengambang, serta burung yang masuk ke area kolam dan menimbulkan riak.

## 5. Gap Penelitian Saat Ini

Pelabelan yang dilakukan masih bersifat **manual dan subjektif**, sehingga belum dapat digunakan sebagai metode deteksi otomatis.

Saat ini belum terdapat mekanisme terprogram untuk mengekstraksi karakteristik aktivitas dari citra, misalnya:

* skor pergerakan per frame menggunakan *frame differencing* atau *optical flow*;
* jumlah dan posisi ikan;
* pola perubahan aktivitas terhadap baseline aerator;
* pemisahan riak yang disebabkan ikan dari gelembung aerator;
* identifikasi gangguan seperti daun, burung, atau pantulan cahaya.

Dengan demikian, **151 event yang diperoleh saat ini lebih tepat diposisikan sebagai data observasi awal untuk memahami pola dan menentukan karakteristik yang perlu dideteksi**, bukan sebagai ground truth bahwa seluruh event tersebut merupakan kondisi lapar.

## 6. Kebutuhan Tahap Berikutnya

Penelitian masih berada pada tahap observasi awal. Data baru mencakup **3 hari**, sedangkan target awal pembimbing adalah minimal sekitar **1 minggu** untuk melihat pola yang lebih stabil sebelum masuk ke tahap penentuan metode dan penyusunan proposal.

Tahap berikutnya perlu berfokus pada:

**penambahan data → pembentukan baseline → ekstraksi fitur aktivitas → pemisahan aktivitas ikan dan noise → analisis hubungan aktivitas dengan waktu/kondisi pakan → validasi indikasi lapar → perumusan metode deteksi otomatis.**

Dengan pendekatan tersebut, sistem tidak langsung mengasumsikan bahwa setiap gerakan air merupakan tanda lapar, tetapi terlebih dahulu memodelkan **aktivitas normal kolam** dan mencari pola perubahan yang secara konsisten berkaitan dengan kondisi ikan.

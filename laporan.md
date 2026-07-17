# Klasifikasi Kelayakan Konsumsi Jamur Berdasarkan Ciri Fisik Menggunakan Algoritma Decision Tree dan Naive Bayes

## 1. Judul Proyek
*   **Kelompok 17** 
    1. Ruby Nabiel Muzaffar Hidayat
*   **Domain Proyek (Latar Belakang):**
    Aktivitas mencari makanan liar (*foraging*) di alam semakin populer, namun hal ini membawa risiko fatal akibat keracunan jamur liar. Beberapa jamur beracun memiliki kemiripan fisik dengan jamur yang aman dikonsumsi sehingga identifikasi manual seringkali bias dan tidak akurat. Oleh karena itu, pendekatan *Machine Learning* sangat dibutuhkan untuk mengklasifikasikan kelayakan konsumsi jamur secara otomatis dan akurat berdasarkan karakteristik fisiknya.

## 2. Business Understanding
*   **Permasalahan Dunia Nyata dan Literatur Review:**
    Masyarakat awam dan pencari jamur pemula kesulitan membedakan antara jamur yang aman dimakan (*edible*) dan yang beracun (*poisonous*). Kesalahan identifikasi ini dapat menyebabkan masalah kesehatan fatal. Literatur terkait botani dan kecerdasan buatan menunjukkan bahwa ciri fisik visual dan penciuman, seperti bentuk tudung, warna insang, dan bau, merupakan indikator paling kuat untuk menentukan tingkat toksisitas jamur.
*   **Tujuan Proyek:**
    Membangun model kecerdasan buatan (klasifikasi) yang mampu mengelompokkan jamur ke dalam kelas beracun atau aman dikonsumsi dengan tingkat akurasi dan metrik *recall* yang tinggi.
*   **Siapa User/Pengguna Sistem:**
    Ahli botani, komunitas pencari jamur (*foragers*), peneliti keamanan pangan, dan pengembang aplikasi identifikasi tanaman.
*   **Solusi dan Manfaat Implementasi AI:**
    Implementasi algoritma AI (Decision Tree dan Naive Bayes) akan memberikan sistem pendukung keputusan yang cepat dan meminimalkan bias *human-error* saat melakukan identifikasi spesies jamur di alam bebas, yang pada akhirnya dapat menyelamatkan nyawa penggunanya dari risiko keracunan.

## 3. Data Understanding
*   **Sumber Data:** 
    Dataset yang digunakan adalah "Mushroom Classification" yang bersumber dari UCI Machine Learning Repository dan diakses melalui [Kaggle](https://www.kaggle.com/datasets/uciml/mushroom-classification).
*   **Deskripsi Setiap Fitur (Atribut):**
    Dataset ini memiliki 22 atribut prediktor, beberapa fitur utamanya antara lain:
    *   `cap-shape`: Bentuk tudung jamur (bell, conical, flat, dll).
    *   `cap-color`: Warna tudung jamur.
    *   `odor`: Bau jamur (almond, anise, foul, none, dll).
    *   `gill-color`: Warna insang jamur.
    *   `habitat`: Lingkungan tempat tumbuh (grasses, leaves, meadows, dll).
*   **Ukuran dan Format Data:** 
    Terdiri dari 8.124 baris observasi dan 23 kolom (22 fitur prediktor + 1 target kelas) dalam format `.csv`.
*   **Tipe Data dan Target Klasifikasi:**
    *   **Tipe Data:** Seluruh kolom berisi tipe data Kategorikal (berwujud teks/huruf tunggal).
    *   **Target Klasifikasi:** Kolom `class` yang memuat target biner, yaitu `e` (*edible*/aman dimakan) dan `p` (*poisonous*/beracun).

## 4. Exploratory Data Analysis (EDA)
*   **Visualisasi Distribusi Data:**

     <img width="588" height="420" alt="Screenshot 2026-07-17 081416" src="https://github.com/user-attachments/assets/46dfc190-794b-43e5-ae75-f9a24b4cbcf9" />

    [Insight: Distribusi antar kelas cukup seimbang, sehingga penanganan imbalance data tidak diperlukan.]
*   **Analisis Korelasi Antar Fitur:**
    <img width="916" height="486" alt="Screenshot 2026-07-17 081730" src="https://github.com/user-attachments/assets/a7fde0cc-be00-4b46-a9e7-deb4b9d5d359" />
    <img width="921" height="305" alt="Screenshot 2026-07-17 081820" src="https://github.com/user-attachments/assets/505da128-0a9d-4bef-b4ab-9e467ac56797" />

*   **Deteksi Data Tidak Seimbang (Imbalanced Classes):**
    Proporsi data cukup proporsional, yaitu sekitar 51,8% berlabel aman dan 48,2% berlabel beracun.
*   **Insight Awal dari Pola Data:**
    Fitur penciuman (`odor`) memiliki pengaruh korelasi yang sangat kuat terhadap target kelas. Sebagian besar jamur yang berbau menyengat dikategorikan beracun, sementara yang tidak berbau rata-rata aman.

## 5. Data Preparation
*   **Data Cleaning:**
    Melakukan pemeriksaan *missing value*. Ditemukan karakter '?' pada kolom `stalk-root` yang kemudian ditangani dengan membuang (drop) kolom tersebut agar tidak mengganggu pemodelan.
*   **Encoding Data Kategorik:**
    Karena seluruh data berformat teks kategorikal nominal, diterapkanlah teknik `Label Encoding` menggunakan *library* Scikit-Learn untuk mengubah huruf-huruf tersebut menjadi matriks angka (0, 1, 2, dst) supaya dapat dihitung oleh algoritma matematika.
*   **Normalisasi / Standardisasi Data Numerik:**
    Tahap ini tidak dilakukan karena dataset murni berisi data kategorik hasil *encoding*, bukan data kontinu dengan rentang variansi matematis yang jauh.
*   **Data Split (Train-Test):**
    Dataset dipisahkan (split) dengan rasio 80% untuk data latih (Data Train) dan 20% untuk data uji (Data Test).

## 6. Modeling
*   **Pemilihan Algoritma:** 
    1. Decision Tree Classifier
    2. Naive Bayes (Gaussian Naive Bayes)
*   **Alasan Pemilihan 2 Algoritma:**
    Decision Tree dipilih karena sangat baik dalam memetakan aturan berbentuk kriteria fisik berjenjang (cocok untuk taksonomi biologis). Naive Bayes dipilih sebagai pembanding karena performanya yang sangat ringan dan cepat dalam memproses probabilitas data-data kategorikal.
*   **Implementasi Model:**
    <img width="784" height="278" alt="Screenshot 2026-07-17 082058" src="https://github.com/user-attachments/assets/597bbb7f-fd87-4af5-b091-fba34be15a2b" />

*   **Perbandingan Model:**
    Secara konsep, Decision Tree membentuk rantai kondisi (*if-else*) dari fitur yang paling membedakan kelas (seperti bau), sedangkan Naive Bayes mengasumsikan bahwa fitur seperti warna dan bentuk tidak saling terkait satu sama lain, lalu menghitung total probabilitas bersyaratnya.
*   **Visualisasi Model:**
   <img width="1371" height="868" alt="Screenshot 2026-07-17 082225" src="https://github.com/user-attachments/assets/4b6c1ada-18e6-453d-88dc-1d66bd58ffa7" />
*   **Perbandingan Model:**
    Kedua model menunjukkan kinerja yang sangat bagus. **Decision Tree** memiliki pola pengambilan keputusan yang sangat tajam berbasis aturan fisik, sementara **Naive Bayes** memberikan estimasi probabilitas yang stabil berdasarkan kemunculan fitur. Pada dataset jamur ini, Decision Tree mampu menangkap pola non-linear dengan lebih efisien karena struktur data yang kategorikal.

## 7. Evaluation
*   **Confusion Matrix:**

    <img width="455" height="328" alt="Screenshot 2026-07-17 082314" src="https://github.com/user-attachments/assets/9086189d-450f-403b-aca7-2cb7ac26722f" />
    <img width="456" height="324" alt="Screenshot 2026-07-17 082322" src="https://github.com/user-attachments/assets/9e2adad6-64aa-41df-bded-7eaa2f8ae41c" />

*   **Metrik Evaluasi:**
    *   **Decision Tree:** 
        * Accuracy: [100 %]
        * Precision: [100 %]
        * Recall: [100 %]
        * F1-score: [100 %]
    *   **Naive Bayes:** 
        * Accuracy: [92 %]
        * Precision: [93 %]
        * Recall: [91 %]
        * F1-score: [92 %]
*   **Penjelasan Kinerja Model:**
    Berdasarkan hasil evaluasi, kedua model menunjukkan akurasi yang sangat tinggi. Namun, **Decision Tree** mencapai akurasi [100]% dengan *Recall* sebesar [100]%. Hal ini menunjukkan bahwa model Decision Tree hampir tidak ada kesalahan mengklasifikasikan jamur beracun sebagai jamur aman (*False Negative*). 
    Dalam konteks keamanan pangan, metrik *Recall* pada kelas "Beracun" menjadi prioritas utama. Karena hasil *False Negative* yang mendekati nol, model ini sangat dapat diandalkan untuk meminimalkan risiko keracunan bagi pengguna. **Naive Bayes** juga memberikan performa yang solid, namun sedikit di bawah Decision Tree pada metrik *F1-Score* karena asumsi kemandirian antar fiturnya yang terkadang terlalu menyederhanakan data.

## 8. Kesimpulan dan Rekomendasi
*   **Ringkasan Hasil Modeling dan Evaluasi:**
    Proyek ini berhasil mengimplementasikan dua model klasifikasi untuk menentukan kelayakan konsumsi jamur. Hasil pengujian menunjukkan bahwa *Decision Tree* adalah model terbaik dengan tingkat akurasi sebesar [100]%. Analisis pada *Confusion Matrix* membuktikan bahwa model mampu mengklasifikasikan jamur dengan tingkat kesalahan yang sangat minimal. Evaluasi secara keseluruhan menunjukkan bahwa fitur `odor` (bau) memiliki dampak paling signifikan terhadap akurasi klasifikasi kedua model yang digunakan.
*   **Apakah Tujuan Proyek Tercapai?:**
    Ya, proyek ini berhasil membangun sistem klasifikasi dengan performa tinggi yang mampu mengidentifikasi jamur beracun secara efektif.
*   **Kelebihan dan Keterbatasan Model:**
    Model mampu memberikan prediksi instan dan sangat akurat dari kombinasi teks atribut. Keterbatasannya adalah pengguna harus memahami istilah bentuk/warna jamur dan memasukkannya secara manual (berbasis data tabular).
*   **Rekomendasi Perbaikan:**
    Untuk pengembangan di masa depan, disarankan membangun model klasifikasi berbasis citra digital (Computer Vision / CNN) agar pengguna cukup mengambil foto jamur menggunakan kamera tanpa perlu menginputkan data tabular satu per satu.

## 9. Referensi
1. Schlimmer, J. (1987). Mushroom Database. *UCI Machine Learning Repository*. https://doi.org/10.24432/C5959T
2. Hayami, R. (2022). Klasifikasi Jamur Menggunakan Algoritma Naïve Bayes. Jurnal Computer Science and Information Technology https://ejurnal.umri.ac.id/index.php/coscitech/article/view/3685.
3. Lim, VR. (2025). Klasifikasi Kelayakan Konsumsi Jamur Menggunakan Algoritma K-Nearest Neighbors, Decision Tree, Support Vector Machine dan Gradient Boosting Classifier. Jurnal Ilmu Komputer dan Informatika [(JKI) Universitas Tarumanagara.](https://journal.untar.ac.id/index.php/JKI/article/view/35640)
4. Saifudin, MAR. (2026). Analisis Perbandingan Hasil Kerja Algoritma C4.5 (Decision Tree) dan Naive Bayes. Jurnal Ilmiah Teknik Elektro Komputer dan Informatika [ (JITET) Universitas Lampung.](https://journal.eng.unila.ac.id/index.php/jitet/article/view/9084)
5. Tarawneh, O. (2023). Mushroom classification using machine-learning techniques. [AIP Conference Proceedings](https://pubs.aip.org/aip/acp/article-abstract/2979/1/030003/2917941/Mushroom-classification-using-machine-learning).

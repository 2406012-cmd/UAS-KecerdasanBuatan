# Panduan Pengerjaan Tugas Besar - UAS Kecerdasan Buatan

## Langkah 1: Persiapan Dataset
1. Mengunduh dataset `mushrooms.csv` dari [Kaggle](https://www.kaggle.com/datasets/uciml/mushroom-classification).
2. Memasukkan dataset ke dalam folder `/data/dataset/` di dalam repositori untuk menjaga kerapian struktur folder.

## Langkah 2: Pemrosesan Data (Preprocessing)
1. **Pembersihan Data**: Melakukan pengecekan *missing value*. Menghapus kolom yang mengandung karakter tidak valid (seperti `?` pada fitur `stalk-root`).
2. **Encoding**: Karena seluruh data bersifat kategorikal (teks), digunakan `LabelEncoder` dari pustaka `sklearn.preprocessing` untuk mengubah data teks menjadi nilai numerik.
3. **Data Splitting**: Membagi dataset menjadi dua bagian menggunakan `train_test_split` dengan komposisi 80% data latih (training set) dan 20% data uji (testing set).

## Langkah 3: Exploratory Data Analysis (EDA)
1. **Visualisasi Distribusi**: Membuat *bar chart* untuk memastikan keseimbangan antara jamur beracun dan jamur aman.
2. **Analisis Korelasi**: Membuat *heatmap* untuk melihat keterkaitan antar fitur. Fitur `odor` (bau) diidentifikasi sebagai prediktor terkuat dalam menentukan kelas jamur.

## Langkah 4: Pemodelan (Modeling)
1. **Pemilihan Algoritma**: Menggunakan dua algoritma klasifikasi, yaitu **Decision Tree** dan **Naive Bayes**.
2. **Pelatihan Model**: Melakukan proses *training* menggunakan perintah `.fit()` pada data latih (`X_train`, `y_train`).
3. **Prediksi**: Melakukan pengujian model menggunakan data uji (`X_test`) untuk mendapatkan hasil prediksi.

## Langkah 5: Evaluasi Model
1. **Confusion Matrix**: Menghasilkan matriks 2x2 untuk melihat jumlah prediksi benar (True Positive/Negative) dan salah (False Positive/Negative).
2. **Metrik Evaluasi**: Menghitung **Accuracy**, **Precision**, **Recall**, dan **F1-Score**.
3. **Analisis**: Membandingkan performa kedua algoritma untuk menentukan model terbaik (dengan fokus pada minimasi *False Negative* pada kelas beracun).

## Langkah 6: Pelaporan
1. Menyusun hasil analisis ke dalam file **`Laporan_uas.md`**.
2. Menyertakan visualisasi (grafik dan *tree plot*) ke dalam folder `/images/` dan menampilkannya di dalam laporan.
3. Menyertakan daftar referensi ilmiah dengan format APA.
4. Melakukan *commit* dan *push* seluruh file ke repositori GitHub publik.

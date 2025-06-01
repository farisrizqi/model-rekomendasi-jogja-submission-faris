
# Sistem Rekomendasi Wisata Jogja

## 1. Project Overview (Ulasan Proyek)

Pariwisata merupakan salah satu sektor utama yang mendukung perekonomian Daerah Istimewa Yogyakarta (DIY). Dengan banyaknya destinasi yang tersedia, wisatawan sering mengalami kesulitan dalam menentukan tempat yang sesuai dengan preferensi mereka. Oleh karena itu, proyek ini bertujuan membangun **sistem rekomendasi wisata** berbasis data yang dapat membantu pengguna menemukan tempat wisata yang relevan dan menarik.

Proyek ini menggunakan dua pendekatan:
- **Content-Based Filtering** dengan TF-IDF.
- **Collaborative Filtering** menggunakan deep learning.

**Referensi**:
- Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems Handbook*.
- Data bersumber dari [Kaggle](https://www.kaggle.com/datasets/ardhiraka/tourism-rating).

## 2. Business Understanding

### Problem Statements  
- Bagaimana cara merekomendasikan tempat wisata yang sesuai preferensi pengguna?
- Bagaimana model dapat mempersonalisasi rekomendasi berdasarkan deskripsi tempat dan interaksi pengguna?

### Goals
- Membangun sistem rekomendasi wisata top-N untuk setiap pengguna.
- Menghasilkan dua pendekatan rekomendasi untuk perbandingan hasil.

### Solution Approach
1. **Content-Based Filtering**:
   - Menggunakan TF-IDF untuk mengukur kemiripan deskripsi antar destinasi.
2. **Collaborative Filtering**:
   - Menggunakan neural network untuk mempelajari preferensi pengguna berdasarkan interaksi rating.

## 3. Data Understanding

### Sumber dan Jumlah Data
- `tourism_jogja.csv`: 574 tempat wisata.
- `tourism_rating.csv`: 9800 rating pengguna.
- `user.csv`: 312 pengguna.

🔗 Link data: [Kaggle Tourism Rating Dataset](https://www.kaggle.com/datasets/ardhiraka/tourism-rating)

### Deskripsi Fitur
- **tourism_jogja.csv**: `place_id`, `name`, `description`, `category`, `type`, `rating`, `latitude`, `longitude`, `htm`.
- **tourism_rating.csv**: `User_Id`, `Place_Id`, `Place_Ratings`.
- **user.csv**: `User_Id`, `Age`, `Location`.

### Visualisasi & Insight
- Sebaran rating sebagian besar berada pada nilai tinggi (3–5).
- Tidak ada korelasi kuat antara rating dengan usia maupun harga tiket.
- Jenis wisata terbanyak adalah wisata sejarah dan alam.

## 4. Data Preparation

### Langkah yang Dilakukan
1. **Content-Based Filtering**:
   - Menggunakan `TfidfVectorizer` pada `description` tempat wisata.
   - Menghapus *stopwords* menggunakan pustaka Sastrawi.

2. **Collaborative Filtering**:
   - Menggabungkan data rating, user, dan wisata.
   - Menggunakan `LabelEncoder` untuk mengubah `User_Id` dan `Place_Id` menjadi numerik.

### Alasan Data Preparation
- TF-IDF butuh teks bersih untuk menghasilkan representasi yang akurat.
- Label encoding diperlukan karena model deep learning hanya menerima input numerik.

## 5. Modeling and Results

### Content-Based Filtering
- Menghitung *cosine similarity* antar deskripsi tempat wisata.
- Fungsi `recommend_places_content_based()` memberikan top-N wisata yang mirip dengan input pengguna.

Contoh Output: Top-10 wisata mirip Candi Borobudur.

### Collaborative Filtering
- Menggunakan arsitektur embedding untuk user dan tempat wisata.
- Melatih model selama 20 epoch, dengan fungsi loss `MSE`.

**Hasil Evaluasi**:
- **MAE (Mean Absolute Error)**: 1.2559

### Kelebihan & Kekurangan

| Pendekatan             | Kelebihan                                         | Kekurangan                                           |
|------------------------|--------------------------------------------------|-----------------------------------------------------|
| Content-Based Filtering | Tidak butuh data user, cocok untuk user baru.    | Terbatas pada item yang mirip secara deskripsi.     |
| Collaborative Filtering | Lebih personalisasi & akurat.                    | Butuh data interaksi yang cukup, tidak cocok untuk *cold-start*. |

## 6. Evaluation

### Metrik Evaluasi
- **Mean Absolute Error (MAE)** digunakan untuk mengukur kinerja prediksi rating.
- Formula:
  ```
  MAE = (1/n) * Σ |y_i - ŷ_i|
  ```

### Hasil Evaluasi
- Model collaborative filtering mencapai MAE **1.2559**, menunjukkan akurasi prediksi rating yang cukup baik untuk data rating 1–5.

## 7. Kesimpulan

- Proyek berhasil membangun dua jenis sistem rekomendasi:
  - **Content-Based Filtering** berbasis deskripsi tempat.
  - **Collaborative Filtering** berbasis deep learning.
- Hasil rekomendasi sesuai dan relevan dengan tujuan awal proyek.
- Sistem dapat diperluas ke konteks wisata daerah lain atau ditambahkan fitur seperti ulasan pengguna.

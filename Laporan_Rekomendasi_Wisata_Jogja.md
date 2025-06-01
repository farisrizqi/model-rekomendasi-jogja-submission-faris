# Sistem Rekomendasi Wisata Jogja
- Author: Faris Nur Rizqiawan
- Platform: Dicoding Submission – Proyek Akhir Machine Learning Terapan
- Domain: Lingkungan
- Metode: Collaborative Filtering (Deep Learning) dan Content-Based Filtering (TF-IDF)

## 1. Project Overview (Ulasan Proyek)

Pariwisata merupakan sektor penting yang mendukung perekonomian dan identitas budaya suatu daerah. Di Daerah Istimewa Yogyakarta, keberagaman objek wisata menjadikannya salah satu tujuan utama wisatawan domestik maupun mancanegara. Namun, dengan banyaknya pilihan tempat wisata, pengguna sering kali kesulitan dalam menentukan tempat mana yang sesuai dengan preferensi dan kebutuhan mereka.

Oleh karena itu, proyek ini bertujuan membangun Sistem Rekomendasi Tempat Wisata di Yogyakarta menggunakan dua pendekatan utama:

1. **Content-Based Filtering** menggunakan TF-IDF dan cosine similarity.
2. **Collaborative Filtering** menggunakan neural network dengan embedding.

**Referensi**:
- Suhailah, Eva, & Hartatik. (2023). Pembuatan sistem rekomendasi pariwisata Yogyakarta menggunakan Triangle Multiplying Jaccard. Jurnal Automation Computer Information System. [Jurnal](https://jacis.pubmedia.id/index.php/jacis/article/view/62/50)
- Nugroho, R.A. et al. (2020). Tourism Site Recommender System Using Item-Based Collaborative Filtering Approach. [Jurnal](https://repository.usd.ac.id/39342/1/6887_Tourism+Site+Recommender+System+Using+Item-Based+Collaborative+Filtering+Approach.pdf)
- Data bersumber dari [Kaggle](https://www.kaggle.com/datasets/farisrizqiawan/dataset-rekomendasi-wisata-jogja).

## 2. Business Understanding

### Problem Statements 
- Bagaimana membangun sistem rekomendasi yang dapat menyarankan tempat wisata di Yogyakarta secara personal, baik berdasarkan deskripsi objek wisata maupun berdasarkan rating dan preferensi pengguna lain?
- Bagaimana cara merekomendasikan tempat wisata yang sesuai preferensi pengguna?
- Bagaimana model dapat mempersonalisasi rekomendasi berdasarkan deskripsi tempat dan interaksi pengguna?

### Goals
- Membangun sistem rekomendasi dengan output Top-N recommendation.
- Meningkatkan relevansi rekomendasi berdasarkan preferensi pengguna.
- Menggunakan dua pendekatan algoritmik yang berbeda untuk memberikan hasil yang komprehensif.

### Solution Approach
1. **Content-Based Filtering**:
   - Menganalisis deskripsi objek wisata untuk merekomendasikan tempat serupa.
   - Menggunakan TF-IDF untuk mengukur kemiripan deskripsi antar destinasi.
2. **Collaborative Filtering**:
   - Menggunakan neural network untuk mempelajari preferensi pengguna berdasarkan interaksi rating.
   - Memprediksi rating untuk user tertentu terhadap objek wisata berdasarkan perilaku pengguna lain.

## 3. Data Understanding

### Sumber dan Jumlah Dataset
- `tourism_jogja.csv`: 437 tempat wisata Yogyakarta.
- `tourism_rating.csv`: 10000 rating pengguna.
- `user.csv`: 300 pengguna.

🔗 Link data: [Kaggle Tourism Rating Dataset](https://www.kaggle.com/datasets/farisrizqiawan/dataset-rekomendasi-wisata-jogja)

### Jumlah dan Kondisi Data
- Tidak terdapat missing value signifikan.
- Tipe data telah sesuai.
- Deskripsi wisata merupakan teks bebas yang akan digunakan dalam TF-IDF.

### Deskripsi Fitur / Variable Perdataset
1. tourism_jogja.csv
   | Atribut       | Tipe Data | Deskripsi                                                              |
   | ------------- | --------- | ---------------------------------------------------------------------- |
   | `place_id`    | Integer   | ID unik untuk tiap tempat wisata.                                      |
   | `name`        | String    | Nama tempat wisata.                                                    |
   | `rating`      | Float     | Rata-rata rating tempat wisata dari berbagai pengguna.                 |
   | `type`        | String    | Jenis tempat wisata berdasarkan karakteristiknya.                      |
   | `htm`         | Integer   | Harga tiket masuk dalam satuan Rupiah.                                 |
   | `latitude`    | Float     | Koordinat lintang lokasi tempat wisata.                                |
   | `longitude`   | Float     | Koordinat bujur lokasi tempat wisata.                                  |
   | `description` | String    | Deskripsi atau informasi singkat tentang tempat wisata.                |

2. rating_tourism.csv
   | Atribut         | Tipe Data | Deskripsi                                                               |
   | --------------- | --------- | ----------------------------------------------------------------------- |
   | `User_Id`       | Integer   | ID unik pengguna yang memberikan rating.                                |
   | `Place_Id`      | Integer   | ID tempat wisata yang dirating.                                         |
   | `Place_Ratings` | Integer   | Nilai rating dari pengguna terhadap tempat wisata (biasanya skala 1–5). |

3. user.csv
   | Atribut    | Tipe Data | Deskripsi                                                   |
   | ---------- | --------- | ----------------------------------------------------------- |
   | `User_Id`  | Integer   | ID unik pengguna.                                           |
   | `Age`      | Integer   | Usia pengguna, digunakan untuk segmentasi berdasarkan umur. |
   | `Location` | String    | Lokasi atau kota asal pengguna, untuk segmentasi geografis. |


### Variable Penting
1. Content-Based Filtering
   | Variabel      | Dataset            | Deskripsi                                                        |
   | ------------- | ------------------ | ---------------------------------------------------------------- |
   | `name`        | tourism\_jogja.csv | Nama tempat wisata yang digunakan untuk mencocokkan konten.      |
   | `description` | tourism\_jogja.csv | Deskripsi tempat wisata sebagai dasar analisis kemiripan konten. |

2. Collaborative Filtering
   | Variabel        | Dataset             | Deskripsi                                                          |
   | --------------- | ------------------- | ------------------------------------------------------------------ |
   | `Place_Ratings` | tourism\_rating.csv | Nilai rating yang diberikan pengguna terhadap suatu tempat wisata. |
   | `User_Id`       | tourism\_rating.csv | ID unik pengguna yang memberikan rating.                           |
   | `Place_Id`      | tourism\_rating.csv | ID tempat wisata yang dirating oleh pengguna.                      |

3. Segmentasi Pengguna
   | Variabel   | Dataset  | Deskripsi                                                        |
   | ---------- | -------- | ---------------------------------------------------------------- |
   | `Age`      | user.csv | Usia pengguna, digunakan untuk segmentasi berdasarkan umur.      |
   | `Location` | user.csv | Lokasi/kota asal pengguna, digunakan untuk segmentasi geografis. |

### Visualisasi dan Insight
1. Distribusi Rating Tempat Wisata

→ Objek wisata cenderung memiliki rating sedang hingga tinggi.

Sebaran Harga Tiket Masuk (HTM)
→ Ditemukan HTM dominan di bawah Rp50.000, cocok untuk wisatawan hemat.

Sebaran Lokasi (Latitude, Longitude)
→ Objek wisata tersebar merata di Yogyakarta dan sekitarnya.

Demografi Pengguna

→ Mayoritas pengguna berusia 20–35 tahun dan berdomisili di Yogyakarta dan sekitarnya.

Distribusi Jumlah Rating per Tempat dan per User
→ Tempat populer mendapat ratusan rating, namun sebagian besar tempat hanya memiliki sedikit rating, menunjukkan efek "long tail".


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
- **MAE (Mean Absolute Error)**: 1.2625

### Kelebihan & Kekurangan

| Pendekatan             | Kelebihan                                         | Kekurangan                                           |
|------------------------|--------------------------------------------------|-----------------------------------------------------|
| Content-Based Filtering | Tidak butuh data user, cocok untuk user baru.    | Terbatas pada item yang mirip secara deskripsi.     |
| Collaborative Filtering | Lebih personalisasi & akurat.                    | Butuh data interaksi yang cukup, tidak cocok untuk *cold-start*. |

## 6. Evaluation

### Metrik Evaluasi
- **Mean Absolute Error (MAE)** digunakan untuk mengukur kinerja prediksi rating.
- Formula:

$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} \left| y_i - \hat{y}_i \right|
$$

### Hasil Evaluasi
- Model collaborative filtering mencapai MAE **1.2559**, menunjukkan akurasi prediksi rating yang cukup baik untuk data rating 1–5.

## 7. Kesimpulan

- Proyek berhasil membangun dua jenis sistem rekomendasi:
  - **Content-Based Filtering** berbasis deskripsi tempat.
  - **Collaborative Filtering** berbasis deep learning.
- Hasil rekomendasi sesuai dan relevan dengan tujuan awal proyek.
- Sistem dapat diperluas ke konteks wisata daerah lain atau ditambahkan fitur seperti ulasan pengguna.

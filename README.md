
# 📍 Sistem Rekomendasi Wisata Jogja

Repositori ini berisi proyek machine learning untuk membangun **sistem rekomendasi tempat wisata di Yogyakarta** menggunakan dua pendekatan:

1. **Content-Based Filtering** (TF-IDF + Cosine Similarity)
2. **Collaborative Filtering** (Deep Learning)

## 📊 Dataset
Data yang digunakan berasal dari [Kaggle - Tourism Rating Dataset](https://www.kaggle.com/datasets/ardhiraka/tourism-rating), terdiri dari:
- Informasi tempat wisata (`tourism_jogja.csv`)
- Data rating pengguna (`tourism_rating.csv`)
- Data pengguna (`user.csv`)

## 📁 Struktur Proyek
- `Rekomendasi_Jogja.ipynb` - Notebook utama berisi pipeline lengkap dari EDA hingga evaluasi model.
- `rekomendasi_jogja.py` - Versi script Python dari proyek.
- `Laporan_Rekomendasi_Wisata_Jogja.md` - Laporan proyek dalam format Markdown.

## 🚀 Cara Menjalankan
1. Clone repositori ini.
2. Jalankan `Rekomendasi_Jogja.ipynb` di Google Colab.
3. Pastikan untuk mengatur mount Google Drive dan jalur file dataset sesuai.

## ✅ Hasil
- Sistem mampu memberikan top-N rekomendasi destinasi wisata berdasarkan deskripsi maupun preferensi pengguna.
- MAE model Collaborative Filtering: **1.2559**

## 🧠 Pembuat
**Faris Nur Rizqiawan**  
Submission untuk proyek akhir Dicoding - Machine Learning Terapan

---

> Sistem ini cocok untuk dikembangkan lebih lanjut sebagai fitur aplikasi pariwisata lokal berbasis data dan preferensi pengguna.

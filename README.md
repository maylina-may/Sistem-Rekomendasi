# 🕵️‍♀️ Laporan Proyek Machine Learning - Maylina Nur'aini

---

## 🎥 Project Overview

Dalam platform hiburan digital seperti Netflix, pengguna dihadapkan pada ribuan pilihan film dan acara TV, yang seringkali membuat keputusan menonton menjadi sulit. Proyek ini bertujuan mengembangkan sistem rekomendasi berbasis content-based filtering untuk membantu pengguna menemukan tayangan yang relevan berdasarkan karakteristik konten seperti genre, deskripsi, sutradara dan pemeran.

Dengan memanfaatkan teknik TF-IDF (Term Frequency–Inverse Document Frequency) dan Cosine Similarity, sistem ini mampu merekomendasikan film atau acara TV yang mirip dengan pilihan pengguna sebelumnya, bahkan tanpa memerlukan data riwayat interaksi. Pendekatan ini tidak hanya efisien dalam konteks keterbatasan data pengguna, tetapi juga sangat cocok diterapkan pada platform streaming seperti Netflix untuk meningkatkan pengalaman pengguna dan mempertahankan keterlibatan.

### 🔖 Referensi:

- [1] Sitorus, M.R. (2023) – Implementasi Model-Based Collaborative Filtering pada Sistem Rekomendasi Film.
  
  👉 [Universitas Medan Area Repository](https://repositori.uma.ac.id/jspui/bitstream/123456789/22762/1/188160044%20-%20Muhammad%20Rizky%20Sitorus%20-%20Fulltext.pdf)

- [2] Ridhwanullah, D., dkk. (2024). Content-Based Filtering pada Sistem Rekomendasi Buku Informatika.
  
  👉 https://www.p3m.sinus.ac.id/jurnal/index.php/e-jurnal_SINUS/article/view/840

- [3] Anonim (2023) – Implementasi Hybrid Recommendation untuk Sistem Rekomendasi Film Netflix.
  
  👉 [Universitas Kristen Satya Wacana Repository](https://repository.uksw.edu/handle/123456789/35187)

---

## 📊 Business Understanding

### ❓ Problem Statements

Pengguna platform streaming seperti Netflix kesulitan menemukan konten (film dan acara TV) baru yang relevan dan sesuai dengan preferensi mereka di tengah banyaknya pilihan yang tersedia. Hal ini dapat mengurangi kepuasan pengguna dan tingkat keterlibatan di platform.

### 🎯 Goals

1. Mengembangkan Sistem Rekomendasi: Membuat sistem rekomendasi yang mampu mengusulkan film atau acara TV baru kepada pengguna.
2. Menerapkan Pendekatan Content-Based Filtering: Menggunakan teknik content-based filtering untuk merekomendasikan konten berdasarkan kemiripan fitur-fitur dari konten itu sendiri.
3. Menggunakan TF-IDF dan Cosine Similarity: Memanfaatkan TF-IDF untuk merepresentasikan genre secara numerik dan Cosine Similarity untuk mengukur kemiripan antar item (film/acara TV).
4. Memberikan Rekomendasi yang Relevan: Menghasilkan daftar rekomendasi konten yang secara genre mirip dengan konten yang diminati oleh pengguna.
5. Meningkatkan Pengalaman Pengguna: Dengan memberikan rekomendasi yang relevan, sistem ini bertujuan untuk meningkatkan pengalaman pengguna dalam menemukan konten baru dan mempertahankan keterlibatan mereka di platform.

### 🧠 Solution Approach

- **Content-Based Filtering**

1. Menggunakan TF-IDF untuk merepresentasikan fitur teks seperti deskripsi, genre, pemeran, dan sutradara.
2. Mengukur kemiripan antar film/acara TV menggunakan Cosine Similarity.
3. Memberikan rekomendasi berdasarkan item yang memiliki atribut konten yang serupa.

- **Collaborative Filtering (alternatif)**
1. Dapat dikembangkan menggunakan pendekatan Matrix Factorization seperti SVD, jika data interaksi pengguna tersedia.
2. Mempersonalisasi rekomendasi berdasarkan pola preferensi pengguna lain yang serupa.

---

## 🗂️ Data Understanding

- **Sumber Data:** [Kaggle - Film dan Acara TV Netflix](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- **Jumlah data:** 8807 baris × 12 kolom
- **Kolom penting:** `title`, `type`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `listed_in`, `description`
- **Missing Values:**
  - `director`: 2634
  - `cast`: 825
  - `country`: 831
  - `date_added`: 11
  - `rating`: 4

---

## 🧹 Data Preparation

- Nilai kosong dihapus dengan `df.dropna()`.
- Pengecekan ulang missing value menggunakan `df.isna().sum()`.
- Fitur teks pada kolom `listed_in` diekstrak dan dibobot menggunakan **TF-IDF Vectorizer**.

---

## ⏳ Modeling

- **Representasi Fitur:** Menggunakan `TF-IDF Vectorizer` mengubah genre teks menjadi vektor numerik.
- **Algoritma Similarity:** Menggunakan `Cosine Similarity` untuk mengukur kemiripan antar konten berdasarkan vektor genre.
- **Mekanisme Rekomendasi:** Mengambil Top-N konten paling mirip berdasarkan skor similarity untuk rekomendasi.

### 📌 Contoh hasil Rekomendasi untuk `Holiday Rush`:

| No | Title                      | listed_in                        |
| -- | -------------------------- | -------------------------------- |
| 1  | Wish Man                   | Children & Family Movies, Dramas |
| 2  | Big Miracle                | Children & Family Movies, Dramas |
| 3  | A Champion Heart           | Children & Family Movies, Dramas |
| 4  | White Fang                 | Children & Family Movies, Dramas |
| 5  | You Are My Home            | Children & Family Movies, Dramas |
| 6  | Hachi: A Dog's Tale        | Children & Family Movies, Dramas |
| 7  | Balto                      | Children & Family Movies, Dramas |
| 8  | The Karate Kid Part III    | Children & Family Movies, Dramas |
| 9  | The Indian in the Cupboard | Children & Family Movies, Dramas |
| 10 | Hugo                       | Children & Family Movies, Dramas |


## 🔍 Evaluation 

- **Metode evaluasi:** Precision@k
- **Hasil:** Dengan threshold kemiripan 0.5, semua 10 rekomendasi teratas untuk `Holiday Rush` dianggap relevan berdasarkan kemiripan genre.
- **Precision@10:** 100% (nilai Precision@10 yang didapat dari output kode)

---

## 🔥 Kelebihan & Kekurangan

### 👍 Kelebihan:

- Tidak butuh data pengguna (bagus untuk pengguna/item baru).
- Rekomendasi spesifik berdasarkan item.
- Penjelasan rekomendasi mudah.
- Cepat setelah matriks dibuat.

### 👎 Kekurangan:
- Rekomendasi cenderung mirip, kurang variasi.
- Butuh deskripsi item yang baik (genre akurat).
- Item baru tidak langsung direkomendasikan.
- Skalabilitas terbatas untuk data sangat besar.

---

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

1. Pengguna kesulitan menemukan konten (film/acara TV) yang relevan di Netflix karena banyaknya pilihan.
2. Netflix memerlukan cara untuk memberikan rekomendasi konten yang dipersonalisasi kepada pengguna.

### 🎯 Goals

1. Membangun sistem rekomendasi berbasis konten yang dapat mengusulkan film atau acara TV berdasarkan kemiripan genre.
2. Mengembangkan fungsi yang dapat memberikan daftar rekomendasi teratas berdasarkan sebuah konten input dan mengevaluasinya.

### 🧠 Solution Approach

**Content-Based Filtering**

1. Merepresentasikan teks dengan TF-IDF Vectorizer
2. Mengukur kemiripan dengan Cosine Similarity
3. Memberikan rekomendasi berdasarkan item yang memiliki atribut konten yang serupa.

**Collaborative Filtering (alternatif)**

1. Dapat dikembangkan menggunakan pendekatan Matrix Factorization seperti SVD, jika data interaksi pengguna tersedia.
2. Mempersonalisasi rekomendasi berdasarkan pola preferensi pengguna lain yang serupa.

---

## 🗂️ Data Understanding

### Informasi Dataset

- **Sumber Data:** [Kaggle - Film dan Acara TV Netflix](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- **Ukuran Dataset:** 8807 baris × 12 kolom
- **Deskripsi Fitur:**

|     Fitur      | Tipe Data |             Keterangan                 |
| -------------- | --------- | ---------------------------------------|
| `show_id`      | string    | ID unik untuk tiap konten              |
| `type`         | string    | Jenis konten: "Movie" atau "TV Show"   |
| `title`        | string    | Judul konten                           |
| `director`     | string    | Nama sutradara (banyak nilai kosong)   |
| `cast`         | string    | Daftar pemeran utama                   |
| `country`      | string    | Negara tempat konten diproduksi        |
| `date_added`   | string    | Tanggal konten ditambahkan ke Netflix  |
| `release_year` | integer   | Tahun rilis                            |
| `rating`       | string    | Kategori usia (TV-MA, PG, dll.)        |
| `duration`     | string    | Durasi film (menit)                    |
| `listed_in`    | string    | Genre atau kategori konten             |
| `description`  | string    | Deskripsi singkat konten               |

### Kondisi Data

- **Missing Values:**

| Fitur        | Jumlah Kosong | 
| ------------ | ------------- | 
| `director`   | 2634          |
| `cast`       | 825           | 
| `country`    | 831           | 
| `date_added` | 10            | 
| `rating`     | 4             |

- **Outlier:** Tidak relevan karena fitur numerik (durasi) disimpan sebagai string, dan tidak terdapat nilai ekstrem yang mengganggu.

- **Duplikasi:** Tidak ditemukan duplikasi

### Penggunaan Fitur dalam Modeling

**Fitur yang Digunakan:**

`listed_in`: Kolom ini digunakan secara langsung sebagai input ke `TfidfVectorizer`, yang mengubah teks genre menjadi vektor numerik. Matriks TF-IDF inilah yang digunakan dalam perhitungan Cosine Similarity untuk menentukan kemiripan antar konten.
  - Alur Model
    - TF-IDF Vectorizer hanya diaplikasikan ke kolom listed_in.
      ```
      tfidf = TfidfVectorizer
      tfidf_matrix = tfidf.fit_transform(df['listed_in'])
      ```
    - Matriks hasil transformasi digunakan untuk menghitung Cosine Similarity antar konten.
    - Rekomendasi dihasilkan berdasarkan nilai similarity tertinggi.

**Fitur yang Tidak Digunakan:**

| Fitur              | Alasan Tidak Digunakan                                                            |
|--------------------|-----------------------------------------------------------------------------------|
| `description`      | Meskipun informatif, **tidak digunakan dalam TF-IDF** pada kode aktual            |
| `cast`, `director` | Tidak dimasukkan ke dalam proses modeling                                         | 
| `country`          | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) | 
| `date_added`       | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) | 
| `release_year`     | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) |
| `duration`         | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) |
| `rating`           | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) |
| `show_id`          | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) |
| `type`             | Tidak relevan untuk pendekatan content-based berbasis teks genre (`listed_in`) |

---

## 🧹 Data Preparation

### Menangani Missing Value 

- Data yang memiliki missing value dihapus menggunakan `dropna()`. 
- Verifikasi jumlah missing value dilakukan dengan df.isna().sum().

### TF-IDF Vectorization

Melakukan ekstrasi fitur menggunakan teknik TF-IDF Vectorizer pada fitur teks "listed_in", proses ini digunakan untuk mengubah data teks menjadi representasi numerik yang mencerminkan pentingnya suatu kata dalam konteks dokumen, sehingga dapat digunakan dalam pemodelan.

---

## ⏳ Modeling

- **Representasi Fitur:** Menggunakan `TF-IDF Vectorizer` mengubah genre teks menjadi vektor numerik.
- **Algoritma Similarity:** Cosine similarity diterapkan untuk menilai sejauh mana dua film memiliki kemiripan genre, dengan memanfaatkan representasi vektor TF-IDF dan DataFrame sebagai alat visualisasi tingkat kemiripan tersebut.
- **Mekanisme Rekomendasi:** Mengambil Top-N konten paling mirip berdasarkan skor similarity untuk rekomendasi.

- **Kelebihan & Kekurangan**
  - Kelebihan:
    1. Bagus untuk pengguna dan item baru (cold-start).
    2. Rekomendasi dapat dijelaskan (mengapa item itu direkomendasikan).
    3. Tidak memerlukan data pengguna lain (privasi terjaga).

  - Kekurangan:
    1. Cenderung merekomendasikan item yang sangat mirip (over-specialization).
    2. Tidak belajar dari perilaku atau preferensi pengguna lain.
    3. Bergantung pada kualitas deskripsi konten yang digunakan.

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

###  Hasil Evaluasi terhadap Business Understanding

Problem Statement 1:

Terjawab: Dengan memanfaatkan pendekatan content-based filtering berbasis genre (`listed_in`), sistem berhasil menyaring dan merekomendasikan konten yang memiliki kemiripan dengan tayangan pilihan pengguna. Hal ini secara langsung membantu pengguna mengurangi beban dalam memilah ribuan konten, sehingga mempermudah proses pengambilan keputusan.

Goal 1:

Tercapai: Sistem rekomendasi berhasil dibangun menggunakan TF-IDF dan Cosine Similarity untuk fitur genre. Hasil Precision@10 menunjukkan bahwa rekomendasi yang dihasilkan sangat relevan (100% untuk studi kasus Holiday Rush), yang menunjukkan keberhasilan sistem dalam mengusulkan konten serupa.

Problem Statement 2:

Terjawab: Sistem yang dibangun telah memberikan rekomendasi berdasarkan kemiripan konten, **tanpa menggunakan data pengguna lain**. Meskipun belum sepenuhnya personal seperti collaborative filtering, pendekatan ini tetap memberikan kesan personalisasi karena merekomendasikan konten serupa dengan yang sedang/baru saja ditonton pengguna. Ini menjadikannya solusi efektif dalam situasi cold-start.

Goal 2:

Tercapai: Fungsi rekomendasi telah dikembangkan dan mampu memberikan daftar rekomendasi teratas berdasarkan input judul. Evaluasi menggunakan Precision@10 memperlihatkan bahwa semua rekomendasi yang diberikan memiliki genre yang sangat mirip dengan input, membuktikan efektivitas model.

Dampak dari Solution Approach: Pendekatan ini memberi solusi yang cepat dan ringan dalam menyajikan rekomendasi relevan tanpa ketergantungan pada data pengguna. Ini bermanfaat bagi pengguna baru dan mempercepat content discovery di platform, yang pada akhirnya bisa meningkatkan **engagement**, **waktu tonton**, dan **retensi pelanggan Netflix**.

---

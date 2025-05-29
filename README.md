# 🕵️‍♀️ Laporan Proyek Machine Learning - Maylina Nur'aini

---

## 🎥 Project Overview

Dalam platform hiburan digital seperti Netflix, pengguna dihadapkan pada ribuan pilihan film dan acara TV, yang seringkali membuat keputusan menonton menjadi sulit. Proyek ini bertujuan mengembangkan sistem rekomendasi berbasis content-based filtering untuk membantu pengguna menemukan tayangan yang relevan berdasarkan karakteristik konten seperti genre, deskripsi, sutradara dan pemeran.

Dengan memanfaatkan teknik TF-IDF (Term Frequency–Inverse Document Frequency) dan Cosine Similarity, sistem ini mampu merekomendasikan film atau acara TV yang mirip dengan pilihan pengguna sebelumnya, bahkan tanpa memerlukan data riwayat interaksi. Pendekatan ini tidak hanya efisien dalam konteks keterbatasan data pengguna, tetapi juga sangat cocok diterapkan pada platform streaming seperti Netflix untuk meningkatkan pengalaman pengguna dan mempertahankan keterlibatan.

### 🔖 Referensi:

- [1] Sitorus, M.R. (2023) – Implementasi Model-Based Collaborative Filtering pada Sistem Rekomendasi Film.
  👉 Universitas Medan Area Repository
- [2] Ridhwanullah, D., dkk. (2024). Content-Based Filtering pada Sistem Rekomendasi Buku Informatika.
  👉 https://www.p3m.sinus.ac.id/jurnal/index.php/e-jurnal_SINUS/article/view/840
- [3] Anonim (2023) – Implementasi Hybrid Recommendation untuk Sistem Rekomendasi Film Netflix.
  👉 Universitas Kristen Satya Wacana Repository

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
- **Jumlah data:**8807 baris × 12 kolom
- **Kolom penting:** `title`, `type`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `listed_in`, `description`
- **Missing Values:**
  - `director`: 2634
  - `cast`: 825
  - `country`: 831
  - `date_added`: 11
  - `rating`: 4

---

## 🧹 Data Preparation



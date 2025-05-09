# Laporan Proyek Machine Learning - Natalio Michael Tumuahi

## :dart: Domain Proyek
Dalam era digital saat ini, ketersediaan data yang sangat besar dan beragam di dunia maya telah menciptakan tantangan sekaligus peluang besar di bidang rekomendasi. Salah satu tantangan terbesar yang dihadapi oleh pengguna internet adalah keputusan dalam memilih buku yang sesuai dengan minat mereka, mengingat banyaknya pilihan buku yang tersedia. Fenomena ini dikenal dengan istilah "Information Overload", di mana pengguna sering kali merasa kebingungan atau kesulitan dalam memilih informasi yang relevan, karena terlalu banyaknya pilihan.

Proyek ini bertujuan untuk memberikan solusi terhadap masalah rekomendasi buku yang tepat, melalui penerapan sistem rekomendasi berbasis teknologi. Sistem rekomendasi ini tidak hanya membantu pengguna untuk menemukan buku yang sesuai dengan preferensi mereka, tetapi juga memberikan pengalaman yang lebih efisien dalam proses pencarian buku. Dengan memanfaatkan berbagai metode seperti Content-Based Filtering dan Collaborative Filtering, proyek ini berfokus pada memberikan rekomendasi yang lebih akurat berdasarkan dua pendekatan utama:
1. Content-Based Filtering: Rekomendasi berdasarkan kesamaan konten antara buku yang sudah diketahui oleh pengguna (misalnya berdasarkan judul, penulis, atau deskripsi buku).
2. Collaborative Filtering: Rekomendasi berdasarkan preferensi pengguna lain yang memiliki pola pembacaan atau rating yang serupa, untuk memperkaya pilihan buku yang relevan bagi pengguna.

## 💹Business Understanding
### 🎗️Problem Statements
1. Bagaimana cara memberikan rekomendasi buku yang relevan bagi pengguna berdasarkan preferensi mereka, mengingat banyaknya pilihan buku yang tersedia di platform?
2. Bagaimana cara mengatasi masalah "Information Overload" pada pengguna yang kesulitan memilih buku dengan banyaknya pilihan yang ada?
3. Bagaimana sistem dapat mengidentifikasi buku yang serupa berdasarkan konten atau preferensi pengguna lain yang memiliki pola rating yang mirip?

### ⛳Goals
1. Membangun sistem rekomendasi buku yang akurat dan personal untuk membantu pengguna menemukan buku yang sesuai dengan minat mereka.
2. Menyediakan solusi efisien untuk mengurangi kebingungan pengguna dalam memilih buku di tengah informasi yang melimpah.
3. Memberikan rekomendasi buku yang lebih tepat berdasarkan dua pendekatan utama: kesamaan konten (Content-Based Filtering) dan kesamaan preferensi pengguna lain (Collaborative Filtering).

#### 💡Solution Statements
1. Content-Based Filtering Approach:
   * Sistem akan menggunakan TF-IDF (Term Frequency-Inverse Document Frequency) untuk menganalisis kesamaan antara buku berdasarkan fitur kontennya seperti judul, penulis, dan deskripsi buku. Dengan demikian, buku yang serupa secara konten akan direkomendasikan kepada pengguna yang mencari buku dengan tema atau genre serupa.

2. Collaborative Filtering Approach:
    * Menggunakan pendekatan K-Nearest Neighbors (KNN), sistem akan menganalisis pola rating dan perilaku pengguna lain yang memiliki kesamaan preferensi dengan pengguna. Buku yang telah diberi rating tinggi oleh pengguna yang memiliki pola preferensi yang mirip akan direkomendasikan kepada pengguna yang sedang mencari buku.

## 📂 Data Understanding
Dataset ini terdiri dari tiga file berbeda dengan jumlahnya masing-masing yaitu: <br>
* users.csv : 278859
* books.csv : 271379
* ratings.csv : 1149780 <br>

Dataset bisa diakses pada link berikut ini: https://www.kaggle.com/datasets/somnambwl/bookcrossing-dataset/data
<br><br>

**Variabel pada dataset**
1. Users.csv
  * User-ID: ID unik untuk setiap pengguna. Digunakan sebagai identitas utama untuk pemetaan user dalam sistem rekomendasi
  * Location: Informasi lokasi pengguna (biasanya dalam format "kota, negara bagian, negara").
  * Age: Usia pengguna
2. Books.csv
* ISBN: Nomor identifikas buky internasional (ID unik untuk setiap buku). Digunakan sebagai primary key untuk menghubungkan data dengan ratings.
* Title: Judul buku. Digunakan untuk menampilkan infomasi ke pengguna dan sebagai fitur dalam Content-Based Filtering
* Author: Nama buku. Digunakan dalam kombinasi judul sebagai fitur deskriptif dalam TF-IDF
* Year: Tahun terbt buku
* Publisher: Penerbit buku
3. Ratings.csv
* User-ID: ID pengguna yang memberikan rating. Dikaitkan dengan users.csv untuk mendapatkan informasi pengguna
* ISBN: ID buku yang diberi rating. Dikaitkan dengan books.csv untuk mendapatkan informasi buku
* Rating: Nilai rating yang diberikan pengguna terhadap buku. Ini adalah variabel target utama dalam sistem rekomendasi collaborative filtering

**Informasi mengenai dataset <br>**
users.csv
```
   <class 'pandas.core.frame.DataFrame'>
   RangeIndex: 278859 entries, 0 to 278858
   Data columns (total 2 columns):
    #   Column                  Non-Null Count    Dtype  
   ---  ------                  --------------    -----  
    0   User-ID                 278859  non-null  object 
    1   Soil_Type               168627  non-null  object 
   dtypes: object(2)
   memory usage: 4.3+ MB
```
books.csv
```
   <class 'pandas.core.frame.DataFrame'>
   RangeIndex: 271379 entries, 0 to 271378
   Data columns (total 5 columns):
    #   Column                  Non-Null Count    Dtype  
   ---  ------                  --------------    -----  
    0   ISBN                    271379  non-null  object 
    1   Title                   271379  non-null  object
    2   Author                  271377  non-null  object
    3   Year                    271379  non-null  int64
    4   Publisher               271377  non-null  object
   dtypes: int64(1), object(4)
   memory usage: 10.4+ MB
```
ratings.csv
```
   <class 'pandas.core.frame.DataFrame'>
   RangeIndex: 1149780 entries, 0 to 1149779
   Data columns (total 3 columns):
    #   Column                  Non-Null Count    Dtype  
   ---  ------                  --------------    -----  
    0   User-ID                 1149780 non-null  int64 
    1   ISBN                    1149780 non-null  object
    2   Rating                  1149780 non-null  int64
   dtypes: int64(2), object(1)
   memory usage: 26.3+ MB
```
**Jumlah missing value <br>**
user.csv
|                         | 0 |
|:------------------------|--:|
|User-ID                  |0.0|
|Age                      |39.5|

dtype:float64
<br>

books.csv
|                         | 0 |
|:------------------------|--:|
|ISBN                     |0.0|
|Title                    |0.0|
|Author                   |0.000737|
|Year                     |0.0|
|Publisher                |0.000737|

dtype:float64
<br>

ratings.csv
|                         | 0 |
|:------------------------|--:|
|User-ID                  |0.0|
|ISBN                     |0.0|
|Rating                   |0.0|

dtype:float64
<br>

**Jumlah duplicate<br>**
users.csv <br>
```np.int64(0)``` <br>
Artinya tidak ada data duplikat dari file <br>

books.csv <br>
```np.int64(1)``` <br>
Artinya ada satu data duplikat dari file <br>

ratings.csv <br>
```np.int64(0)``` <br>
Artinya tidak ada data duplikat dari file <br>

## 📋 Data Preparation
1. Menghapus Duplikat <br>
* Dataset yang dicek: user, book, dan rating.<br>
* Teknik: ```df.duplicated().sum()``` dan ```df.drop_duplicates()``` <br>
* Alasan: Duplikat dapat menyebabkan bias, terutama jika ada data rating yang sama berulang. Ini akan mengacaukan model dan evaluasi.

2. Menangani Missing Values
* Dataset yang dicek: user dan book.
* Teknik: ```df.isnull().mean() * 100``` → melihat persentase nilai kosong.
* Aksi: ```user['Age']``` diisi dengan median: ```user['Age'].fillna(user['Age'].median())```.
* book dihapus baris yang kosong: ```book.dropna(inplace=True)```.
* Alasan: Nilai kosong menyebabkan error saat pemrosesan dan model training. Median dipilih untuk mengisi Age karena robust terhadap outlier.

3. Menangani Outliers
* Kolom yang diperiksa: user['Age'], book['Year'], rating['Rating'].
* Teknik: Menggunakan IQR (Interquartile Range): <br>
```
Q1 = df_numeric.quantile(0.25)
Q3 = df_numeric.quantile(0.75)
IQR = Q3 - Q1
df = df[~((df_numeric < (Q1 - 1.5 * IQR)) | (df_numeric > (Q3 + 1.5 * IQR)))]
```  

* Alasan: Outlier dapat memengaruhi statistik dan membuat model tidak akurat (misal umur 200 tahun atau buku terbit tahun 0).
4. Filtering Data
* Aksi:
   - Filter umur yang masuk akal: hanya ambil usia 5–80 tahun.
   - Hapus rating yang tidak valid: rating > 0 saja.
* Alasan: Data ekstrem tidak merepresentasikan user realistik. Rating 0 bisa berarti tidak valid atau placeholder.

5. Pembersihan Teks (Nama Penulis)
* Teknik: Fungsi process_author_name() dengan regex (re.sub) digunakan untuk:
   - Menghapus titik dan mengatur spasi antar inisial.
   - Menangani apostrof (misal: "D'Angelo" jadi "D Angelo").
* Alasan: Konsistensi teks penting agar tidak ada duplikasi nama penulis karena format penulisan berbeda.

6. Membuat Fitur Gabungan (Untuk TF-IDF)
* Fitur baru: combined_features = Title + Author
* Alasan: Kombinasi judul dan penulis membantu dalam membuat representasi konten buku yang lebih lengkap untuk content-based filtering.

7. Encoding Kategori (User dan Buku)
* Teknik: LabelEncoder dari sklearn.
   - ```book_ratings['user_enc'] = LabelEncoder().fit_transform(User-ID)```
   - ```book_ratings['book_enc'] = LabelEncoder().fit_transform(Title)```
* Alasan: Untuk membuat indeks integer yang bisa digunakan dalam sparse matrix sebagai input ke model KNN.

8. Pembuatan Matriks Sparse
* Teknik: csr_matrix dari scipy.sparse.
* Format: Matriks (buku × user) dengan nilai = rating.
* Alasan: Matriks sparse hemat memori dan efisien untuk dataset besar, serta cocok untuk algoritma KNN.
  
##  🤖 Modelling
Dua pendekatan algoritmik yang digunakan untuk menyelesaikan masalah rekomendasi buku, yaitu:
1. **Content-Based Filtering (TF-IDF + Cosine Similiarity)**
   - Deskripsi <br>
     Model ini merekomendasikan buku berdasarkan kemiripan konten, khususnya kombinasi dari judul dan nama penulis. Teknik utama yang digunakan adalah:
        * TF-IDF Vectorizer: Mengubah teks (judul + penulis) menjadi representasi numerik.
        *  Cosine Similarity: Mengukur kemiripan antar vektor (buku) dalam ruang fitur.<br><br>

   - Top- N Output:
     ````
     Showing recommendations for book: Clara Callan
     ========================================
     Books with similar content (TF-IDF)
      ----------------------------------------
      Wildblossom
      Going Native
      Der Gesang des Troubadours.
      The Dollhouse Murders
      Globalhead
      What Am I Doing Here
      Distraction: A Novel
      The Real Mother Goose
      The SEARCH FOR SNOUT: BRUCE COVILLE'S ALIEN ADVENTURES : THE SEARCH         FOR SNOUT: BRUCE COVILLE'S ALIEN ADVENTURES
      One
      ```
   - Kelebihan
     * Tidak membutuhkan interaksi pengguna lain.
     * Rekomendasi bisa diberikan bahkan untuk pengguna baru (cold-start user).
     * Transparan: alasan rekomendasi jelas (karena konten mirip).
   - Kekurangan:
     * Tidak bisa menangkap selera kolektif (misalnya: buku populer).
     * Cenderung merekomendasikan item yang sangat mirip saja (kurang diversifikasi).
     <br>
     
2. Collaborative Filtering (KNN User-Based via Cosine Similarity)
   - Deskripsi
     Model ini merekomendasikan buku berdasarkan preferensi pengguna lain yang mirip, dengan pendekatan:.<br>
     * Label Encoding untuk membuat indeks pengguna dan buku.
     * Sparse Matrix (CSR): Representasi efisien dari data user-item.
     * KNN (K-Nearest Neighbors): Menemukan tetangga terdekat untuk setiap buku berdasarkan interaksi pengguna.<br>
   - Top-N Output:
     Contoh output untuk buku Clara Callan
     ```
     Top book recommendations from similar users (KNN)
     ----------------------------------------
     Women Talking Dirty
     Spanish Lessons : Beginning a New Life in Spain
     Algebra and Trigonometry, Unit Circle (6th Edition)
     The Dinosaur Project: The Story of the Greatest Dinosaur Hunt Ever Mounted
     The Best of Creative Computing
     The Biosphere.
     Fireworks 2 for Windows and Macintosh Visual Quickstart Guide
     Elementary Statistics
     Elementary Linear Algebra
     The Fractal Geometry of Nature
     ```
   - Kelebihan
     * Menangkap pola kolektif dari preferensi pengguna.
     * Bisa merekomendasikan buku yang tidak terlalu mirip tapi disukai user serupa.
    - Kekurangan:
       * Cold-start problem: Tidak bisa merekomendasikan untuk buku/user baru yang belum punya rating.
       * Butuh interaksi pengguna yang cukup banyak agar akurat.

## 📌 Evaluation
**Metrik evaluasi yang digunakan yaitu MSE** <br>
Mean Absolute Error (MSE) <br>
MAE mengukur rata-rata selisih absolut antara nilai rating yang diprediksi dan nilai aktual yang diberikan oleh pengguna. Semakin kecil nilai MAE, maka semakin akurat model dalam merepresentasikan preferensi pengguna. <br>
Rumus: <br>
MSE = (1/n) * Σ(yᵢ - ŷᵢ)

**Hasil Evaluasi Model**
``` Mean Absolute Error (MAE): 0.8171```

**Interpretasi Hasil berdasarkan problem statement**
1. Masalah 1: Bagaimana cara memberikan rekomendasi buku yang relevan bagi pengguna berdasarkan preferensi mereka, mengingat banyaknya pilihan buku yang tersedia di platform? <br>
Solusi:
Collaborative Filtering dengan pendekatan K-Nearest Neighbors (KNN) mampu mempelajari pola rating antar pengguna dan menyarankan buku yang disukai oleh pengguna lain yang memiliki preferensi serupa. <br>
Dampak:
Dengan MAE sebesar 0.8171, sistem mampu memberikan rekomendasi yang cukup akurat dan relevan, membantu pengguna menemukan buku favorit secara efisien. <br>

2. Masalah 2: Bagaimana cara mengatasi masalah "Information Overload" pada pengguna yang kesulitan memilih buku dengan banyaknya pilihan yang ada? <br>
Solusi : 
Model menyaring dan merekomendasikan Top-N buku dengan prediksi rating tertinggi berdasarkan preferensi pengguna yang mirip. <br>
Dampak : Pemilihan Random Forest sebagai model terbaik mendukung pencapaian target bisnis untuk meningkatkan akurasi prediksi, meminimalisir kerugian akibat prediksi yang tidak tepat.

3. Masalah 3:  Bagaimana sistem dapat mengidentifikasi buku yang serupa berdasarkan konten atau preferensi pengguna lain yang memiliki pola rating yang mirip? <br>
Solusi:
   * Content-Based Filtering: Menggunakan TF-IDF dari judul + penulis untuk mengukur kesamaan antar buku.
   * Collaborative Filtering: Mengandalkan pola rating pengguna lain yang mirip. <br> <br>
  Dampak:
Pengguna memperoleh rekomendasi dari dua sisi: kemiripan konten dan kesamaan selera pengguna, memperluas cakupan dan relevansi sistem.

# Laporan Proyek Machine Learning - Saila Julia

## Project Overview
Perkembangan teknologi digital telah memberikan dampak positif bagi industri pariwisata, terutama dengan semakin mudahnya akses informasi dan pilihan destinasi yang melimpah. Namun, banyaknya opsi yang tersedia justru dapat menyulitkan wisatawan dalam menentukan destinasi atau aktivitas yang sesuai dengan minat mereka. Dalam konteks ini, sistem rekomendasi perjalanan memainkan peran penting sebagai solusi untuk membantu pengguna menavigasi berbagai pilihan dan menemukan destinasi wisata yang paling relevan dengan preferensi mereka.

### Proyek ini penting karena 
1. Membantu wisatawan menemukan destinasi yang relevan
   - Sistem rekomendasi dapat menyarankan destinasi berdasarkan preferensi pengguna, Wisatawan tidak perlu mencari informasi dari banyak sumber sistem langsung memberikan opsi terbaik, dan Rekomendasi yang sesuai minat membuat pengalaman wisata lebih memuaskan.
2. Mendukung industri pariwisata
   - Tempat wisata yang kurang terkenal bisa terekspos lewat rekomendasi sistem, bukan hanya yang populer saja, Tempat wisata yang direkomendasikan dengan tepat cenderung mengalami peningkatan kunjungan
3. Pengambilan keputusan yang lebih baik
   - Wisatawan dapat membandingkan berbagai opsi berdasarkan rating, ulasan, dan fitur yang sesuai dan membantu dalam perencanaan perjalanan yang lebih terstruktur dan efektif.

### Hasil riset dan referensi 
Sistem rekomendasi mampu memberikan saran yang dipersonalisasi berdasarkan histori pengguna, rating, lokasi, dan atribut destinasi. Hal ini mendukung konsep smart tourism serta meningkatkan pengalaman pengguna sekaligus memperluas eksposur bagi destinasi-destinasi yang kurang populer.[ https://ieeexplore.ieee.org/document/1423975/footnotes#footnotes ]
"Adomavicius, G., & Tuzhilin, A. (2005). Toward the next generation of recommender systems: A survey of the state-of-the-art and possible extensions. IEEE Transactions on Knowledge and Data Engineering."

## Business Understanding
Dalam era digital saat ini, calon wisatawan memiliki akses ke berbagai informasi mengenai destinasi wisata. Meskipun hal ini memberikan keuntungan, banyaknya pilihan justru dapat menimbulkan kebingungan dalam menentukan tujuan yang sesuai. Beberapa permasalahan utama yang perlu dipecahkan dalam pengembangan sistem rekomendasi wisata adalah:
- Kurangnya Ketepatan Rekomendasi: Sistem rekomendasi sering kali belum mampu memahami minat spesifik pengguna, seperti preferensi terhadap jenis wisata (alam, budaya, atau buatan), lokasi yang diinginkan, hingga kisaran harga.
- Terlalu Banyak Alternatif: Pengguna dihadapkan pada banyaknya pilihan destinasi sehingga sulit memutuskan tujuan yang paling sesuai.
- Permasalahan Data Baru (Cold Start): Ketika sistem dihadapkan pada pengguna baru atau tempat wisata yang belum memiliki cukup data, performa rekomendasi menjadi kurang optimal.
- Keterbatasan Data Interaksi: Jumlah interaksi pengguna yang minim terhadap destinasi tertentu (seperti ulasan atau rating) menyebabkan sistem kesulitan dalam memberikan saran yang tepat.

### Problem Statements
- Bagaimana membangun sistem rekomendasi yang mampu menyarankan tempat wisata secara personal dan relevan bagi setiap pengguna?
- Bagaimana sistem dapat membantu pengguna dalam menyaring banyaknya pilihan destinasi secara efisien?
- Bagaimana strategi terbaik untuk menangani kondisi cold start dan minimnya data interaksi agar sistem tetap mampu memberikan saran yang bernilai?

### Goals
- Membangun sistem rekomendasi tempat wisata yang bersifat personal dan akurat, dengan memanfaatkan pendekatan berbasis konten maupun berbasis interaksi pengguna.
- Menyediakan rekomendasi top-N yang memudahkan pengguna dalam menjelajahi dan memilih tempat wisata yang sesuai dengan preferensinya.
- Mengatasi masalah cold start dan sparsity serta mengoptimalkan algoritma untuk meningkatkan performa sistem rekomendasi.

### Solution Apporch:
Untuk merealisasikan tujuan di atas, sistem rekomendasi akan dibangun dengan dua pendekatan utama berikut:

#### Content-Based Filtering dengan Cosine Similarity 
Metode pendekatan ini menyarankan destinasi wisata berdasarkan kemiripan fitur antara tempat wisata, seperti kategori, lokasi, dan nilai rata-rata ulasan.
- Ekstraksi Fitur
Mengidentifikasi atribut penting dari tiap destinasi.
- Vektorisasi Fitur
Mengubah atribut tersebut menjadi format numerik representasi berbasis TF-IDF).
- Penghitungan Kemiripan
Mengukur kedekatan antar destinasi menggunakan metode cosine similarity.
- Rekomendasi
Memberikan daftar rekomendasi berdasarkan kesamaan destinasi dengan yang pernah disukai pengguna.

####  Collaborative Filtering dengan Teknik Singular Value Decomposition (SVD)
Metode ini memanfaatkan perilaku pengguna lain untuk memberikan saran berdasarkan pola kesamaan dalam pemberian rating.
- Faktorisasi Matriks
Menguraikan matriks rating pengguna dan destinasi menggunakan SVD untuk mengungkap representasi laten.
- Estimasi Rating
Menghitung prediksi rating yang kemungkinan akan diberikan pengguna terhadap destinasi yang belum pernah dikunjungi.
- Rekomendasi 
Memberikan daftar tempat wisata dengan estimasi nilai tertinggi untuk setiap pengguna.

## Data Understanding
Dataset yang digunakan dalam proyek ini merupakan data dari kaggle Indonesia-Tourism-Destination. Dataset ini terdiri dari 3 komponen data yang diambil yaitu tourism dengan jumlah data 437 dengaan 13 kolom, data rating dengan jumlah 10000 dengan 3 kolom, dan data user dengan jumlah data 300 dengan 3 kolom. Dataset diambil dari [https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination].

1. Tourism Dataset
Dataset ini memuat informasi tempat wisata dengan total 437 baris dan 13 kolom. Terdapat satu kolom (Unnamed: 11) yang seluruhnya bernilai null dan merupakan kolom kosong yang tidak digunakan. Adapun kolom Time_Minutes memiliki banyak nilai kosong (sekitar 53%), sementara kolom lainnya lengkap tanpa nilai null. Tidak terdapat baris yang duplikat.
Berikut adalah kolom-kolom dalam Tourism Dataset:
- Place_Id : ID unik untuk tiap tempat wisata. Merupakan nilai unique ID yang berisi 437
- Place_Name : Nama tempat wisata. 
- Description : Deskripsi tempat wisata.
- Category : Jenis wisata (misalnya: alam, budaya, buatan).
- City : Lokasi kota dari tempat wisata.
- Price : Estimasi harga masuk tempat wisata.
- Rating : Nilai rating yang diberikan untuk tempat wisata.
- Time_Minutes : Estimasi waktu kunjungan dalam menit (hanya tersedia sebagian).
- Coordinate : Koordinat gabungan (string).
- Lat : Koordinat lintang tempat wisata.
- Long : Koordinat bujur tempat wisata.
- Unnamed: 11 : Kolom kosong (semua nilai null).
- Unnamed: 12 : Kolom tambahan berupa ID atau indikator lain (semua nilai terisi).

2. Ratings Dataset
Dataset ini berisi informasi interaksi berupa penilaian (rating) yang diberikan pengguna terhadap tempat wisata. Terdapat 10.000 baris dan 3 kolom, seluruh data tidak mengandung null dan memiliki 79 duplikat.
Berikut adalah kolom-kolom dalam Ratings Dataset:
- User_Id : ID unik pengguna yang memberikan rating.
- Place_Id : ID tempat wisata yang dinilai oleh pengguna.
- Place_Ratings : Nilai rating yang diberikan oleh pengguna terhadap tempat wisata.

3. Users Dataset
Dataset ini mencatat informasi pengguna yang memberikan rating. Terdapat 300 baris dan 3 kolom, tanpa nilai null maupun data duplikat.
Berikut adalah kolom-kolom dalam Users Dataset:
- User_Id : ID unik pengguna.
- Location : Lokasi tempat tinggal pengguna.
- Age : Usia pengguna.

## Data Preparation
Tahap data preparation bertujuan untuk membersihkan, mengubah, dan menyiapkan data agar dapat digunakan secara optimal dalam pemodelan sistem rekomendasi tempat wisata. Pada proyek ini, terdapat tiga sumber data utama yang digunakan, yaitu:
- tourisms: berisi informasi tentang tempat wisata, seperti name, category, city, dan description.
- rating: berisi data rating dari pengguna terhadap tempat wisata, dengan kolom User_Id, Place_Id, dan Place_Ratings.
- user: berisi informasi pengguna (tidak digunakan langsung dalam pemodelan, tetapi disiapkan untuk pengembangan lebih lanjut)

### General Data Preparation
- Pemeriksaan dan penghapusan nilai null
Data diperiksa untuk memastikan tidak terdapat nilai kosong (null) pada kolom-kolom penting seperti name, category, Place_Id, dan Place_Ratings.
- Pembersihan teks kategori
Kolom category dibersihkan dari karakter non-alfabet untuk memastikan konsistensi format, yang penting dalam analisis berbasis konten.
- Pembuatan kolom fitur gabungan
Kolom baru combined_features dibuat dengan menggabungkan name dan category sebagai representasi konten dari tempat wisata. Kolom ini akan digunakan dalam model content-based filtering

#### Data Preparation untuk Content-Based Filtering
Untuk mendukung sistem rekomendasi berbasis konten, beberapa langkah tambahan dilakukan
- Vektorisasi fitur teks menggunakan TF-IDF
Kolom combined_features diubah ke dalam bentuk numerik menggunakan metode TF-IDF (Term Frequency–Inverse Document Frequency), untuk menghitung bobot kata pada tiap tempat wisata..
- Perhitungan similarity antar destinasi
Menggunakan cosine similarity, sistem menghitung tingkat kemiripan antar tempat wisata berdasarkan nilai TF-IDF

### Data Preparation untuk Collaborative Filtering
- Membuat user-item matrix (pivot table)
Data rating diubah ke dalam format matriks pengguna vs tempat wisata, dengan nilai berupa rating yang diberikan. Nilai kosong diisi dengan nol untuk menandakan tempat yang belum dirating.
- Matrix factorization dengan SVD
Metode Truncated SVD (Singular Value Decomposition) digunakan untuk mendekomposisi matriks rating menjadi bentuk vektor yang lebih padat (dimensi lebih rendah), yang memungkinkan sistem mempelajari pola tersembunyi antara pengguna dan tempat wisata
- Membagi dataset menjadi data pelatihan dan pengujian
Pembagian data dilakukan untuk melatih model dan mengevaluasi performanya menggunakan data yang belum pernah dilihat oleh model.
pembagian data dilakukan menggunakan fungsi train_test_split dari sklearn.model_selection. Proses ini membagi data rating menjadi data pelatihan (train_data) dan data pengujian (test_data) dengan proporsi 80:20.

## Modeling
Pada tahap modeling, digunakan dua algoritma sistem rekomendasi yang berbeda, yaitu:
- Content-Based Filtering menggunakan Cosine Similarity
- Collaborative Filtering menggunakan Singular Value Decomposition (SVD)

### Content-Based Filtering
Pada metode content-based filtering, sistem merekomendasikan tempat wisata berdasarkan kesamaan kontennya dengan tempat yang telah disukai atau diberikan rating tinggi oleh pengguna. Informasi konten yang digunakan berasal dari atribut seperti name dan category dari tempat wisata.

#### Cara Kerja dan Parameter
Langkah-langkah yang dilakukan dalam proses content-based filtering pada sistem ini adalah sebagai berikut:
Alur Kerja Fungsi recommend_places
- Input Tempat Wisata
  - Pengguna memberikan nama tempat wisata Seperti "Air Mancur Menari" sebagai input.
- Pencarian Indeks
  - Sistem mencari indeks tempat wisata tersebut di dalam DataFrame tourisms untuk mengetahui posisinya dalam matriks fitur.
- Perhitungan Similarity
  - Cosine Similarity digunakan untuk menghitung tingkat kemiripan antara tempat wisata input dan seluruh tempat wisata lain berdasarkan fitur gabungan teks (combined_features). Fitur ini merupakan penggabungan 
    nama dan kategori tempat wisata, yang telah diubah menjadi representasi numerik menggunakan TF-IDF.
- Penyortiran Skor Kesamaan
  - Sistem mengurutkan semua tempat wisata berdasarkan skor kesamaan dengan tempat wisata input, dari yang paling mirip hingga yang paling tidak mirip.
- Pemilihan Top-N Rekomendasi
  - Tempat wisata yang sama dengan input akan diabaikan. Sistem akan menampilkan Top-N tempat wisata yang paling mirip berdasarkan nilai Cosine Similarity tertinggi.
- Output
  - Sistem mengembalikan informasi seperti name, category, city, dan description dari tempat wisata yang direkomendasikan.

#### Teknologi yang Digunakan
- TF-IDF Vectorization
Mengubah data teks gabungan (nama dan kategori) menjadi vektor numerik berdasarkan frekuensi kata dan pentingnya kata dalam dokumen.
- Cosine Similarity
Digunakan untuk menghitung kemiripan antar tempat wisata. Nilainya berkisar antara 0 hingga 1, di mana nilai mendekati 1 menunjukkan kemiripan yang tinggi antar tempat.

#### Rekomendasi
Setelah proses perhitungan kesamaan dilakukan, sistem menyajikan rekomendasi tempat wisata yang memiliki karakteristik paling mirip dengan input pengguna. Rekomendasi berbasis content-based filtering untuk input seperti "Trans Studio Bandung", dan "Air Mancur Menari":

### Collaborative Filtering
Model collaborative filtering dalam proyek ini dilatih menggunakan data rating pengguna terhadap tempat wisata. Model mempelajari pola preferensi dengan menguraikan matriks rating menjadi sejumlah faktor laten yaitu fitur tersembunyi yang merepresentasikan hubungan antara pengguna dan destinasi wisata.

#### Cara Kerja
Langkah-langkah dalam membangun dan menjalankan sistem rekomendasi collaborative filtering ini adalah:
#### Alur Kerja Sistem Rekomendasi
Pembuatan User-Item Matrix
Dibentuk pivot table dari data rating dengan baris berupa User_Id, kolom berupa Place_Id, dan nilai berupa Place_Ratings.
- Matriks ini kemudian digunakan untuk membentuk representasi preferensi pengguna terhadap tempat wisata.
Pemodelan dengan SVD (Singular Value Decomposition)
- Algoritma SVD digunakan untuk mendekomposisi matriks user-item menjadi komponen laten.
- Hasil dekomposisi menghasilkan matriks fitur pengguna dan fitur tempat wisata dalam bentuk vektor berdimensi lebih rendah.
- Ini memungkinkan model mengenali pola tersembunyi seperti jenis tempat yang disukai oleh kelompok pengguna tertentu.
Prediksi Rating
- Setelah pelatihan model selesai, dilakukan rekonstruksi matriks prediksi (pred_matrix) dari hasil dot product antara fitur pengguna dan fitur destinasi.
- Prediksi ini berisi nilai rating estimasi dari setiap pengguna untuk tempat wisata yang belum mereka rating sebelumnya.
Fungsi get_recommendations
- Fungsi ini menerima User_Id, DataFrame tourisms, serta rating_matrix dan pred_matrix sebagai input.
- Sistem mengidentifikasi tempat wisata yang belum pernah dirating oleh pengguna, lalu mengambil prediksi skor tertinggi dari tempat-tempat tersebut.
- Tempat wisata dengan skor prediksi tertinggi dipilih sebagai rekomendasi.
 Output
- Fungsi mengembalikan nama, kategori, kota, dan deskripsi dari tempat wisata yang direkomendasikan untuk pengguna tertentu.

### Teknologi yang Digunakan
- TruncatedSVD (Singular Value Decomposition)
Digunakan untuk memproyeksikan matriks sparse (user-item) ke dalam ruang dimensi yang lebih rendah. Algoritma efisien untuk model yang dianalisa
- Dot Product Reconstruction
Digunakan untuk mengalikan hasil matriks pengguna dan tempat wisata kembali menjadi prediksi rating.

### Rekomendasi Top-N Tempat Wisata
Rekomendasi dilakukan menggunakan ID 22, ID 67, ID 1

### Kelebihan dan Kekurangan

#### Content-Based Filtering
Kelebihan:
- Pendekatan ini merekomendasikan tempat wisata berdasarkan kemiripan kontennya, seperti nama dan kategori. Sistem membandingkan fitur dari tempat yang disukai pengguna dengan tempat lainnya menggunakan algoritma Cosine Similarity.
- Cocok untuk pengguna baru yang belum memiliki banyak riwayat interaksi, karena hanya mengandalkan informasi dari konten tempat wisata itu sendiri.
- Hasil rekomendasi lebih relevan secara personal karena berdasarkan preferensi sebelumnya.

Kekurangan:
- Rekomendasi cenderung terbatas hanya pada tempat wisata yang mirip dengan yang sudah disukai, sehingga kurang bervariasi.
- Tempat baru yang belum punya cukup informasi bisa sulit untuk direkomendasikan.
- Sistem tidak mengenali selera pengguna di luar pola yang sudah ada, sehingga kurang adaptif pada perubahan minat.

#### Collaborative Filtering
Kelebihan:
- Menggunakan data rating dari banyak pengguna untuk mengenali pola preferensi tersembunyi. Dengan metode SVD, sistem dapat memprediksi tempat wisata yang disukai meskipun belum pernah dikunjungi.
- Tidak perlu informasi konten dari tempat wisata; cukup berdasarkan perilaku pengguna lain.
- Dapat menghasilkan rekomendasi yang lebih beragam karena mempertimbangkan pengalaman kolektif pengguna lain.

Kekurangan:
- Tidak efektif untuk pengguna baru yang belum memberi rating (cold start).
- Jika sebagian besar tempat belum dirating, sistem kesulitan memberikan rekomendasi yang tepat (sparse matrix).
-  Proses training dan prediksi lebih berat secara komputasi dibanding content-based.

Kesimpulan:
Kedua pendekatan memiliki keunggulan dan keterbatasan masing-masing. Dengan menggabungkan content-based dan collaborative filtering, sistem rekomendasi dapat saling melengkapi dan memberikan hasil yang lebih optimal.

## Evaluation
### Content-Based Filtering
#### Metrik Evaluasi
Evaluasi pada metode content-based menggunakan dua metrik utama:
1. Precision\@K
   Mengukur seberapa banyak dari K tempat wisata teratas yang direkomendasikan benar-benar mirip (relevan) dengan input pengguna.
2. Recall\@K
   Mengukur seberapa banyak tempat yang mirip (relevan) berhasil ditemukan dari keseluruhan tempat mirip yang tersedia.
Metrik ini digunakan karena dapat menilai kualitas relevansi dan cakupan dari rekomendasi berdasarkan kemiripan konten.

#### Hasil Evaluasi
Evaluasi dilakukan pada dua tempat wisata sebagai input:
1. Air Mancur Menari
- Precision\@5: **17.03%
- Recall\@5: 100.00%
Menunjukkan bahwa dari 5 rekomendasi teratas, hanya sebagian kecil yang benar-benar relevan, tetapi sistem berhasil menangkap semua tempat yang mirip dari daftar lengkap.
2. Trans Studio Bandung
- Precision\@5: 1.57%
- Recall\@5: 100.00%
Sistem berhasil mencakup semua tempat yang mirip, tetapi sebagian besar rekomendasi tidak cukup relevan di posisi teratas.
Hasil ini mengindikasikan bahwa cakupan sistem cukup baik (recall tinggi), namun tingkat ketepatan (precision) masih perlu ditingkatkan agar rekomendasi lebih fokus pada tempat yang paling relevan.

### Collaborative Filtering
#### Metrik Evaluasi
Evaluasi collaborative filtering dilakukan dengan dua metrik error prediktif:
1. RMSE (Root Mean Squared Error)
  Mengukur rata-rata kesalahan kuadrat antara rating prediksi dengan rating sebenarnya.
2. MAE (Mean Absolute Error)
  Mengukur rata-rata selisih absolut antara prediksi dan nilai rating asli.

#### Hasil Evaluasi
RMSE: 2.5964
MAE: 2.3106
Nilai RMSE dan MAE yang diperoleh masih tergolong tinggi, menunjukkan bahwa prediksi rating oleh model SVD belum sepenuhnya akurat. Hal ini bisa disebabkan oleh sebaran data rating yang masih terbatas atau sparsity yang tinggi pada dataset.

### Fungsi Rekomendasi
Pada collaborative filtering, fungsi `get_recommendations` digunakan untuk:
1. Menentukan daftar tempat wisata yang belum diberi rating oleh pengguna.
2. Menghitung prediksi rating terhadap tempat-tempat tersebut.
3. Mengurutkan dan menampilkan 10 tempat teratas berdasarkan prediksi.
Fungsi ini membantu sistem memberikan rekomendasi berbasis pola dari pengguna lain yang serupa.

### Kesimpulan
Sistem rekomendasi tempat wisata yang dikembangkan telah menggabungkan dua pendekatan:
- Content-Based Filtering(menggunakan Cosine Similarity):
  Memberikan rekomendasi berdasarkan kemiripan fitur tempat wisata, cocok untuk pengguna baru atau saat data interaksi masih terbatas.
- Collaborative Filtering** (menggunakan SVD):
  Mengandalkan data rating antar pengguna, cocok untuk mengenali pola preferensi yang kompleks.

Hasil evaluasi menunjukkan:
* Sistem content-based memiliki cakupan rekomendasi yang baik (recall tinggi), namun precision masih perlu ditingkatkan untuk meningkatkan relevansi rekomendasi teratas.
* Sistem collaborative filtering menghasilkan prediksi yang belum cukup presisi, namun berpotensi lebih baik jika data rating pengguna lebih lengkap.
* Kombinasi dua pendekatan ini dapat mengatasi berbagai tantangan, seperti cold start dan sparsity, sekaligus meningkatkan kualitas rekomendasi yang personal dan relevan bagi pengguna.

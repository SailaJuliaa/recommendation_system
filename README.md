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
Sistem rekomendasi mampu memberikan saran yang dipersonalisasi berdasarkan histori pengguna, rating, lokasi, dan atribut destinasi. Hal ini mendukung konsep smart tourism serta meningkatkan pengalaman pengguna sekaligus memperluas eksposur bagi destinasi-destinasi yang kurang populer [1]. Sistem rekomendasi juga telah menjadi komponen penting dalam mendukung keputusan wisatawan, terutama dalam konteks pariwisata cerdas (smart tourism). Dengan memanfaatkan pendekatan berbasis data dan algoritma machine learning, sistem ini mampu memberikan rekomendasi yang dipersonalisasi sesuai dengan karakteristik pengguna, seperti demografi, preferensi individu, hingga tingkat kepuasan pengguna terhadap destinasi yang pernah dikunjungi sebelumnya. Pendekatan ini tidak hanya meningkatkan relevansi hasil rekomendasi, tetapi juga mampu memperbaiki pengalaman wisata secara keseluruhan [2].

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
- tourisms: berisi informasi tentang tempat wisata, seperti name, category, city, dan description.
- rating: berisi data rating dari pengguna terhadap tempat wisata, dengan kolom User_Id, Place_Id, dan Place_Ratings.
- user: berisi informasi pengguna (tidak digunakan langsung dalam pemodelan, tetapi disiapkan untuk pengembangan lebih lanjut)

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

## Exploratory Data Analysis (EDA)
Exploratory Data Analysis (EDA) merupakan tahap penting dalam proses analisis data yang bertujuan untuk memahami karakteristik dan pola umum dari dataset yang digunakan. Pada tahap ini, dilakukan eksplorasi terhadap data pengguna, data tempat wisata, serta data rating yang diberikan oleh pengguna. Proses ini melibatkan visualisasi dan analisis statistik sederhana untuk mendapatkan gambaran awal mengenai distribusi data, keberagaman informasi, serta potensi masalah yang mungkin ada, seperti outlier atau ketidakseimbangan distribusi.

Dengan memahami struktur dan distribusi data melalui EDA, dapat diperoleh wawasan awal yang berguna dalam proses pemodelan sistem rekomendasi, baik berbasis konten (content-based filtering) maupun kolaboratif (collaborative filtering).

1. Melihat nilai unique pada dataframe tourism dan rating dengan :
- jumlah tempat wisata :437
- Jumlah user: 300
- Jumlah rating: 10000
- Jumlah kategori: 6
  
2. cek nilai unique category untuk mengetahui nama katergori pada kolom
- Budaya, Taman Hiburan, Cagar Alam, Bahari, Pusat Perbelanjaan, Tempat Ibadah
  
3. categoty count digunakan untuk menghitung jumlah masing-masing kategori wisata yang mungkin berada dalam satu kolom dengan hasil 
- Taman Hiburan 135
- Budaya 117
- Cagar Alam 106
- Bahari 47
- Tempat Ibadah 17
- Pusat Perbelanjaan 15
  
4. Distribusi Category
- Visualisasi dilakukan menggunakan barplot horizontal terhadap atribut Category dari data tempat wisata.
- Menghitung frekuensi jumlah tempat wisata per kategori.
Kesimpulan:
- Kategori Taman Hiburan, Budaya, dan Cagar Alam merupakan kategori tempat wisata yang paling banyak tersedia.
- Sementara kategori seperti Pusat Perbelanjaan dan Tempat Ibadah memiliki jumlah tempat wisata yang lebih sedikit.
Hal ini menunjukkan bahwa sistem rekomendasi kemungkinan akan lebih kaya dalam menyarankan destinasi dari tiga kategori utama tersebut.
![Distribusi category](https://github.com/user-attachments/assets/2bc8ed22-dfed-4886-8d70-dd8536af0ab6)

5. Distribusi Rating
- Visualisasi dilakukan menggunakan countplot untuk atribut Place_Ratings.
- Menghitung jumlah rating untuk setiap skor dari 1 hingga 5.
Kesimpulan:
- Distribusi rating cukup merata antara skor 2 sampai 5, dengan skor 1 sedikit lebih rendah.
- Skor 4 merupakan rating yang paling banyak diberikan.
Hal ini menunjukkan bahwa user cenderung memberikan penilaian positif terhadap tempat wisata, dan hanya sedikit yang memberikan skor rendah.
![Distribusi Rating](https://github.com/user-attachments/assets/c142e6d7-1758-427f-83c1-8ef1d5442e0b)

6. Distribusi Lokasi
- Visualisasi dilakukan menggunakan barplot horizontal terhadap atribut Location pada data user.
- Menghitung frekuensi user berdasarkan kota asal.
Kesimpulan:
- Kota dengan jumlah user terbanyak adalah Bekasi, diikuti oleh Semarang, Yogyakarta, dan Bogor.
- Beberapa kota seperti Madura, Nganjuk, dan Purwakarta memiliki jumlah pengguna yang sangat sedikit
- Ini menunjukkan bahwa pengguna banyak berasal dari kota besar atau wilayah dengan populasi padat di Pulau Jawa
- User tersebar dari berbagai kota di Indonesia, meskipun tidak merata.
Informasi ini penting untuk memahami konsentrasi geografis pengguna, yang bisa digunakan untuk rekomendasi lokal atau berbasis lokasi.
![Distribusi lokasi](https://github.com/user-attachments/assets/ffd4b56f-5b63-44c5-97d0-de2c1fd514cb)

7. Distribusi usia user
- Visualisasi menggunakan boxplot untuk menggambarkan sebaran usia user.
- Data yang digunakan berasal dari atribut Age pada data user.
Kesimpulan:
- Usia user mayoritas berada pada rentang 20 hingga 40 tahun.
- Median usia user adalah sekitar 29 tahun.
- Tidak terdapat outlier yang ekstrem pada distribusi usia, menunjukkan data relatif bersih.
Artinya, target pengguna aplikasi atau sistem rekomendasi ini cenderung berada pada usia produktif dan dewasa muda.
![Distrubusi umur user](https://github.com/user-attachments/assets/17ebd67c-45d2-4ae6-a3a4-4f236507fb4d)

8. Membuat worldcoud untuk category, nama tempat, lokasi, deskripsi dengan tujuannya untuk memahami distribusi dan frekuensi kata yang muncul dalam atribut-atribut penting yang digunakan untuk merekomendasikan tempat wisata
- WordCloud Category menggambarkan frekuensi kemunculan tiap kategori wisata dalam dataset. Kata-kata yang lebih besar menunjukkan kategori yang lebih sering muncul. Misalnya, kategori seperti "Taman Hiburan", "Cagar Alam", dan "Budaya" mendominasi, yang berarti jenis tempat wisata ini paling banyak terdapat di data. Informasi ini penting untuk mengetahui minat umum pengguna atau dominasi kategori tertentu dalam sistem rekomendasi.
![wordcloud category](https://github.com/user-attachments/assets/9563338f-5584-4b16-8e47-fc49a16afd6a)

- WordCloud lokasi menunjukkan distribusi geografis tempat wisata. Nama provinsi dan kota seperti "Jawa Barat", "DKI Jakarta", "Jawa Tengah", dan "Sumatera Selatan" muncul cukup besar, menandakan bahwa sebagian besar tempat wisata dalam dataset berada di daerah-daerah tersebut. Informasi ini bisa digunakan untuk mempersonalisasi rekomendasi berdasarkan lokasi geografis pengguna.
![wordcloud lokasi](https://github.com/user-attachments/assets/02e4e030-8abb-4e5f-9599-71bd61ff149a)

- WordCloud nama tempat menampilkan nama-nama umum atau kata kunci yang sering muncul dalam penamaan tempat wisata. Misalnya, kata "Museum", "Taman", "Pantai", dan "Kampung" adalah nama tempat yang sering muncul. Ini membantu memahami jenis tempat wisata yang populer dan bisa digunakan dalam analisis berbasis konten atau klasifikasi jenis wisata.
![wordcloud nama tempat](https://github.com/user-attachments/assets/e13bc8d1-bf36-45ff-942f-4ffc50d7a11c)

- WordCloud deskripsi ini dihasilkan dari teks deskripsi tempat wisata. Tujuannya untuk mengekstrak kata-kata yang paling sering muncul dalam deskripsi dan dapat menggambarkan ciri khas tempat tersebut. Kata-kata seperti "yang", "dan", "dengan", "terletak", serta nama objek seperti "Pantai", "Taman", dan "Museum" sering muncul, menunjukkan bahwa deskripsi sering menyebutkan lokasi geografis, jenis objek, serta fasilitas atau karakteristik unik. Hasil ini bisa digunakan untuk fitur berbasis konten dalam sistem rekomendasi.
![wordcloud deskripsi](https://github.com/user-attachments/assets/8203d45c-4f61-4d8c-9769-1240fd393512)

   
9. Tempat dengan Rata-Rata Rating Tertinggi (4.0)
Semua tempat berikut mendapatkan rating rata-rata 4.0, menunjukkan kepuasan tinggi dari pengunjung:
- Bukit Bintang Yogyakarta, Bukit Jamur, Wisata Agro Edukatif Istana Susu Cibugary, Bukit Moko, Museum Tekstil, Glamping Lakeside Rancabali, Kampung Cina, Teras Cikapundung BBWS, Sanghyang Heuleut, Pintoe Langit Dahromo
- Tempat-tempat ini cenderung memiliki daya tarik visual atau edukatif, serta kemungkinan besar menawarkan pengalaman positif dan memuaskan.
  
10. Tempat dengan Rata-Rata Rating Terendah (2.0)
Sebaliknya, tempat berikut mendapatkan rating terendah, yaitu 2.0, yang menandakan tingkat ketidakpuasan yang tinggi dari pengguna:
- Wot Batu, Brown Canyon, Taman Tabanas, Tebing Breksi, Taman Barunawati, Taman, Bungkul, Pasar Tanah Abang, Patung Sura dan Buaya, Pantai Sanglen, Pantai Sepanjang
- Rendahnya rating ini bisa disebabkan oleh kurangnya fasilitas, kebersihan, aksesibilitas, atau ekspektasi yang tidak terpenuhi.

11. Tempat yang Paling Banyak Diberi Rating
Berikut adalah tempat-tempat yang paling populer berdasarkan jumlah rating tertinggi:
- Pantai Parangtritis (39 rating), Gunung Lalakon (39 rating), Gereja Perawan, Maria Tak Berdosa Surabaya (38 rating), Pantai Kesirat (37 rating), Taman Sungai Mudal (36 rating), Geoforest Watu Payung Turunan (34 rating), Kampung Batu Malakasari (34 rating), Pantai Marina (33 rating), Food Junction Grand Pakuwon (33 rating), Wisata Kuliner Pecenongan (33 rating)

- Tempat-tempat ini menunjukkan tingkat kunjungan dan perhatian publik yang tinggi. Ini bisa dijadikan prioritas dalam pengembangan atau promosi pariwisata lebih lanjut.

## Data Preparation
Tahap data preparation bertujuan untuk membersihkan, mengubah, dan menyiapkan data agar dapat digunakan secara optimal dalam pemodelan sistem rekomendasi tempat wisata. Pada proyek ini, terdapat tiga sumber data utama yang digunakan, yaitu:
- Menggabungkan dataset tourism dan rating berdasarkan Place_Id.
- Menangani Missing Value
- Menghapus data duplikat dengan drop_duplicates().
- KOnversi Palce_Ratings dengan mengubah tipe data dan memastikan kolom price aman dengan nilai 0 dan cek apakah ada NaN akibat error
- Penanganan Price dengan Cek apakah 0 berarti gratis atau data tidak tersedia dan ditangani dengan median
- Menggabungkan Dataframe city dan category sebagai fitur tambahan CBF
- pembuatan list:
  1. Konversi kolom Place_Id menjadi list dan simpan sebagai place_id
  2. Ambil nilai dari kolom Place_Name dalam bentuk list
  3. Simpan kategori tempat wisata sebagai list
  4. Ubah deskripsi tempat wisata menjadi list
  5. Ekstrak data kota ke dalam list
- Menggabungkan semua dataframe yang sudah dibuat menjadi tourisms
- teks processing, membersihkan kolom deksripsi dengan mengubah lowercase, hilangkan angka, hilangkan tanda baca, hilangkan whitespace berlebih dan kolom deskripsi digabungkan ke dataframe tourisms
- Membuat dataframe tourisms_unique untuk tempat wisata dan Penghapusan Duplikat
   - Menghapus duplikasi tempat wisata berdasarkan nama dari dataframe tourisms menggunakan drop_duplicates dan mereset indeksnya, agar tidak muncul rekomendasi dari entitas yang sama.

## Modeling
Pada tahap modeling, digunakan dua algoritma sistem rekomendasi yang berbeda, yaitu:
- Content-Based Filtering menggunakan Cosine Similarity
- Collaborative Filtering menggunakan Singular Value Decomposition (SVD)

### Content-Based Filtering
Pada metode content-based filtering, sistem merekomendasikan tempat wisata berdasarkan kesamaan kontennya dengan tempat yang telah dipilih oleh pengguna. Informasi konten yang digunakan berasal dari atribut seperti kategori, deskripsi, dan kota dari tempat wisata.

#### Cara Kerja dan Parameter
Langkah-langkah yang dilakukan dalam proses content-based filtering pada sistem ini adalah sebagai berikut:
##### Alur Kerja Fungsi rekomendasi_wisata:
1. Penggabungan Fitur
- Atribut category, description, dan city digabungkan ke dalam satu kolom combined, untuk mewakili keseluruhan karakteristik tempat wisata.
2. Vektorisasi Teks
- Data `combined` diubah menjadi vektor numerik menggunakan `CountVectorizer` (dengan penghapusan stop words).
3. Perhitungan Similarity
- Matriks Cosine Similarity dihitung dari hasil vektorisasi untuk mengetahui tingkat kemiripan antar tempat wisata.
4. Pemilihan Top-N Rekomendasi
- Tempat wisata dengan skor kemiripan tertinggi (kecuali tempat input) diurutkan dan dipilih Top-N untuk ditampilkan.

#### Output
Sistem mengembalikan informasi `name`, `category`, `description`, dan `city` dari tempat wisata yang direkomendasikan.

#### Teknologi yang Digunakan
- CountVectorizer
  Mengubah teks gabungan menjadi vektor berdasarkan frekuensi kata (bag-of-words).
- Cosine Similarity
  Mengukur tingkat kemiripan antar vektor tempat wisata.

#### Rekomendasi
Sistem menyajikan rekomendasi tempat wisata yang memiliki karakteristik paling mirip dengan input pengguna. Contoh rekomendasi berhasil diberikan untuk:
- Trans Studio Bandung
  ![Trans Studio bandung](https://github.com/user-attachments/assets/631b2c11-a158-4ba8-b903-28ca46223216)

  
- Air Mancur Menari
 ![Air mancur menari](https://github.com/user-attachments/assets/fd675bcc-f212-4adb-8e0e-59c9292a4ae6)

  
- Pantai Marina
  ![Pantai marina](https://github.com/user-attachments/assets/dd24300f-9ac9-4f29-93d4-5133d4bf781a)


### Collaborative Filtering
Model collaborative filtering dalam proyek ini mempelajari pola rating pengguna terhadap tempat wisata menggunakan pendekatan matrix factorization. Sistem ini dapat merekomendasikan tempat wisata baru yang belum pernah dinilai oleh pengguna namun kemungkinan besar akan disukai.

#### Cara Kerja
##### Alur Kerja Sistem Rekomendasi:
1. Pembuatan User-Item Matrix
- Menggunakan pivot table, data rating diubah menjadi matriks pengguna-tempat, dengan pengguna sebagai baris dan tempat sebagai kolom. Nilai adalah rating yang diberikan.
2. Pemodelan dengan SVD
- Matriks rating didekomposisi menggunakan TruncatedSVD menjadi matriks pengguna dan tempat wisata berdimensi rendah (n\_components=20).
- Pendekatan ini memungkinkan identifikasi pola preferensi tersembunyi.
3. Prediksi Rating
- Setelah pembelajaran, matriks prediksi dibentuk dari hasil perkalian dot product antara representasi pengguna dan tempat wisata.
4. Fungsi `get_recommendations`
- Fungsi ini menerima `User_Id`, memeriksa tempat wisata yang belum dirating, lalu merekomendasikan tempat dengan prediksi skor tertinggi.

#### Output
- Rekomendasi diberikan dalam bentuk `name`, `category`, dan `city` dari tempat wisata yang belum pernah dirating tetapi kemungkinan besar relevan.

#### Teknologi yang Digunakan
- TruncatedSVD
  Digunakan untuk mengurangi dimensi data dan mempelajari fitur laten dari pengguna dan item.
- Dot Product Reconstruction
  Digunakan untuk merekonstruksi prediksi rating antara pengguna dan tempat wisata.

### Rekomendasi Top-N Tempat Wisata
Berikut adalah contoh hasil rekomendasi berdasarkan Collaborative Filtering:
- Untuk User ID 1
  ![CF id 1](https://github.com/user-attachments/assets/33523097-92d4-4e04-a5b2-cf3f8b64a7b0)

- Untuk User ID 2
  ![CF id 2](https://github.com/user-attachments/assets/e50c650f-13fb-4175-abf8-375b309d6380)

- Untuk User ID 3
  ![CF id 3](https://github.com/user-attachments/assets/6157d673-c1db-4336-839c-113395b8207f)


### Kelebihan dan Kekurangan

#### Content-Based Filtering
Kelebihan:
- Sistem ini merekomendasikan tempat wisata berdasarkan kemiripan konten dari atribut seperti kategori, deskripsi, dan kota tempat wisata. Proses ini dilakukan dengan menggabungkan fitur-fitur tersebut ke dalam satu kolom, kemudian dianalisis menggunakan CountVectorizer dan Cosine Similarity.
- Cocok digunakan untuk pengguna baru (cold-start user) yang belum memiliki riwayat interaksi atau rating, karena sistem hanya membutuhkan informasi dari tempat wisata itu sendiri.
- Rekomendasi yang dihasilkan lebih sesuai dengan minat pengguna karena berdasarkan konten yang mirip dengan tempat wisata yang telah dipilih sebelumnya.

Kekurangan:
- Rekomendasi yang dihasilkan cenderung terbatas pada tempat-tempat wisata yang mirip secara deskripsi atau kategori, sehingga kurang memberikan keberagaman.
- Tempat wisata baru yang belum memiliki deskripsi yang cukup atau kurang informatif akan sulit untuk direkomendasikan.
- Sistem ini tidak dapat memahami preferensi pengguna secara luas karena hanya fokus pada kesamaan konten, bukan perilaku pengguna lainnya.

#### Collaborative Filtering
Kelebihan:
- Menggunakan data rating dari banyak pengguna dan melakukan dekomposisi matriks menggunakan TruncatedSVD untuk menemukan pola tersembunyi dalam preferensi pengguna.
- Sistem ini dapat merekomendasikan tempat wisata yang belum pernah dikunjungi oleh pengguna, selama ada pola kesamaan dengan pengguna lain.
- Lebih fleksibel dan dapat memberikan rekomendasi yang lebih beragam, karena tidak bergantung pada konten tempat wisata tetapi pada perilaku kolektif pengguna

Kekurangan:
- Tidak efektif untuk pengguna baru yang belum memberikan rating (masalah cold-start), karena sistem membutuhkan data interaksi historis.
- Jika sebagian besar tempat wisata belum banyak dirating, sistem akan menghadapi masalah data sparsity dan kesulitan memberikan rekomendasi yang akurat.
- Komputasi untuk training dan prediksi memerlukan sumber daya yang lebih besar dibandingkan dengan metode content-based, terutama saat menggunakan matrix factorization.

Kesimpulan:
- Metode content-based filtering bekerja dengan baik untuk memberikan rekomendasi yang relevan dan personal berdasarkan konten dari tempat wisata. Sementara itu, collaborative filtering mampu mengenali preferensi pengguna secara lebih luas dan memberikan rekomendasi yang lebih bervariasi, dengan memanfaatkan data dari pengguna lain.
- Namun, kedua pendekatan ini memiliki keterbatasan masing-masing. Oleh karena itu, dalam praktiknya, penggabungan kedua metode ini (hybrid system) dapat menjadi solusi terbaik untuk mengoptimalkan hasil rekomendasi—mengatasi masalah cold-start dan sparsity sekaligus mempertahankan relevansi rekomendasi.

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
- Precision@5: 15.49%
- Recall@5: 100.00%
Sistem berhasil mengidentifikasi semua tempat wisata yang mirip dengan Air Mancur Menari (recall sempurna), meskipun hanya sebagian kecil dari rekomendasi teratas yang benar-benar relevan. Hal ini menunjukkan bahwa sistem memiliki cakupan yang baik, namun masih perlu perbaikan dalam menyaring hasil yang paling tepat di posisi teratas.
2. Trans Studio Bandung
- Precision@5: 8.16%
- Recall@5: 100.00%
Semua tempat wisata yang relevan berhasil teridentifikasi oleh sistem, tetapi proporsi rekomendasi yang benar-benar relevan masih rendah. Ini menandakan bahwa meskipun sistem memiliki jangkauan yang luas, kualitas hasil yang direkomendasikan pada posisi teratas masih bisa ditingkatkan
3. Pantai Marina
- Precision@5: 48.16%
- Recall@5: 100.00%
Rekomendasi untuk Pantai Marina menunjukkan hasil yang sangat baik, dengan tingkat ketepatan tinggi pada lima hasil teratas. Hal ini menunjukkan bahwa sistem mampu menempatkan tempat wisata yang relevan di posisi awal sekaligus mencakup seluruh tempat mirip yang tersedia, menjadikan kombinasi precision dan recall-nya sangat optimal.

### Collaborative Filtering
#### Metrik Evaluasi
Evaluasi collaborative filtering dilakukan dengan dua metrik error prediktif:
1.RMSE (Root Mean Squared Error)
Mengukur rata-rata kesalahan kuadrat antara rating prediksi dengan rating sebenarnya. Semakin kecil nilai RMSE, semakin baik akurasi prediksi model.
2. MAE (Mean Absolute Error)
Mengukur rata-rata selisih absolut antara prediksi dan nilai rating asli. MAE yang lebih rendah menunjukkan bahwa prediksi model semakin mendekati rating aktual pengguna.

#### Hasil Evaluasi
RMSE: 3.1634
MAE: 2.8359

Nilai RMSE dan MAE yang diperoleh masih tergolong tinggi, menunjukkan bahwa prediksi rating oleh model SVD belum sepenuhnya akurat. Hal ini kemungkinan disebabkan oleh keterbatasan data latih, sparsity yang tinggi pada matriks user-item, atau jumlah rating yang tidak seimbang antar pengguna dan tempat wisata.

### Fungsi Rekomendasi
Pada collaborative filtering, fungsi `get_recommendations` digunakan untuk:
1. Menentukan daftar tempat wisata yang belum diberi rating oleh pengguna.
2. Menghitung prediksi rating terhadap tempat-tempat tersebut menggunakan hasil dekomposisi matriks SVD.
3. Mengurutkan dan menampilkan 10 tempat teratas berdasarkan skor prediksi tertinggi.

Fungsi ini memungkinkan sistem memberikan rekomendasi berdasarkan pola dan kesamaan perilaku pengguna lain yang memiliki preferensi serupa
   
### Kesimpulan
Sistem rekomendasi tempat wisata yang dikembangkan menggabungkan dua pendekatan utama, yaitu Content-Based Filtering dan Collaborative Filtering, untuk menghasilkan rekomendasi yang lebih personal dan adaptif. Pendekatan Content-Based Filtering, yang menggunakan kemiripan fitur seperti kategori, deskripsi, dan lokasi tempat wisata melalui metode cosine similarity, terbukti efektif dalam memberikan rekomendasi bagi pengguna baru yang belum memiliki histori rating. Sementara itu, pendekatan Collaborative Filtering berbasis Singular Value Decomposition (SVD) mengandalkan data rating dari banyak pengguna untuk menangkap pola preferensi tersembunyi.

### Daftar Pustaka
[1] G. Adomavicius and A. Tuzhilin, "Toward the next generation of recommender systems: A survey of the state-of-the-art and possible extensions," IEEE Transactions on Knowledge and Data Engineering, vol. 17, no. 6, pp. 734–749, Jun. 2005. [Online]. Available: https://ieeexplore.ieee.org/document/1423975
Hasil evaluasi menunjukkan bahwa Content-Based Filtering mampu memberikan cakupan rekomendasi yang baik dengan nilai recall yang tinggi, meskipun nilai precision-nya masih perlu ditingkatkan agar rekomendasi menjadi lebih relevan. Di sisi lain, Collaborative Filtering menunjukkan performa prediksi yang belum optimal akibat keterbatasan jumlah interaksi pengguna, namun memiliki potensi besar untuk meningkat seiring bertambahnya data rating yang tersedia.
[2] D. Shrestha, T. Wenan, D. Shrestha, N. Rajkarnikar, and S.-R. Jeong, "Personalized Tourist Recommender System: A Data-Driven and Machine-Learning Approach," Computation, vol. 12, no. 3, p. 59, 2024. [Online]. Available: https://doi.org/10.3390/computation12030059

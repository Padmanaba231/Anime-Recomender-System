# Laporan Proyek Machine Learning - Putu Padmanaba
### Project Overview
Anime adalah kata yang diambil dari kata "Animasi" dan kini telah mendapatkan basis penggemar yang besar di seluruh dunia. Bisnis anime telah berkembang dengan sangat pesat dalam beberapa tahun terakhir, menghasilkan miliaran dolar setiap tahunnya[[1](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4121831)]. Baik anak muda maupun orang dewasa banyak yang menyukai animasi jepang ini. Anime sendiri tersedia dari berbagai macam genre. Mulai dari romance, fantasy, action, horror, komedi, dan masih banyak lainnya. Anime sendiri bisa diakses melalui beberapa _website_ dan aplikasi. Contohnya seperti _website_ Chrunchyroll atau Bilibili maupun pada aplikasi Netflix. Setiap harinya, _website_ dan aplikasi penyedia anime dibanjiri oleh banyak pengguna. Jika penyedia _website_ dan aplikasi tidak memiliki algoritma atau sistem yang baik dalam merekomendasikan anime, para pengguna tentunya akan mengalami kesulitan dan bingun ketika mengakses _website_ dan aplikasi tersebut. Jika ini dibiarkan, ditakutkan pengguna akan merasa kecewa kepada _website_ maupun penyedia anime dan akhirnya tidak akan menggunakan layanan tersebut lagi.
<br><br>
Sistem rekomendasi menggunakan _Machine Learning_ bisa menjadi solusi untuk masalah ini. Dengan meningkatnya volume informasi online, sistem rekomendasi telah menjadi strategi yang efektif untuk mengatasi kelebihan informasi[[2](https://dl.acm.org/doi/abs/10.1145/3285029)]. Sistem pemberi rekomendasi memberikan dukungan layanan yang dipersonalisasi kepada pengguna dengan mempelajari perilaku mereka sebelumnya dan memprediksi preferensi mereka saat ini terhadap produk tertentu[[3](https://link.springer.com/article/10.1007/s40747-020-00212-w)]. Dalam hal ini, sistem rekomendasi akan memberikan rekomendasi anime yang mungkin disukainya berdasarkan beberapa faktor, seperti kebiasanaan pengguna ataupun dengan cara mencari anime yang mirip yang telah ditonton oleh pengguna sebelumnya.
<br><br>
Pada proyek ini akan dibuat sistem rekomendasi untuk merekomendasikan anime yang sekiranya akan disukai atau cocok dengan pengguna. Pada proyek ini akan dilakukan 2 pendekatan sistem rekomendasi. Pendekatan pertama menggunakan metode _Content Based Filtering_ dimana fitur atau filter yang akan digunakan adalah filter genre dan _type_ dari anime. Pendekatan kedua menggunakan metode _Collaborative Filtering_ dimana filter yang dipakai adalah rating anime yang diberikan berdasarkan pengguna. Pada _Content Based Filtering_ kita akan menggunakan model _Cosine Similarity_ sedangkan pada _Collaborative Filtering_ kita akan menggunakan pendekatan _Deep Learning_.


# Business Understanding
### Problem Steatment
+ Bagaimana cara memproses data agar dapat dilatih dengan baik oleh model?
+ Model _Machine Learning_ apa yang cocok digunakan?
+ Bagaimana performa dari model _Machine Learning_ yang digunakan?

### Goals
+ Mengetahui cara memproses data agar dapat dilatih dengan baik oleh model
+ Mengetahui model _Machine Learning_ Yang cocok
+ Mengetahui performa dari model yang telah dipilih

### Solution Approach
+ Menerapkan beberapa metode dalam melakukan pemrosesan data seperti menghapus missing value , membagi dataset menjadi data latih dan data pengujian, serta melakukan reduksi terhadap fitur yang tidak terlalu berguna
+ Menggunakan dua metode pendekatan dalam sistem rekomendasi. Pendekatan pertama menggunakan metode _Content Based Filtering_ menggunakan model _Cosine Similarity_. Pendekatan kedua menggunakan metode _Collaborative Filtering_ menggunakan metode _Deep Learning_


# Data Understanding
Pada proyek ini menggunakan 2 _dataset_, yaitu dataset anime.csv dan rating.csv yang dapat diunduh di: [anime recomendation database](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)
Informasi dataset:
+ anime.csv
  + Memiliki 7 fitur dengan 12294 sample
  + Memiliki 3 fitur numerik dan memiliki 4 fitur obyek
  + Terdapat _missing value_ pada data
+ rating.csv
  + Memiliki 3 fitur
  + Semua fitur bertipe numerik
  + Terdapat _missing value_ berupa nilai -1 pada fitur rating

### Variable pada _dataset_
+ __anime.csv__:
  + anime_id - id unik myanimelist.net yang mengidentifikasi sebuah anime.
  + name - nama lengkap anime.
  + genre - daftar genre yang dipisahkan koma untuk anime ini.
  + type - jenis anime apakah film, TV, OVA, dll.
  + episode - berapa banyak episode dalam acara ini. (1 jika film).
  + rating - rating rata-rata dari 10 untuk anime ini.(1-10)
  + member - jumlah anggota komunitas yang ada di anime ini
<br><br>
+ __rating.csv__:
  + anime_id - id unik myanimelist.net yang mengidentifikasi sebuah anime.
  + user_id - id pengguna yang dihasilkan secara acak dan tidak dapat diidentifikasi.
  + rating - rating dari 10 yang ditetapkan pengguna ini (-1 jika pengguna menontonnya tetapi tidak memberikan peringkat).(1-10)

### Exploratory Data Analys
#### _Missing value_
Terdapat _missing value_ pada kedua _dataset_. Pada _dataset_ anime.csv terdapat _missing value_ sebanyak 62 pada fitur genre, 25 pada fitur type, 230 pada fitur rating. Sementara untuk _dataset_ rating.csv memiliki _missing value_ sebanyak 1476496 pada fitur rating. Agar model dapat bekerja dengan baik, _missing value_ harus diatasi. _Missing value_ ini akan dieliminasi pada tahap data preparation
#### Persebaran Data
##### _Dataset_ anime.csv
![Screenshot 2024-03-06 195524](https://github.com/Padmanaba231/Anime-Recomender-System/assets/157343566/be19311f-5704-49a0-acda-7d57cd046c40)
<br>
Gambar 1 Persebaran fitur type
<br><br>
![Screenshot 2024-03-06 195538](https://github.com/Padmanaba231/Anime-Recomender-System/assets/157343566/43dc6379-723f-47ac-b6e4-a1e66e54c1c6)
<br>
Gambar 2 Persebaran fitur rating
<br><br>
Pada _dataset_ anime.csv bisa dilihat persebaran data dari fitur type dan fitur rating. Pada gambar 1 bisa dilihat bahwa tipe anime TV memiliki jumlah terbanyak yang disusul oleh tipe OVA dan juga Movie. Hal ini menunjukan kebanyakan anime bertipe TV series. Lalu pada gambar 2 bisa dilihat persebaran dari rating anime. Bisa dilihat persebaran rating berkisaran dari 1 hingga 10. Jika dicek kembali dari deskripsi fitur ratung, dikatan fitur rating memiliki rentang 1 hingga 10. Pada gambar 2 terlihat data tidak memiliki outlier atau nilai rating di luar rentang 1 hingga 10.
<br>
##### _Dataset_ rating.csv
![Screenshot 2024-03-06 195643](https://github.com/Padmanaba231/Anime-Recomender-System/assets/157343566/41a9961c-e569-4833-82e9-e7e2686e8660)
<br>
Gambar 3 Persebaran fitur rating
<br><br>
Gambar 3 merupakan persebaran rating yang diberikan pengguna kepada suatu anime. Bisa dilihat bahwa kebanyakan pengguna memberikan rating 8 ke suatu anime. Selain itu jika diperhatikan lebih baik, terdapat nilai rating -1 yang memiliki nilai terbanyak ke dua dari gambar. Rating -1 menandakan pengguna tidak memberikan rating kepada anime tersebut. Kasus ini bisa dianggap sebagai _missing value_ yang nantinya akan diatasi pada data preparation.


# Data Preparation
#### Mengatasi missing value
Seperti yang sudah dijelaskan sebelumnya pada bagian data understanding, _dataset_ memiliki beberapa _missing value_. _Missing value_ ini harus dieliminasi sehingga model dapat bekerja dengan baik. Karena jumlah dataset terbilang banyak(anime.csv memiliki 12294 data, rating.csv memiliki 7813737 data), jadi ketika mendrop _missing value_ _dataset_ masih memiliki cukup banyak informasi untuk diproses oleh model. Pada _dataset_ anime.csv _missing value_ akan dieliminasi menggunakan fungsi dropna. Sedangkan pada _dataset_ rating.csv, data yang memiliki nilai -1 pada kolom/fitur rating akan dieliminasi.
#### Reduksi fitur
Pada _dataset_ anime.csv terdapat beberapa fitur yang kurang relevant atau kurang berguna. Oleh karena itu, fitur-fitur tersebut akan dieliminasi. Fitur episodes dieliminasi karena kurang penting dalam keputusan pengguna dalam menentukan pilihan anime yang akan ditonton. Fitur anime_id dan members dieliminasi karena tidak diperlukan saat proses pembentukan model _content based filtering_. 
#### Encode user_id dan anime_id 
Pada tahap ini dilakukan encode untuk menyandikan user_id dan anime_id ke dalam indeks integer. Tahapan ini diperlukan karena kedua data tersebut berisi integer yang tidak berurutan (acak). Untuk itu perlu diubah ke dalam bentuk indeks.
#### Membagi data menjadi data latih dan data validasi
Data dibagi menjadi 2, yaitu data yang akan digunakan untuk melatih model (sebesar 80%) dan data untuk memvalidasi model (sebesar 20%). Tujuan dari membagi data ini adalah untuk proses pelatihan model serta mengukur kinerja model.

# Modeling and Result
## Content Based Filtering
Pada bagian _Content Based Filtering_ model yang digunakan pada proyek ini adalah metode Cosine Similarity. Cosine similarity akan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Cosine Similarity akan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. Rumus dari Cosine Similarity adalah sebagai berikut:
<br>
$$Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||)$$ 
<br>
Keterangan:
+ (A·B)menyatakan produk titik dari vektor A dan B.
+ ||A|| mewakili norma Euclidean (magnitudo) dari vektor A.
+ ||B|| mewakili norma Euclidean (magnitudo) dari vektor B.

Setelah membangun model, model perlu diuji terlebih dahulu. Pada proyek ini dibuat model _Content Based Filtering_ menggunakan 2 filter, yaitu genre dan type. Berikut merupakan hasil rekomendasi top-5 berdasarkan fitur genre dan fitur type:
<br>
Melakukan pengujian fitur genre:
```
anime_recommendations('Charlotte')
```
<br> 
Hasil: 
<br><br>

|   | name                                | genre                               |
|---|-------------------------------------|-------------------------------------|
| 0 |         Charlotte: Tsuyoi Monotachi |                 School, Super Power |
| 1 | Baka to Test to Shoukanjuu: Matsuri |         Comedy, School, Super Power |
| 2 |                Kill la Kill Special | Action, Comedy, School, Super Power |
| 3 |                        Kill la Kill | Action, Comedy, School, Super Power |
| 4 |                               X-Men |          Action, Drama, Super Power |
<br>
Tabel 1 Hasil rekomendasi berdasarkan genre

<br><br>
Melakukan pengujian fitur type:
```
anime_recommendations2('Charlotte')
```
<br> 
Hasil:
<br><br>

|   | name                                             | type  |
|---|--------------------------------------------------|-------|
| 0 |                    Tantei Kageki Milky Holmes TD |    TV |
| 1 |                                        Red Baron |    TV |
| 2 | Sora wo Miageru Shoujo no Hitomi ni Utsuru Sekai |    TV |
| 3 |                                         Himegoto |    TV |
| 4 |                           SF Saiyuuki Starzinger |    TV |
<br> 
Tabel 2 Hasil rekomendasi berdasarkan type

<br><br>
Berdasarkan pengujian yang telah dilakukan, bila melihat pada tabel 1 dan tabel 2 ada beberapa hal yang bisa disimpulkan. Sebelumnya, anime yang akan direkomendasikan adalah anime dengan judul Charlotte yang memiliki type TV dan memiliki genre, yaitu Drama, School, Super Power. Pada tabel 1 dan 2 terlihat bahwa model memberikan anime sejenis dengan anime Charlotte berdasarkan fitur genre dan type. Pada tabel 1 bisa dilihat bahwa anime yang direkomendasikan model memiliki kemiripan pada genre. Sedangkan pada tabel 2 bisa dilihat bahwa semua anime yang direkomendasikan memiliki type yang sama terhadap anime Charlotte. Bisa disimpulkan bahwa model telah berhasil memberikan rekomendasi anime yang serupa dengan anime input.
#### Kelebihan
Kelebihan dari model Cosine Similarity adalah modelnya yang terbilang sederhana sehingga tidak memerlukan kompusitas yang tinggi dan waktu yang lama saat melatih model tersebut
#### Kekurangan
Karena hanya menggunakan arah vektor dan tidak menghitung besaran vektornya. Hal ini mungkin dapa mengakibatkan jika dua vektor memiliki panjang yang sangat berbeda, meskipun arahnya sama, nilai cosine similarity dapat menjadi tidak representatif. Hal ini dapat menyebabkan ketidakakuratan dalam perbandingan dan peringkat item.
<br><br>


## Collaborative Filtering
Pada _Collaborative Filtering_ akan dilakukan pendekatan dengan _deep learning_.  Model yang akan dipakai dalam _Collaborative Filtering_ adalah RecommenderNet. Model ini menghitung skor kecocokan antara pengguna dan anime melalui _dot product_, dan menambahkan bias per anime dan per pengguna. Skor kecocokan diskalakan ke interval [0, 1] melalui sigmoid. Selanjutnya dilakukan proses compile pada model dengan binary crossentropy sebagai loss function, adam sebagai optimizer, dan RMSE sebagai metrik dari model. Setelah model berhasil dibuat, saatnya untuk menguji model dalam menentukan rekomendasi anime. Pada proses ini, akan dipilih satu pemgguna secara acak lalu model akan memberikan rekomendasi anime yang cocok dengan pengguna tersebut.
<br>
![Screenshot 2024-03-07 234020](https://github.com/Padmanaba231/Anime-Recomender-System/assets/157343566/247fa519-aaf8-4d2c-888e-92cfc6f02027)
<br>
Gambar 4 Hasil rekomendasi _Collaborative Filtering_
<br><br>
Pada gambar 4 bisa dilihat hasil dari rekomendasi anime berdasarkan pengguna. Bisa dilihat beberapa kemiripan pada genre antara anime yang diberi rating tinggi oleh pengguna dengan anime yang diberikan oleh sistem rekomendasi. Hal ini menunjukan bahwa model sudah dapat bekerja dengan cukup baik dalam merekomendasikan anime kepada pengguna.
#### Kelebihan
Dalam sistem rekomendasi, deep learning dapat secara efektif menangkap preferensi pengguna yang kompleks dan nuansa dalam data perilaku mereka, seperti sejarah tontonan atau penilaian. Selain itu pada data yang besar Metode deep learning dapat memberikan tingkat akurasi yang tinggi dalam memprediksi preferensi pengguna.
#### Kekurangan
Sumber daya komputasi yang dibutuhkan untuk melatih model deep learning dapat menjadi mahal dan berat, dan hal ini dapat menjadi hambatan terutama untuk organisasi atau individu dengan anggaran terbatas. Karena komputasi yang berat, hal ini mengakibatkan model memerlukan waktu yang lama dalam melatih data.


# Evaluation
### Content Based Filtering
Pada _Content Based Filtering_ metrik evaluasi yang akan digunakan adalah _Precission_. _Precission_ adalah metrik yang digunakan untuk mengevaluasi kinerja model pengelompokan. Metrik ini menghitung rasio prediksi positif sejati terhadap jumlah total prediksi positif (positif sejati dan positif palsu).
$$Precision = {TP \over TP + FP}$$
Keterangan:
<br>
<strong>True Positive (TP)</strong>: Jumlah observasi positif yang benar-benar diprediksi sebagai positif oleh model.
<br>
<strong>False Positive (FP)</strong>: Model salah memberi label pada data kategori negatif sebagai positif.
<br>
<br>
Berdasarkan hasil ujicoba pada model Content Base Filtering menggunakan Filter Genre, dan Type didapat bahwa 5/5 hasil rekomendasi memiliki jenis Genre, dan Type yang serupa dengan anime yang sebelumnya ditonton oleh pengguna. Anime yang ditonton pengguna yaitu anime Charlotte memiliki genre Drama, School, Super Power dan type TV. Pada hasil prediksi, model berhasil memprediksi anime yang memiliki genre dan type yang serupa dengan anime Charlotte. Dengan demikian Top-5 Reccomender System yang dibangun memiliki presisi sebesar 5/5 = 100%

### Collaborative Filtering
Pada collaborative filtering, metrik evaluasi yang digunakan adalah RMSE(_root mean square error_). RMSE adalah ukuran yang sering digunakan untuk perbedaan antara nilai (nilai sampel atau populasi) yang diprediksi oleh model atau penduga dan nilai yang diamati. RMSE merupakan metode pengukuran yang mengevaluasi perbedaan antara nilai prediksi dari sebuah model dengan nilai yang diobservasi, dihitung sebagai akar kuadrat dari Mean Square Error. Keakuratan estimasi kesalahan pengukuran dapat dilihat dari nilai RMSE yang rendah.
<br><br>
![Screenshot 2024-03-08 000510](https://github.com/Padmanaba231/Anime-Recomender-System/assets/157343566/ddfb19cc-78be-4f87-9780-761b62de9db2)
<br>
Gambar 5 Hasil Metrik Evaluasi
<br><br>
Bila dilihat pada gambar 5, nilai error yang dimiliki pada model terbilang cukup rendah. Model memperoleh nilai error akhir sekitar 0.1509 pada data latih dan 0.2845 pada data evaluasi. Nilai tersebut cukup bagus untuk sistem rekomendasi. Hal ini dapat dibuktikan pada gambar 4. Pada gambar 4 bisa diperhatikan bahwa model telah berhasil merekomendasikan anime yang serupa dengan anime yang ditonton oleh pengguna. Anime yang direkomendasikan model memiliki genre yang serupa dengan anime yang diberi rating tinggi oleh pengguna. Dari sini dapat disimpulkan bahwa model bekerja dengan baik.

# Referensi 
[1] Jena, Abhipsa & Jaiswal, Arunima & Lal, Dakshita & Rao, Soumya & Ayubi, Afshan & Sachdeva, Nitin. (2022). Recommendation System For Anime Using Machine Learning Algorithms. 10.2139/ssrn.4121831.
[2] Zhang, Shuai & Yao, Lina & Sun, Aixin & Tay, Yi. (2019). Deep Learning Based Recommender System: A Survey and New Perspectives. 10.1145/3285029
[3] Zhang, Qian & Lu, Jie & Jin, Yaochu. (2021). Artificial intelligence in recommender systems. 10.1007/s40747-020-00212-w

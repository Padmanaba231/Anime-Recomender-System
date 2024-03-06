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
  + rating - rating rata-rata dari 10 untuk anime ini.
  + member - jumlah anggota komunitas yang ada di anime ini
<br><br>
+ __rating.csv__:
  + anime_id - id unik myanimelist.net yang mengidentifikasi sebuah anime.
  + user_id - id pengguna yang dihasilkan secara acak dan tidak dapat diidentifikasi.
  + rating - rating dari 10 yang ditetapkan pengguna ini (-1 jika pengguna menontonnya tetapi tidak memberikan peringkat).

### Exploratory Data Analys
#### _Missing value_
Terdapat _missing value_ pada kedua _dataset_. Pada _dataset_ anime.csv terdapat _missing value_ sebanyak 62 pada fitur genre, 25 pada fitur type, 230 pada fitur rating. Sementara untuk _dataset_ rating.csv memiliki _missing value_ sebanyak 1476496 pada fitur rating.

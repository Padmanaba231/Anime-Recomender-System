# Laporan Proyek Machine Learning - Putu Padmanaba
## Project Overview
Anime adalah kata yang diambil dari kata "Animasi" dan kini telah mendapatkan basis penggemar yang besar di seluruh dunia. Bisnis anime telah berkembang dengan sangat pesat dalam beberapa tahun terakhir, menghasilkan miliaran dolar setiap tahunnya[[1](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4121831)]. Baik anak muda maupun orang dewasa banyak yang menyukai animasi jepang ini. Anime sendiri tersedia dari berbagai macam genre. Mulai dari romance, fantasy, action, horror, komedi, dan masih banyak lainnya. Anime sendiri bisa diakses melalui beberapa _website_ dan aplikasi. Contohnya seperti _website_ Chrunchyroll atau Bilibili maupun pada aplikasi Netflix. Setiap harinya, _website_ dan aplikasi penyedia anime dibanjiri oleh banyak pengguna. Jika penyedia _website_ dan aplikasi tidak memiliki algoritma atau sistem yang baik dalam merekomendasikan anime, para pengguna tentunya akan mengalami kesulitan dan bingun ketika mengakses _website_ dan aplikasi tersebut. Jika ini dibiarkan, ditakutkan pengguna akan merasa kecewa kepada _website_ maupun penyedia anime dan akhirnya tidak akan menggunakan layanan tersebut lagi.
<br><br>
Sistem rekomendasi menggunakan _Machine Learning_ bisa menjadi solusi untuk masalah ini. Dengan meningkatnya volume informasi online, sistem rekomendasi telah menjadi strategi yang efektif untuk mengatasi kelebihan informasi[[2](https://dl.acm.org/doi/abs/10.1145/3285029)]. Sistem pemberi rekomendasi memberikan dukungan layanan yang dipersonalisasi kepada pengguna dengan mempelajari perilaku mereka sebelumnya dan memprediksi preferensi mereka saat ini terhadap produk tertentu[[3](https://link.springer.com/article/10.1007/s40747-020-00212-w)]. Dalam hal ini, sistem rekomendasi akan memberikan rekomendasi anime yang mungkin disukainya berdasarkan beberapa faktor, seperti kebiasanaan pengguna ataupun dengan cara mencari anime yang mirip yang telah ditonton oleh pengguna sebelumnya.
<br><br>
Pada proyek ini akan dibuat sistem rekomendasi untuk merekomendasikan anime yang sekiranya akan disukai atau cocok dengan pengguna. Pada proyek ini akan dilakukan 2 pendekatan sistem rekomendasi. Pendekatan pertama menggunakan metode _Content Based Filtering_ dimana fitur atau filter yang akan digunakan adalah filter genre dan _type_ dari anime. Pendekatan kedua menggunakan metode _Collaborative Filtering_ dimana filter yang dipakai adalah rating anime yang diberikan berdasarkan pengguna. Pada _Content Based Filtering_ kita akan menggunakan model _Cosine Similarity_ sedangkan pada _Collaborative Filtering_ kita akan menggunakan pendekatan _Deep Learning_.


# Business Understanding
## Problem Steatment
+ Bagaimana cara memproses data agar dapat dilatih dengan baik oleh model?
+ Model _Machine Learning_ apa yang cocok digunakan?
+ Bagaimana performa dari model _Machine Learning_ yang digunakan?

## Goals
+ Mengetahui cara memproses data agar dapat dilatih dengan baik oleh model
+ Mengetahui model _Machine Learning_ Yang cocok
+ Mengetahui performa dari model yang telah dipilih

## Solution Approach

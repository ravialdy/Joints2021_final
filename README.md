# (Final Lomba Joints 2021 UGM) : Model Random Forest dalam memprediksi jenis pelanggan yang tepat untuk perusahaan “J Taxi”  
### Model kelompok saya berhasil memperoleh akurasi sekitar 76% (3rd rank on Private Leaderboard Kaggle) pada lomba Data Mining tingkat nasional yang diselenggarakan oleh HIMAKOM UGM.
#### Link Kaggle : https://www.kaggle.com/c/final-data-mining-competition-joints-2021/leaderboard

### Latar Belakang
* Terdapat suatu perusahaan taksi online yang telah beroperasi selama setahun, yakni “J Taxi”.
* Perusahaan ingin memberikan rekomendasi yang tepat mengenai jenis pelayanan taksi kepada pelanggan berdasarkan data yang dimiliki.
* Ingin dibuat suatu model Machine Learning yang dapat memprediksi 3 jenis target pelanggan.
* Model akan digunakan untuk memudahkan "J Taxi" dalam mencocokkan taksi apa yang tepat kepada pelanggan.

### Deskripsi Data
* ID - ID dari setiap trip
* Jarak_Perjalanan - Jarak perjalanan yang diminta oleh pelanggan
* Tipe_Kendaraan - Kategori taksi yang diminta oleh pelanggan
* Pelanggan_Sejak_Bulan - Lama pelanggan menggunakan layanan dalam bulan; 0 bulan berarti bulan ini
* Indeks_Gaya_Hidup - Indeks kepemilikan yang dibuat oleh J Taxi yang menunjukkan gaya hidup pelanggan berdasarkan perilaku mereka
* Tipe_Tujuan - Tempat tujuan dari J Taxi (terbagi atas 14 kategori)
* Rating_Pelanggan - Rata-rata peringkat yang diberikan pelanggan hingga saat ini
* Pembatalan_Sebulan_Terakhir - Jumlah perjalanan yang dibatalkan oleh pelanggan dalam 1 bulan terakhir
* Encode_1, Encode_2, Encode_3 - Variabel kontinu yang ditutupi oleh perusahaan
* Gender - Jenis kelamin pelanggan
* Target - Target (terdapat 3 jenis)

### Data Preparation: Informasi dan Tipe Data
* Pada data training terdapat 98749 observasi dan 13 kolom.
* Dari hasil tersebut, terdapat beberapa tipe data yang kurang tepat.
     * Fitur *Pembatalan_Sebulan_Terakhir* seharusnya float64 (numerik).
     * Fitur *Target* seharusnya data kategorik.
* Masih terdapat banyak missing values pada data.

### Koreksi Tipe Data yang Kurang Tepat
* Data pada fitur *Target* diubah menjadi kategori.
* Data pada fitur *Pembatalan_Sebulan_Terakhir* diubah menjadi data numerik.
* Variabel lainnya yang memiliki tipe data object diubah menjadi tipe data kategori.




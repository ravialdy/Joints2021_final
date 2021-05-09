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

### Data Overview

![image](https://user-images.githubusercontent.com/68768305/117524871-ca3a6f00-afe9-11eb-860e-c5d8646a8515.png)

### Data Preparation: Informasi dan Tipe Data

![image](https://user-images.githubusercontent.com/68768305/117524916-02da4880-afea-11eb-8fdd-c58142bb1a28.png)

* Pada data training terdapat 98749 observasi dan 13 kolom.
* Dari hasil tersebut, terdapat beberapa tipe data yang kurang tepat.
     * Fitur *Pembatalan_Sebulan_Terakhir* seharusnya float64 (numerik).
     * Fitur *Target* seharusnya data kategorik.
* Masih terdapat banyak missing values pada data.

### Koreksi Tipe Data yang Kurang Tepat

![image](https://user-images.githubusercontent.com/68768305/117524947-35844100-afea-11eb-92ff-fdfaf7bd6e54.png)

* Data pada fitur *Target* diubah menjadi kategori.
* Data pada fitur *Pembatalan_Sebulan_Terakhir* diubah menjadi data numerik.
* Variabel lainnya yang memiliki tipe data object diubah menjadi tipe data kategori.

### Statistik Deskriptif

![image](https://user-images.githubusercontent.com/68768305/117524793-497b7300-afe9-11eb-8229-9ac19db1ac4c.png)

![image](https://user-images.githubusercontent.com/68768305/117525055-cc50fd80-afea-11eb-99b3-330e05f3ae6e.png)

* Hanya terdapat 2 nilai pada fitur Gender dengan modus adalah Pria dengan 60470 observasi. 
* Sedangkan untuk fitur *Tipe_Kendaraan*, terdapat 10 nilai berbeda dengan modus “B” sebanyak 19870, dan modus fitur *Tipe_Tujuan* adalah “A” sebanyak 44359 observasi.

### Visualisasi fitur *Target*

![image](https://user-images.githubusercontent.com/68768305/117526935-636d8380-aff2-11eb-81a8-5e3cfc9d79df.png)

#### Insight yang didapatkan :

* Persentase jumlah pelanggan yang paling besar adalah jenis pelanggan ke-2, lalu diikuti jenis pelanggan ke-3, dan yang paling sedikit adalah jenis pelanggan ke-1.

### Visualisasi fitur *Jarak_Perjalanan*

![image](https://user-images.githubusercontent.com/68768305/117527012-e55dac80-aff2-11eb-921a-ffd024ed05f8.png)

* Kebanyakan pelanggan meminta jarak perjalanan antara 5-60.
* Jenis pelanggan ke-3 cenderung meminta jarak perjalanan yang cukup jauh (> 60).
* Jenis pelanggan ke-1 dan 2 cenderung memilih jarak perjalanan yang dekat (<60).

### Visualisasi fitur *Pembatalan_Sebulan_Terakhir*

![image](https://user-images.githubusercontent.com/68768305/117527035-13db8780-aff3-11eb-9f8d-38245943f2a5.png)

* Kebanyakan pelanggan tidak pernah membatalkan atau sekali membatalkan jumlah perjalanan dalam sebulan terakhir.
* Banyaknya pelanggan yang membatalkan jumlah perjalanan lebih dari 4x relatif sedikit.
* Jenis pelanggan ke-3 cenderung sedikit yang tidak membatalkan jumlah perjalanan, sedangkan cenderung mendominasi ketika ada pembatalan minimal sekali dalam sebulan terakhir.

### Visualisasi fitur *Gender*
![image](https://user-images.githubusercontent.com/68768305/117527065-58ffb980-aff3-11eb-9a6f-97481594955f.png)

* Kebanyakan pelanggan dari perusahaan “J Taxi” memiliki jenis kelamin pria.
* Baik pada jenis pelanggan ke-1, ke-2, maupun ke-3, pria cenderung jauh lebih banyak dibanding wanita.

### Visualisasi fitur *Tipe_Kendaraan*
![image](https://user-images.githubusercontent.com/68768305/117527110-a845ea00-aff3-11eb-9606-17e1dbd9ceb8.png)

* Secara umum, persentase jumlah pelanggan “J Taxi” yang paling besar adalah mereka yang memiliki tipe kendaraan B, lalu C, hingga yang paling kecil adalah tipe kendaraan e.
* Di kalangan jenis pelanggan ke-1, tipe kendaraan yang paling banyak adalah A, jenis pelanggan ke-2 didominasi tipe kendaraan B dan C, sedangkan jenis pelanggan ke-3 lebih banyak tipe kendaraan D.

### Imputasi Data Kategorik

#### Fitur *Gender* 

   * Variabel *gender* diimputasi menggunakan modus karena gender pria mendominasi pada fitur ini.

#### Fitur *Tipe_Kendaraan* 

   * Variabel ini diimputasi menggunakan modus tipe kendaraan pada setiap kategori Target. 
   * Jika target = 1 maka tipe kendaraan adalah A, B untuk target = 2, dan D untuk target = 3. Hal ini dikarenakan karena modus pada setiap kategori target berbeda-beda.

#### Fitur *Tipe_Tujuan* 

   * Sebelum melakukan imputasi, perlu diperhatikan bahwa pada kategori tujuan terdapat 15 kategori padahal dari informasi dataset, tujuan hanya memiliki 14 kategori. 
   * Ternyata terdapat 1 kategori kosong yaitu “-” yang belum dihitung sebagai *missing values*. Sehingga kategori “-” harus diubah terlebih dahulu menjadi bentuk NaN.
   * Setelah itu, Tipe_Tujuan diimputasi menggunakan modus “A” karena pada fitur tujuan nilai “A” cukup mendominasi dataset, yaitu sebesar 57.6%.

### Persiapan Imputasi Data Numerik

Sebelum imputasi, ada beberapa hal yang perlu diperhatikan,

* Fitur *Rating_Pelanggan*
   * Dengan melihat nilai-nilai pada variabel ini, kami menafsirkan bahwa variabel ini seharusnya hanya berisi nilai antara 1-5 saja (tidak mungkin terdapat nilai rating       98.2763. 
   * Sehingga kami melakukan standarisasi dengan mengubah semua nilai rating yang lebih besar dari 5 menjadi 5. 

* Fitur *Pembatalan_Sebulan_Terakhir*
   * Hal yang sama juga terjadi pada variabel ini.
   * Karena variabel ini berisi banyaknya pembatalan, maka nilainya tidak mungkin negatif.
![image](https://user-images.githubusercontent.com/68768305/117527352-8d747500-aff5-11eb-8d58-d2ca811e51aa.png)

### Imputasi Data Numerik

* Fitur *Jarak_Perjalanan, Rating_Pelanggan, Pembatalan_Sebulan_Terakhir*
   * Akan diimputasi menggunakan median karena distribusi tidak mendekati distribusi normal.
* Fitur *Pelanggan_Sejak_Bulan*
   * Akan diimputasi menggunakan modus.
* Fitur *Indeks_Gaya_Hidup, Encode1, Encode2, Encode3*
   * Akan diimputasi menggunakan mean karena dari grafik distribusi mendekati distribusi normal.
   
### Persiapan Pembuatan Model

![image](https://user-images.githubusercontent.com/68768305/117527408-14c1e880-aff6-11eb-9087-be798ad4ccb5.png)

* Drop kolom yang tidak dipakai seperti *ID* dan *Target*.
* *One-hot encoding* untuk konversi variabel-variabel kategorik menjadi numerik.

### Transformasi untuk variabel “Encoding”

![image](https://user-images.githubusercontent.com/68768305/117528652-67eb6980-affd-11eb-8026-e235e782d1ce.png)

### Pembagian data latih dan data validasi

![image](https://user-images.githubusercontent.com/68768305/117528675-8fdacd00-affd-11eb-8ca1-0526e64ef086.png)

* Data dibagi menjadi data latih (*X_train, y_train*) dan data validasi (*X_test, y_test*) dengan pembagian 80/20.
* *Evaluation Metric* yang dipakai adalah akurasi.

### Random Forest

![image](https://user-images.githubusercontent.com/68768305/117528724-d3cdd200-affd-11eb-88ba-83e8c386eb4b.png)

* Dipilih *max_depth* = 22  untuk mencegah *overfitting* dan variabel *warm_start* = True yang artinya memakai hasil sebelumnya.
* Runtime agak lama dibandingkan dengan model-model yang lain.
* Akurasi paling tinggi di Kaggle ≈ 0.76, paling tinggi dibandingkan model-model lain, seperti *Decision Tree, Cat Boost, Logistic Regression,* dan *Gradient Boosting Classifier*

### Feature Importances

Akan dilihat untuk fitur mana yang paling berkontribusi pada kolom “Target”

![image](https://user-images.githubusercontent.com/68768305/117528800-463eb200-affe-11eb-9f43-f5ee08b50e59.png)

### Interpretasi Model : Feature Importances

![image](https://user-images.githubusercontent.com/68768305/117528818-5d7d9f80-affe-11eb-9792-bf4d87c3019e.png)

Tipe Kendaraan merupakan variabel yang cukup berpengaruh dibandingkan dengan variabel-variabel lainnya.

**Rekomendasi : Dalam mencocokkan taksi apa yang tepat kepada pelanggan, perusahaan “J Taxi” harus lebih memperhatikan tipe kendaraan dari jenis-jenis pelanggan yang ada.**

### Team Members : 
   * Ravialdy Hidayat
   * Stanley Pratama
   * Kevin Prawira









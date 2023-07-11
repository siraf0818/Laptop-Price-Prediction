# Laporan Akhir Kecerdasan Buatan - Kelompok 1

**Anggota Kelompok :**

1. Faris Adhi Laksana Yusuf	-	3.34.21.3.09
2. Febrian Giovanni                  -    3.34.21.3.10

## Domain Proyek

Laptop di era digital saat ini menjadi perangkat yang sangat penting untuk mendukung pembelajaran dan pekerjaan. Menurut data dari Asosiasi Penyelenggara Jasa Internet Indonesia (APJII) tahun 2022, diperkirakan sekitar 85,5% penduduk Indonesia memiliki setidaknya satu laptop [1]. Bahkan lebih dari 60% penduduk memiliki lebih dari satu laptop. Harga laptop menjadi faktor yang sangat berpengaruh dalam keputusan pembelian seseorang. Oleh karena itu, kemampuan machine learning dalam memprediksi harga laptop menjadi sangat berharga bagi masyarakat yang ingin mencari laptop sesuai kebutuhan mereka.

Telah banyak penelitian yang memiliki proyek memprediksi harga. Untuk membuat harga
prediksi, algoritma regresi umumnya digunakan dalam penelitian. Penelitian [2] menyajikan metode untuk memprediksi harga laptop menggunakan metode Machine Learning dengan algoritma regresi dikonfigurasi dengan penyetelan hyper-parameter, yaitu XGBoost.

Untuk mengatasi permasalahan tersebut, metode Machine Learning diperlukan untuk memprediksi harga laptop berdasarkan parameternya yaitu spesifikasi laptop. Penulis menyajikan beberapa Machine Learning menggunakan algoritma regresi dalam proyek ini. Setelah pemodelan, algoritma dengan nilai akurasi tertinggi akan digunakan untuk memprediksi harga laptop. Dengan metode ini, diharapkan model yang dibuat dapat memprediksi harga laptop dengan minimum akurasi diatas 80%.

## Business Understanding

Setiap tahun terdapat berbagai jenis tipe *laptop* dengan fitur yang bermacam-macam. Umumnya *laptop* tipe tertentu meng-*upgrade* perangkatnya dari segi penambahan kapasitas RAM, kartu grafis dan kapasitas penyimpanan, serta kecepatan prosesor. Penambahan fitur pada *laptop* akan mempengaruhi kenaikan harga *laptop* tersebut. Oleh karena itu calon konsumen harus memahami spesifikasi *laptop* yang akan dibeli disesuaikan dengan budget yang dimiliki. Diperlukan sebuah model *machine learning* yang dapat memprediksi harga *laptop* dengan akurat. Sehingga calon konsumen dapat menyiapkan budget yang digunakan untuk membeli *laptop* dengan spesifikasi yang dia inginkan.

#### Problem Statements

Tujuan yang hendak dicapai dari proyek ini adalah sebagai berikut

1. Fitur-fitur apa saja yang paling berpengaruh terhadap harga *laptop* ?
2. Bagaimana proses *Pre-Processing* yang dilakukan agar menghasilkan model *machine learning* yang akurat.
3. Bagaimana membuat atau memilih model *machine learning* yang memiliki akurasi terbaik dalam memprediksi harga *laptop* ?

#### Goals

Tujuan yang hendak dicapai dari proyek ini adalah sebagai berikut 

1. Mengetahui fitur yang paling berkorelasi dengan penentuan harga *laptop*.
2. Membuat model *machine learning* yang dapat memprediksi harga *laptop*.
3. Memilih model *machine learning* yang menghasilkan prediksi paling akurat berdasarkan proses *preprocessing* yang dilakukan

####  Solution Statements

Solusi yang diajukan untuk menyelesaikan masalah yang telah diuraikan adalah sebagai berikut.

1. Melakukan analisis deskriptif untuk mengetahui pola dan informasi yang tersimpan di data mengenai fitur atau spesifikasi yang mempengaruhi harga *laptop*.
2. Melakukan proses *Data Manipulation* untuk menggabungkan kolom-kolom yang berpengaruh terhadap akurasi predisi harga *laptop*
3. Melakukan Proses Preprocessing seperti :
   - Mengecek *missing value* dan duplikasi data. Kebetulan dataset yang digunakan tidak ada *missing value* dan duplikasi data.
   - Menghapus kolom yang tidak berpengaruh terhadap prediksi harga.
   - Melakukan visualisasi data untuk melihat persebaran dan korelasi antar kolom.
   - Membagi data menjadi *training* dan *test set*, dengan prosentase 85% banding 15%. Alasan menggunakan 15% karena jumlah data yang digunakan banyak, jadi hanya dengan 15% sudah didapatkan banyak data tes.
   - Melakukan *Encoding* terhadap kolom yang bertipe objek / kategorikal menggunakan fungsi `Map`.
4. Melakukan pemilihan model terbaik menggunakan LazyPredict :
   - Memilih algoritma yang menghasilkan model dengan performa terbaik.
   - Perfoma model terbaik dilihat dari skor *Mean Square Error* (MSE), *Root Mean Square Error* (RMSE), dan *R Square* (R2).

## Data Understanding

Dataset yang digunakan pada proyek ini diperoleh dari Kaggle. Silahkan kunjungi tautan berikut [Laptop Price Prediction](https://www.kaggle.com/datasets/arnabchaki/laptop-price-prediction) untuk mengakses dataset yang dipakai. Adapun variabel-variabel yang terdapat pada dataset adalah sebagai berikut :

1. **Manufacturer**: Nama brand *Laptop*
2. **Model Name**: Nama model *laptop*
3. **Category**: Kategori *laptop*
4. **Screen Size**: Ukuran layar dalam Inchi
5. **Screen**: Model layar yang digunakan
6. **CPU**: Prosesor *laptop*
7. **RAM**: RAM *laptop*
8. **Storage**: Kapasitas penyimpanan *laptop*
9. **GPU**: Kartu grafis *laptop*
10. **Operating System**: Sistem operasi *laptop*
11. **Operating System Version**: Versi sistem operasi yang digunakan
12. **Weight**: Berat *laptop*
13. **Price**: Harga *laptop* dalam mata uang india (INR)

Pada dataset, terdapat 6 fitur numerikal dan 7 fitur kategorikal. Ringkasan statistik dari data-data numerikal dapat dilihat pada Tabel 1.

<div style="text-align:center">Tabel 1. Ringkasan Statistik Data-Data Numerikal Pada Dataset</div>

|       | **Screen Size** | **CPU**   | **RAM**   | **Storage** | **Weight** | **Price**    | **ScreenX** | **ScreenY** |
| ----- | --------------- | --------- | --------- | ----------- | ---------- | ------------ | ----------- | ----------- |
| count | 977.00000       | 977.00000 | 977.00000 | 977.00000   | 977.00000  | 9.770000e+02 | 977.00000   | 977.00000   |
| mean  | 15.05261        | 2.284033  | 8.528147  | 220.554759  | 2.039128   | 1.001899e+07 | 1767.783009 | 1079.545548 |
| std   | 1.41895         | 0.523576  | 4.997487  | 172.133316  | 0.666009   | 6.306430e+06 | 469.422398  | 285.087803  |
| min   | 10.10000        | 0.900000  | 2.000000  | 1.000000    | 0.690000   | 1.706375e+06 | 4.000000    | 768.000000  |
| 25%   | 14.00000        | 1.800000  | 4.000000  | 32.000000   | 1.500000   | 5.326308e+06 | 1440.000000 | 1080.000000 |
| 50%   | 15.60000        | 2.500000  | 8.000000  | 256.000000  | 2.020000   | 8.527428e+06 | 1920.000000 | 1080.000000 |
| 75%   | 15.60000        | 2.700000  | 8.000000  | 256.000000  | 2.300000   | 1.311570e+07 | 1920.000000 | 1080.000000 |
| max   | 18.40000        | 3.600000  | 32.000000 | 512.000000  | 4.700000   | 5.423231e+07 | 3200.000000 | 2160.000000 |

Pada tahap *Data Understanding* dilakukan analisis data eksploratif untuk mendapatkan wawasan tentang karakteristik data, memahami struktur data, dan mengidentifikasi potensi masalah atau kesalahan yang mungkin terjadi. Kegiatan Data Understanding yang dilakukan pada Proyek ini antara lain :

- Memberikan informasi seperti jumlah data, *missing value*, duplikasi data, korelasi antar kolom, dan sebaran data.

- Melakukan manipulasi data untuk mendapatkan variabel atau fitur baru seperti menggabungkan kolom Resolution X dan Resolution Y untuk mendapatkan nilai PPI (*Pixel Per Inch*).

- Melakukan visualisasi data untuk mengetahui korelasi dan sebaran data. Visualisasi korelasi antar kolom digambarkan dalam heatmap seperti ditunjukan Gambar 1. Berdasarkan diagaram heatmap Gambar 1 diketahui bahawa terdapat beberapa kolom seperti Weight, CPU, RAM, dll yang berkorelasi dengan kolom 'Prize'.  Semakin mendekati nilai 1 maka korelasi semakin tinggi. Kemudian hasil visualisasi heatmap hanya menampilkan korelasi pada kolom yang memberikan data numerikal, sedangkan kolom yang memberikan hasil kategorikal tidak dapat diketahui korelasinya.

  ![image-20230711192516323](https://github.com/siraf0818/Laptop-Price-Prediction/assets/81822076/0a91c485-fa59-4e76-82e0-06112ab4f131)
  
  <div style="text-align:center">Gambar 1. Visualisasi Korelasi Data dengan Heatmap</div>
  
  Sedangkan contoh visualisasi dari sebaran data ditunjukan pada Gambar 2. Visualisasi yang ditunjukan pada Gambar 2 menunjukan bahwa ada ketidakseimbangan data pada kolom CPU, Storage, Weight, dan RAM.
  
  ![image-20230711192726048](https://github.com/siraf0818/Laptop-Price-Prediction/assets/81822076/f1dfd3d9-395a-4a8f-be18-f95e1b56b553)
  
  ![image-20931](https://github.com/siraf0818/Laptop-Price-Prediction/assets/81822076/495b85ab-c34e-4ebc-baf4-2fdaba13570e)

<div style="text-align:center">Gambar 2. Visualisasi Data pada Dataset</div>

## Data Preparation

Teknik data preparation yang dilakukan pada proyek ini adalah sebagai berikut : 

1. Feature Selection : Melakukan seleksi fitur untuk menyeleksi kolom yang berperan sebagai data fitur dan kolom yang menjadi data label.

2. Data Splitting: Membagi dataset menjadi data latih dan data uji. Pada proyek ini perbandingan data latih dan data uji adalah 85 : 15.

3. Menampilkan informasi jumlah data latih dan data uji. Jumlah data latih adalah 830, sedangkan data uji terdat 147data. jumlah data fitur yang dipakai untuk pelatihan adalah 8.

   


## Modelling

Pada tahap ini dilakukan proses pelatihan untuk mendapatkan model dengan performa terbaik. Tahapan yang dilakukan pada proses Modelling adalah sebagai berikut.

1. Memprediksi algoritma dengan performa terbaik menggunakan Lazy Predict

   Lazy Predict adalah library Python yang membantu dalam membuat model *machine learning* dengan cepat dan mudah. Library ini dikembangkan untuk mempercepat proses eksplorasi data dan pemodelan awal. Hasil dari proses pelatihan yang dilakukan Lazy Predict ditunjukan pada Tabel 2.

   <div style="text-align:center">Tabel 2. Hasil Perbandingan model menggunakan Lazy Predict</div>

   | Model                             | Adjusted R-Squared | R-Squared | RMSE | Time Taken |
   | --------------------------------- | ------------------ | --------- | ---- | ---------- |
   | **XGBRegressor**                  | 0.86               | 0.87      | 0.22 | 0.08       |
   | **SVR**                           | 0.86               | 0.86      | 0.23 | 0.05       |
   | **NuSVR**                         | 0.85               | 0.86      | 0.23 | 0.05       |
   | **RandomForestRegressor**         | 0.85               | 0.86      | 0.23 | 0.23       |
   | **GradientBoostingRegressor**     | 0.85               | 0.86      | 0.23 | 0.08       |
   | **HistGradientBoostingRegressor** | 0.84               | 0.85      | 0.24 | 0.46       |
   | **ExtraTreesRegressor**           | 0.84               | 0.85      | 0.24 | 0.23       |
   | **LGBMRegressor**                 | 0.84               | 0.85      | 0.24 | 0.09       |
   | **BaggingRegressor**              | 0.83               | 0.84      | 0.25 | 0.03       |
   | **KNeighborsRegressor**           | 0.80               | 0.81      | 0.27 | 0.02       |
   
   Algoritma dengan performa terbaik dilihat dari nilai R-Square dan RMSE. Semakin besar nilai R-Square (mendekati 1) maka model semakin akurat. Sedangkan pada RMSE, apabila nilai semain kecil (mendekati 0), maka akurasi model akan semakin tinggi. Berdasarkan hasil R-Square dan RMSE menggunakan Lazy Predict pada Tabel 1, disimpulkan bahwa algoritma terbaik yang akan digunakan untuk mempredikasi harga adalah **XGBRegressor**.
   
2. Menggunakan `ColumnTransformer` untuk mengubah data kategorik menjadi numerik

   Pada proyek ini masih mempertahankan kolom kategorikal yaitu Manufacturer, GPU, dan OS. Sebab pada saat ingin mempredikasi harga laptop, calon pembeli tentunya akan memilih Manufacturer, GPU,dan OS dalam bentuk kategori bukan numerik. Oleh karena itu kita ubah data kategorik menjadi numberik menggunkan teknik OneHotEncoding. Tapi sebelum dilakukan teknik `OneHotEncoding` dilakukan harus menampilkan indeks dari masing-masing kolom menggunakan fungsi `enumerate()`. Dan selanjutnya dilakukan proses `ColumnTransformer`.

3. Membuat pipeline untuk menggabungkan data numerik dan kategorik

   Hasil penggunakan teknik `ColumnTransformer` disimpan dalam objek feature. Selanjutnya dilakukan proses pipeline untuk menggabungkan dan meng-optimasi kolom numerikal dan kategorikal agar dapat di proses oleh algoritma machine learning. 

4. Setelah dilakukan proses pelatihan oleh Lazy Predict, diperoleh algoritma dengan performa terbaik yaitu :

   - **XGBRegressor**

     XGBRegressor adalah sebuah model regresi yang menggunakan algoritma XGBoost (eXtreme Gradient Boosting). XGBoost adalah sebuah metode yang populer dalam machine learning untuk masalah regresi dan klasifikasi. XGBRegressor adalah salah satu implementasi khusus dari XGBoost yang digunakan khusus untuk tugas regresi.

     XGBoost adalah algoritma yang berbasis pada ensemble learning, yang berarti ia menggabungkan prediksi dari beberapa model (disebut weak learner) yang lemah menjadi satu prediksi yang lebih kuat. XGBoost menggunakan teknik boosting, di mana model-model lemah ditambahkan secara berurutan, dengan setiap model berusaha memperbaiki kesalahan prediksi model sebelumnya. XGBRegressor memiliki banyak fitur dan keuntungan, di antaranya:

     1. Handling Data yang Kompleks: XGBRegressor dapat bekerja dengan baik pada dataset yang memiliki banyak fitur dan tipe data yang berbeda. Ini dapat mengatasi variabel numerik, kategorikal, dan teks dengan menggunakan encoding yang sesuai.
     2. Regularisasi: XGBRegressor memiliki beberapa teknik regularisasi yang membantu mengurangi overfitting. Regularisasi dapat mengontrol kompleksitas model dan mencegah model menjadi terlalu rumit atau terlalu spesifik terhadap data pelatihan.
     3. Pengaturan Hyperparameter yang Fleksibel: XGBRegressor memiliki banyak hyperparameter yang dapat disesuaikan, seperti jumlah pohon (trees), kedalaman pohon (depth), dan laju pembelajaran (learning rate). Ini memberikan fleksibilitas dalam menyesuaikan model dengan karakteristik dataset dan memperbaiki performa prediksi.
     4. Kecepatan dan Skalabilitas: XGBRegressor dirancang dengan fokus pada kecepatan dan skalabilitas. Implementasi XGBoost menggunakan optimasi dan paralelisasi yang efisien sehingga dapat menangani dataset besar dengan cepat.
   
     Dengan kombinasi fitur-fitur tersebut, XGBRegressor telah terbukti efektif dalam banyak kasus regresi dan sering digunakan dalam kompetisi data dan proyek machine learning.
   
5. Menambahkan parameter tunning untuk mengingkatkan performa model

   Penambahan parameter menggunakan **Teknik Grid Search**. Sehingga diperoleh hyperparameter dari algoritma adalah sebagai berikut.

   - Parameter XGBRegressor
   
     - 'n_estimators': [100, 200, 300]
     - 'max_depth': [3, 5, 7]
     - 'learning_rate': [0.1, 0.01, 0.001]
     - 'gamma': [0, 0.1, 0.2]
     - 'min_child_weight': [1, 3, 5]
     - 'subsample': [0.8, 1.0]
     - 'colsample_bytree': [0.8, 1.0]
     - 'reg_alpha': [0, 0.1, 0.5]
     - 'reg_alpha': [0, 0.1, 0.5]
     - 'reg_lambda': [0, 1, 10]
     - 'scale_pos_weight': [1, 3, 5]
     - 'random_state': [42]
     - 'n_jobs': [-1]


## Evaluation

- Metrik evaluasi yang digunakan adalah *Mean Square Error* (MSE), *Root Mean Square Error* (RMSE), dan *R Square* (R2 Score)

- MSE melakukan pengurangan nilai data aktual dengan data peramalan dan hasilnya dikuadratkan (*squared*) kemudian dijumlahkan secara keseluruhan dan membaginya dengan banyaknya data yang ada. Rumus dari MSE adalah sebagai berikut 
  $$
  MSE = \frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2
  $$
  Diketahui:

  - n = Jumlah Data
  - yi = *Actual Value* / Nilai Sebenarnya
  - ŷi = *Predicted Value* / Nilai Prediksi

- RMSE adalah jumlah dari kesalahan kuadrat atau selisih antara nilai sebenarnya dengan nilai prediksi yang telah ditentukan. Cara menghitungnya tinggal mengakar kan mse menggunakan fungsi *np.sqrt*. Rumus dari RMSE adalah sebagai berikut.
  $$
  RMSE = \sqrt{(\frac{1}{n})\sum_{i=1}^{n}(y_{i} - x_{i})^{2}}
  $$
  Diketahui:

  - n = Jumlah Data
  - yi = *Actual Value* / Nilai Sebenarnya
  - ŷi = *Predicted Value* / Nilai Prediksi

- R2 Score dijadikan sebagai pengukuran seberapa baik garis regresi mendekati nilai data asli yang dibuat melalui model. Rumus dari R2 Score adalah sebagai berikut.
  $$
  R^2 = 1 - {SS_R \over SS_T} =  1 - {\sum_{i} (y_i - ŷ_p) ^ 2 \over \sum_{i} (y_i - ȳ) ^ 2}
  $$

  - SSR : Kuadrat dari selisih nilai Y prediksi dengan nilai rata-rata Y = ∑ (Ypred – Yrata-rata)²
  - SST : Kuadrat dari selisih nilai Y aktual dengan nilai rata-rata Y = ∑ (Yaktual – Yrata-rata)²

- Setelah melalui tahap pelatihan dan evaluasi menggunakan MSE, RMSE, dan R Square, diperoleh hasil bahwa algoritma **XGBRegressor** memiliki performa seperti ditunjukan Tabel 3. 

  <div style="text-align:center">Tabel 3. Hasil Pengujian dari 3 Algoritma Teratas</div>

  | id   | Model_Name   | MSE       | R2 Score  | RMSE      |
  | ---- | ------------ | --------- | --------- | --------- |
  | 0    | XGBRegressor | 0.2078768 | 0.4463952 | 0.4559351 |
  
- Membandingkan data sebenarnya dengan hasil prediksi. Hasil perbandingan dapat dilihat pada Tabel 4.

  <div style="text-align:center">Tabel 4. Hasil Perbandingan Data Sebenarnya dengan Hasil Prediksi</div>
  
  | Id      | y_true     | **prediksi_XGB** |
  | :------ | :--------- | :--------------- |
  | **966** | 21.0168476 | 20.6000004       |
  | **879** | 21.0336742 | 20.8999996       |
  | **436** | 20.1507893 | 20.5000000       |
  | **970** | 21.8505459 | 21.7000008       |
  | **261** | 20.3972893 | 21.0000000       |
  | ...     | ...        | ...              |
  | **54**  | 20.2521057 | 20.2999992       |
  | **34**  | 21.2072182 | 21.7000008       |
  | **434** | 22.1048985 | 21.0000000       |
  | **30**  | 19.8026810 | 21.5000000       |
  | **862** | 21.4599781 | 21.3999996       |

## Conclussion

1. Berdasarkan hasil pengukuran, terdapat 7 kolom atau fitur yang mempengaruhi *Price* yaitu Screen Size, CPU, RAM, Storage, Weight, ScreenX, dan ScreenX.
2. Proses preprocessing yang dilakukan adalah dengan melakukan manipulasi data seperti mengabungkan ScreenX dan ScreenX untuk menghasilkan fitur baru yaitu PPI. Menghapus data yang tidak memiliki korelasi yang signifikan dengan *Price*, dan mengubah format tipe data pada setiap kolom yang memiliki korelasi.
3. Berdasarkan hasil pengujian model, diperoleh hasil bahwa algoritma XGBRegressor memiliki performa yang baik dengan nilai RMSE sebesar 0.4559351 dan R2 Score sebesar 0.4463952.
4. Meningkatkan performa model dapat dilakukan dengan menambahkan hyperparameter.  Pemilihan hyperparameter yang menghasilkan performa terbaik dapat dilakukan menggunakan teknik Grid Search.
5. Dataset yang digunakan memiliki rentang jangkauan yang berbeda (imbalace), oleh sebab itu agar performa model lebih baik maka perlu dilakukan teknik SMOTE untuk menangani imbalance dataset.

## Referensi

[1]   APJII, “Laporan Survei Internet APJII 2021 - 2021,” 2022. [Online]. Available: [https://apjii.or.id/survei](https://apjii.or.id/survei).

[2]   Astri Dahlia Siburian, Daniel Ryan Hamonangan Sitompul, Stiven Hamonangan Sinurat Andreas Situmorang, Ruben, Dennis Jusuf Ziegel, Evta Indra, “Laptop Price Prediction with Machine Learning Using Regression Algorithm,” 2022.




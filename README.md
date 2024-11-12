# House-Price-Prediction-Kota-Bandung

Proyek ini merupakan hasil kolaborasi dengan [@Haris Muhammad](https://github.com/harishmuh) 

### **Metric Evaluation**

metrik yang akan di gunakan untuk mengukur performa dari model adalah : 

**1. MAPE (mean absolute percentage error)**

MAPE didefinisikan sebagai rata-rata kesalahan absolut antara nilai aktual dan nilai prediksi, dinyatakan dalam persentase dari nilai aktual. 

$$MAPE = \frac{1}{n} \sum\limits_{i=1}^n |\frac{y_i - \hat{y}_i}{y_i}|$$

cara kerja MAPE : 
- menghitung error (selisih) dari nilai actual - prediksi. kemudian di absolutkan 
- menghitung persentasi dari error . error yang sudah absolut di bagi dengan nilai aktual untuk mendapatkan error dalam bentuk persentase
- Hitung rata-rata dari semua kesalahan persentase untuk mendapatkan MAPE.

Keunggulan MAPE : 
- karena dalam bentuk persentasi akan lebih mudah di interpretasi dan di jelaskan untuk orang yang non-teknis. 
- lebih mudah membandingkan untuk evaluasi metrik antar model 

Kekurangan MAPE : 
- jika nilai aktual mendekati nol maka mape bisa menjadi sangat besar karena pembagian dengan nol. 
- MAPE cenderung memberikan bobot yang lebih besar pada kesalahan yang terjadi pada nilai aktual yang kecil, karena kesalahan persentasenya menjadi besar
- sensitif terhadap outlier

**2. MAE (mean absolute error)**

MAE didefinisikan sebagai rata-rata dari semua nilai absolut selisih antara nilai aktual dan nilai prediksi. 

$$MAE = \frac{1}{n} \sum\limits_{i=1}^n |y_i - \hat{y}_i|$$

cara kerja MAE : 
- menghitung error (selisih) dari nilai aktual - nilai prediksi kemudian di absolutkan 
- menghitung rata rata dari semua error untuk mendapatkan MAE 

keunggulan MAE : 
- MAE mudah dihitung dan diinterpretasikan, karena menggambarkan kesalahan rata-rata dalam unit yang sama dengan data asli
- karena menghitung nilai absolut maka MAE lebih robust terhadap outlier di bandingkan metrik lain seperti MSE. 

kekurangan MAE : 
- MAE hanya memperhitungkan besarnya kesalahan tanpa memperhatikan apakah prediksi terlalu tinggi atau terlalu rendah.

**3. RMSE (root mean squared error)**

RMSE didefinisikan sebagai akar kuadrat dari rata-rata kuadrat perbedaan antara nilai aktual dan nilai prediksi

$$RMSE = \sqrt{\frac{1}{n} \sum\limits_{i=1}^n (y_i - \hat{y}_i)^2}$$

cara kerja RMSE : 
- menghitung selisih nilai aktual - prediksi. kemudian selisih akan di kuadratkan untuk mendapatkan error kuadrat 
- menghitung rata rata dari jumlah seluruh error kuadrat untuk mendapatkan MSE
- mengambil akar kuadrat dari MSE agar menjadi RMSE 

keunggulan RMSE : 
- Karena RMSE mengkuadratkan selisih antara nilai aktual dan nilai prediksi, kesalahan yang lebih besar memiliki pengaruh yang lebih signifikan terhadap nilai RMSE dibandingkan kesalahan yang lebih kecil. hal ini berarti jika terdapat nilai prediksi yang memiliki perbedaan sangat besar terhadap nilai aktual maka RMSE akan lebih tinggi.  
- RMSE diukur dalam unit yang sama dengan variabel yang diprediksi. Ini memudahkan interpretasi hasil karena kita dapat langsung memahami besaran kesalahan dalam konteks yang sama dengan data yang digunakan. jika memprediksi ribuan Dollar maka RMSE juga akan berada dalam ribuan dollar. 

kekurangan RMSE : 
- Sensitivitas terhadap kesalahan besar dapat menjadi kelemahan jika data memiliki outlier yang tidak representatif

Alasan Menggunakan MAPE, MAE, dan RMSE : 
- RMSE :  Karena diukur dalam unit yang sama dengan variabel yang diprediksi yaitu rp House Price Kota Bandung, RMSE memberikan gambaran yang mudah dipahami tentang skala kesalahan dalam bentuk Rupiah. RMSE memberikan penalti yang besar terhadap outlier di residual (error) sehingga cocok untuk mendapatkan gambaran model terbaik dalam memprediksi nilai *House Price*. 
- MAPE : dalam bisnis MAPE lebih mudah di pahami dan di interpretasikan oleh orang non teknis karena kesalahan yang di hitung di tampilkan dalam bentuk persen. dalam hal ini adalah kesalahan antara nilai aktual dan prediksi terhadap *House Price* dan di sajikan dalam persen. 
- MAE : MAE dihitung dengan mengambil rata-rata dari nilai absolut selisih antara nilai prediksi dan nilai aktual. MAE dapat dengan mudah diinterpretasikan sebagai kesalahan rata-rata yang dihasilkan oleh model. Unit MAE sama dengan unit Variabel Target *House Price* sehingga mudah dalam menjelaskannya. 

Metrik yang menjadi prioritas adalah : 
1. untuk komparasi model metrik yang di gunakan adalah RMSE. 
2. untuk penjelasan dalam bisnis metrik yang di gunakan adalah MAPE karena lebih mudah di interpretasikan.



#### **Final Model**

setelah melakukan tuning ke 3 model terbaik (Random Forest regressor, LGBM Regressor, Gradient Boosting Regressor) maka akan di ambil satu model sebagai final model. ketiga model tersebut akan di komparasikan berdasarkan RMSE. karena cara kerja RMSE yang memberikan penalti lebih besar terhadap outlier residual maka akan sagat membantu dalam menangani kesalahan prediksi yang besar. RMSE terkecil lah yang akan di gunakan sebagai final model. 

Metrik MAPE dari model dengan RMSE terkecil akan  di gunakan untuk penjelasan dalam bisnis agar lebih mudah di interpretasikan. berikut hasil RMSE dan MAPE setelah di Tuning. 



<div style="display: flex; justify-content: center;">

| Model                       | RMSE Train   | RMSE Test   | MAPE Train | MAPE Test |
|-----------------------------|--------------|-------------|------------|-----------|
| **Random Forest Regressor**     | 532.080.695  | 644.888.857 | 18 %       | 17 %      |
| **Light GBM Regressor**        | 530,876,376  | 640,545,737 | 19 %       | 17 %      |
| **Gradient Boosting Regressor** | 544,173,380  | 656,156,979 | 18 %       | 16 %      |

</div>



berdasarkan informasi di atas akan di ambil keputusan bahwa model **Light GBM Regressor** sebagai final model untuk memprediksi House Price Prediction. hal ini di karenakan model **Light GBM Regressor** setelah di tuning memiliki RMSE paling kecil di bandingkan 2 model lainnya, walaupun perbedaan nya sangat tipis dengan Random Forest Regressor. **Parameter terbaik untuk Light GBM Regressor** : 

<div style="display: flex; justify-content: center;">

| num_leaves | n_estimators | min_data_in_leaf | max_depth | learning_rate | 
|------------|--------------|------------------|-----------|---------------|
| 100        | 300          | 50               | 5         | 0.05          | 

| lambda_l2 | lambda_l1 | feature_fraction | bagging_freq | bagging_fraction |
|-----------|-----------|------------------|--------------|------------------|
0.1       | 1         | 1.0              | 5            | 0.8             |

</div>


<p align='center'><b><span style="font-size:22px">LIGHT GRADIENT BOOSTING MACHINE REGRESSOR</span></b></p>

LightGBM Regressor adalah algoritma machine learning berbasis gradient boosting yang dirancang untuk menangani tugas-tugas regresi. Dikembangkan oleh Microsoft, algoritma ini merupakan bagian dari keluarga LightGBM (Light Gradient Boosting Machine) yang terkenal karena kecepatan dan efisiensinya, khususnya pada dataset besar. Gradient boosting adalah teknik yang menggabungkan beberapa model pohon keputusan sederhana (biasanya pohon yang dangkal) secara bertahap untuk membentuk model yang kuat. berikut saya sertakan gambar simulasi bagaimana **LightGBM Regressor** bekerja.

<p align="center">
<img src="https://www.mdpi.com/jmse/jmse-09-00496/article_deploy/html/images/jmse-09-00496-g001.png" width="700" height="500">
</p>

LightGBM bekerja dengan prinsip gradient boosting, yaitu secara iteratif membangun pohon keputusan baru untuk memperbaiki kesalahan model sebelumnya. Namun, LightGBM menggunakan teknik pertumbuhan pohon leaf-wise daripada level-wise, yang umum dalam algoritma boosting lainnya.

Berikut ringkasan dari cara kerja LightGBM Regressor:

- Inisialisasi Model: Model dimulai dengan inisialisasi yang membuat prediksi awal (biasanya rata-rata target pada tahap awal).

- Pembentukan Pohon secara Iteratif: Pada setiap iterasi, LightGBM membangun pohon baru yang ditujukan untuk meminimalkan loss dari prediksi yang ada. LightGBM memilih daun (leaf) dengan loss tertinggi pada setiap langkah (leaf-wise growth), yang memungkinkan model untuk belajar lebih cepat dan efektif.

- Optimasi dan Penurunan Loss: Setiap pohon baru menambah informasi untuk memperbaiki prediksi. Pada dasarnya, setiap pohon memprediksi residual (sisa kesalahan) dari model sebelumnya. Model kemudian menggabungkan hasil dari semua pohon untuk membuat prediksi akhir yang lebih akurat.

- Pengaturan Hyperparameter: LightGBM menyediakan parameter seperti learning_rate, num_leaves, max_depth, dan feature_fraction untuk mengontrol kompleksitas dan kecepatan konvergensi. Tuning parameter ini membantu mencegah overfitting dan memastikan performa optimal.

Dengan strategi ini, LightGBM Regressor dapat belajar dengan lebih cepat dan efisien dibandingkan algoritma boosting lainnya, sambil menghasilkan model yang akurat untuk tugas regresi.



### **Conclussion**

- Metrik Utama yang di gunakan adalah RMSE dan MAPE.
    - RMSE di gunakan untuk menilai performa model agar mendapatkan model terbaik. karena cara kerja RMSE yang memberikan penalti besar terhadap residual(error) dalam prediksi sehingga kita bisa mendapatkan performa model secara maksimal. 
    - MAPE di gunakan untuk menginterpretasikan perfroma model, karena bentuk MAPE dalam persentasi maka akan lebih mudah menjelaskan performa model kepada orang non teknis. 

- Berdasarkan Hyperparameter Tuning model terbaik adalah : 
    - Light Gradient Boosting Machine Regressor
    - Nilai RMSE pada data test : 640,545,737
    - Nilai MAPE pada secara kesulurhan data test : 17% 
    - Nilai MAPE per segmentasi :
        - LOW Price : 22.9 %
        - MEDIUM Price : 13.3 %
        - HIGH Price : 17.8 % 
        - model cukup baik dan stabil dalam memprediksi *House Price* untuk segmentasi Medium Price dan High Price. dan performanya berkurang saat memprediksi segmentasi Low Price. 

- Limitasi Model : 

    Model ini hanya valid untuk memprediksi target : 
    - **House Price kota Bandung** : 135 jt - 7.5 M
    
    dan model ini valid di gunakan jika menggunakan feature : 
    - **Luas Tanah** : 556 m (max)
    - **Luas Bangunan** : 507 m (max)
    - **Jumlah Kamar** : 1 - 8
    - **Kecamatan** : 'antapani', 'sukasari', 'cibeunying kidul', 'buahbatu', 'coblong','mandalajati', 'arcamanik', 'bojongloa kaler', 'rancasari','gedebage', 'cibeunying kaler', 'bandung kidul', 'kiaracondong','ujungberung', 'sukajadi', 'regol', 'cidadap', 'lengkong','cibiru', 'batununggal', 'cicendo', 'bandung kulon', 'andir','panyileukan', 'astana anyar', 'bojongloa kidul', 'bandung wetan','babakan ciparay', 'cinambo'
    
    Berdasarkan informasi di atas dapat disimpulkan bahwa model tidak akan valid di gunakan jika terdapat nilai atau kategori yang tidak sesuai.

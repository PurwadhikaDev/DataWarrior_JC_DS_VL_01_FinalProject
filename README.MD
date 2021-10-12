![Banner](https://github.com/PurwadhikaDev/DataWarrior_JC_DS_VL_01_FinalProject/blob/main/Img/Olist%20(2).png)

# Olist Customer Segmentation Based on Customer Behavior
Team Members:
* **Muhammad Ariq Budipraja** (muhammad.ariq15@gmail.com)
* **Rendi Salim** (rendisalim10@gmail.com)

## Table of Contents
* [Project Description](#project-description)
    * [Background](#background)
    * [Business Problem Statement](#business-problem-statement)
* [Data Understanding](#data-understanding)
* [Modeling](#modeling)
* [File Content](#file-content)
* [Reference](#reference)

## Project Description:
Project ini menggunakan data transaksi di sebuah e-commerce di Brazil yang diambil dari [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce/). Tujuan dari proeject ini adalah analisa customer segmentation berdasarkan behavior transaksi dari para customers. Model yang digunakan pada project ini adalah RFM (Recency, Frequency, & Monetary) model, K-Means Clustering, dan Gaussian Clustering. 

### Background:
Pada era teknologi saat ini, bisnis *E-commerce* merupakan hal umum yang dapat ditemukan. *E-commerce* sendiri adalah model bisnis yang memungkinkan sebuah perusahaan atau individu bisa membeli atau menjual produknya melalui internet. Pengguna *E-commerce* dari tiap tahunnya juga mengalami kenaikan, khususnya untuk negara Brazil. Berikut data pengguna *E-commerce* dari tahun 2017 - 2025.

<p align="center">
  <img src="https://cdn.statcdn.com/Statistic/250000/251659-blank-754.png" alt="Tren_E-commerce_Brazil"/>
</p>

Di dalam *E-commerce*, salah satu model bisnis yang dapat ditemukan adalah *marketplace*. *Marketplace* adalah model bisnis yang menyediakan tempat bertemunya seorang penjual dan pembeli. Salah satu contoh *marketplace* yang berada di Brazil adalah *Olist*. 

<p align="center">
  <img src="https://res.cloudinary.com/crunchbase-production/image/upload/c_lpad,h_256,w_256,f_auto,q_auto:eco,dpr_1/h8ccwg5vhjcoqu1qfuwv" alt="Olist Logo"/>
</p>

*Revenue* dari model bisnis *marketplace* bisa berasal dari fitur berbayar, iklan, payment gateway, dan partnership. Intinya semakin banyak *user* atau *trafic* pada suatu *marketplace* maka revenue yang didapatkan juga akan semakin banyak. Salah satu cara agar *user* atau *traffic* pada sebuah *marketplace* mengalami kenaikan adalah dengan adalah dengan melakukan *Marketing Campaign*, seperti pemberian *discount*, *copywriting*, dan lainnya. Pada umumnya, perusahaan menyiapkan budget sebesar 5%-12% dari total *revenue* yang didapatkan untuk melakukan *marketing campaign*. Namun, masalah yang terjadi adalah *marketing campaign* yang dilakukan tidak tepat sasaran sehingga perusahaan mengalami kerugian. Sebuah *marketing campaign* dapat dikatakan sukses bukan hanya diukur berdasarkan berapa banyak *user* baru yang berhasil didapatkan, melainkan juga berapa banyak *user* lama yang berhasil dipertahankan agar tetap menggunakan *marketplace* tersebut.  
<p> <p>

Untuk mengatasi hal tersebut, salah satu cara yang dapat dilakukan adalah melakukan segmentasi pada *customer* atau yang biasa disebut dengan *Customer Segmentation*. *Customer Segmentation* membantu pemilik *marketplace* untuk mengelompokkan *customer* yang memiliki sifat yang sama. Dengan menggunakan *Customer Segmentation*, perusahaan dapat melakukan *marketing campaign* secara efektif sehingga jumlah transaksi *user* dan loyalitas *user* dapat meningkat. Menurut survey yang dilakukan oleh *Researchscape and Evergage* pada tahun 2020, 99% *marketer* setuju bahwa personalisasi membantu menguatkan hubungan dengan customer dan 78% dari hasil tersebut memberikan klaim bahwa *impact*-nya sangat kuat. 
<p> <p>


### Business Problem Statement:
#### Business Problem Statement for Machine Learning?
**How to segment customers so we can divide customers based on their shopping behavior?**
* Value: Customer Segmentation
* Goals: Divide customers based on their shopping behavior

#### Business Problem Statement for Analytics?
* Value: Give treatment for each cluster
* Goals: Increase retention rate customer

## Data Understanding:
Berdasarkan *Problem Statement* yang ada di atas, kami akan menyelesaikan masalah yang dimiliki sebuah perusahaan *E-commerce* di Brazil, yaitu perusahaan *Olist*. Data ini diambil dari tahun 2016 - 2018 dan disebarkan secara public di <a href = "https://www.kaggle.com/olistbr/brazilian-ecommerce">Kaggle</a> pada tahun 2018 bulan September. Data-data yang ada berisi tentang transaksi *customer* dan *seller*. Untuk menyelesaikan masalah tersebut, kami hanya membutuhkan data-data yang berhubungan dengan transaksi *customer* saja karena yang ingin kami lakukan adalah *customer segmentation* yang berguna untuk mengetahui behavior seorang *customer* dalam bertransaksi. 

![Scheme_data](https://i.imgur.com/HRhd2Y0.png)

### Attribute Information:
   <table>
  <tr>
    <th>Attribute</th>
    <th>Data Type</th>
    <th>Description</th>
    <th>Unit Analysis</th>
  </tr>
  <tr>
    <td>order_id</td>
    <td>object</td>
    <td>Unik ID dari order</td>
    <td>Setiap baris merepresentasikan ID order yang yang muncul ketika customer
    melakukan order</td>
  </tr>
  <tr>
    <td>order_purchase_stamp</td>
    <td>datetime64[s]</td>
    <td>Waktu pembelian customer</td>
    <td>Setiap baris merepresentasikan waktu ketika customer melakukan order</td>
  </tr>
  <tr>
    <td>order_item_id</td>
    <td>float64</td>
    <td>Jumlah barang per-order</td>
    <td>Setiap baris merepresentasikan jumlah barang yang dibeli customer dalam sekali order</td>
  </tr>
  <tr>
    <td>product_id</td>
    <td>object</td>
    <td>ID dari sebuah product</td>
    <td>Setiap baris merepresentasikan ID dari sebuah product yang diorder oleh customer</td>
  </tr>
  <tr>
    <td>price</td>
    <td>float64</td>
    <td>Harga dari sebuah product</td>
    <td>Setiap baris merepresentasikan harga dari sebuah product yang diorder oleh customer</td>
  </tr>
  <tr>
    <td>freight_value</td>
    <td>float64</td>
    <td>Nilai pengiriman product</td>
    <td>Setiap baris merepresentasikan nilai pengirim dari sebuah product yang diorder oleh customer. Apabila item lebih dari 1, nilainya dipisah</td>
  </tr>
  <tr>
    <td>product_photo_qty</td>
    <td>float64</td>
    <td>Jumlah foto sebuah product</td>
    <td>Setiap baris merepresentasikan jumlah foto dari sebuah product yang diiklankan</td>
  </tr>
  <tr>
    <td>payment_sequential</td>
    <td>float64</td>
    <td>Jumlah payment method</td>
    <td>Setiap baris merepresentasikan jumlah metode payment yang dilakukan oleh customer. Customer dapat membayar sebuah transaksi lebih dari 1 metode</td>
  </tr>
  <tr>
    <td>payment_type</td>
    <td>object</td>
    <td>Metode pembayaran</td>
    <td>Setiap baris merepresentasikan metode yang digunakan customer dalam membayar sebuah transaksi</td>
  </tr>
  <tr>
    <td>payment_value</td>
    <td>float64</td>
    <td>Nilai Transaksi</td>
    <td>Setiap baris merepresentasikan nilai transaksi yang harus dibayar customer</td>
  </tr>
  <tr>
    <td>review_score</td>
    <td>float64</td>
    <td>Tingkat kepuasan customer</td>
    <td>Setiap baris merepresentasikan tingkat kepuasan customer dalam bertransaksi, nilainya dari 1 - 5</td>
  </tr>
  <tr>
    <td>customer_unique_id</td>
    <td>object</td>
    <td>Unik ID dari customer</td>
    <td>Setiap baris merepresentasikan ID customer yang melakukan
    order</td>
  </tr>
  <tr>
    <td>customer_zip_code_prefix</td>
    <td>int64</td>
    <td>Kode pos dari customer</td>
    <td>Setiap baris merepresentasikan kode pos dari tempat tinggal customer, namun hanya 5 kode awal</td>
  </tr>
  <tr>
    <td>customer_city</td>
    <td>object</td>
    <td>Nama kota dari customer</td>
    <td>Setiap baris merepresentasikan nama kota tempat tinggal customer</td>
  </tr>
  <tr>
    <td>customer_state</td>
    <td>object</td>
    <td>Negara Bagian customer</td>
    <td>Setiap baris merepresentasikan negara bagian dari tempat tinggal customer</td>
  </tr>
  <tr>
    <td>product_category_name_english</td>
    <td>object</td>
    <td>Kategori product</td>
    <td>Setiap baris merepresentasikan nama kategori dari sebuah product dalam Bahasa Inggris</td>
  </tr>
  <tr>
    <td>month_order</td>
    <td>object</td>
    <td>Nama bulan order dilakukan</td>
    <td>Setiap baris merepresentasikan nama bulan dari tanggal pembelian dilakukan</td>
  </tr>
  <tr>
    <td>weekday_order</td>
    <td>object</td>
    <td>Nama hari order dilakukan</td>
    <td>Setiap baris merepresentasikan nama hari dari tanggal pembelian dilakukan</td>
  </tr>
  <tr>
    <td>month_year_order</td>
    <td>period[M]</td>
    <td>Tahun dan bulan pembelian</td>
    <td>Setiap baris merepresentasikan tahun dan bulan dari tanggal pembelian dilakukan</td>
  </tr>
</table>

## Modeling:
Pada bagian ini, kami feature yang kami gunakan adalah *Recency*, *Frequency*, dan *Monetary* dari *customer*. Ketiga hal tersebut dapat menggambarkan transaksi *behavior* dari seorang *customer*. Arti dari *RFM* sendiri adalah:
* *Recency*: Waktu terakhir kali *customer* melakukan pembelian
* *Frequency*: Jumlah transaksi
* *Monetary*: Kekuatan belanja dari sebuah *customer*
Model yang kami coba ada 3 model, yaitu RFM Segmentation, K-Means, dan Gaussian Models

### RFM Segmentation:
Pada RFM Segmentation, kami melakukan perhitungan skor segmentasinya dengan cara mengkombinasikan skor dari R, F, dan M menjadi sebuah kombinasi unik dalam bentuk string. Contohnya jika R = 1, F = 1, dan M = 1 maka RFM Segmentation Score nya menjadi 1 + 1 + 1 = 111 dan dari score tersebut kami memberikan segmentasi pada *customer*

#### Hasil dari RFM Segmentation:
![Model RFM Segmentation](Img/RFMsegmentasi.JPG)

### K-Means:
Dengan menggunakan feature RFM, kami menggunakan algoritma K-Means untuk melakukan *customer segmentation*

#### Hasil dari K-Means:
![K-Means](Img/KMeans.JPG)

### Gaussians:
Model ini menggunakan gaussian method untuk membentuk suatu cluster.

#### Hasil dari Gaussians:
![Gaussians](Img/Gaussians.JPG)

## File Content:
* Dataset: Folder yang berisi dataset dari [Kaggle]("https://www.kaggle.com/olistbr/brazilian-ecommerce")
* Img: Folder yang berisi gambar-gambar dari hasil project ini
* **data_outlist_clean.csv**: Data gabungan dari dataset
* **customer.csv**: Data transaksi behavior dari setiap customer
* **Part01-Cleaning-Data.ipynb**: Notebook file yang berisi bagaimana cara kami merge data, handling missing value, handling duplicate value, casting data type, handling inconsisten variable, dan save data menjadi dataset baru
* **Part02-EDA.ipynb**: Notebook file yang berisi EDA kami dan beberapa feature engineering untuk mendapatkan feature transaksi behavior dari seorang customer
* **Part03-Methodology(Data Analytics).ipynb**: Notebook file yang berisi Descriptive dan Inferential Analysis dari perusahaan *Olist*
* **Part04-Modeling_RFM.ipynb**: Notebook file yang berisi model-model untuk *customer segmentation*

[(Back to top)](#table-of-contents)
   
## Reference:
* <sup>[1]</sup> https://www.invespcro.com/blog/customer-acquisition-retention/
* <sup>[2]</sup> https://www.statista.com/forecasts/251659/e-commerce-users-in-brazil
* <sup>[3]</sup> https://clevertap.com/blog/rfm-analysis/
* <sup>[4]</sup> Prescription for Cutting Costs, Bain & Company
* <sup>[5]</sup> https://www.ngdata.com/how-to-improve-customer-retention/

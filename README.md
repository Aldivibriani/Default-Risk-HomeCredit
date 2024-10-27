# Default-Risk-HomeCredit
Implementasi Machine Learning untuk Memprediksi Default Risk di HomeCredit

# Company Profile
Banyak calon nasabah yang kesulitan mengajukan pinjaman karena kurangnya atau tidak ada sama sekali memiliki riwayat kredit, sehingga mereka berakhir menggunakan peminjam yang kurang dipercaya dan sering dimanfaatkan (contoh rate bunga yang tinggi). HomeCredit ingin menyediakan pinjaman yang aman dan nyaman untuk para nasabahnya. Untuk memastikan bahwa nasabah yang memiliki riwayat kredit yang lemah itu mampu memenuhi pembayaran, maka HomeCredit ingin mengidentifikasi karakteristik nasabah apa saja yang berpotensi gagal bayar dan tidak, sehingga HomeCredit bisa memberikan pinjaman untuk nasabah yang memiliki riwayat kredit yang kurang.

# Business Understanding
Tim kami berupaya untuk mengurangi nasabah yang berpotensi dalam risiko gagal bayar. Maka dari itu, goal utama dari analisis dataset HomeCredit adalah mengidentifikasi nasabah gagal bayar (default rate) dengan lebih akurat. Melalui analisis data ini, perusahaan dapat memahami pola dan karakteristik nasabah seperti jenis kelamin, demografis, status pernikahan, tanggungan, riwayat kredit, dan lainnya. Dari uraian karakteristik tadi, perusahaan bisa melihat nasabah atau calon nasabah yang memiliki potensi gagal bayar, sehingga risiko kredit macet bisa diminimalisir dan menerima calon nasabah yang memiliki riwayat kredit lemah.

# Goals
Tim kami berupaya untuk mengurangi nasabah yang berpotensi dalam risiko gagal bayar. Maka dari itu, goal utama dari analisis dataset HomeCredit adalah mengidentifikasi nasabah gagal bayar (default rate) dengan lebih akurat. Melalui analisis data ini, perusahaan dapat memahami pola dan karakteristik nasabah seperti jenis kelamin, demografis, status pernikahan, tanggungan, riwayat kredit, dan lainnya. Dari uraian karakteristik tadi, perusahaan bisa melihat nasabah atau calon nasabah yang memiliki potensi gagal bayar, sehingga risiko kredit macet bisa diminimalisir dan menerima calon nasabah yang memiliki riwayat kredit lemah. 

# Business Insight
**Mengidentifikasi Risiko Kredit**
Objective: Meningkatkan akurasi prediksi dalam mengidentifikasi nasabah yang berisiko tinggi gagal bayar.
Key Results:
- Meningkatkan tingkat prediksi akurasi hingga 90% dalam model prediksi gagal bayar.
- Mengurangi tingkat kredit macet (non-performing loans) sebesar 20% dalam 12 bulan.
- Memperbaiki proses penilaian kredit dengan mempertimbangkan lebih banyak variabel prediktif (status pernikahan, jenis pekerjaan, pendapatan lain, riwayat kredit, tanggungan, demografis.

# Exploratory Data Analysis
Berdasarkan Hasil exploratory data analysis (EDA) yang telah kami lakukan, terdapat beberapa insight menarik. Nasabah yang paling banyak melakukan pinjaman antara alain adalah mereka yang berjenis kelamin wanita, tidak memiliki kendaraan namun memiliki properti yang berupa rumah / apartemen, berstatus keluarga sudah menikah dengan jumlah anggota keluarga yaitu dua orang dan tidak memiliki anak. 

Kemudian, berdasarkan status pendapatan yaitu dari bekerja dengan total pendapatan di sekitar 90.000 - 180.000 dan posisi sebagai buruh (Laborers). berdasarkan tipe organisasi tempat mereka bekerja, banyak dari mereka bekerja disebuah perusahaan, disusul dengan mereka yang self-employed. Secara usia, rata - rata nasabah yang melakukan pinjaman berada di kelompok usia 40-an dan juga sebagai kelompok yang capable untuk melakukan pembayaran tepat waktu. Selanjutnya, secara background pendidikan rata - rata nasabah yang melakukan pinjaman paling banyak adalah secondary / secondary special.

# Data Preprocessing
Pada data ini, terdapat ... dataset yang akan kami uji untuk melakukan model machine learning classification pada label "TARGET". 

## Handling Null Value

### Application Train Test
Pada application Train dan Test, langkah pertama yang kami lakukan adalah melakukan handling null value. Dari 307.511 data rows, terdapat 67 features yang memiliki null value. Feature COMMONAREA_MODE, COMMONAREA_MODE_MEDI, COMMONAREA_MODE_AVG, NONLIVINGAPARTMENTS_MEDI, dan NONLIVINGAPARTMENTS_AVG menjadi top 5 features yang memiliki null value tertinggi, yaitu sekitar 69%. Penanganan yang kami lakukan adalah melakukan drop semua null value karena apabila kami mengubah null value menjadi median (karena lebih robust) atau modus, ditakutkan akan mengubah keseluruhan bentuk data yang dapat menyebabkan misinterpretasi data. 
 
### Bureau & Bureau_Balance Merge Dataset
Sedangkan data merger Bureau dan Bureau_Balance (yang sudah include label "TARGET" dari application_train), memiliki jumlah total 25.121.815 rows data. Kami melakukan drop null value untuk data yang memiliki null value di atas 5%, antara lain AMT_ANNUITY dan AMT_CREDIT_SUM_DEBT. Untuk data null value yang berada dibawah 5% seperti MONTHS_BALANCE, STATUS, dan AMT_CREDIT_SUM diubah menjadi nilai median untuk data numerical (karena lebih robust terhadap outliers) dan nilai modus untuk data categorical (karena menambahkan null value ke value yang paling sering muncul tidak akan mengubah keseluruhan data secara signifikan). Jumlah total rows data setelah handling value pada dataset merger Bureau & Bureau_balance menjadi 12.051.047 data.

## Handling Duplicated

### Application Train Test
Pada application Train dan Test tidak ditemukan adanya data duplikat sehingga tidak ada penanganan lebih lanjut unutk handling duplicated data.

### Bureau & Bureau_Balance Merge Dataset
Pada data merge Bureau ini, terdapat 4.919 data duplikat sehingga kami memutuskan untuk membuang data duplikat tersebut. Namun, saat kami mengetest cek data duplikat setelah drop SK_ID_CURR (primary key), terdapat 3.640 data duplikat sehingga dilakukan drop duplicated data dan sisa data rows yang digunakan adalah sebesar 12.047.407.

## Handling Outliers & Feature Transformation

## Application Train test
Sebelum menangani data outliers, kami membagi variable ke dalam X_train, X_test, dan y_train. Hal ini dilakukan agar data yang dilakukan handling outliers itu hanya X_train saja agar model machine learning bisa mempelajari data terlebih dahulu agar menghasilkan output yang best fit dan bisa membedakan customer yang default dan tidak. Terdapat banyak outliers yang dibuang menggunakan z-score dan IQR, lalu sisanya outliers yang masih dianggap masuk akal (data outliers masih diterima) langsung dilakukan outliers. Pada Feature transformation ini, kami melakukan yeojohnson untuk setiap feature yang skewed karena yeojohnson merupakan metode lanjutan dari boxcox yang mampu melakukan transformasi untuk data yang positif dan negatif (pada application_train | test dan Bureau & Bureau_balance terdapat features ber-value negatif). Selain yeojohnson, kami juga menggunakan log transformation untuk feature yang tidak bisa dilakukan metode yeojohnson. Namun, untuk data yang tetap tidak terdistribusi normal akan dilakukan Standardization (StandarScaler).

## Bureau & Bureau_Balance Merge Dataset
pada Bureau & Bureau_Balance merge Dataset juga memiliki perlakukan transformation yang sama dengan application_tain | test, yaitu menggunakan metode yeojohnson, log transformation, dan Standardization.

## Feature Encoding

### Application Train Test
Terdapat 16 features yang bersifat categorical. Pada application_train | test ini akan dilakukan label encoding dan One-Hot-Encoding. Feature yang dilakukan label encoding antara lain: CODE_GENDER, FLAG_OWN_CAR, FLAG_OWN_REALTY, NAME_EDUCATION_TYPE dan EMERGENCYSTATE_MODE karena feature tersebut memiliki identitas yang bersifat 2 distinct values dan ordinal. Sisanya dilakukan One-Hot-Encoding karena tidak memenuhi criteria label encoding.

### Bureau & Bureau_Balance Merge Dataset
Terdapat 4 Features categorical dan semua feature tersebut tidak memiliki 2 value atau bersifat ordinal sehingga penanganan feature encoding menggunakan One-Hot-Encoding karena selain mengubah feature categorical menjadi numeric, OHE dapat menghindari masalah urutan (ordinal) yang tidak diinginkan pada data categorical dan mempertahankan informasi kategorikal tanpa membuat asumsi tentang hubungan antar kategori. CREDIT_ACTIVE, CREDIT_TYPE, STATUS, dan CREDIT_CURRENCY dilakukan One-Hot-Encoding dan kini jumlah features menjadi 25 Features dan siap untuk dilakukan proses modelling machine learning.

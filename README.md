# Default-Risk-HomeCredit
Implementasi Machine Learning untuk Memprediksi Default Risk di HomeCredit

Datasets are from this kaggle: https://www.kaggle.com/competitions/home-credit-default-risk

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
Pada data ini, terdapat 8 dataset yang akan kami uji untuk melakukan model machine learning classification pada label "TARGET". Kami mengubah missing value di atas 60% dengan drop feature tersebut karena tidak terlalu memberikan banyak insight dan mengubah missing value di bawah 60% ke dalam median dan modus untuk mencegah data - data penting yang terhapus. Tidak ada data duplikat di setiap dataset dan handling skewness menggunakan yeo-johnson karena mampu handling data - data yang memiliki skew negatif. Kami juga mmebuat feature engineering seperti debt_to_income ratio untuk melihat kemampuan nasabah dalam membayar pinjaman dilihat dari pendapatan mereka. Kami menggabungkan seluruh dataset ke dalam application_train untuk pengujian model.

# Modelling
Kami menggunakan logistic regression, decision tree, random forest, ada boost, dan xgboost. Pada logistic regression kami lakukan standardisasi karena logistic regression sangat sensitif terhadap perbedaan skala dan outliers. Kami tidak banyak melakukan hyperparameter tuning karena banyaknya data dan kapasitas komputer yang tidak kuat untuk menjalankan model. Metrics yang kami gunakan adalah ROC AUC dan Recall. ROC AUC mampu membedakan mana kelas yang positif dan negatif, mengingat label memiliki imbalance class yang extreme. Lalu, Recall digunakan karena tujuan prediksi ini yaitu mengurangi jumlah nasabah yang berpotensi gagal bayar sehingga model diharapkan mampu menolak nasabah - nasabah yang berpotensi gagal bayar.

# Model Result
Kami memilih logistic regression karena memberikan performa yang baik, yaitu ROC_AUC sebesar 0.74 dan Recall dengan score 0.66.

# Business Recommendation
Berdasarkan feature importance AMT_GOODS_PRICE, EXT_SOURCE_MEAN, dan DEBT_TO_INCOME memiliki korelasi yang kuat dengan label. Sehingga, rekomendasi yang kami buat antara lain:
- penilaian bobot score lebih memberatkan pada jenis barang yang dibeli menggunakan pinjaman Home Credit (AMT_GOODS_PRICE), data - data external nasabah / peminjam (EXT_SOURCE_MEAN), dan perbandingan pendapatan dan jumlah pinjaman yang diminta nasabah (DEBT_TO_INCOME).
- Mengembangkan risk-based pricing untuk menentukan suku bunga berdasarkan customer risk.
- Melakukan monitoring untuk melihat default rate dan profit margins setiap 4 bulan (quarters).
- Menerapkan sistem auto reminders untuk mencegah nasabah yang lupa bayar dan early detection and warning untuk nasabah yang sering telat bayar paling minimal 3 kali.

# Eksplorasi KNIME

Pada tugas ini, saya melakukan eksplorasi di knime, dengan menggunakan DB tradisional dan Hive, serta dilakukan pengecekan melalui DBClient (DBeaver).

# Apa yang dibutuhkan:
1. KNIME
2. DBClient (Saya menggunakan DBeaver)

# Tugas 1_DB/2_Exercise
Sebelum mengerjakan latihan, saya melakukan rename dari tabel di sqlite, dengan menggunakan DBeaver,
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/rename/renamed-table.png)

Diatas adalah beberapa tabel yang akan kita pakai di tahap selanjutnya.
1. DB Connect
Koneksi DB dilakukan dengan SQLite DB Connector, dengan konfigurasi berikut:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/1/sqlite-connect.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/1/sqlite-connect-config.png)

Melakukan select table 05111740000026.ss13pme
Select table dilakukan dengan DB Table Selector, dengan konfigurasi sebagai berikut:

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/1/select-ss13pme.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/1/select-ss13pme-config.png)

Melakukan import data
Import data ke KNIME, dengan DB Reader, agar bisa diproses data di databasenya lewat KNIME.

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/1/import-ss13pme.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/1/imported-data.png)

2. DB_InDB_Processing<br>
2.1 Melakukan join ss13hme dan ss13pme dengan acuan serialno, serta memfilter kolom PUMA* dan PWGTP*
Melakukan filter kolom PUMA* dan PWGTP*
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/filter-kolom-puma.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/filter-kolom-puma-config.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/filter-kolom-puma-pwgtp-ss13pme.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/filter-kolom-puma-pwgtp-ss13pme-config.png)

Melakukan join
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/join-kolom-filtered.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/join-kolom-filtered-config.png)

Melakukan import data
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/import-data.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/1/imported-data.png)

2.2 Filter row yang mempunyai nilai NULL pada kolom COW
Melakukan konfiurasi pada DB row filter
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/2/filter-config.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/2/hasil%20akhir.png)

Melakukan import data
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/2/import-data.png)

2.3 Filter row yang mempunyai nilai NOT NULL pada kolom COW
Melakukan konfiurasi pada DB row filter
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/3/conifg-filter.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/3/hasil-akhir.png)

Melakukan import data
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/3/import%20data.png)

2.4 Menghitung rata-rata AGEP
Melakukan konfigurasi pada DBGroupBy:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/4/hasil-akhir.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/4/config-1.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/4/config-2.png)

Melakukan import data
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/4/imported-data.png)

2.5 Descending sort data dengan acuan kolom AGEP, dan limit menjadi 10 baris
Melakukan beberapa konfigurasi
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/5/hasil-akhir.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/5/sort-config.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/5/limit-config.png)

Melakukan import data
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/2/5/imported-data.png)

3. DB Modelling
Melakukan modelling pada data, dengan cara mengisi nilai cow yang null tadi dengan nilai prediksi dengan decision tree yang dikonfigurasi

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/3/hasil-akhir.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/3/tree-config.png)

Berikut adalah tree yang dihasilkan dari learningnya:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/3/tree.png)

Data hasil prediksi
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/3/predicted-cow-data.png)

4. DB WritingToDB
Setelah melakukan training dan mendapatkan value dari kolom COW melalui learning, lalu kita masukkan ke database, seperti berikut:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/4/hasil-akhir.png)

Melakukan konfigurasi DB Update, untuk memasukkan value COW ke value yang COW is NULL
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/4/db-update-config.png)

Melakukan konfigurasi DB Writer, untuk mencatat waktu
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/4/db-writer-config.png)

Setelah update DB, maka lakukan pengecekan dengan Row Filter, dengan konfigurasi berikut:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/4/filter-config.png)

Dimana sukses jika bernilai 1 pada kolom updateStatus:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/1_DB/4/data-update-status.png)

# Tugas 2_Hadoop/2_Exercise
Melakukan install environment big data, dengan menjalankan workspace berikut:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/setup-hadoop.png)

Rename table
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/rename-ss13pme.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/rename-ss13hme.png)

Setelah environment hive terinstall, lakukan koneksi dengan hive DB, melalui DBClient. Disini saya gunakan DBeaver, berikut konfigurasinya

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/hive-config-to-connect.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/connect-dbeaver-config.png)

Lakukan pengecekan dengan men-query table ss13pme dan ss13hme:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/select-ss13pme.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/0/select-ss13hme.png)

Setelah query berhasil dilakukan, maka koneksi ke hiveDB selesai.

1. Hive-modelling
Sama dengan yang tugas 1_DB tadi, kita buat modelling dengan melakukan train dari kolom COW, untuk mendapatkan nilai COW. Bedanya, kita melakukan modelling dari hiveDB (environment big data), sehingga setup connection databasenya berbeda.

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/1/hasil%20akhir.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/1/config-hive.png)

Berikut hasil dari learning tree:

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/1/tree.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/1/predicted.png)

2. Hive WritingToDB
Setelah mendapatkan hasil learningnya, saya rebuild datasetnya dengan predicted value dari COW column:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/2/hasil-akhir.png)

Beberapa konfigurasi:
DB Table Creator (membuat table baru, berisi data dengan dataset yang sudah diprediksi dengan decision tree):

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/2/new-table-config.png)

DB Loader (meload table):

![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/2/db-loader-config.png)

Create HDFS PATH dan temp Dir (untuk menyimpan table dalam hiveDB) :
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/2/create-path-config.png)
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/2/temp-dir-config.png)

Lalu, saya bisa mengakses table baru tersebut, 05111740000026_newTable, dengan DBeaver:
![alt](https://github.com/hisamwp/tugas2-bigdata/blob/master/2_Hadoop/2/data-from-dbeaver.png)

Sekian dari saya, terima kasih.


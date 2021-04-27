<p align="justify"><b>Customer segmentation</b> adalah proses penting yang diperlukan di bisnis untuk mengenal customer dengan lebih baik.
Dengan demikian proses bisnis di marketing (pemasaran) dan CRM (customer relationship management) bisa dilakukan lebih tajam. <b>Contoh: </b> pesan marketing bisa lebih personal untuk setiap segment dengan biaya lebih optimal. Dengan proses yang lebih tajam, performa bisnis berpotensi tinggi menjadi lebih baik juga.
Untuk menemukan segmentasi yang baik, perlu proses analisa data dari profile customer yang cukup banyak dan rutin. Ini bisa dibantu dengan algoritma komputer.</p>
<p align="justify"><b>Persiapan data</b> adalah langkah pertama yang kita lakukan sebelum menggunakan algoritma apapun untuk melakukan analisa data.</br>
Ini dikarenakan tiap implementasi algoritma menuntut struktur dan tipe data yang berbeda.</br>
Dan untuk kasus algoritma K-Means yang akan kita gunakan untuk otomatisasi clustering, maka struktur datanya adalah data.frame atau matrix yang di dalamnya berisi angka semua. Tidak ada yang boleh bertipe karakter.
</p>
<p align="justify">Namun pada kasus riil, hal ini tentulah tidak mungkin. Contoh, isi data profesi seperti "Professional", "Ibu Rumah Tangga" adalah teks. Dan ini perlu dikonversi dulu ke numerik, namun jika diperlukan tetap bisa kembali mengambil data teks.
</br></br>
Nah, untuk lebih jelasnya. Kita akan lakukan langkah-langkah praktek yang akan kita lakukan berikut ini adalah untuk mempersiapkan data sebelum dapat digunakan algoritma clustering:</p>
<ol align="justify">
<li>Mengenal Contoh File Dataset Pelanggan</li>
<li>Membaca File dengan read.csv</li>
<li>Vector untuk Menyimpan Nama Field</li>
<li>Konversi Data dengan data.matrix</li>
<li>Menggabungkan Hasil Konversi</li>
<li>Menormalisasikan Nilai Belanja</li>
<li>Membuat Data Master</li></ol>

#### Membaca data dengan fungsi read.csv

```{r}
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan
pelanggan[c("Nama.Pelanggan","Profesi")]
pelanggan[c("Jenis.Kelamin", "Umur", "Profesi", "Tipe.Residen")]
```

```{r}
Output : 


   Jenis.Kelamin  Umur         Profesi   Tipe.Residen
1           Pria   58       Wiraswasta       Sector
2         Wanita   14          Pelajar      Cluster
3           Pria   48     Professional      Cluster
4           Pria   53     Professional      Cluster
5         Wanita   41       Wiraswasta      Cluster
6         Wanita   24     Professional      Cluster
7           Pria   64       Wiraswasta       Sector
8           Pria   52     Professional      Cluster
9         Wanita   29     Professional       Sector
10          Pria   33     Professional      Cluster
11        Wanita   50     Professional       Sector
12        Wanita   49     Professional       Sector
13        Wanita   64       Wiraswasta      Cluster
14          Pria   60       Wiraswasta      Cluster
15        Wanita   20       Wiraswasta      Cluster
16          Pria   35     Professional      Cluster
17        Wanita   32 Ibu Rumah Tangga      Cluster
18        Wanita   63 Ibu Rumah Tangga      Cluster
19        Wanita   32       Wiraswasta      Cluster
20        Wanita   16          Pelajar       Sector
21        Wanita   38       Wiraswasta      Cluster
22        Wanita   52     Professional      Cluster
23          Pria   34     Professional      Cluster
24        Wanita   39       Wiraswasta      Cluster
25        Wanita   29       Wiraswasta       Sector
26        Wanita   55     Professional      Cluster
27        Wanita   35       Wiraswasta      Cluster
28        Wanita   40 Ibu Rumah Tangga      Cluster
29        Wanita   56     Professional      Cluster
30        Wanita   46 Ibu Rumah Tangga       Sector
31        Wanita   19        Mahasiswa      Cluster
32        Wanita   47       Wiraswasta       Sector
33        Wanita   19        Mahasiswa      Cluster
34        Wanita   21       Wiraswasta       Sector
35        Wanita   39     Professional       Sector
36        Wanita   30       Wiraswasta      Cluster
37        Wanita   25     Professional       Sector
38        Wanita   46       Wiraswasta       Sector
39        Wanita   20     Professional      Cluster
40        Wanita   14          Pelajar       Sector
41        Wanita   24 Ibu Rumah Tangga      Cluster
42        Wanita   26       Wiraswasta      Cluster
43        Wanita   31     Professional      Cluster
44        Wanita   18       Wiraswasta      Cluster
45        Wanita   22     Professional      Cluster
46        Wanita   25       Wiraswasta       Sector
47        Wanita   55 Ibu Rumah Tangga      Cluster
48        Wanita   45       Wiraswasta       Sector
49        Wanita   33 Ibu Rumah Tangga       Sector
50        Wanita   55       Wiraswasta       Sector 
```

<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>
#Membaca data csv dan dimasukkan ke variable pelanggan</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt",sep="\t")</br>
#Buat variable field_yang_digunakan dengan isi berupa vector "Jenis.Kelamin", "Umur" dan "Profesi"</br>
field_yang_digunakan <- c("Jenis.Kelamin","Umur","Profesi")</br>
#Tampilan data pelanggan dengan nama kolom sesuai isi vector field_yang_digunakan</br>
pelanggan[field_yang_digunakan]</summary>
  <table border="0"><tr><td>  Jenis.Kelamin Umur          Profesi</br>
1           Pria   58       Wiraswasta</br>
2         Wanita   14          Pelajar</br>
3           Pria   48     Professional</br>
4           Pria   53     Professional</br>
5         Wanita   41       Wiraswasta</br>
6         Wanita   24     Professional</br>
7           Pria   64       Wiraswasta</br>
8           Pria   52     Professional</br>
9         Wanita   29     Professional</br>
10          Pria   33     Professional</br>
11        Wanita   50     Professional</br>
12        Wanita   49     Professional</br>
13        Wanita   64       Wiraswasta</br>
14          Pria   60       Wiraswasta</br>
15        Wanita   20       Wiraswasta</br>
16          Pria   35     Professional</br>
17        Wanita   32 Ibu Rumah Tangga</br>
18        Wanita   63 Ibu Rumah Tangga</br>
19        Wanita   32       Wiraswasta</br>
20        Wanita   16          Pelajar</br>
21        Wanita   38       Wiraswasta</br>
22        Wanita   52     Professional</br>
23          Pria   34     Professional</br>
24        Wanita   39       Wiraswasta</br>
25        Wanita   29       Wiraswasta</br>
26        Wanita   55     Professional</br>
27        Wanita   35       Wiraswasta</br>
28        Wanita   40 Ibu Rumah Tangga</br>
29        Wanita   56     Professional</br>
30        Wanita   46 Ibu Rumah Tangga</br>
31        Wanita   19        Mahasiswa</br>
32        Wanita   47       Wiraswasta</br>
33        Wanita   19        Mahasiswa</br>
34        Wanita   21       Wiraswasta</br>
35        Wanita   39     Professional</br>
36        Wanita   30       Wiraswasta</br>
37        Wanita   25     Professional</br>
38        Wanita   46       Wiraswasta</br>
39        Wanita   20     Professional</br>
40        Wanita   14          Pelajar</br>
41        Wanita   24 Ibu Rumah Tangga</br>
42        Wanita   26       Wiraswasta</br>
43        Wanita   31     Professional</br>
44        Wanita   18       Wiraswasta</br>
45        Wanita   22     Professional</br>
46        Wanita   25       Wiraswasta</br>
47        Wanita   55 Ibu Rumah Tangga</br>
48        Wanita   45       Wiraswasta</br>
49        Wanita   33 Ibu Rumah Tangga</br>
50        Wanita   55       Wiraswasta</td></tr></table>
</details>

<details>
  <summary><b>Konversi Data dengan data.matrix </b></br>pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt",sep="\t")</br>
#Konversi data menjadi numerik</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/1.png"> alt="Trulli" width="500" height="333"></td></tr></table>
</details>

<details>
  <summary><b>Menggabungkan Hasil Konversi </b></br>pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt",sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
#Penggabungan data</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
#Tampilkan kembali data hasil penggabungan</br>
pelanggan</summary>
  <table border="0"><tr><td>   Customer_ID        Nama.Pelanggan Jenis.Kelamin Umur          Profesi</br>
1     CUST-001          Budi Anggara          Pria   58       Wiraswasta</br>
2     CUST-002      Shirley Ratuwati        Wanita   14          Pelajar</br>
3     CUST-003          Agus Cahyono          Pria   48     Professional</br>
4     CUST-004      Antonius Winarta          Pria   53     Professional</br>
5     CUST-005   Ibu Sri Wahyuni, IR        Wanita   41       Wiraswasta</br>
6     CUST-006       Rosalina Kurnia        Wanita   24     Professional</br>
7     CUST-007         Cahyono, Agus          Pria   64       Wiraswasta</br>
8     CUST-008        Danang Santosa          Pria   52     Professional</br>
9     CUST-009 Elisabeth Suryadinata        Wanita   29     Professional</br>
10    CUST-010        Mario Setiawan          Pria   33     Professional</br>
11    CUST-011        Maria Suryawan        Wanita   50     Professional</br>
12    CUST-012       Erliana Widjaja        Wanita   49     Professional</br>
13    CUST-013          Cahaya Putri        Wanita   64       Wiraswasta</br>
14    CUST-014        Mario Setiawan          Pria   60       Wiraswasta</br>
15    CUST-015      Shirley Ratuwati        Wanita   20       Wiraswasta</br>
16    CUST-016          Bambang Rudi          Pria   35     Professional</br>
17    CUST-017             Yuni Sari        Wanita   32 Ibu Rumah Tangga</br>
18    CUST-018           Nelly Halim        Wanita   63 Ibu Rumah Tangga</br>
19    CUST-019          Mega Pranoto        Wanita   32       Wiraswasta</br>
20    CUST-020        Irene Novianto        Wanita   16          Pelajar</br>
21    CUST-021      Lestari Fabianto        Wanita   38       Wiraswasta</br>
22    CUST-022          Novita Purba        Wanita   52     Professional</br>
23    CUST-023       Denny Amiruddin          Pria   34     Professional</br>
24    CUST-024         Putri Ginting        Wanita   39       Wiraswasta</br>
25    CUST-025        Julia Setiawan        Wanita   29       Wiraswasta</br>
26    CUST-026     Christine Winarto        Wanita   55     Professional</br>
27    CUST-027         Grace Mulyati        Wanita   35       Wiraswasta</br>
28    CUST-028         Adeline Huang        Wanita   40 Ibu Rumah Tangga</br>
29    CUST-029          Tia Hartanti        Wanita   56     Professional</br>
30    CUST-030        Rosita Saragih        Wanita   46 Ibu Rumah Tangga</br>
31    CUST-031         Eviana Handry        Wanita   19        Mahasiswa</br>
32    CUST-032       Chintya Winarni        Wanita   47       Wiraswasta</br>
33    CUST-033       Cecilia Kusnadi        Wanita   19        Mahasiswa</br>
34    CUST-034        Deasy Arisandi        Wanita   21       Wiraswasta</br>
35    CUST-035               Ida Ayu        Wanita   39     Professional</br>
36    CUST-036        Ni Made Suasti        Wanita   30       Wiraswasta</br>
37    CUST-037      Felicia Tandiono        Wanita   25     Professional</br>
38    CUST-038          Agatha Salim        Wanita   46       Wiraswasta</br>
39    CUST-039          Gina Hidayat        Wanita   20     Professional</br>
40    CUST-040        Irene Darmawan        Wanita   14          Pelajar</br>
41    CUST-041      Shinta Aritonang        Wanita   24 Ibu Rumah Tangga</br>
42    CUST-042          Yuliana Wati        Wanita   26       Wiraswasta</br>
43    CUST-043          Yenna Sumadi        Wanita   31     Professional</br>
44    CUST-044                  Anna        Wanita   18       Wiraswasta</br>
45    CUST-045        Rismawati Juni        Wanita   22     Professional</br>
46    CUST-046          Elfira Surya        Wanita   25       Wiraswasta</br>
47    CUST-047           Mira Kurnia        Wanita   55 Ibu Rumah Tangga</br>
48    CUST-048      Maria Hutagalung        Wanita   45       Wiraswasta</br>
49    CUST-049       Josephine Wahab        Wanita   33 Ibu Rumah Tangga</br>
50    CUST-050        Lianna Nugraha        Wanita   55       Wiraswasta</br>
   Tipe.Residen NilaiBelanjaSetahun Jenis.Kelamin.1 Profesi.1 Tipe.Residen.1</br>
1        Sector             9497927               1         5              2</br>
2       Cluster             2722700               2         3              1</br>
3       Cluster             5286429               1         4              1</br>
4       Cluster             5204498               1         4              1</br>
5       Cluster            10615206               2         5              1</br>
6       Cluster             5215541               2         4              1</br>
7        Sector             9837260               1         5              2</br>
8       Cluster             5223569               1         4              1</br>
9        Sector             5993218               2         4              2</br>
10      Cluster             5257448               1         4              1</br>
11       Sector             5987367               2         4              2</br>
12       Sector             5941914               2         4              2</br>
13      Cluster             9333168               2         5              1</br>
14      Cluster             9471615               1         5              1</br>
15      Cluster            10365668               2         5              1</br>
16      Cluster             5262521               1         4              1</br>
17      Cluster             5677762               2         1              1</br>
18      Cluster             5340690               2         1              1</br>
19      Cluster            10884508               2         5              1</br>
20       Sector             2896845               2         3              2</br>
21      Cluster             9222070               2         5              1</br>
22      Cluster             5298157               2         4              1</br>
23      Cluster             5239290               1         4              1</br>
24      Cluster            10259572               2         5              1</br>
25       Sector            10721998               2         5              2</br>
26      Cluster             5269392               2         4              1</br>
27      Cluster             9114159               2         5              1</br>
28      Cluster             6631680               2         1              1</br>
29      Cluster             5271845               2         4              1</br>
30       Sector             5020976               2         1              2</br>
31      Cluster             3042773               2         2              1</br>
32       Sector            10663179               2         5              2</br>
33      Cluster             3047926               2         2              1</br>
34       Sector             9759822               2         5              2</br>
35       Sector             5962575               2         4              2</br>
36      Cluster             9678994               2         5              1</br>
37       Sector             5972787               2         4              2</br>
38       Sector            10477127               2         5              2</br>
39      Cluster             5257775               2         4              1</br>
40       Sector             2861855               2         3              2</br>
41      Cluster             6820976               2         1              1</br>
42      Cluster             9880607               2         5              1</br>
43      Cluster             5268410               2         4              1</br>
44      Cluster             9339737               2         5              1</br>
45      Cluster             5211041               2         4              1</br>
46       Sector            10099807               2         5              2</br>
47      Cluster             6130724               2         1              1</br>
48       Sector            10390732               2         5              2</br>
49       Sector             4992585               2         1              2</br>
50       Sector            10569316               2         5              2</td></tr></table>
</details>


<details>
  <summary><b>Menormalisasikan Nilai Belanja </b></br>pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
#Normalisasi Nilai</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</summary><table border="0"><tr><td>> #Normalisasi Nilai</br>
  > pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</td></tr></table>
</details>


<details>
  <summary><b>Membuat Data Master </b></br>pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt",sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
pelanggan$NilaiBelanjaSetahun = pelanggan$NilaiBelanjaSetahun/1000000</br>
#Mengisi data master</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Residen <- unique(pelanggan[c("Tipe.Residen"," Tipe.Residen.1")])</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar2.jpg"></td></tr></table>
</details>

<p align="justify"><b>Apa itu Clustering dan algoritma K-Means?</b></br></br><b>Clustering </b>adalah proses pembagian objek-objek ke dalam beberapa kelompok (cluster) berdasarkan tingkat kemiripan antara satu objek dengan yang lain.</br></p>
Beberapa contoh clustering:<ol><li>Pengelompokan manusia berdasarkan umur: bayi, balita, anak, remaja, dewasa, tua.</li>
<li>Pengelompokan customer berdasarkan daya belinya: regular dan premium.</li>
<li>Pengelompokan makanan berdasarkan kandungan gizinya: biji-bijian, sayuran, buah-buahan, minyak, protein, dan lain-lain.</li></ol>
<b>K-means</b> adalah algoritma yang membagi data menjadi sejumlah partisi dengan cara sederhana: mencari kedekatan dari tiap titik pada suatu cluster dengan sejumlah nilai rata-rata atau mean.
Ada dua konsep kunci yang juga menjadi nama asal k-means:<ol>
<li>Jumlah partisi yang diinginkan, diwakili oleh huruf k</li>
<li>Mencari "jarak" kedekatan tiap titik ke sejumlah nilai rata-rata cluster yang diamati, diwakili oleh means</li></ol>

Function kmeans memerlukan minimal 2 parameter, yaitu:<ol>
<li>x: data yang digunakan, dimana semua isi datanya harus berupa numerik.</li>
<li>centers: jumlah cluster yang diinginkan.</li></ol>



<details>
  <summary><b>x: berisi data pelanggan dengan field-field yang diambil dari vector field_yang_digunakan (sudah didefinisikan di potongan code)
    centers: jumlah segmen / cluster yang kita inginkan. Isi dengan 5.</br>
    nstart: isi dengan angka 25</b></br>#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
#fungsi kmeans untuk membentuk 5 cluster dengan 25 skenario random dan simpan ke dalam variable segmentasi</br>
segmentasi <- kmeans(x=field_yang_digunakan, centers=5, nstart=25)</br>
#tampilkan hasil k-means</br>
segmentasi</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar17.png"></td></tr></table>
</details>


<details>
  <summary><b>Analisa Hasil Cluster Size</b></br>#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)</br>
pelanggan$cluster <- segmentasi$cluster</br>
#Analisa hasil</br>
#Filter cluster ke-1</br>
which(pelanggan$cluster == 1)</br>
length(which(pelanggan$cluster == 2))</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar3.jpg"></td></tr></table>
</details>


<details>
  <summary><b>Melihat Data pada Cluster ke-N </b></br>#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)</br>
pelanggan$cluster <- segmentasi$cluster</br>
#Analisa hasil</br>
#Melihat data cluster ke-1</br>
pelanggan[which(pelanggan$cluster == 3),]</br>
pelanggan[which(pelanggan$cluster == 4),]</br>
pelanggan[which(pelanggan$cluster == 5),]</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar5.jpg"></td></tr></table>
</details>

<details>
  <summary><b>Analisa Hasil Cluster Means </b></br>Cluster means adalah hasil nilai rata-rata atau titik sentral (centroid) dari seluruh titik tiap cluster.</br>
#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)</br>
pelanggan$cluster <- segmentasi$cluster</br>
#Analisa hasil</br>
#Melihat cluster means dari objek</br>
segmentasi$centers</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_1.jpg"></td></tr></table>
</details>
<details>
  <summary><b>Analisa Hasil Sum of Squares </b></br>#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Membandingkan dengan 2 cluster kmeans, masing-masing 2 dan 5 set.seed(100)</br>
kmeans(x=pelanggan[field_yang_digunakan], centers=2, nstart=25)</br>
set.seed(100)</br>
kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25).</br>
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_2.jpg"></td></tr></table>
</details>

<details>
  <summary><b>Available Components</b></br>#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)</br>
segmentasi$withinss</br>
segmentasi$cluster</br>
segmentasi$tot.withinss
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_3.jpg"></td></tr></table>
</details>


<details>
  <summary><b>Simulasi Jumlah Cluster dan SS</b></br>
#Bagian Data Preparation</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <-pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
sse
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_4.jpg"></td></tr></table>
</details>



<details>
  <summary><b>Grafik Elbow Effect</b></br>library(ggplot2)
#Bagian Data Preparation</br>
pelanggan <- read.csv("https://storage.googleapis.com/dqlab-dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
#Bagian K-Means</br>
set.seed(100)</br>
sse <- sapply(1:10, function(param_k){kmeans(pelanggan[field_yang_digunakan], param_k, nstart=25)$tot.withinss})</br>
jumlah_cluster_max <- 10</br>
ssdata = data.frame(cluster=c(1:jumlah_cluster_max),sse)</br>
ggplot(ssdata, aes(x=cluster,y=sse)) + </br>
  	geom_line(color="red") + geom_point() + </br>
 	ylab("Within Cluster Sum of Squares") + xlab("Jumlah Cluster") +</br>
 	geom_text(aes(label=format(round(sse, 2), nsmall = 2)),hjust=-0.2, vjust=-0.5) +</br>
  scale_x_discrete(limits=c(1:jumlah_cluster_max))
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/elbow_effect.png"></td></tr></table>
</details>



<p align="justify"><b>Menamakan Segmen</b></br> #Lengkapi dengan dua vector bernama cluster dan Nama.Segmen </br>
Segmen.Pelanggan <- data.frame(cluster=c(1,2,3,4,5), Nama.Segmen=c("Silver Youth Gals", "Diamond Senior Member", "Gold Young Professional", "Diamond Professional", "Silver Mid Professional"))</p>


<details>
  <summary><b>Menggabungkan Referensi</b></br>#Membaca data csv dan dimasukkan ke variable pelanggan</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
pelanggan$NilaiBelanjaSetahun = pelanggan$NilaiBelanjaSetahun/1000000</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Residen <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
#Bagian K-Means</br>
set.seed(100)</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)</br>
Segmen.Pelanggan <- data.frame(cluster=c(1,2,3,4,5), Nama.Segmen=c("Silver Youth Gals", "Diamond Senior Member", "Gold Young Professional", "Diamond Professional", "Silver Mid Professional"))</br>
#Menggabungkan seluruh aset ke dalam variable Identitas.Cluster</br>
Identitas.Cluster <- list(Profesi=Profesi, Jenis.Kelamin=Jenis.Kelamin, Tipe.Residen=Tipe.Residen, Segmentasi=segmentasi, Segmen.Pelanggan=Segmen.Pelanggan, field_yang_digunakan=field_yang_digunakan)
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_5.jpg"></td></tr></table>
</details>



<p align="justify"><b>Menyimpan Objek dalam Bentuk File</b></br>#Membaca data csv dan dimasukkan ke variable pelanggan</br>
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])</br>
pelanggan <- data.frame(pelanggan, pelanggan_matrix)</br>
pelanggan$NilaiBelanjaSetahun = pelanggan$NilaiBelanjaSetahun/1000000</br>
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])</br>
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])</br>
Tipe.Residen <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])</br>
#Bagian K-Means</br>
set.seed(100)</br>
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")</br>
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)</br>
Segmen.Pelanggan <- data.frame(cluster=c(1,2,3,4,5), Nama.Segmen=c("Silver Youth Gals", "Diamond Senior Member", "Gold Young Professional", "Diamond Professional", "Silver Mid Professional"))</br>
Identitas.Cluster <- list(Profesi=Profesi, Jenis.Kelamin=Jenis.Kelamin, Tipe.Residen=Tipe.Residen, Segmentasi=segmentasi, Segmen.Pelanggan=Segmen.Pelanggan, field_yang_digunakan=field_yang_digunakan)</br>
saveRDS(Identitas.Cluster,"cluster.rds") </p>


<details>
  <summary align="justify"><b>Data Baru</b></br>databaru <- data.frame(Customer_ID="CUST-100", Nama.Pelanggan="Rudi Wilamar",Umur=20,Jenis.Kelamin="Wanita",Profesi="Pelajar",Tipe.Residen="Cluster",NilaiBelanjaSetahun=3.5) databaru
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_6.jpg"></td></tr></table>
</details>


<details>
  <summary><b>Memuat Objek Clustering dari File</b></br>Identitas.Cluster <- readRDS(file="cluster.rds") Identitas.Cluster
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_7.jpg"></td></tr></table>
</details>


<details>
  <summary><b>Merge dengan Data Referensi</b></br> databaru <- data.frame(Customer_ID="CUST-100", Nama.Pelanggan="Rudi Wilamar",Jenis.Kelamin="Wanita",Profesi="Pelajar",Tipe.Residen="Cluster",NilaiBelanjaSetahun=3.5)</br>
Identitas.Cluster <- readRDS(file="cluster.rds")</br>
#Masukkan perintah untuk penggabungan data</br>
databaru <- merge(databaru, Identitas.Cluster$Profesi)</br>
databaru <- merge(databaru, Identitas.Cluster$Jenis.Kelamin)</br>
databaru <- merge(databaru, Identitas.Cluster$Tipe.Residen)</br>
databaru
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_8.jpg"></td></tr></table>
</details>


<details>
  <summary><b>Menentukan Cluster</b></br> #membuat data bar </br>
databaru <- data.frame(Customer_ID="CUST-100", Nama.Pelanggan="Rudi Wilamar",Umur=32,Jenis.Kelamin="Wanita",Profesi="Pelajar",Tipe.Residen="Cluster",NilaiBelanjaSetahun=3.5)</br>
Identitas.Cluster <- readRDS(file="cluster.rds")</br>
databaru <- merge(databaru, Identitas.Cluster$Profesi)</br>
databaru <- merge(databaru, Identitas.Cluster$Jenis.Kelamin)</br>
databaru <- merge(databaru, Identitas.Cluster$Tipe.Residen)</br>
#menentukan data baru di cluster mana</br>
which.min(sapply( 1:5, function( x ) sum( ( databaru[Identitas.Cluster$field_yang_digunakan] - Identitas.Cluster$Segmentasi$centers[x,])^2 ) ))</br>
Identitas.Cluster$Segmen.Pelanggan[which.min(sapply( 1:5, function( x ) sum( ( databaru[Identitas.Cluster$field_yang_digunakan] -Identitas.Cluster$Segmentasi$centers[x,])^2 ) )),]
</summary>
<table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_9.jpg"></td></tr></table>
</details>





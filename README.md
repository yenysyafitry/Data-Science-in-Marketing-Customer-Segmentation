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

<p align="justify"><b>Output :</b></p>

```{r}
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

<p align="justify"><b>Vector untuk Menyimpan Nama Field </b></p>

```{r}
# Membaca data csv dan dimasukkan ke variable pelanggan
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
# Buat variable field_yang_digunakan dengan isi berupa vector "Jenis.Kelamin", "Umur" dan "Profesi"
field_yang_digunakan <- c("Jenis.Kelamin", "Umur", "Profesi")
# Tampilan data pelanggan dengan nama kolom sesuai isi vector field_yang_digunakan
pelanggan[field_yang_digunakan]
```

<p align="justify"><b>Output :</b></p>

```{r}
    Jenis.Kelamin Umur          Profesi
1           Pria   58       Wiraswasta
2         Wanita   14          Pelajar
3           Pria   48     Professional
4           Pria   53     Professional
5         Wanita   41       Wiraswasta
6         Wanita   24     Professional
7           Pria   64       Wiraswasta
8           Pria   52     Professional
9         Wanita   29     Professional
10          Pria   33     Professional
11        Wanita   50     Professional
12        Wanita   49     Professional
13        Wanita   64       Wiraswasta
14          Pria   60       Wiraswasta
15        Wanita   20       Wiraswasta
16          Pria   35     Professional
17        Wanita   32 Ibu Rumah Tangga
18        Wanita   63 Ibu Rumah Tangga
19        Wanita   32       Wiraswasta
20        Wanita   16          Pelajar
21        Wanita   38       Wiraswasta
22        Wanita   52     Professional
23          Pria   34     Professional
24        Wanita   39       Wiraswasta
25        Wanita   29       Wiraswasta
26        Wanita   55     Professional
27        Wanita   35       Wiraswasta
28        Wanita   40 Ibu Rumah Tangga
29        Wanita   56     Professional
30        Wanita   46 Ibu Rumah Tangga
31        Wanita   19        Mahasiswa
32        Wanita   47       Wiraswasta
33        Wanita   19        Mahasiswa
34        Wanita   21       Wiraswasta
35        Wanita   39     Professional
36        Wanita   30       Wiraswasta
37        Wanita   25     Professional
38        Wanita   46       Wiraswasta
39        Wanita   20     Professional
40        Wanita   14          Pelajar
41        Wanita   24 Ibu Rumah Tangga
42        Wanita   26       Wiraswasta
43        Wanita   31     Professional
44        Wanita   18       Wiraswasta
45        Wanita   22     Professional
46        Wanita   25       Wiraswasta
47        Wanita   55 Ibu Rumah Tangga
48        Wanita   45       Wiraswasta
49        Wanita   33 Ibu Rumah Tangga
50        Wanita   55       Wiraswasta  
```


<p align="justify"><b>Konversi Data dengan data.matrix </b></p>

```{r}
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/1.png"></p>

<p align="justify"><b>Menggabungkan Hasil Konversi </b></p>

```{r}
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt",sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
# Penggabungan data
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
# Tampilkan kembali data hasil penggabungan
pelanggan
```

<p align="justify"><b>Output :</b></p>

```{r}
  Customer_ID        Nama.Pelanggan Jenis.Kelamin Umur          Profesi
1     CUST-001          Budi Anggara          Pria   58       Wiraswasta
2     CUST-002      Shirley Ratuwati        Wanita   14          Pelajar
3     CUST-003          Agus Cahyono          Pria   48     Professional
4     CUST-004      Antonius Winarta          Pria   53     Professional
5     CUST-005   Ibu Sri Wahyuni, IR        Wanita   41       Wiraswasta
6     CUST-006       Rosalina Kurnia        Wanita   24     Professional
7     CUST-007         Cahyono, Agus          Pria   64       Wiraswasta
8     CUST-008        Danang Santosa          Pria   52     Professional
9     CUST-009 Elisabeth Suryadinata        Wanita   29     Professional
10    CUST-010        Mario Setiawan          Pria   33     Professional
11    CUST-011        Maria Suryawan        Wanita   50     Professional
12    CUST-012       Erliana Widjaja        Wanita   49     Professional
13    CUST-013          Cahaya Putri        Wanita   64       Wiraswasta
14    CUST-014        Mario Setiawan          Pria   60       Wiraswasta
15    CUST-015      Shirley Ratuwati        Wanita   20       Wiraswasta
16    CUST-016          Bambang Rudi          Pria   35     Professional
17    CUST-017             Yuni Sari        Wanita   32 Ibu Rumah Tangga
18    CUST-018           Nelly Halim        Wanita   63 Ibu Rumah Tangga
19    CUST-019          Mega Pranoto        Wanita   32       Wiraswasta
20    CUST-020        Irene Novianto        Wanita   16          Pelajar
21    CUST-021      Lestari Fabianto        Wanita   38       Wiraswasta
22    CUST-022          Novita Purba        Wanita   52     Professional
23    CUST-023       Denny Amiruddin          Pria   34     Professional
24    CUST-024         Putri Ginting        Wanita   39       Wiraswasta
25    CUST-025        Julia Setiawan        Wanita   29       Wiraswasta
26    CUST-026     Christine Winarto        Wanita   55     Professional
27    CUST-027         Grace Mulyati        Wanita   35       Wiraswasta
28    CUST-028         Adeline Huang        Wanita   40 Ibu Rumah Tangga
29    CUST-029          Tia Hartanti        Wanita   56     Professional
30    CUST-030        Rosita Saragih        Wanita   46 Ibu Rumah Tangga
31    CUST-031         Eviana Handry        Wanita   19        Mahasiswa
32    CUST-032       Chintya Winarni        Wanita   47       Wiraswasta
33    CUST-033       Cecilia Kusnadi        Wanita   19        Mahasiswa
34    CUST-034        Deasy Arisandi        Wanita   21       Wiraswasta
35    CUST-035               Ida Ayu        Wanita   39     Professional
36    CUST-036        Ni Made Suasti        Wanita   30       Wiraswasta
37    CUST-037      Felicia Tandiono        Wanita   25     Professional
38    CUST-038          Agatha Salim        Wanita   46       Wiraswasta
39    CUST-039          Gina Hidayat        Wanita   20     Professional
40    CUST-040        Irene Darmawan        Wanita   14          Pelajar
41    CUST-041      Shinta Aritonang        Wanita   24 Ibu Rumah Tangga
42    CUST-042          Yuliana Wati        Wanita   26       Wiraswasta
43    CUST-043          Yenna Sumadi        Wanita   31     Professional
44    CUST-044                  Anna        Wanita   18       Wiraswasta
45    CUST-045        Rismawati Juni        Wanita   22     Professional
46    CUST-046          Elfira Surya        Wanita   25       Wiraswasta
47    CUST-047           Mira Kurnia        Wanita   55 Ibu Rumah Tangga
48    CUST-048      Maria Hutagalung        Wanita   45       Wiraswasta
49    CUST-049       Josephine Wahab        Wanita   33 Ibu Rumah Tangga
50    CUST-050        Lianna Nugraha        Wanita   55       Wiraswasta

    Tipe.Residen  NilaiBelanjaSetahun   Jenis.Kelamin.1   Profesi.1    Tipe.Residen.1
1        Sector             9497927               1         5              2
2       Cluster             2722700               2         3              1
3       Cluster             5286429               1         4              1
4       Cluster             5204498               1         4              1
5       Cluster            10615206               2         5              1
6       Cluster             5215541               2         4              1
7        Sector             9837260               1         5              2
8       Cluster             5223569               1         4              1
9        Sector             5993218               2         4              2
10      Cluster             5257448               1         4              1
11       Sector             5987367               2         4              2
12       Sector             5941914               2         4              2
13      Cluster             9333168               2         5              1
14      Cluster             9471615               1         5              1
15      Cluster            10365668               2         5              1
16      Cluster             5262521               1         4              1
17      Cluster             5677762               2         1              1
18      Cluster             5340690               2         1              1
19      Cluster            10884508               2         5              1
20       Sector             2896845               2         3              2
21      Cluster             9222070               2         5              1
22      Cluster             5298157               2         4              1
23      Cluster             5239290               1         4              1
24      Cluster            10259572               2         5              1
25       Sector            10721998               2         5              2
26      Cluster             5269392               2         4              1
27      Cluster             9114159               2         5              1
28      Cluster             6631680               2         1              1
29      Cluster             5271845               2         4              1
30       Sector             5020976               2         1              2
31      Cluster             3042773               2         2              1
32       Sector            10663179               2         5              2
33      Cluster             3047926               2         2              1
34       Sector             9759822               2         5              2
35       Sector             5962575               2         4              2
36      Cluster             9678994               2         5              1
37       Sector             5972787               2         4              2
38       Sector            10477127               2         5              2
39      Cluster             5257775               2         4              1
40       Sector             2861855               2         3              2
41      Cluster             6820976               2         1              1
42      Cluster             9880607               2         5              1
43      Cluster             5268410               2         4              1
44      Cluster             9339737               2         5              1
45      Cluster             5211041               2         4              1
46       Sector            10099807               2         5              2
47      Cluster             6130724               2         1              1
48       Sector            10390732               2         5              2
49       Sector             4992585               2         1              2
50       Sector            10569316               2         5              2
```

<p align="justify"><b>Menormalisasikan Nilai Belanja </b></p>

```{r}
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
# Normalisasi Nilai
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun / 1000000
```

<p align="justify"><b>Membuat Data Master</b></p>

```{r}
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Residen <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar2.jpg"></p>


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

<p align="justify"><b>Konversi Data dengan data.matrix </b></br>
x: berisi data pelanggan dengan field-field yang diambil dari vector field_yang_digunakan (sudah didefinisikan di potongan code)
centers: jumlah segmen / cluster yang kita inginkan. Isi dengan 5.
nstart: isi dengan angka 25</p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
#fungsi kmeans untuk membentuk 5 cluster dengan 25 skenario random dan simpan ke dalam variable segmentasi
segmentasi <- kmeans(x=field_yang_digunakan, centers=5, nstart=25)
#tampilkan hasil k-means
segmentasi
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar17.png"></p>


<p align="justify"><b>Analisa Hasil Cluster Size </b></p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)
pelanggan$cluster <- segmentasi$cluster
#Analisa hasil
#Filter cluster ke-1
which(pelanggan$cluster == 1)
length(which(pelanggan$cluster == 2))
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar3.jpg"></p>

<p align="justify"><b>Melihat Data pada Cluster ke-N  </b></p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)
pelanggan$cluster <- segmentasi$cluster
#Analisa hasil
#Melihat data cluster ke-1
pelanggan[which(pelanggan$cluster == 3),]
pelanggan[which(pelanggan$cluster == 4),]
pelanggan[which(pelanggan$cluster == 5),]
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/gambar5.jpg"></p>


<p align="justify"><b>Analisa Hasil Cluster Means </b></br>Cluster means adalah hasil nilai rata-rata atau titik sentral (centroid) dari seluruh titik tiap cluster</p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)
pelanggan$cluster <- segmentasi$cluster
#Analisa hasil
#Melihat cluster means dari objek
segmentasi$centers
 ```
 
 <p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_1.jpg"></p>


  <p align="justify"><b>Analisa Hasil Sum of Squares </b></p>
 
 ```{r}
  #Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Membandingkan dengan 2 cluster kmeans, masing-masing 2 dan 5 set.seed(100)
kmeans(x=pelanggan[field_yang_digunakan], centers=2, nstart=25)
set.seed(100)
kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25).
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_2.jpg"></p>


<p align="justify"><b>Available Components</b></p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)
segmentasi$withinss
segmentasi$cluster
segmentasi$tot.withinss
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_3.jpg"></p>


<p align="justify"><b>Simulasi Jumlah Cluster dan SS</b></p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <-pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
sse
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_4.jpg"></p>

<p align="justify"><b>Grafik Elbow Effect</b></p>

```{r}
#Bagian Data Preparation
pelanggan <- read.csv("https://storage.googleapis.com/dqlab-dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Profesi <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
pelanggan$NilaiBelanjaSetahun <- pelanggan$NilaiBelanjaSetahun/1000000
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
#Bagian K-Means
set.seed(100)
sse <- sapply(1:10, function(param_k){kmeans(pelanggan[field_yang_digunakan], param_k, nstart=25)$tot.withinss})
jumlah_cluster_max <- 10
ssdata = data.frame(cluster=c(1:jumlah_cluster_max),sse)
ggplot(ssdata, aes(x=cluster,y=sse)) + 
  	geom_line(color="red") + geom_point() + 
 	ylab("Within Cluster Sum of Squares") + xlab("Jumlah Cluster") +
 	geom_text(aes(label=format(round(sse, 2), nsmall = 2)),hjust=-0.2, vjust=-0.5) +
  scale_x_discrete(limits=c(1:jumlah_cluster_max))
```



<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/elbow_effect.png"></p>


<p align="justify"><b>Menamakan Segmen</b></br> #Lengkapi dengan dua vector bernama cluster dan Nama.Segmen </br>
Segmen.Pelanggan <- data.frame(cluster=c(1,2,3,4,5), Nama.Segmen=c("Silver Youth Gals", "Diamond Senior Member", "Gold Young Professional", "Diamond Professional", "Silver Mid Professional"))</p>

<p align="justify"><b>Menggabungkan Referensi</b></p>

```{r}
#Membaca data csv dan dimasukkan ke variable pelanggan
pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")
pelanggan_matrix <- data.matrix(pelanggan[c("Jenis.Kelamin", "Profesi", "Tipe.Residen")])
pelanggan <- data.frame(pelanggan, pelanggan_matrix)
pelanggan$NilaiBelanjaSetahun = pelanggan$NilaiBelanjaSetahun/1000000
Profesi <- unique(pelanggan[c("Profesi","Profesi.1")])
Jenis.Kelamin <- unique(pelanggan[c("Jenis.Kelamin","Jenis.Kelamin.1")])
Tipe.Residen <- unique(pelanggan[c("Tipe.Residen","Tipe.Residen.1")])
#Bagian K-Means
set.seed(100)
field_yang_digunakan = c("Jenis.Kelamin.1", "Umur", "Profesi.1", "Tipe.Residen.1","NilaiBelanjaSetahun")
segmentasi <- kmeans(x=pelanggan[field_yang_digunakan], centers=5, nstart=25)
Segmen.Pelanggan <- data.frame(cluster=c(1,2,3,4,5), Nama.Segmen=c("Silver Youth Gals", "Diamond Senior Member", "Gold Young Professional", "Diamond Professional", "Silver Mid Professional"))
#Menggabungkan seluruh aset ke dalam variable Identitas.Cluster
Identitas.Cluster <- list(Profesi=Profesi, Jenis.Kelamin=Jenis.Kelamin, Tipe.Residen=Tipe.Residen, Segmentasi=segmentasi, Segmen.Pelanggan=Segmen.Pelanggan, field_yang_digunakan=field_yang_digunakan)
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_5.jpg"></p>


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


<p align="justify"><b>Data Baru</b></p>

```{r}
databaru <- data.frame(Customer_ID="CUST-100", 
Nama.Pelanggan="Rudi Wilamar",
Umur=20,
Jenis.Kelamin="Wanita",
Profesi="Pelajar",
Tipe.Residen="Cluster",
NilaiBelanjaSetahun=3.5) 
databaru
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_6.jpg"></p>


<p align="justify"><b>Memuat Objek Clustering dari File</b></p>

```{r}
Identitas.Cluster <- readRDS(file="cluster.rds")
Identitas.Cluster
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_7.jpg"></p>

<p align="justify"><b>Merge dengan Data Referensi</b></p>

```{r}
databaru <- data.frame(Customer_ID="CUST-100", 
                       Nama.Pelanggan="Rudi Wilamar",
                       Jenis.Kelamin="Wanita",
                       Profesi="Pelajar",
                       Tipe.Residen="Cluster",
                       NilaiBelanjaSetahun=3.5)
Identitas.Cluster <- readRDS(file="cluster.rds")
# Masukkan perintah untuk penggabungan data
databaru <- merge(databaru, Identitas.Cluster$Profesi)
databaru <- merge(databaru, Identitas.Cluster$Jenis.Kelamin)
databaru <- merge(databaru, Identitas.Cluster$Tipe.Residen)
databaru
```

<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_8.jpg"></p>


<p align="justify"><b>Menentukan Cluster </b></p>

```{r}
# membuat data baru
databaru <- data.frame(Customer_ID="CUST-100", 
                       Nama.Pelanggan="Rudi Wilamar",
                       Umur=32,
                       Jenis.Kelamin="Wanita",
                       Profesi="Pelajar",
                       Tipe.Residen="Cluster",
                       NilaiBelanjaSetahun=3.5)
Identitas.Cluster <- readRDS(file="cluster.rds")
databaru <- merge(databaru, Identitas.Cluster$Profesi)
databaru <- merge(databaru, Identitas.Cluster$Jenis.Kelamin)
databaru <- merge(databaru, Identitas.Cluster$Tipe.Residen)
# menentukan data baru di cluster mana
which.min(sapply(1:5, 
                 function(x) 
                   sum((databaru[Identitas.Cluster$field_yang_digunakan] - 
                          Identitas.Cluster$Segmentasi$centers[x,])^2)))
				 
Identitas.Cluster$Segmen.Pelanggan[which.min(sapply(1:5,
                                                    function(x) 
                                                      sum((databaru[Identitas.Cluster$field_yang_digunakan] -
                                                             Identitas.Cluster$Segmentasi$centers[x,])^2))),]
```



<p align="justify"><b>Output :</b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/Screenshot_9.jpg"></p>



</br></br></br>
<p align="center"><b>E-Sertifikat </b></br><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/e-sertifikat.jpg"></p>

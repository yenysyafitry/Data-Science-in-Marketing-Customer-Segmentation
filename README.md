<p align="justify">Customer segmentation adalah proses penting yang diperlukan di bisnis untuk mengenal customer dengan lebih baik.
Dengan demikian proses bisnis di marketing (pemasaran) dan CRM (customer relationship management) bisa dilakukan lebih tajam. Contoh: pesan marketing bisa lebih personal untuk setiap segment dengan biaya lebih optimal.
Dengan proses yang lebih tajam, performa bisnis berpotensi tinggi menjadi lebih baik juga.
Untuk menemukan segmentasi yang baik, perlu proses analisa data dari profile customer yang cukup banyak dan rutin. Ini bisa dibantu dengan algoritma komputer.</p>
<p align="justify">Persiapan data adalah langkah pertama yang kita lakukan sebelum menggunakan algoritma apapun untuk melakukan analisa data.</br>
Ini dikarenakan tiap implementasi algoritma menuntut struktur dan tipe data yang berbeda.</br>
Dan untuk kasus algoritma K-Means yang akan kita gunakan untuk otomatisasi clustering, maka struktur datanya adalah data.frame atau matrix yang di dalamnya berisi angka semua. Tidak ada yang boleh bertipe karakter.
</p>
Namun pada kasus riil, hal ini tentulah tidak mungkin. Contoh, isi data profesi seperti "Professional", "Ibu Rumah Tangga" adalah teks. Dan ini perlu dikonversi dulu ke numerik, namun jika diperlukan tetap bisa kembali mengambil data teks.
</br><ol>
Nah, untuk lebih jelasnya. Kita akan lakukan langkah-langkah praktek yang akan kita lakukan berikut ini adalah untuk mempersiapkan data sebelum dapat digunakan algoritma clustering:

<li>Mengenal Contoh File Dataset Pelanggan</li>
<li>Membaca File dengan read.csv</li>
<li>Vector untuk Menyimpan Nama Field</li>
<li>Konversi Data dengan data.matrix</li>
<li>Menggabungkan Hasil Konversi</li>
<li>Menormalisasikan Nilai Belanja</li>
<li>Membuat Data Master</li></ol>

<details>
  <summary><b>Membaca data dengan fungsi read.csv</b></br>pelanggan <- read.csv("https://academy.dqlab.id/dataset/customer_segments.txt", sep="\t")</br>
pelanggan[c("Jenis.Kelamin","Umur","Profesi","Tipe.Residen")]</summary>
  <table border="0"><tr><td>  Jenis.Kelamin Umur          Profesi Tipe.Residen</br>
1           Pria   58       Wiraswasta       Sector</br>
2         Wanita   14          Pelajar      Cluster</br>
3           Pria   48     Professional      Cluster</br>
4           Pria   53     Professional      Cluster</br>
5         Wanita   41       Wiraswasta      Cluster</br>
6         Wanita   24     Professional      Cluster</br>
7           Pria   64       Wiraswasta       Sector</br>
8           Pria   52     Professional      Cluster</br>
9         Wanita   29     Professional       Sector</br>
10          Pria   33     Professional      Cluster</br>
11        Wanita   50     Professional       Sector</br>
12        Wanita   49     Professional       Sector</br>
13        Wanita   64       Wiraswasta      Cluster</br>
14          Pria   60       Wiraswasta      Cluster</br>
15        Wanita   20       Wiraswasta      Cluster</br>
16          Pria   35     Professional      Cluster</br>
17        Wanita   32 Ibu Rumah Tangga      Cluster</br>
18        Wanita   63 Ibu Rumah Tangga      Cluster</br>
19        Wanita   32       Wiraswasta      Cluster</br>
20        Wanita   16          Pelajar       Sector</br>
21        Wanita   38       Wiraswasta      Cluster</br>
22        Wanita   52     Professional      Cluster</br>
23          Pria   34     Professional      Cluster</br>
24        Wanita   39       Wiraswasta      Cluster</br>
25        Wanita   29       Wiraswasta       Sector</br>
26        Wanita   55     Professional      Cluster</br>
27        Wanita   35       Wiraswasta      Cluster</br>
28        Wanita   40 Ibu Rumah Tangga      Cluster</br>
29        Wanita   56     Professional      Cluster</br>
30        Wanita   46 Ibu Rumah Tangga       Sector</br>
31        Wanita   19        Mahasiswa      Cluster</br>
32        Wanita   47       Wiraswasta       Sector</br>
33        Wanita   19        Mahasiswa      Cluster</br>
34        Wanita   21       Wiraswasta       Sector</br>
35        Wanita   39     Professional       Sector</br>
36        Wanita   30       Wiraswasta      Cluster</br>
37        Wanita   25     Professional       Sector</br>
38        Wanita   46       Wiraswasta       Sector</br>
39        Wanita   20     Professional      Cluster</br>
40        Wanita   14          Pelajar       Sector</br>
41        Wanita   24 Ibu Rumah Tangga      Cluster</br>
42        Wanita   26       Wiraswasta      Cluster</br>
43        Wanita   31     Professional      Cluster</br>
44        Wanita   18       Wiraswasta      Cluster</br>
45        Wanita   22     Professional      Cluster</br>
46        Wanita   25       Wiraswasta       Sector</br>
47        Wanita   55 Ibu Rumah Tangga      Cluster</br>
48        Wanita   45       Wiraswasta       Sector</br>
49        Wanita   33 Ibu Rumah Tangga       Sector</br>
50        Wanita   55       Wiraswasta       Sector </td></tr></table>
</details>
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
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Marketing-Customer-Segmentation/blob/main/1.png" alt="Trulli" width="500" height="333"></td></tr></table>
</details>

<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>


<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>


<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>

<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>

<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>


<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>


<details>
  <summary><b>Vector untuk Menyimpan Nama Field  </b></br>length(isi.vector)</summary>
  <table border="0"><tr><td><i>Output :</i></td><td>> isi.vector <- c(1, 2, 3, NA, 5, NULL, 7)</br>> length(isi.vector)</br>[1] 6</td></tr></table>
</details>

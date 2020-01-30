# HACKTIV8 THT
​
Kamu akan membuat sistem pendaftaran dan handled patient di suatu klinik THT, menggunakan Express dan Sequelize. Baca tiap spesifikasi yang akan diminta.
​
nama database yang digunakan adalah: live_code_week4
​
Demo: [demo](https://secret-fortress-61139.herokuapp.com/hospitals)
​
> RELEASE 0
​
Buatlah migration dan model untuk:
​
1. Doctor
   * name (string)
   * specialities (string)
2. Patient
   * name (string)
   * disease (string)
   * status (boolean)
   * pay_code (string)
​
> RELEASE 1
​
Relasi antara `Doctor` dan `Patient`, 1 `Doctor` memiliki banyak `Patient` dan 1 `Patient` hanya memiliki 1 `Doctor` 
​
Buatlah migration baru untuk menambahkan kolom baru untuk memenuhi requirement di atas.
​
> RELEASE 2
​
Buatlah seeding untuk menginput list dokter yang akan menjadi dokter di klinik tersebut:
​
1. * name: Hary Dhimas
   * specialities: Tenggorokan
2. * name: Wika Silo
   * specialities: Hidung
3. * name: Arnold Therigan
   * specialities: Telinga
​
> RELEASE 3
​
Buatlah routing untuk sistem klinik yang **HARUS**  mengikuti format berikut : 
​
| Method | Route                                | Description                                                  |
| ------ | ------------------------------------ | ------------------------------------------------------------ |
| GET    | /doctorList                          | Menampilkan Seluruh Dokter yang tersedia                     |
| POST   | /addPatient                          | menambahkan data patient                                     |
| GET    | /addPatient                          | Menampilkan form add patient                                 |
| GET    | /patientList/:doctorId/:specialities | Menampilkan seluruh patient yang mengidap penyakit sesuai specialities si dokter |
| GET    | /acceptPatient/:doctorId/:patientId  | Menerima pasien sebagai handled pasien                       |
| GET    | /curePatient/:patientId              | Menyembuhkan pasien yang sudah di handled                    |
| GET    | /curedPatient                        | Menampilkan seluruh patient yang sudah di sembuhkan oleh semua dokter |
| GET    | /deletePatient/:patientId            | Menghapus salah satu patient dari list cured patient         |
​
​
> RELEASE 4
​
Pada routing `/doctorList` akan menampilkan table list dari dokter yang sudah di seed sebelumnya, data yang akan ditampilkan terdiri dari `nama dokter`, `specialities`, `action`. `Action` adalah sebuah link bernama `See` yang akan menampilkan seluruh patient yang penyakitnya sesuai dari specialities dokter tersebut. Ketika `See` ini diklik, maka akan berpindah halaman ke routing `/patientList/:doctorId/:specialities`. (Detail route `See` akan dilanjutkan pada Release 8)
​
> RELEASE 5
​
Pada routing /addPatient akan menampilkan form untuk menambahkan patient ke database, dimana:
​
* input type `name` adalah text
* input type `disease` adalah select, dimana option nya ada: 
  * Tenggorokan
  * Hidung
  * Telinga
* button `submit` untuk submit data patient ke database 
​
> RELEASE 6
​
Pada submit button di release 5, apabila ditekan akan mengakses routing `/addPatient` yang akan menyimpan data ke database. Buatlah sebuah validasi, ketika field nama tidak diisi maka akan menampilkan error message. (boleh menggunakan res.send selama messagenya jelas)
​
> RELEASE 7
​
Sebelum menyimpan data set `status` menjadi false, serta buatlah hooks untuk mengenerate pay_code yang terkombinasi dari kode dari penyakit yang di alami si pasien yaitu:
​
* Tenggorokan : TNG
* Hidung: HDG
* Telinga: TLG
​
di tambah dengan nama pasien tersebut, format sesuai contoh di bawah ini:
​
contoh:
​
* name: Isro Tri Pambudi
* disease: Tenggorokan
* status: false
* pay_code: TNGisrotripambudi (wajib dibuat lewat hooks)
* ID relasinya dibuat null
​
> RELEASE 8
​
Pada routing `/doctorList` jika link action pada salah satu dokter ditekan, maka halaman akan berpindah ke routing `/patientList/:doctorId/:specialities` yang menampilkan data pasien yang penyakitnya sama dengan specialities si dokter, tampilan tersebut terdiri dari `name pasien` `disease` `pay_code` `status` `action`.
​
> RELEASE 9
​
Pada routing `/patientList/:doctorId/:specialities` akan menampilkan seluruh pasien yang sesuai dengan specialities dokter tersebut. Pasien yang ditampilkan hanyalah yang ID relasinya masih null dan status pasien false.
​
Pada routing `/patientList/:doctorId/:specialities` jika ID relasinya adalah null maka
`status di tabel` adalah unhandled, serta action yang di tampilkan adalah link `Terima Pasien` yang akan menghubungkan routing `acceptPatient/:doctorId/:patientId` menambahkan ID relasi ke tabel tersebut.
​
Pada routing `/patientList/:doctorId/:specialities` jika ID relasinya udah terisi namun status false maka `status di tabel` adalah handled, serta action yang di tampilkan adalah link `Sembuhin` yang akan menghubungkan routing `/curePatient/:patientId` mengubah status menjadi true.
​
Dan juga ketika status pasien adalah true maka pasien tersebut sudah tidak adalagi pada routing `/patientList/:doctorId/:specialities`.
​
> RELEASE 10
​
Pada routing `/curedPatient` akan menampilkan tabel seluruh pasien yang telah di sembuhkan oleh seluruh dokter di klinik, yang terdiri dari `name` `disease` `pay_code` `doctor` `action`.
​
> RELEASE 11
​
Pada routing `/curedPatient` , ketika tombol `delete` pada kolom `action` ditekan, maka data pasien akan terhapus dari database, `action` ini dilakukan menggunakan routing `/deletePatient/:patientId`.
Collaps

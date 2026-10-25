# SPEECH PRESENTASI UJI KUALITAS PERANGKAT LUNAK MSS

> **Catatan penting:** Naskah ini menggunakan angka, status, dan hasil pada tiga LK sebagai **simulasi/dummy akademik**. Angka seperti `342 ms`, `1.240 ms`, status lulus/gagal, hasil PHPStan, ZAP, dan pengujian beban tidak boleh disebut sebagai hasil eksekusi nyata apabila belum benar-benar dijalankan. Jika diperlukan, bacakan kalimat “berdasarkan simulasi pada lembar kerja” secara konsisten.

## Identitas Presentasi

- **Nama:** Miftah Rafli Nuryatama
- **NIM:** 124230098
- **Proyek:** MSS atau SIM MSS, yaitu aplikasi Sistem Informasi Muslimah Swimming Squad
- **Mata kuliah:** Uji Kualitas Perangkat Lunak
- **Durasi target:** 10–15 menit
- **Kasus utama:** alur pencatatan presensi
- **Dokumen pendukung:**
  - [LK-01 Static Testing MSS](./LK_01_Static_Testing_MSS.md)
  - [LK-02 Pengujian Non-Fungsional MSS](./LK_02_Pengujian_Non_Fungsional_MSS.md)
  - [LK-03 Analisis Kasus Kualitas Perangkat Lunak MSS](./LK_03_Analisis_Kasus_Kualitas_Perangkat_Lunak_MSS.md)

## Alur dan Pembagian Waktu

| Bagian | Materi | Durasi |
|---|---|---:|
| 1 | Pendahuluan dan identitas aplikasi | 1–2 menit |
| 2 | Kasus dan kebutuhan yang direview | 1–2 menit |
| 3 | Analisis Static Testing | 3 menit |
| 4 | Analisis Pengujian Non-Fungsional | 3–4 menit |
| 5 | Simulasi keterhubungan dan tujuh perspektif kualitas | 2–3 menit |
| 6 | Rekomendasi dan kesimpulan | 1–2 menit |
| **Total** |  | **11–14 menit** |

---

## 1. Pendahuluan — Identitas Aplikasi dan Kasus

**Perkiraan durasi: 1–2 menit**

### Naskah

> Assalamualaikum warahmatullahi wabarakatuh.
>
> Perkenalkan, nama saya Miftah Rafli Nuryatama, NIM 124230098. Pada video ini saya akan mempresentasikan keterhubungan tiga lembar kerja Uji Kualitas Perangkat Lunak pada proyek MSS atau SIM MSS, yaitu aplikasi Sistem Informasi Muslimah Swimming Squad.
>
> Aplikasi ini berbasis web. Dari source code yang tersedia, teknologi yang teridentifikasi adalah PHP procedural, HTML, CSS, JavaScript, serta database MySQL atau MariaDB yang diakses menggunakan `mysqli`.
>
> Fitur yang terlihat pada aplikasi antara lain login dan logout, dashboard berdasarkan role, pengelolaan jadwal, presensi, data member, transaksi, dan pilihan cetak laporan. Role yang teridentifikasi adalah Admin, Pelatih, dan Member.
>
> Kasus yang saya pilih adalah alur pencatatan presensi. Scope ini dipilih karena cukup sempit untuk direview, tetapi memiliki hubungan langsung antara antarmuka, handler PHP, session, query database, dan schema tabel.
>
> Perlu saya tegaskan bahwa data hasil pengujian pada lembar kerja yang saya tampilkan merupakan simulasi atau dummy akademik untuk memperlihatkan cara analisis. Data tersebut bukan klaim bahwa aplikasi sudah benar-benar diuji menggunakan tool di environment nyata.

### Tampilan/bukti yang disarankan

Tampilkan secara singkat:

1. Nama aplikasi atau halaman login.
2. Struktur folder `pages/`, `config/`, dan `assets/`.
3. Judul kasus pada [LK-03](./LK_03_Analisis_Kasus_Kualitas_Perangkat_Lunak_MSS.md).

---

## 2. Kasus, Scope, dan Kebutuhan

**Perkiraan durasi: 1–2 menit**

### Naskah

> Pada kasus ini, saya membatasi review pada handler presensi di file `pages/presensi.php`, khususnya aksi `hadir` dan `absen` pada baris 45 sampai 60, serta tombol yang memanggil aksi tersebut pada baris 263 sampai 272.
>
> Dokumen requirement formal tidak ditemukan di repository. Karena itu, requirement pada LK-01 dan LK-03 diberi status kebutuhan yang direkonstruksi dari source code dan schema, bukan requirement resmi dari dosen atau pemilik proyek.
>
> Requirement sementara yang digunakan diberi ID PR-01 sampai PR-07. Contohnya, PR-01 menyatakan bahwa pengguna yang sudah login dapat melihat daftar jadwal presensi. PR-02 menyatakan bahwa pengguna dapat memilih Hadir atau Absen. PR-03 sampai PR-05 berhubungan dengan identitas member, jadwal, tanggal, dan status presensi. PR-06 membahas hak akses, sedangkan PR-07 membahas pembedaan antara penyimpanan berhasil dan gagal.
>
> Requirement ini digunakan agar tiga lembar kerja memiliki traceability yang konsisten. Namun, validasi formal tetap perlu dilakukan kepada dosen atau pemilik proyek.

### Tampilkan

Pada [LK-01](./LK_01_Static_Testing_MSS.md), tampilkan tabel requirement PR-01 sampai PR-07. Tekankan bahwa statusnya adalah rekonstruksi/simulasi.

---

## 3. Analisis Static Testing

**Perkiraan durasi: 3 menit**

### Naskah

> Selanjutnya saya menjelaskan LK-01 Static Testing. Review yang digunakan adalah informal review dengan scope satu modul kecil, yaitu handler presensi.
>
> Pada pemeriksaan manual, saya menemukan lima temuan utama dengan ID ST-01 sampai ST-05.
>
> Temuan pertama, ST-01, merupakan temuan paling penting. Pada `presensi.php` baris 47 sampai 58, query INSERT menggunakan kolom `tanggal_presensi`, tidak mengisi `member_id`, dan menggunakan status `Absen`.
>
> Jika dibandingkan dengan schema pada `sim_mss.sql` baris 98 sampai 103, tabel `presensi` justru memiliki kolom `member_id`, `jadwal_id`, `tanggal`, dan status enum `Hadir`, `Izin`, `Sakit`, dan `Alpa`. Jadi, terdapat ketidaksesuaian antara query dan schema.
>
> Temuan kedua, ST-02, adalah penggunaan parameter GET untuk mutasi data. Nilai `hadir` atau `absen` diambil dari URL dan langsung dimasukkan ke query. Validasi ID jadwal dan pencegahan duplikasi tidak terlihat pada handler.
>
> Temuan ketiga, ST-03, adalah hasil `mysqli_query` tidak diperiksa. Setelah query, aplikasi langsung melakukan redirect. Akibatnya, pengguna berpotensi tidak mendapatkan pesan yang membedakan proses berhasil atau gagal.
>
> Temuan keempat, ST-04, adalah pemeriksaan session memang terlihat untuk masuk ke halaman, tetapi pemeriksaan role khusus pada aksi mutasi belum terlihat.
>
> Temuan kelima, ST-05, berkaitan dengan kemungkinan ketidaksesuaian mapping `users.id`, `members.id`, `members.user_id`, dan `presensi.member_id`. Dashboard menggunakan `user_id` session sebagai filter presensi, sedangkan foreign key presensi mengarah ke `members.id`.
>
> Dalam klasifikasi awal, ST-01 menjadi defect kandidat prioritas tinggi. ST-02 dan ST-04 menjadi pertanyaan atau potensi defect karena masih memerlukan role matrix dan reproduksi runtime. ST-03 menjadi defect kandidat tingkat sedang, sedangkan ST-05 memerlukan verifikasi data.

### Static analysis tool

> LK-01 juga menyediakan bagian static analysis tool. Pada dokumen simulasi, tool yang dicontohkan adalah PHPStan versi 1.12.0 level 5. Hasil dummy mencatat nol error sintaks, dua issue type atau undefined symbol, tiga issue SQL/security, dan empat issue code style atau maintainability.
>
> Tiga issue teratas yang ditampilkan tetap mengacu pada bukti source code: ketidaksesuaian kolom dan member ID, status `Absen` yang tidak ada pada enum schema, serta penggunaan parameter GET langsung untuk mutasi.
>
> Bagian ini harus dipahami sebagai data simulasi. Tool PHPStan tidak boleh diklaim sudah dijalankan apabila output aslinya belum tersedia.

### Tampilkan

1. [presensi.php](../sim-mss/sim-mss/pages/presensi.php), baris 47–58.
2. [sim_mss.sql](../sim_mss.sql), baris 98–103.
3. Tabel ST-01 sampai ST-05 pada [LK-01](./LK_01_Static_Testing_MSS.md).
4. Jika menampilkan tabel PHPStan, sebutkan “hasil simulasi”.

---

## 4. Analisis Pengujian Non-Fungsional

**Perkiraan durasi: 3–4 menit**

### Pembuka

> LK-02 menggunakan lima aspek yang tersedia pada lembar kerja, yaitu kinerja, keamanan, kompatibilitas, keandalan, dan skalabilitas. Angka pada LK asli adalah contoh target, sedangkan angka pada LK saya adalah data dummy simulasi.

### 4.1 Kinerja

> Pada aspek kinerja, target simulasi yang digunakan adalah p95 kurang dari 800 milidetik dan error kurang dari satu persen.
>
> Untuk membuka halaman presensi, skenario T-01 menggunakan sepuluh pengguna simulasi, p95 sebesar 342 milidetik, dan error nol persen. Skenario ini dinyatakan lulus secara simulasi.
>
> Untuk aksi presensi pada T-02, p95 simulasi adalah 418 milidetik, tetapi error mencapai seratus persen karena query presensi tidak sesuai dengan schema. Jadi, secara simulasi halaman dapat cepat, tetapi kecepatan tidak berarti fitur berhasil apabila operasi datanya gagal.

### 4.2 Keamanan

> Pada aspek keamanan, pemeriksaan simulasi mencakup akses tanpa login, akses role yang tidak berwenang, ID invalid atau injection, XSS, batas salah password, dan penyimpanan password.
>
> T-03, yaitu akses tanpa login, diasumsikan lulus simulasi karena diarahkan ke `login.php`.
>
> T-04 sampai T-05 dinyatakan gagal simulasi karena aksi mutasi memakai parameter langsung dan pemeriksaan role pada endpoint belum terlihat.
>
> T-07 menunjukkan tidak adanya rate limit yang terlihat pada kode login. T-08 juga menunjukkan bahwa data contoh pada dump SQL menggunakan password plaintext. Temuan ini perlu disampaikan sebagai risiko dari pemeriksaan source code dan data dump, bukan sebagai hasil pemindaian ZAP yang benar-benar dijalankan.

### 4.3 Kompatibilitas

> Untuk kompatibilitas, skenario simulasi menggunakan alur login, daftar presensi, dan aksi Hadir atau Absen pada lima kombinasi browser dan viewport. Hasil dummy menyatakan lima kombinasi lulus dan tidak ditemukan masalah layout.
>
> Namun, hasil ini masih harus diganti dengan screenshot dan catatan versi browser jika pengujian nyata dilakukan.

### 4.4 Keandalan

> Pada aspek keandalan, T-10 mengulang operasi sebanyak sepuluh kali. Simulasi mencatat dua kegagalan dan perubahan jumlah baris dari 500 menjadi 508, sehingga dinyatakan gagal.
>
> Pada gangguan database T-11, simulasi mencatat error koneksi mentah dan recovery 18 detik, sehingga gagal terhadap target pesan yang tertangani.
>
> Pada restart server T-12, simulasi mencatat recovery 12 detik tanpa kehilangan data dan dinyatakan lulus.

### 4.5 Skalabilitas

> Untuk skalabilitas, skenario T-13 menggunakan 100 pengguna. Hasil simulasi menunjukkan p95 1.240 milidetik, throughput 42 request per detik, dan error 3,2 persen. Karena melewati target, titik ini dianggap jenuh.
>
> Pada skala data 500 baris, T-14 mencatat p95 610 milidetik dan error 0,8 persen, sehingga lulus secara simulasi.

### Tampilkan

Tampilkan tabel hasil pada [LK-02](./LK_02_Pengujian_Non_Fungsional_MSS.md), tetapi sebutkan bahwa semua angka adalah simulasi. Jangan menampilkan report tool palsu sebagai file asli.

---

## 5. Simulasi Keterhubungan Tiga LK

**Perkiraan durasi: 2 menit**

### Naskah

> Keterhubungan tiga lembar kerja dapat dijelaskan melalui satu alur.
>
> Pertama, LK-01 menemukan ST-01 pada source code, yaitu query presensi tidak sesuai dengan schema.
>
> Kedua, temuan itu menjadi dasar skenario T-02 pada LK-02. Dalam data simulasi, aksi presensi menghasilkan error schema seratus persen. Jadi, static testing memberikan hipotesis dan pengujian non-fungsional memberikan skenario serta indikator hasil.
>
> Ketiga, hasil tersebut dibawa ke LK-03 untuk dianalisis dari perspektif kualitas. Masalah yang sama berhubungan dengan kesesuaian fungsi karena pencatatan presensi tidak memenuhi kontrak data, dengan keandalan karena data tidak tersimpan secara konsisten, dengan keamanan karena mutasi memakai input langsung, dan dengan maintainability karena query serta schema tidak konsisten.
>
> Dengan demikian, LK-01 menjawab apa yang terlihat dari dokumen dan source code. LK-02 menjawab bagaimana skenario pengujian disusun dan apa hasil simulasinya. LK-03 menghubungkan temuan dan hasil tersebut menjadi analisis kualitas serta rencana perbaikan.

### ID yang ditunjukkan

- Requirement: `PR-01` sampai `PR-07`
- Static finding: `ST-01` sampai `ST-05`
- Skenario pengujian: `T-01` sampai `T-14`
- Bukti: `B-01` sampai `B-12`

---

## 6. Analisis Tujuh Perspektif Kualitas

**Perkiraan durasi: 2 menit**

### Naskah

> Pada LK-03 terdapat tabel tujuh perspektif kualitas. Sumber resmi yang menyebut nama dan urutan tujuh perspektif tidak ditemukan pada repository. Karena itu, tabel utama menggunakan label sementara, yaitu Perspektif 1 sampai Perspektif 7 dan perlu dikonfirmasi.
>
> Sebagai pemetaan sementara, saya menggunakan functional suitability, performance efficiency, compatibility, reliability, security, maintainability, dan usability. Pemetaan ini bukan klaim bahwa daftar tersebut adalah daftar resmi dosen.
>
> Functional suitability berkaitan dengan apakah presensi memenuhi kebutuhan dan schema. Performance efficiency berkaitan dengan p95 dan error. Compatibility berkaitan dengan browser serta viewport. Reliability berkaitan dengan konsistensi data dan recovery. Security berkaitan dengan role, input, session, dan password. Maintainability berkaitan dengan mismatch query-schema serta penanganan error. Usability berkaitan dengan apakah pengguna mendapatkan alur dan pesan yang jelas.
>
> Tidak semua perspektif boleh dinyatakan terdampak tanpa bukti. Karena data pada presentasi ini simulasi, kesimpulan kualitas juga harus disebut sebagai kesimpulan simulasi.

### Tampilkan

Tampilkan bagian perspektif pada [LK-03](./LK_03_Analisis_Kasus_Kualitas_Perangkat_Lunak_MSS.md). Tekankan label **usulan sementara — bukan ketentuan resmi**.

---

## 7. Rekomendasi Perbaikan dan Pengujian Ulang

**Perkiraan durasi: 1–2 menit**

### Naskah

> Berdasarkan temuan tersebut, rekomendasi pertama adalah menyelaraskan query presensi dengan schema dan requirement yang telah dikonfirmasi. Perlu dipastikan identitas member, jadwal, tanggal, dan nilai status yang benar.
>
> Rekomendasi kedua adalah memvalidasi ID dan membatasi hak akses pada endpoint mutasi, bukan hanya menyembunyikan tombol pada antarmuka.
>
> Rekomendasi ketiga adalah memeriksa hasil query dan menampilkan status berhasil atau gagal secara jelas.
>
> Setelah perubahan disetujui, pengujian ulang harus menggunakan database disposable dan dataset yang setara. Skenario T-01 sampai T-05 dijalankan kembali, kemudian aspek non-fungsional yang relevan diulang dengan target yang sama.
>
> Pada LK-03, hasil perbandingan before-after masih merupakan data simulasi. Karena itu saya tidak menyatakan bahwa source code sudah diperbaiki atau performa benar-benar meningkat.

---

## 8. Kesimpulan

**Perkiraan durasi: 1 menit**

### Naskah

> Kesimpulan dari simulasi ini adalah bahwa masalah utama berada pada ketidaksesuaian antara implementasi presensi dan schema database. Temuan ini pertama kali terlihat melalui static testing dengan ID ST-01.
>
> Pada pengujian non-fungsional simulasi, masalah tersebut berhubungan dengan kegagalan aksi presensi, reliabilitas penyimpanan, potensi risiko keamanan pada input dan otorisasi, serta kemungkinan masalah maintainability.
>
> Tiga lembar kerja saling terhubung melalui requirement PR, temuan ST, skenario T, dan bukti B. LK-01 menemukan masalah dari source code, LK-02 menyusun dan mencatat skenario pengujian, sedangkan LK-03 menghubungkan hasil tersebut dengan analisis kualitas dan rencana pengujian ulang.
>
> Rekomendasi utama adalah mengonfirmasi requirement dan role matrix, menyelaraskan query dengan schema, menambahkan validasi dan pemeriksaan hasil query, kemudian melakukan pengujian ulang pada environment lokal yang aman.
>
> Sekali lagi, angka dan status yang ditampilkan dalam video ini adalah simulasi atau dummy untuk kebutuhan akademik. Hasil final harus diganti dengan bukti nyata apabila pengujian aplikasi telah dilakukan.
>
> Demikian presentasi saya. Terima kasih.
>
> Wassalamualaikum warahmatullahi wabarakatuh.

## Checklist Sebelum Rekaman

- [ ] Pastikan nama dan NIM sudah benar.
- [ ] Tampilkan tiga LK yang dikumpulkan.
- [ ] Sebutkan kasus presensi dan scope baris kode yang direview.
- [ ] Tampilkan bukti `presensi.php` dan `sim_mss.sql`.
- [ ] Sebutkan ID `PR`, `ST`, `T`, dan `B`.
- [ ] Jelaskan bahwa angka dan status adalah simulasi/dummy.
- [ ] Jangan menyebut PHPStan, ZAP, k6, atau JMeter sebagai benar-benar dijalankan jika tidak ada output asli.
- [ ] Jangan mengklaim source code sudah diperbaiki jika belum ada perubahan dan pengujian ulang.
- [ ] Pastikan durasi akhir berada antara 10 dan 15 menit.

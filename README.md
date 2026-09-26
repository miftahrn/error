# PrintManager
## Sistem Informasi Manajemen Percetakan

## 1. Deskripsi Aplikasi

PrintManager adalah aplikasi mobile berbasis Flutter untuk membantu mengelola kegiatan percetakan secara sederhana. Aplikasi ini dibuat sebagai proyek tugas kuliah dan menggunakan database lokal SQLite sehingga tidak membutuhkan backend atau server.

Aplikasi menyediakan fitur login, session pengguna, data anggota, komputasi percetakan, pengelolaan pesanan, konversi kalender, konversi umur, stopwatch, dan halaman bantuan.

Nama aplikasi: **PrintManager – Sistem Informasi Manajemen Percetakan**

Platform utama: **Android**

Teknologi: **Flutter dan Dart**

## 2. Tujuan Aplikasi

Tujuan pembuatan aplikasi ini adalah:

1. Membuat aplikasi manajemen percetakan yang dapat digunakan secara lokal.
2. Menerapkan login dan session menggunakan penyimpanan perangkat.
3. Menerapkan database SQLite untuk menyimpan data anggota dan pesanan.
4. Menerapkan operasi CRUD pada data pesanan.
5. Menyediakan fitur perhitungan yang berkaitan dengan kegiatan percetakan.
6. Menerapkan pemisahan source code berdasarkan fungsi agar lebih mudah dipelajari dan dipelihara.

## 3. Teknologi dan Dependency

Aplikasi dibuat menggunakan teknologi berikut:

- Flutter stable
- Dart
- Material Design 3
- SQLite melalui package `sqflite`
- Penyimpanan session melalui package `shared_preferences`
- Format tanggal dan mata uang melalui package `intl`
- Pengelolaan lokasi database melalui package `path`

Dependency utama pada `pubspec.yaml`:

```yaml
intl: ^0.20.2
shared_preferences: ^2.5.3
sqflite: ^2.4.2
path: ^1.9.1
```

## 4. Struktur Project

Struktur utama source code adalah sebagai berikut:

```text
lib/
├── main.dart
├── database/
│   └── database_helper.dart
├── models/
│   ├── member.dart
│   └── order.dart
├── services/
│   ├── balinese_calendar_service.dart
│   └── session_service.dart
└── screens/
    ├── age_page.dart
    ├── calendar_page.dart
    ├── computation_page.dart
    ├── help_page.dart
    ├── home_page.dart
    ├── login_page.dart
    ├── member_page.dart
    ├── order_page.dart
    └── stopwatch_page.dart
```

### Penjelasan folder

- `lib/main.dart`: entry point aplikasi, konfigurasi tema, dan pemeriksaan session.
- `lib/database`: berisi helper untuk membuat dan mengakses database SQLite.
- `lib/models`: berisi class model yang mewakili data anggota dan pesanan.
- `lib/services`: berisi logika session dan konversi kalender Saka Bali.
- `lib/screens`: berisi halaman-halaman yang ditampilkan kepada pengguna.

## 5. Alur Kerja Aplikasi

Alur utama aplikasi adalah:

```text
Aplikasi dibuka
      |
      v
SessionGate memeriksa SharedPreferences
      |
      +-- Belum login --> LoginPage
      |
      +-- Sudah login --> HomePage
                              |
                              +-- Home
                              +-- Stopwatch
                              +-- Bantuan
```

Setelah login, pengguna diarahkan ke halaman Home. Tombol Back tidak dapat digunakan untuk kembali ke halaman login karena halaman login diganti dengan `pushReplacement`. Ketika logout, seluruh stack navigasi dihapus menggunakan `pushAndRemoveUntil` sehingga pengguna kembali ke login dan tidak dapat kembali ke Home menggunakan tombol Back.

## 6. Penjelasan Source Code Utama

### 6.1 `main.dart`

File ini adalah titik awal aplikasi.

Fungsi utamanya:

1. Memastikan Flutter siap digunakan melalui `WidgetsFlutterBinding.ensureInitialized()`.
2. Menginisialisasi locale Indonesia untuk package `intl` melalui `initializeDateFormatting('id_ID')`.
3. Menjalankan widget `PrintManagerApp`.
4. Mengatur tema Material dengan warna biru tua, putih, dan abu-abu.
5. Menampilkan `SessionGate` sebagai halaman awal.

`SessionGate` memakai `FutureBuilder` untuk memeriksa apakah pengguna sudah login. Jika session bernilai `true`, aplikasi membuka `HomePage`. Jika belum, aplikasi menampilkan `LoginPage`.

### 6.2 `login_page.dart`

Halaman ini berisi:

- Input username
- Input password
- Tombol Login
- Tombol untuk menampilkan atau menyembunyikan password
- Pesan kesalahan jika data login salah

Akun demo yang digunakan:

```text
Username: admin
Password: admin123
```

Jika login berhasil, `SessionService.login()` menyimpan nilai session ke `SharedPreferences`.

### 6.3 `session_service.dart`

Class `SessionService` menangani session login secara lokal.

Method yang tersedia:

- `isLoggedIn()`: membaca status login.
- `login()`: menyimpan status login `true`.
- `logout()`: menghapus status login.

Contoh konsep penyimpanan session:

```dart
await preferences.setBool('is_logged_in', true);
```

Dengan cara ini, status login tetap tersimpan walaupun aplikasi ditutup dan dibuka kembali.

### 6.4 `home_page.dart`

`HomePage` menggunakan `NavigationBar` dengan tiga menu:

1. Home
2. Stopwatch
3. Bantuan

Pada halaman Home terdapat lima menu utama yang disusun secara vertikal:

1. Daftar Anggota
2. Komputasi Percetakan
3. Data Pesanan
4. Konversi Kalender
5. Konversi Umur

Setiap menu membuka halaman menggunakan `Navigator.push`.

### 6.5 `database_helper.dart`

`DatabaseHelper` adalah singleton yang digunakan untuk mengelola database SQLite.

Database yang dibuat bernama:

```text
print_manager.db
```

Database memiliki dua tabel utama.

#### Tabel `members`

| Kolom | Tipe | Keterangan |
|---|---|---|
| `id` | INTEGER | Primary key dan auto increment |
| `name` | TEXT | Nama anggota |
| `nim` | TEXT | Nomor induk mahasiswa |
| `role` | TEXT | Peran anggota |

Saat database pertama kali dibuat, data anggota berikut dimasukkan:

```text
Nama: Miftah Rafli Nuryatama
NIM: 124230098
Role: Mahasiswa
```

#### Tabel `orders`

| Kolom | Tipe | Keterangan |
|---|---|---|
| `id` | INTEGER | Primary key dan auto increment |
| `customer_name` | TEXT | Nama pelanggan |
| `print_type` | TEXT | Jenis cetakan |
| `paper_size` | TEXT | Ukuran kertas |
| `quantity` | INTEGER | Jumlah cetakan |
| `price_per_sheet` | REAL | Harga per lembar |
| `total_price` | REAL | Total harga |
| `status` | TEXT | Status pesanan |

Method database yang digunakan:

- `getMembers()`: mengambil seluruh data anggota.
- `getOrders()`: mengambil seluruh pesanan.
- `insertOrder()`: menambahkan pesanan.
- `updateOrder()`: memperbarui pesanan.
- `deleteOrder()`: menghapus pesanan.

### 6.6 `member.dart` dan `member_page.dart`

`Member` adalah model untuk data anggota. Data dari SQLite diubah menjadi object menggunakan factory constructor `Member.fromMap`.

`MemberPage` mengambil data menggunakan `FutureBuilder`, kemudian menampilkannya dalam bentuk `ListView` dan `Card`.

Keuntungan menggunakan model adalah data lebih terstruktur dibandingkan menggunakan `Map` secara langsung pada seluruh halaman.

### 6.7 `order.dart` dan `order_page.dart`

`PrintOrder` adalah model untuk data pesanan.

Total harga dihitung melalui getter:

```dart
double get totalPrice => quantity * pricePerSheet;
```

`OrderPage` menyediakan fitur CRUD lengkap:

- Create: tombol `Tambah` membuka form pesanan.
- Read: daftar pesanan diambil dari SQLite.
- Update: menu `Edit` mengubah data pesanan.
- Delete: menu `Hapus` menghapus data setelah konfirmasi.

Jenis cetakan yang tersedia:

- Dokumen
- Brosur
- Poster
- Undangan
- Banner
- Kartu nama

Ukuran kertas yang tersedia:

- A4
- A3
- F4
- B5

Status pesanan yang tersedia:

- Menunggu
- Diproses
- Selesai

Sebelum disimpan, form melakukan validasi agar nama pelanggan, jumlah, dan harga tidak kosong atau tidak valid.

### 6.8 `computation_page.dart`

Halaman Komputasi Percetakan memiliki tiga fitur.

#### Kalkulator

Kalkulator mendukung:

- Penjumlahan
- Pengurangan
- Perkalian
- Pembagian
- Bilangan desimal menggunakan titik
- Bilangan negatif melalui tombol `+/-`
- Tombol `C`
- Tombol `=`
- Persentase

Nilai kalkulator menggunakan tipe `double`, sehingga contoh berikut dapat dilakukan:

```text
5.5 + 2.5 = 8
10 / 4 = 2.5
(-70) - (-40) = -30
```

#### Ganjil dan Genap

Fitur ini menggunakan operasi modulus:

```dart
number % 2 == 0
```

Jika hasil modulus sama dengan nol, bilangan dinyatakan genap. Jika tidak, bilangan dinyatakan ganjil.

#### Jumlah Digit

Fitur ini menghitung banyaknya digit, bukan menjumlahkan nilai digit.

Contoh:

```text
12345   -> Jumlah angka: 5
1457294 -> Jumlah angka: 7
10      -> Jumlah angka: 2
7       -> Jumlah angka: 1
```

Tanda minus pada bilangan negatif dihapus terlebih dahulu sehingga hanya digit yang dihitung.

### 6.9 `calendar_page.dart`

Halaman Konversi Kalender menerima tanggal Masehi melalui `showDatePicker`.

Hasil yang ditampilkan:

- Tanggal Hijriah perkiraan
- Nama hari
- Pasaran atau weton
- Tahun Saka Bali
- Tanggal Nyepi sebagai awal tahun Saka
- Hari keberapa dalam tahun Saka
- Sasih perkiraan

Konversi Hijriah pada source code masih menggunakan pendekatan pengurangan jumlah hari tetap, sehingga hasilnya diberi label `perkiraan`.

Perhitungan weton menggunakan daftar pasaran:

```dart
['Legi', 'Pahing', 'Pon', 'Wage', 'Kliwon']
```

### 6.10 `balinese_calendar_service.dart`

Service ini berisi logika kalender Saka Bali.

Data Nyepi modern tahun 2020 sampai 2030 disimpan dalam `Map<int, DateTime>`. Tahun Saka ditentukan dari tahun Nyepi:

```text
Tahun Saka = Tahun Masehi Nyepi - 78
```

Contoh:

```text
Nyepi 2026 -> Tahun Saka 1948
```

Service juga menghitung:

- Awal tahun Saka berdasarkan tanggal Nyepi.
- Hari keberapa sejak Nyepi.
- Sasih menggunakan pembagian pendekatan 30 hari.

Perlu diperhatikan bahwa penentuan sasih pada aplikasi masih berupa pendekatan. Kalender Bali sebenarnya menggunakan perhitungan pawukon dan sistem lunar-solar yang lebih kompleks. Struktur service sengaja dibuat terpisah agar dapat dikembangkan kemudian tanpa mengubah tampilan halaman kalender.

### 6.11 `age_page.dart`

Halaman Konversi Umur menerima tanggal lahir dari date picker.

Hasil perhitungan ditampilkan dalam:

- Tahun
- Bulan
- Hari
- Jam
- Menit
- Detik

`Timer.periodic` digunakan setiap satu detik agar informasi waktu terus diperbarui.

### 6.12 `stopwatch_page.dart`

Stopwatch menggunakan `Timer.periodic` dengan interval satu detik.

Tombol yang disediakan:

- `Start`: memulai timer.
- `Pause`: menghentikan sementara timer.
- `Reset`: mengembalikan waktu ke nol.

Timer dibatalkan pada method `dispose()` untuk mencegah timer tetap berjalan ketika halaman sudah ditutup.

### 6.13 `help_page.dart`

Halaman Bantuan menampilkan panduan singkat untuk:

- Login
- Komputasi
- CRUD pesanan
- Konversi kalender
- Konversi umur
- Stopwatch

Tombol Logout tersedia pada tab Bantuan. Logout menghapus session dan mengarahkan pengguna kembali ke halaman Login.

## 7. Desain Antarmuka

Aplikasi menggunakan Material Design dengan karakteristik:

- Warna utama biru tua.
- Latar belakang abu-abu muda.
- Card untuk menampilkan menu dan data.
- Icon untuk membantu mengenali fungsi menu.
- NavigationBar untuk navigasi utama.
- Form dengan validasi input.
- Layout yang dapat digunakan pada layar Android.

Tema global ditetapkan di `main.dart`, sehingga warna dan gaya dasar dapat digunakan oleh seluruh halaman.

## 8. Cara Menjalankan Project

### Persyaratan

Pastikan perangkat sudah memiliki:

- Flutter stable
- Dart SDK yang sesuai dengan versi Flutter
- Android Studio atau Android SDK
- Emulator Android atau perangkat Android fisik
- VS Code atau IDE lain yang mendukung Flutter

### Langkah menjalankan

Masuk ke folder project:

```bash
cd print_manager
```

Ambil dependency:

```bash
flutter pub get
```

Periksa perangkat yang tersedia:

```bash
flutter devices
```

Jalankan aplikasi:

```bash
flutter run
```

Untuk menjalankan pada Android dalam mode debug:

```bash
flutter run -d <device_id>
```

## 9. Cara Login

Gunakan akun demo berikut:

```text
Username: admin
Password: admin123
```

Setelah login berhasil, session disimpan secara lokal. Saat aplikasi dibuka kembali, pengguna langsung diarahkan ke Home selama session belum dihapus.

## 10. Pengujian dan Validasi

Widget test tersedia pada:

```text
test/widget_test.dart
```

Perintah untuk menjalankan test:

```bash
flutter test
```

Perintah untuk memeriksa kode:

```bash
flutter analyze
```

Perintah untuk membuat APK Android:

```bash
flutter build apk --debug
```

Hasil APK debug berada di:

```text
build/app/outputs/flutter-apk/app-debug.apk
```

Widget test login telah berhasil dijalankan dan build APK Android berhasil dibuat. Analyzer masih dapat menampilkan beberapa informasi lint terkait gaya penulisan satu baris dan penggunaan API `DropdownButtonFormField.value` yang deprecated pada versi Flutter terbaru, tetapi tidak menghalangi proses build aplikasi.

## 11. Kelebihan Aplikasi

1. Tidak membutuhkan server atau koneksi backend.
2. Data pesanan tersimpan di database lokal.
3. Struktur file dipisahkan berdasarkan tanggung jawab.
4. Memiliki CRUD pesanan lengkap.
5. Memiliki login dan session.
6. Memiliki beberapa fitur komputasi yang relevan dengan tugas.
7. Source code masih sederhana dan mudah dipelajari mahasiswa pemula.

## 12. Keterbatasan dan Pengembangan Berikutnya

Beberapa bagian masih dapat dikembangkan lebih lanjut:

1. Login masih menggunakan akun demo tetap dan belum memiliki tabel pengguna.
2. Konversi Hijriah masih berupa pendekatan, bukan perhitungan astronomi atau library kalender Hijriah penuh.
3. Perhitungan Sasih Bali masih menggunakan pendekatan pembagian 30 hari.
4. Data Nyepi yang tersedia pada service saat ini berfokus pada tahun modern 2020 sampai 2030.
5. Weton yang ditampilkan baru menggunakan pasaran dasar dan belum menghitung siklus wuku secara lengkap.
6. Belum tersedia fitur pencarian dan filter pesanan.
7. Belum tersedia laporan atau export data ke PDF.
8. Belum tersedia backup dan restore database.
9. Belum terdapat manajemen banyak pengguna atau role pengguna.

## 13. Kesimpulan

PrintManager berhasil dibuat sebagai aplikasi mobile sederhana untuk mendukung pengelolaan percetakan. Aplikasi telah menerapkan Flutter, Dart, Material Design, SQLite, SharedPreferences, model data, service, navigasi, session, CRUD, serta beberapa fitur perhitungan dan konversi kalender.

Pemisahan source code ke dalam folder `models`, `database`, `services`, dan `screens` membuat aplikasi lebih mudah dibaca, diuji, dan dikembangkan. Aplikasi ini dapat menjadi dasar untuk pengembangan sistem manajemen percetakan yang lebih lengkap, seperti laporan transaksi, pencarian pesanan, autentikasi pengguna, dan perhitungan kalender yang lebih akurat.

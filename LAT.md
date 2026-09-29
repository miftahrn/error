# Aplikasi Data Hewan

Aplikasi Flutter sederhana untuk latihan Praktikum Pemrograman Aplikasi Mobile. Aplikasi ini memiliki fitur login, daftar data hewan, halaman detail hewan, dan logout.

## Menjalankan Aplikasi

Jalankan perintah berikut dari folder project:

```bash
flutter pub get
flutter run
```

Untuk memeriksa kode dan menjalankan test:

```bash
flutter analyze
flutter test
```

## Login Latihan

Gunakan data berikut untuk masuk:

- Username/NIM: `12345678`
- Password/program studi: `Informatika`

Nilai login dapat diubah di `lib/pages/login_page.dart`:

```dart
final String usernameBenar = '12345678';
final String passwordBenar = 'Informatika';
```

## Struktur Folder

```text
lib/
|-- main.dart
|-- models/
|   `-- animal.dart
|-- data/
|   `-- animals_data.dart
`-- pages/
  |-- login_page.dart
  |-- home_page.dart
  `-- animal_detail_page.dart
```

## Penjelasan File

### `main.dart`

File ini adalah titik awal aplikasi.

- `main()` menjalankan aplikasi dengan `runApp(const MyApp())`.
- `MyApp` adalah widget utama aplikasi.
- `MaterialApp` mengatur judul, tema warna, dan halaman pertama.
- `home: const LoginPage()` membuat halaman login tampil pertama kali.

### `models/animal.dart`

File ini berisi class `Animal` sebagai model data satu hewan. Field-nya adalah `name`, `type`, `weight`, `habitat`, `height`, `activities`, dan `image`.

Constructor `Animal` digunakan untuk mengisi semua field ketika object hewan dibuat. Konsep OOP yang digunakan adalah:

- **Class**: cetakan object, yaitu `Animal`.
- **Object**: data hewan yang dibuat berdasarkan class `Animal`.
- **Constructor**: fungsi khusus untuk mengisi data saat object dibuat.
- **Field**: variabel yang dimiliki object, seperti `name` dan `type`.

### `data/animals_data.dart`

File ini menyimpan list object `Animal` bernama `dummyAnimals`.

```dart
List<Animal> dummyAnimals = [
  Animal(
    name: 'Bengal Tiger',
    type: 'Mammal',
    // field lainnya
  ),
];
```

`List<Animal>` berarti list hanya berisi object bertipe `Animal`. Data ini digunakan oleh `HomePage` untuk menampilkan daftar hewan.

### `pages/login_page.dart`

File ini menampilkan form login menggunakan `StatefulWidget` karena halaman memiliki input yang dapat berubah.

#### `TextEditingController`

Ada dua controller untuk mengambil teks yang diketik pengguna:

```dart
final TextEditingController _usernameController = TextEditingController();
final TextEditingController _passwordController = TextEditingController();
```

#### Method `_login()`

Method ini:

1. Mengambil teks dari kedua controller.
2. Menghapus spasi dengan `trim()`.
3. Membandingkan input dengan `usernameBenar` dan `passwordBenar`.
4. Jika benar, membuka `HomePage`.
5. Jika salah atau kosong, menampilkan `SnackBar` merah.

```dart
if (username == usernameBenar && password == passwordBenar) {
  // Login berhasil
} else {
  // Login gagal
}
```

`dispose()` membersihkan controller ketika halaman tidak lagi digunakan.

#### `Navigator.pushReplacement`

Saat login berhasil, kode berikut mengganti halaman login dengan HomePage:

```dart
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => const HomePage()),
);
```

Pengguna tidak dapat kembali ke halaman login dengan tombol back setelah login berhasil.

### `pages/home_page.dart`

`HomePage` menampilkan semua data dari `dummyAnimals`.

#### `ListView.builder`

`ListView.builder` membuat item berdasarkan jumlah data:

```dart
itemCount: dummyAnimals.length,
itemBuilder: (context, index) {
  final Animal animal = dummyAnimals[index];
  // menampilkan animal
}
```

- `itemCount` menentukan jumlah item.
- `index` adalah posisi data yang sedang dibuat.
- `dummyAnimals[index]` mengambil satu object hewan.
- `Image.network` menampilkan foto dari URL.

Setiap item menampilkan foto, nama, tipe, dan habitat. Ketika item ditekan, method `_openAnimalDetail()` dijalankan.

#### Mengirim object ke detail

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => AnimalDetailPage(animal: animal),
  ),
);
```

Object `animal` dikirim melalui constructor `AnimalDetailPage`, sehingga halaman detail mengetahui data hewan yang dipilih.

#### Logout

Tombol logout berada di AppBar. Method `_logout()` membuka LoginPage dengan `Navigator.pushReplacement`, sehingga HomePage digantikan dan pengguna harus login kembali.

### `pages/animal_detail_page.dart`

Halaman ini menerima object hewan melalui constructor:

```dart
final Animal animal;

const AnimalDetailPage({super.key, required this.animal});
```

Kemudian semua data ditampilkan: Name, Type, Weight, Habitat, Height, Activities, dan Image.

Method `_infoRow()` membuat tampilan label dan nilai secara berulang, misalnya `Name: Bengal Tiger`.

Tombol kembali menjalankan:

```dart
Navigator.pop(context);
```

`Navigator.pop` menutup halaman detail dan kembali ke HomePage.

## Alur Aplikasi

```text
LoginPage
  | login berhasil: Navigator.pushReplacement
  v
HomePage --> tekan item hewan: Navigator.push --> AnimalDetailPage
  ^                                             |
  `------------- Navigator.pop <---------------'

HomePage --> tekan logout: Navigator.pushReplacement --> LoginPage
```

## Bagian Penting untuk Dipelajari

1. Membuat class dan constructor `Animal`.
2. Membuat dan membaca `List<Animal>`.
3. Mengambil input dengan `TextEditingController`.
4. Membuat validasi menggunakan `if/else`.
5. Memahami `Navigator.push`, `Navigator.pop`, dan `Navigator.pushReplacement`.
6. Mengirim data antar halaman melalui constructor.
7. Menampilkan list dinamis menggunakan `ListView.builder`.
8. Memahami perbedaan `StatelessWidget` dan `StatefulWidget`.

## Catatan Latihan

Aplikasi ini sengaja menggunakan data dan login sederhana di dalam source code agar mudah dipelajari. Pada aplikasi nyata, username, password, dan data sebaiknya disimpan serta divalidasi menggunakan backend atau database.

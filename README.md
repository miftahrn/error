# PROJECT SISTEM INFORMASI AKUNTANSI
## Studi Kasus: Sistem Informasi Akuntansi pada Perusahaan Percetakan

> Catatan: semua data perusahaan, observasi, wawancara, dan dokumentasi
> pada dokumen ini adalah data dummy dan wajib diganti dengan data nyata.

---

# DATA DASAR PERUSAHAAN

## 1. Identitas Perusahaan

- Nama perusahaan: CV Cetak Maju (data dummy)
- Bidang usaha: Percetakan / Offset Printing
- Alamat: Jl. Merdeka No. 25, Kota Bandung (data dummy)
- Tahun berdiri: 2018 (data dummy)
- Skala usaha: Usaha kecil menengah (data dummy)
- Jumlah karyawan: 12 orang (data dummy)
- Pemilik/pimpinan: Budi Santoso (data dummy)
- Jam operasional: Senin-Sabtu, 08.00-17.00 WIB (data dummy)

## 2. Gambaran Umum Perusahaan

CV Cetak Maju merupakan perusahaan yang bergerak di bidang percetakan,
khususnya jasa percetakan offset dan produk cetak lainnya. Perusahaan
melayani pesanan mulai dari penerimaan pesanan, penentuan kebutuhan
produksi, penggunaan bahan baku, proses produksi, hingga penyerahan hasil
cetak kepada pelanggan.

Sebagian proses pencatatan masih dilakukan secara manual sehingga terdapat
kendala dalam pencatatan pelanggan, pesanan, produk, bahan, karyawan, dan
transaksi. Sistem Informasi Akuntansi ini digunakan untuk menganalisis
kebutuhan sistem yang membantu pengelolaan transaksi dan informasi akuntansi.

---

# 3. KONDISI SISTEM SAAT INI (AS-IS)

## 3.1 Penerimaan Pesanan

1. Pelanggan menghubungi atau datang ke perusahaan.
2. Pelanggan menyampaikan kebutuhan cetak.
3. Admin mencatat informasi pesanan.
4. Admin menentukan produk atau jasa yang dipesan.
5. Perusahaan mengecek bahan dan kemampuan produksi.
6. Pesanan diteruskan ke bagian produksi.
7. Produk diproses sampai selesai.
8. Hasil cetak diserahkan kepada pelanggan.
9. Pembayaran dicatat sesuai kondisi transaksi.

Masalah utama: pencatatan pesanan, pelanggan, dan pembayaran masih
menggunakan buku catatan serta spreadsheet sederhana.

### Dokumentasi
- [FOTO 1 - Kegiatan penerimaan/administrasi pesanan]
- [FOTO 2 - Kondisi tempat kerja bagian administrasi]

## 3.2 Proses Produksi

1. Bagian produksi menerima informasi pesanan.
2. Bagian produksi mengecek kebutuhan bahan.
3. Bahan disiapkan.
4. Proses produksi dilakukan.
5. Hasil produksi diperiksa.
6. Pesanan yang sesuai diserahkan kepada pelanggan.
7. Jika terdapat masalah, dilakukan perbaikan atau produksi ulang.

### Dokumentasi
- [FOTO 3 - Aktivitas proses produksi]
- [FOTO 4 - Mesin/peralatan percetakan]

## 3.3 Pengelolaan Bahan

1. Stok bahan diperiksa.
2. Bahan yang tersedia digunakan untuk produksi.
3. Jika tidak mencukupi, dilakukan pembelian.
4. Bahan yang diterima dicatat.
5. Bahan disimpan dan digunakan sesuai kebutuhan.

Pembaruan stok belum selalu dilakukan segera setelah bahan digunakan atau
diterima dari pemasok.

### Dokumentasi
- [FOTO 5 - Gudang/tempat penyimpanan bahan]
- [FOTO 6 - Contoh bahan baku percetakan]

---

# 4. TRANSAKSI / SIKLUS SIA

## 4.1 Siklus Pendapatan (Revenue Cycle)

Pelanggan -> Pesanan -> Penjualan -> Piutang (jika ada) -> Pembayaran ->
Penerimaan kas.

Data yang dicatat meliputi pelanggan, pesanan, detail pesanan, harga, jumlah,
total transaksi, status pembayaran, metode pembayaran, dan tanggal pembayaran.

## 4.2 Siklus Pengeluaran (Expenditure Cycle)

Kebutuhan bahan -> Pembelian bahan -> Penerimaan bahan -> Utang (jika kredit)
-> Pembayaran kepada pemasok.

Data yang dicatat meliputi pemasok, bahan, pembelian, detail pembelian,
jumlah, harga, total pembelian, status pembayaran, dan tanggal pembayaran.

---

# 5. MASALAH SISTEM SAAT INI

## Masalah 1 - Pencatatan masih manual

Pencatatan dilakukan melalui buku dan spreadsheet dengan format yang belum
seragam, sehingga admin perlu memeriksa beberapa sumber.

Dampak: risiko kesalahan, data sulit dicari, dan waktu pencatatan lebih lama.

## Masalah 2 - Pemantauan status pesanan

Status pesanan dikonfirmasi melalui komunikasi langsung antara admin dan
produksi. Belum tersedia daftar status terpusat.

Dampak: posisi pesanan sulit diketahui dan risiko keterlambatan meningkat.

## Masalah 3 - Pengelolaan bahan baku

Stok kertas, tinta, dan bahan pendukung dicatat secara berkala, tetapi tidak
selalu diperbarui saat bahan digunakan atau diterima.

Dampak: risiko kekurangan atau kelebihan stok dan gangguan produksi.

## Masalah 4 - Pencatatan transaksi dan pembayaran

Nota dan bukti pembayaran disimpan secara terpisah. Rekap transaksi dibuat
secara manual pada akhir periode.

Dampak: rekap membutuhkan waktu dan riwayat pembayaran sulit ditelusuri.

---

# 6. DATA COLLECTION

## 6.1 Observasi

Aspek yang diamati:

- [x] Penerimaan pesanan
- [x] Pencatatan pelanggan
- [x] Pencatatan transaksi
- [x] Proses produksi
- [x] Penggunaan bahan
- [x] Pengadaan bahan
- [x] Penerimaan bahan
- [x] Pembayaran
- [x] Penyimpanan dokumen
- [x] Pelaporan

### Dokumentasi Observasi
- [FOTO 7 - Kegiatan observasi]
- [FOTO 8 - Aktivitas karyawan]
- [FOTO 9 - Proses administrasi]

## 6.2 Wawancara

Informan:
- Nama: Rina Permata (data dummy)
- Jabatan: Admin Operasional (data dummy)
- Tanggal: 15 September 2026 (data dummy)
- Lokasi: Kantor CV Cetak Maju (data dummy)

### Daftar Pertanyaan

1. Bagaimana proses penerimaan pesanan pelanggan?
2. Bagaimana data pelanggan dicatat?
3. Bagaimana harga pesanan ditentukan?
4. Bagaimana proses pembayaran pelanggan?
5. Bagaimana transaksi penjualan dicatat?
6. Bagaimana perusahaan mengetahui stok bahan?
7. Bagaimana proses pembelian bahan?
8. Bagaimana pembayaran kepada pemasok dilakukan?
9. Bagaimana status pesanan dipantau?
10. Laporan apa yang dibutuhkan pemilik?

### Hasil Wawancara

Pelanggan menyampaikan kebutuhan melalui WhatsApp atau datang langsung. Admin
mencatat spesifikasi, menghitung estimasi harga, dan meneruskan detail kepada
produksi. Pembayaran dilakukan melalui transfer atau tunai. Stok diperiksa
sebelum produksi dan bahan dibeli jika persediaan tidak cukup. Pemilik
membutuhkan laporan pesanan, penjualan, pembayaran, pembelian, dan stok.

## 6.3 Dokumen yang Diamati

Nota, invoice, bukti pembayaran, catatan pesanan, catatan pembelian, catatan
stok, dokumen produksi, data pelanggan, dan data pemasok.

---

# 7. DOKUMENTASI LAPANGAN

## Foto 1
**Kegiatan:** Penerimaan pesanan pelanggan (data dummy)  
**Lokasi:** Ruang administrasi (data dummy)  
**Tanggal:** 15 September 2026 (data dummy)  
**Keterangan:** Admin mencatat detail pesanan.  
[MASUKKAN FOTO]

## Foto 2
**Kegiatan:** Proses produksi (data dummy)  
**Lokasi:** Area produksi (data dummy)  
**Tanggal:** 16 September 2026 (data dummy)  
**Keterangan:** Operator menyiapkan bahan dan menjalankan mesin.  
[MASUKKAN FOTO]

## Foto 3
**Kegiatan:** Pemeriksaan bahan baku (data dummy)  
**Lokasi:** Gudang bahan (data dummy)  
**Tanggal:** 16 September 2026 (data dummy)  
**Keterangan:** Admin memeriksa jumlah kertas dan tinta.  
[MASUKKAN FOTO]

---

# 8. DATA YANG DIPERLUKAN SISTEM

## 8.1 Data Master

### Pelanggan
- id_pelanggan, nama_pelanggan, alamat, nomor_telepon, email

### Produk/Jasa
- id_produk, nama_produk, jenis, ukuran, harga

### Bahan
- id_bahan, nama_bahan, satuan, stok

### Karyawan
- id_karyawan, nama, jabatan, gaji

### Pemasok
- id_pemasok, nama_pemasok, alamat, nomor_telepon

## 8.2 Data Transaksi

### Pesanan
- id_pesanan, id_pelanggan, tanggal_pesanan, status_pesanan

### Detail Pesanan
- id_detail_pesanan, id_pesanan, id_produk, jumlah, harga, subtotal

### Pembayaran Pelanggan
- id_pembayaran, id_pesanan, tanggal_pembayaran, jumlah_bayar, metode_pembayaran

### Pembelian Bahan
- id_pembelian, id_pemasok, tanggal_pembelian, status_pembelian

### Detail Pembelian
- id_detail_pembelian, id_pembelian, id_bahan, jumlah, harga, subtotal

### Pembayaran Pemasok
- id_pembayaran_pemasok, id_pembelian, jumlah_bayar, metode_pembayaran

---

# 9. RANCANGAN ENTITAS SIA

Pelanggan, Pesanan, Detail_Pesanan, Produk, Bahan, Karyawan, Pemasok,
Pembayaran_Pelanggan, Pembelian, Detail_Pembelian, dan Pembayaran_Pemasok.

# 10. HUBUNGAN ANTAR ENTITAS

- Pelanggan 1:N Pesanan
- Pesanan 1:N Detail_Pesanan
- Produk 1:N Detail_Pesanan
- Pesanan 1:N Pembayaran_Pelanggan
- Pemasok 1:N Pembelian
- Pembelian 1:N Detail_Pembelian
- Bahan 1:N Detail_Pembelian
- Pembelian 1:N Pembayaran_Pemasok

# 11. FUNCTIONAL REQUIREMENTS

- **FR-01:** Sistem dapat menyimpan data pelanggan.
- **FR-02:** Sistem dapat mencatat pesanan dan detail pesanan.
- **FR-03:** Sistem dapat mencatat pembayaran pelanggan.
- **FR-04:** Sistem dapat mencatat data bahan.
- **FR-05:** Sistem dapat mencatat pembelian bahan.
- **FR-06:** Sistem dapat mencatat pembayaran kepada pemasok.
- **FR-07:** Sistem dapat memperbarui stok bahan.
- **FR-08:** Sistem dapat menghasilkan laporan transaksi.

# 12. NON-FUNCTIONAL REQUIREMENTS

- **NFR-01 Security:** Login berdasarkan hak akses pengguna.
- **NFR-02 Performance:** Data transaksi ditampilkan dalam waktu wajar.
- **NFR-03 Usability:** Antarmuka mudah digunakan admin dan perusahaan.
- **NFR-04 Data Integrity:** Data wajib harus lengkap sebelum disimpan.
- **NFR-05 Audit Trail:** Perubahan transaksi penting dapat ditelusuri.

# 13. USER STORIES

- **US-01:** Sebagai admin, saya ingin mencatat pelanggan agar datanya dapat digunakan kembali.
- **US-02:** Sebagai admin, saya ingin mencatat pesanan agar transaksi terdokumentasi.
- **US-03:** Sebagai admin, saya ingin mencatat pembayaran agar status pembayaran diketahui.
- **US-04:** Sebagai bagian pembelian, saya ingin mencatat pembelian bahan.
- **US-05:** Sebagai pemilik, saya ingin melihat laporan transaksi.

# 14. MOSCOW PRIORITIZATION

| ID | Requirement | Prioritas |
|---|---|---|
| FR-01 | Data pelanggan | Must |
| FR-02 | Pesanan | Must |
| FR-03 | Pembayaran pelanggan | Must |
| FR-04 | Data bahan | Must |
| FR-05 | Pembelian bahan | Must |
| FR-06 | Pembayaran pemasok | Must |
| FR-07 | Stok bahan | Must |
| FR-08 | Laporan | Should |

# 15. NORMALISASI

## Tabel Awal

Contoh data belum ternormalisasi: satu baris memuat pelanggan, pesanan,
beberapa produk, bahan, dan pembayaran sekaligus.

## 1NF

Setiap kolom berisi satu nilai dan setiap detail produk dibuat sebagai baris
terpisah pada tabel Detail_Pesanan.

## 2NF

Data pelanggan dan produk dipisahkan dari detail pesanan agar tidak bergantung
sebagian pada kunci gabungan.

## 3NF

Data pemasok, bahan, pembayaran, dan pesanan dipisahkan sehingga tidak ada
ketergantungan transitif.

# 16. DATABASE DESIGN

```sql
CREATE TABLE pelanggan (
    id_pelanggan INT PRIMARY KEY,
    nama_pelanggan VARCHAR(100) NOT NULL,
    alamat TEXT,
    nomor_telepon VARCHAR(20),
    email VARCHAR(100)
);
```

---

# 17. DATA DICTIONARY

| Tabel | Field | Tipe Data | Key | Keterangan |
|---|---|---|---|---|
| pelanggan | id_pelanggan | INT | PK | ID pelanggan |
| pelanggan | nama_pelanggan | VARCHAR(100) | - | Nama pelanggan |
| pesanan | id_pesanan | INT | PK | ID pesanan |
| pesanan | id_pelanggan | INT | FK | Relasi ke pelanggan |
| pesanan | tanggal_pesanan | DATE | - | Tanggal pesanan |
| pesanan | status_pesanan | VARCHAR(30) | - | Status pesanan |
| pembayaran_pelanggan | id_pembayaran | INT | PK | ID pembayaran |
| pembayaran_pelanggan | id_pesanan | INT | FK | Relasi ke pesanan |

Data dictionary ini masih berupa contoh awal dan akan dilengkapi setelah ERD
final disepakati.

# 18. TRACEABILITY MATRIX

| Requirement | Sumber | Entitas/Tabel |
|---|---|---|
| FR-01 | Wawancara admin (dummy) | Pelanggan |
| FR-02 | Observasi pesanan (dummy) | Pesanan, Detail_Pesanan |
| FR-03 | Wawancara admin (dummy) | Pembayaran_Pelanggan |
| FR-04 | Observasi gudang (dummy) | Bahan |
| FR-05 | Observasi pengadaan (dummy) | Pembelian, Detail_Pembelian |
| FR-06 | Wawancara pemilik (dummy) | Pembayaran_Pemasok |

# 19. TRIANGULASI

**Observasi:** Pencatatan pesanan dan stok masih dilakukan secara manual.  
**Wawancara:** Admin membutuhkan pencatatan terpusat dan laporan berkala.  
**Dokumen:** Nota dan catatan stok menjadi bukti utama transaksi (dummy).  
**Kesimpulan:** Ketiga sumber menunjukkan kebutuhan sistem terintegrasi.

**Prosedur tertulis:** Setiap pesanan dan perubahan stok dicatat pada dokumen.  
**Praktik sebenarnya:** Sebagian informasi disampaikan melalui chat dan direkap kemudian.  
**Perbedaan:** Pencatatan aktual tidak selalu dilakukan saat transaksi.  
**Dampak:** Informasi dapat terlambat dan tidak sinkron.

# 20. DOKUMENTASI PENDUKUNG

Daftar bukti dummy: foto kegiatan KP, foto administrasi, foto produksi, foto
mesin, foto bahan, foto dokumen transaksi, foto nota/invoice, foto lingkungan
perusahaan, hasil wawancara, dan hasil observasi.

Foto atau dokumen yang mengandung data sensitif akan disensor sebelum dimasukkan
ke laporan.

# 21. STRUKTUR LAPORAN UTS

- **BAB I - Profil dan Analisis Masalah:** profil, struktur, proses bisnis, siklus, masalah, tujuan, dan ruang lingkup.
- **BAB II - Pengumpulan Data:** metode, wawancara, observasi, studi dokumen, hasil, dan triangulasi.
- **BAB III - SRS:** functional requirements, non-functional requirements, MoSCoW, user stories, traceability, konflik, dan verifikasi.
- **BAB IV - Perancangan Basis Data:** kebutuhan data, ERD, relasi, skema, normalisasi, DDL, sample data, dan data dictionary.
- **BAB V - Progres dan Rencana Tahap 2:** progres, kontribusi, pengembangan, pembagian tugas, teknologi, dan refleksi.
- **LAMPIRAN:** dokumentasi foto, bukti wawancara, dokumen, DDL SQL, pengujian, log progres, kontribusi, dan deklarasi penggunaan AI.

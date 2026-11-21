# TUGAS MANDIRI 02E – DETEKTIF AUDIT BLUEPRINT CACAT

**Nama:** Hanif Abdurrahman Arrifa'i

## 1. Mismatch 1 (Pseudocode vs Flowchart)

Pada Pseudocode terdapat pengecekan kondisi `voucher.kuota_pakai <= 0` untuk memastikan apakah kuota voucher masih tersedia sebelum digunakan. Selain itu, terdapat proses pengurangan kuota voucher setelah voucher berhasil digunakan.

Namun, pada Flowchart kedua logika tersebut belum digambarkan secara lengkap.

**Perbaikan:**
Tambahkan langkah pengecekan sisa kuota voucher pada Flowchart. Jika kuota voucher sudah habis, proses penggunaan voucher dihentikan. Jika kuota masih tersedia, proses dapat dilanjutkan dan kuota voucher dikurangi setelah berhasil digunakan.

## 2. Mismatch 2 (Logika vs Atribut ERD)

Pada Pseudocode dan Flowchart terdapat pemeriksaan syarat `minimal_belanja` untuk menentukan apakah pembeli memenuhi ketentuan minimum transaksi agar dapat menggunakan voucher.

Namun, pada ERD entitas `VOUCHER` belum memiliki atribut `minimal_belanja`.

Hal ini menyebabkan ketidaksesuaian antara logika program dengan struktur basis data karena sistem memeriksa suatu kondisi yang datanya belum tersedia dalam ERD.

**Perbaikan:**
Tambahkan atribut `minimal_belanja` dengan tipe data `int` pada entitas `VOUCHER` agar sistem dapat menyimpan dan memeriksa batas minimum transaksi sebelum voucher digunakan.

## 3. Mismatch 3 (Konsistensi Penamaan Atribut)

Terdapat perbedaan penamaan atribut untuk menyimpan jumlah kuota voucher. Pada Pseudocode digunakan nama `kuota_pakai`, sedangkan pada ERD digunakan nama `sisa_kuota`.

Perbedaan tersebut dapat menyebabkan kebingungan dalam proses pengembangan sistem karena satu data memiliki dua nama atribut yang berbeda.

Selain itu, penamaan atribut harus konsisten antara Pseudocode, Flowchart, dan ERD.

**Perbaikan:**
Seragamkan nama atribut di seluruh dokumen menjadi:
- `kode_voucher` sebagai identitas voucher.
- `minimal_belanja` sebagai batas minimum transaksi.
- `nilai_potongan` sebagai jumlah potongan harga.
- `sisa_kuota` sebagai jumlah kuota voucher yang masih tersedia.

Dengan demikian, penggunaan atribut `kuota_pakai` pada Pseudocode perlu diubah menjadi `sisa_kuota` agar sesuai dengan ERD.

## 4. Kesimpulan

Berdasarkan hasil pemeriksaan blueprint, ditemukan tiga ketidaksinkronan antara Pseudocode, Flowchart, dan ERD.

Pertama, terdapat logika pengecekan dan pengurangan kuota voucher pada Pseudocode yang belum digambarkan secara lengkap pada Flowchart. Kedua, terdapat kondisi pemeriksaan `minimal_belanja` dalam logika program, tetapi atribut tersebut belum tersedia pada ERD. Ketiga, terdapat ketidakkonsistenan penamaan atribut antara `kuota_pakai` pada Pseudocode dan `sisa_kuota` pada ERD.

Oleh karena itu, ketiga bagian tersebut perlu diperbaiki agar Pseudocode, Flowchart, dan ERD memiliki logika serta struktur data yang konsisten. Dengan adanya perbaikan ini, rancangan sistem penggunaan voucher dapat menjadi lebih jelas, terstruktur, dan mudah dikembangkan.

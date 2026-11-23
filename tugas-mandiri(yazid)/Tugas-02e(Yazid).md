# Tugas Mandiri 02e — Detektif Audit Blueprint Cacat
Nama:Ahmad Yazid

## 1. Mismatch 1 (Pseudocode vs Flowchart):
Di Pseudocode ada pengecekan `JIKA voucher.kuota_pakai <= 0` yang menampilkan "Kuota voucher sudah habis", dan ada langkah `UBAH voucher.kuota_pakai = voucher.kuota_pakai - 1` setelah voucher dipakai. Kedua langkah itu tidak digambar di Flowchart: tidak ada simbol keputusan untuk cek kuota, dan tidak ada langkah proses untuk mengurangi kuota. Akibatnya Flowchart akan mengizinkan voucher dipakai terus-menerus tanpa batas.

## 2. Mismatch 2 (Variabel Siluman yang Tidak Ada di ERD):
Pseudocode dan Flowchart sama-sama memeriksa syarat `total_belanja < voucher.minimal_belanja`, tetapi entitas `VOUCHER` di ERD belum memiliki atribut `minimal_belanja (int)`. Nilai yang dibutuhkan algoritma tidak punya tempat penyimpanan di basis data.

## 3. Mismatch 3 (Ketidakkonsistenan Nama Atribut):
Untuk menyimpan jumlah kuota voucher, Pseudocode menulis `kuota_pakai` sedangkan ERD menulis `sisa_kuota`. Selain itu, pengenal voucher disebut `kode_input` di Pseudocode, sedangkan di ERD kunci utamanya bernama `kode_voucher`.

**Perbaikan:** Seragamkan nama atribut di Pseudocode, Flowchart, dan ERD menjadi `kode_voucher`, `minimal_belanja`, `nilai_potongan`, dan `kuota_pakai`. Variabel input pengguna boleh tetap `kode_input`, tetapi saat pencarian harus jelas dicocokkan ke `voucher.kode_voucher`.

## 4. Cek Pemahaman Diri

1. Jika ada variabel di Flowchart yang tidak punya kolom di ERD, tim tidak tahu di mana data itu disimpan saat mulai ngoding di Bulan 2. Programmer harus menebak atau menambah kolom sendiri, sehingga nama dan tipe datanya bisa berbeda-beda antar anggota tim, dan kodenya bisa error atau datanya hilang.
2. Setiap blok `JIKA ... MAKA ... LAINNYA` adalah titik percabangan, dan di Flowchart percabangan hanya digambar dengan belah ketupat (Decision) yang punya jalur Ya dan Tidak. Jika tidak berpasangan, salah satu cabang hilang dari gambar, dan pembaca Flowchart tidak tahu apa yang terjadi di kondisi tersebut.

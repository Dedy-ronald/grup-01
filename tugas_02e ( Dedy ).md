# Tugas Mandiri 02e — Detektif Audit Blueprint Cacat
Nama: [Dedy]

## 1. Mismatch 1 (Pseudocode vs Flowchart):
Di dalam Pseudocode terdapat logika validasi ketersediaan kuota (`JIKA voucher.kuota_pakai <= 0 MAKA TAMPILKAN "Kuota voucher sudah habis"`) serta proses pembaruan data kuota setelah digunakan (`UBAH voucher.kuota_pakai = voucher.kuota_pakai - 1`). Namun, pada diagram Flowchart kedua proses penting tersebut hilang dan tidak digambarkan sama sekali.

## 2. Mismatch 2 (Logika vs Atribut ERD):
Pada Pseudocode (`JIKA total_belanja < voucher.minimal_belanja`) dan Flowchart, sistem sama-sama melakukan pengecekan syarat batas minimum transaksi menggunakan atribut `minimal_belanja`. Akan tetapi, pada potongan ERD entitas `VOUCHER` belum memiliki kolom atribut `minimal_belanja (int)` sehingga logika tersebut tidak memiliki sumber data di basis data.

## 3. Mismatch 3 (Konsistensi Penamaan):
Terdapat perbedaan penamaan atribut kuota antara Pseudocode yang menggunakan nama `voucher.kuota_pakai` dan ERD yang menuliskannya sebagai `sisa_kuota`. Selain itu, terdapat perbedaan penyebutan kode voucher antara variabel input `kode_input` dengan kunci utama `kode_voucher`.

**Perbaikan:** 
Seragamkan seluruh nama atribut dan kolom pada Pseudocode, Flowchart, maupun ERD menggunakan satu standar baku (misalnya: `kode_voucher`, `minimal_belanja`, `nilai_potongan`, dan `sisa_kuota`), serta pastikan proses pengecekan dan pengurangan `sisa_kuota` ditambahkan ke dalam Flowchart.

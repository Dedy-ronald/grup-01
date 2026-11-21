# Tugas Mandiri 02e — Detektif Audit Blueprint Cacat

**Nama:** Aliffuddin Adilla Rafif

## 1. Mismatch 1 (Pseudocode vs Flowchart)

Pada Pseudocode terdapat pengecekan `voucher.kuota_pakai <= 0` untuk memastikan kuota voucher masih tersedia. Selain itu, terdapat proses pengurangan kuota setelah voucher berhasil digunakan.

Namun, pada Flowchart kedua proses tersebut belum digambarkan. Akibatnya, alur program tidak sepenuhnya sesuai dengan logika Pseudocode.

**Perbaikan:** Tambahkan proses pengecekan kuota voucher dan proses pengurangan kuota setelah voucher berhasil digunakan ke dalam Flowchart.

## 2. Mismatch 2 (Logika vs Atribut ERD)

Pada Pseudocode dan Flowchart terdapat pengecekan `minimal_belanja` untuk memastikan total belanja pelanggan memenuhi syarat penggunaan voucher.
s
Namun, pada tabel ERD `VOUCHER` belum terdapat atribut `minimal_belanja` untuk menyimpan batas minimum belanja tersebut.

**Perbaikan:** Tambahkan atribut `minimal_belanja` dengan tipe data `int` ke dalam entitas `VOUCHER`.

## 3. Mismatch 3 (Konsistensi Penamaan)

Terdapat perbedaan nama atribut antara Pseudocode dan ERD. Pada Pseudocode menggunakan nama `kuota_pakai`, sedangkan pada ERD menggunakan nama `sisa_kuota`.

Selain itu, kode voucher juga harus menggunakan nama yang konsisten agar tidak membingungkan saat proses pengambilan data.

**Perbaikan:** Samakan nama atribut di seluruh rancangan menjadi:
- `kode_voucher` untuk kode voucher.
- `minimal_belanja` untuk syarat minimum pembelian.
- `nilai_potongan` untuk jumlah diskon.
- `kuota_pakai` untuk jumlah kuota voucher yang tersisa.

## 4. Kesimpulan

Dari hasil pemeriksaan, dapat disimpulkan bahwa Pseudocode, Flowchart, dan ERD harus memiliki alur dan penamaan yang konsisten. Jika terdapat perbedaan, program dapat mengalami kesalahan ketika dikembangkan menjadi kode sebenarnya.

Oleh karena itu, ketiga rancangan harus diperiksa dan disesuaikan terlebih dahulu agar fitur penggunaan voucher dapat berjalan dengan baik.
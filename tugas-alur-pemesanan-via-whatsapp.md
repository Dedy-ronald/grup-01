### KNTL (Keep Never Tired Learning) Squad

## Laporan Workshop Squad: Alur Pemesanan Via Whatsapp

**1.Dekomposisi dan Pengenalan Pola"**
*A. Dekomposisi Alur Pemesanan (8 Langkah berurutan)*
1. Pembukaan Katalog: Pembeli membuka katalog dan melihat-lihat produk yang tersedia.
2. Pemilihan Produk: Pembeli memilih produk yang tertarik dan ingin ia beli serta memasukkan jumlah barang yang ingin dia beli.
3. Pengisian Data Pengiriman: Pembeli mengisi nama penerima, no handphone agar bisa dihubungi, dan alamat untuk tujuan pengantaran barang agar bisa dihitung jarak pengiriman.
4. Validasi Input & Stok. Sistem memeriksa kelengkapan data pembeli serta memastikan jumlah pesanan tidak melebihi sisa stok toko
5. Kalkulasi Tagihan. Sistem menghitung subtotal belanja, potongan diskon, dan biaya ongkos kirim menjadi total akhir.
6. Konfirmasi Ringkasan Pesanan. Pembeli meninjau rincian pesanan beserta total tagihan pada layar konfirmasi sebelum mengirim.
7. Pembuatan Pesan Otomatis. Sistem menyusun format teks rincian pesanan dan mengonversinya menjadi tautan khusus (URL encoding).
8. Pengalihan ke WhatsApp. Sistem mengarahkan pembeli membuka aplikasi WhatsApp dengan pesan yang sudah terisi otomatis ke nomor pedagang.

*B. Identifikasi Pola Berulang*
1. Pola Validasi Input Kosong dan Nilai Negatif/Nol: kedua proses sama-sama mewajibkan sistem memeriksa apakah kolom isian wajib sudah terisi sebelum data diproses lebih lanjut.
2. Penerapan pada Pembeli: sistem mengecek agar kolom nama tidak kosong dan jumlah beli bernilai minimal 1 (jumlah_beli > 0).
3. Penerapan pada Pedagang: sistem mengecek agar kolom nama produk tidak kosong serta harga dan stok produk bernilai lebih dari nol (harga > 0 dan stok > 0).


**2.Abstraksi dan Penulisan Pseudo Code"**
**3.Stretch Goal: Algoritma Peringatan Stok Menipis"**
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
Berikut saya kerjakan seluruh tugas nomor 1 sampai nomor 3 berdasarkan instruksi pada gambar. Jawaban sudah disusun dengan bahasa sederhana dan format yang bisa langsung kamu salin ke tugas.

# TAHAP 2: ABSTRAKSI & PENULISAN PSEUDOCODE

## 1. Abstraksi Data Inti

Data yang wajib ada untuk menghitung total pembayaran pembeli pada aplikasi kasir warung adalah:

1. Total Belanja (`total_belanja`): Untuk mengetahui jumlah harga seluruh barang yang dibeli.
2. Jarak Pengiriman (`jarak_km`): Untuk mengetahui jarak pengiriman barang ke rumah pembeli.
3. Diskon (`diskon`): Untuk menghitung potongan harga yang diberikan kepada pembeli.
4. Ongkos Kirim (`ongkir`): Untuk menghitung biaya pengiriman barang.
5. Total Akhir (`total_akhir`): Untuk mengetahui jumlah uang yang harus dibayar oleh pembeli.

Contoh 2 Noise yang tidak perlu dicatat aplikasi:

1. Warna pakaian yang digunakan pembeli.
2. Kondisi cuaca ketika pembeli berbelanja.

Alasannya, kedua informasi tersebut tidak berpengaruh terhadap perhitungan harga barang, diskon, maupun ongkos kirim.

## 2. Pseudocode Wajib — Algoritma Hitung Diskon & Ongkir Warung

Aturan yang digunakan:

- Jika total belanja minimal Rp100.000, pembeli mendapatkan diskon 10%.
- Diskon maksimal adalah Rp20.000.
- Jika jarak pengiriman 3 km atau kurang, ongkos kirim gratis.
- Jika jarak lebih dari 3 km, ongkos kirim Rp2.500 per km kelebihannya.
- Total pembayaran dihitung dari total belanja dikurangi diskon ditambah ongkos kirim.

Pseudocode:

```

MULAI

INPUT total_belanja
INPUT jarak_km

diskon = 0
ongkir = 0

JIKA total_belanja >= 100000 MAKA
    diskon = total_belanja * 10 / 100

    JIKA diskon > 20000 MAKA
        diskon = 20000
    AKHIR-JIKA
LAINNYA
    diskon = 0
AKHIR-JIKA

JIKA jarak_km <= 3 MAKA
    ongkir = 0
LAINNYA
    ongkir = (jarak_km - 3) * 2500
AKHIR-JIKA

total_akhir = total_belanja - diskon + ongkir

OUTPUT diskon
OUTPUT ongkir
OUTPUT total_akhir

SELESAI

```

Contoh hasil perhitungan:

Diketahui:

- Total belanja = Rp200.000
- Jarak pengiriman = 5 km

Perhitungan:

- Diskon = 10% × Rp200.000 = Rp20.000
- Ongkir = (5 − 3) × Rp2.500 = Rp5.000
- Total akhir = Rp200.000 − Rp20.000 + Rp5.000

TOTAL YANG HARUS DIBAYAR

# Rp182.500

Total belanja

Rp200.000

Diskon

-Rp20.000

Ongkos kirim

+Rp5.000

## 3. Tantangan Tambahan — Algoritma Peringatan Stok Menipis

Tujuan:

Membuat algoritma yang dapat memeriksa persediaan produk di warung. Jika jumlah stok barang 3 atau kurang, nama produk akan dimasukkan ke dalam daftar "Peringatan Restok Segera".

Contoh daftar produk:

| Nama Produk | Jumlah Stok |
| ----------- | ----------- |
| Indomie     | 10          |
| Kopi        | 2           |
| Gula        | 5           |
| Susu        | 3           |
| Teh         | 1           |

Pseudocode:

```

MULAI

daftar_peringatan = []

UNTUK SETIAP produk DALAM daftar_produk LAKUKAN

    JIKA produk.stok <= 3 MAKA
        MASUKKAN produk.nama KE daftar_peringatan
    AKHIR-JIKA

AKHIR-UNTUK

OUTPUT "Peringatan Restok Segera"
OUTPUT daftar_peringatan

SELESAI

```

Hasil pemeriksaan stok:

Produk yang masuk ke dalam daftar peringatan adalah:

1. Kopi (stok 2).
2. Susu (stok 3).
3. Teh (stok 1).

Produk Indomie dan gula tidak masuk daftar peringatan karena jumlah stoknya masih lebih dari 3.

## Kesimpulan

Dari tugas ini, saya belajar bahwa abstraksi digunakan untuk memilih data penting dan mengabaikan informasi yang tidak diperlukan. Pseudocode digunakan untuk menyusun langkah-langkah penyelesaian masalah sebelum dibuat menjadi program komputer. Selain itu, saya juga belajar menggunakan percabangan untuk menentukan diskon dan ongkos kirim, serta perulangan untuk memeriksa persediaan barang di warung.

Ketiga nomor sudah dikerjakan, termasuk contoh perhitungan dan hasil algoritmanya.

## Tahap 3: Uji Coba Manual / Dry Run Table (15 Menit)
Berikut pengujian pseudocode Diskon & Ongkir dengan 3 skenario. Aturan yang diuji: diskon 10% jika belanja ≥ Rp100.000 (maksimal Rp20.000), ongkir gratis jika jarak ≤ 3 km, selebihnya Rp2.500 per km kelebihan.

**Skenario 1: Belanja kecil, jarak dekat (tidak ada diskon, ongkir gratis)**

Input: total_belanja = 50.000, jarak_km = 2

| Langkah | Hasil |
|---|---|
| 50.000 >= 100.000? | Salah → diskon = 0 |
| 2 <= 3? | Benar → ongkir = 0 |
| total_akhir | 50.000 − 0 + 0 = **Rp50.000** |

**Skenario 2: Belanja sedang, jarak jauh (diskon 10% di bawah batas maksimal, ongkir berbayar)**

Input: total_belanja = 150.000, jarak_km = 7

| Langkah | Hasil |
|---|---|
| 150.000 >= 100.000? | Benar → diskon = 150.000 × 10 / 100 = 15.000 |
| 15.000 > 20.000? | Salah → diskon tetap 15.000 |
| 7 <= 3? | Salah → ongkir = (7 − 3) × 2.500 = 10.000 |
| total_akhir | 150.000 − 15.000 + 10.000 = **Rp145.000** |

**Skenario 3: Belanja besar, jarak tepat di batas (diskon dibatasi maksimal, ongkir gratis)**

Input: total_belanja = 300.000, jarak_km = 3

| Langkah | Hasil |
|---|---|
| 300.000 >= 100.000? | Benar → diskon = 30.000 |
| 30.000 > 20.000? | Benar → diskon dibatasi menjadi 20.000 |
| 3 <= 3? | Benar → ongkir = 0 |
| total_akhir | 300.000 − 20.000 + 0 = **Rp280.000** |

**Ringkasan**

| Skenario | Fokus yang diuji | Diskon | Ongkir | Total akhir |
|---|---|---|---|---|
| 1 | Di bawah syarat diskon, jarak dekat | 0 | 0 | Rp50.000 |
| 2 | Diskon normal, ongkir berbayar | 15.000 | 10.000 | Rp145.000 |
| 3 | Plafon diskon, jarak batas | 20.000 | 0 | Rp280.000 |

**Kesimpulan:** Ketiga skenario menghasilkan nilai yang sesuai dengan aturan, sehingga tidak ditemukan bug logika. Skenario ini mencakup cabang diskon tidak berlaku, diskon normal, dan diskon yang dibatasi plafon, serta cabang ongkir gratis dan ongkir berbayar. Skenario 3 sekaligus menguji batas jarak tepat 3 km (operator `<=`).

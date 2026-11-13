# Blueprint Fitur Terpadu: Konfirmasi Pesanan WA oleh Merchant & Potong Stok Otomatis (Opsi A)

## 1. Dekomposisi Masalah

1. **Penerimaan Input Konfirmasi**: Sistem menerima input `id_pesanan` saat merchant menekan tombol "Terima Pesanan" di dashboard.
2. **Pengambilan Data Pesanan**: Sistem mencari dan mengambil data pesanan dari tabel `PESANAN` berdasarkan `id_pesanan`.
3. **Validasi Status Pesanan**: Sistem memeriksa apakah `status_pesanan` bernilai `"Diteruskan ke WA"`. Jika tidak sesuai, sistem menolak proses dan menampilkan pesan kesalahan.
4. **Pengambilan Daftar Item & Data Produk**: Sistem mengambil seluruh daftar item dari `ITEM_PESANAN` yang terkait dengan `id_pesanan`, beserta data `stok` terkini dari tabel `PRODUK`.
5. **Validasi Ketersediaan Stok**: Sistem memeriksa untuk setiap item apakah `produk.stok >= item_pesanan.jumlah`.
6. **Penanganan Kegagalan Stok**: Jika ditemukan minimal satu item dengan `produk.stok < item_pesanan.jumlah`, sistem membatalkan proses konfirmasi, mengubah `status_pesanan` menjadi `"Batal"`, dan menampilkan peringatan gagal.
7. **Pembaruan Stok & Status Sukses**: Jika semua stok mencukupi, sistem mengurangi `produk.stok` sebanyak `item_pesanan.jumlah`, mengubah `status_pesanan` menjadi `"Dikonfirmasi Penjual"`, dan menampilkan pesan sukses.

---

## 2. Pseudocode Lengkap
## 3. Diagram Flowchart (Mermaid)
## 4. Potongan ERD (Mermaid)
## 5. Tabel Audit Konsistensi Silang
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
 
 MERCHANT ||--o{ PRODUK : memiliki
    KATEGORI ||--o{ PRODUK : mengelompokkan
    MERCHANT ||--o{ PESANAN : menerima
    PESANAN ||--|{ ITEM_PESANAN : memuat
    PRODUK ||--o{ ITEM_PESANAN : tercatat_dalam

    MERCHANT {
        string id_merchant PK
        string nama_toko
        string no_whatsapp
        string alamat
    }

    KATEGORI {
        string id_kategori PK
        string nama_kategori
    }

    PRODUK {
        string id_produk PK
        string id_merchant FK
        string id_kategori FK
        string nama_produk
        int harga
        int stok
    }

    PESANAN {
        string id_pesanan PK
        string id_merchant FK
        string tanggal_pesanan
        string nama_pembeli
        string wa_pembeli
        int total_bayar
        string status_pesanan
    }

    ITEM_PESANAN {
        string id_item PK
        string id_pesanan FK
        string id_produk FK
        int jumlah_beli
        int harga_satuan
        int subtotal
    }

## 5. Tabel Audit Konsistensi Silang
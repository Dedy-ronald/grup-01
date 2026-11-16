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

    '''MERCHANT {
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
    

## **5. Tabel Audit Konsistensi Silang**

| No. | Variabel / Kondisi yang Dicek | Pseudocode                              | Flowchart                                                         | ERD (Atribut)                                  | Status |
| --- | ----------------------------- | --------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------- | ------ |
| 1   | Mengecek stok produk          | `JIKA stok >= jumlah_beli`              | Menggunakan simbol belah ketupat untuk mengecek ketersediaan stok | `PRODUK.stok` dan `ITEM_PESANAN.jumlah_beli`   | Sesuai |
| 2   | Mengecek jumlah pembelian     | `jumlah_beli` diinput oleh pembeli      | Terdapat proses memasukkan jumlah produk                          | `ITEM_PESANAN.jumlah_beli`                     | Sesuai |
| 3   | Menghitung harga satuan       | Mengambil harga produk                  | Terdapat proses mengambil harga produk                            | `PRODUK.harga` dan `ITEM_PESANAN.harga_satuan` | Sesuai |
| 4   | Menghitung subtotal           | `subtotal = jumlah_beli * harga_satuan` | Terdapat proses perhitungan subtotal                              | `ITEM_PESANAN.subtotal`                        | Sesuai |
| 5   | Menghitung total pembayaran   | `total_bayar = jumlah seluruh subtotal` | Terdapat proses menghitung total pembayaran                       | `PESANAN.total_bayar`                          | Sesuai |
| 6   | Mengecek status pesanan       | `JIKA status_pesanan = "Diproses"`      | Menggunakan simbol belah ketupat untuk mengecek status pesanan    | `PESANAN.status_pesanan`                       | Sesuai |

## **Kesimpulan**

Berdasarkan tabel audit konsistensi silang, variabel yang digunakan dalam proses pemesanan produk sudah memiliki pasangan atribut pada ERD. Setiap kondisi pada pseudocode juga perlu digambarkan menggunakan simbol keputusan (belah ketupat) pada flowchart.

Dengan demikian, pseudocode, flowchart, dan ERD memiliki hubungan yang saling mendukung dalam menggambarkan alur sistem pemesanan produk UMKM.


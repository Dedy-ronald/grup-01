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

## 5. Tabel Audit Konsistensi Silang

Tabel ini digunakan untuk memeriksa apakah Pseudocode, Flowchart, dan ERD sudah saling sesuai.

### **1. Tabel Audit Konsistensi**

Berikut format tabel yang bisa dimasukkan ke file `blueprint-fitur-terpadu.md`.

| No. | Komponen yang Dicek     | Pseudocode                                      | Flowchart                                      | ERD                                                                    | Status |
| --- | ----------------------- | ----------------------------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------- | ------ |
| 1   | Kondisi pertama         | Kondisi `JIKA` sudah dituliskan                 | Sudah memiliki simbol belah ketupat (Decision) | Variabel kondisi tersedia sebagai atribut jika disimpan dalam database | Sesuai |
| 2   | Kondisi kedua           | Kondisi `JIKA` sudah dituliskan                 | Sudah memiliki simbol belah ketupat (Decision) | Variabel kondisi tersedia sebagai atribut jika disimpan dalam database | Sesuai |
| 3   | Variabel input          | Variabel sudah digunakan dalam pseudocode       | Variabel digunakan dalam alur proses           | Nama atribut tersedia di ERD                                           | Sesuai |
| 4   | Variabel perubahan data | Variabel sudah diperbarui menggunakan `SET`     | Terdapat proses perubahan data                 | Kolom atribut tersedia di ERD                                          | Sesuai |
| 5   | Hasil proses            | Output sudah dituliskan menggunakan `TAMPILKAN` | Terdapat simbol output                         | Data hasil proses sesuai dengan atribut ERD jika disimpan              | Sesuai |

### **2. Kesimpulan Audit**

Berdasarkan tabel audit konsistensi, setiap kondisi pada pseudocode harus memiliki percabangan yang sesuai pada flowchart. Selain itu, setiap variabel yang digunakan atau mengalami perubahan harus diperiksa kesesuaiannya dengan atribut pada ERD apabila variabel tersebut merupakan data yang disimpan dalam database.

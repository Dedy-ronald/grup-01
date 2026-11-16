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

    ALGORITMA KonfirmasiPesananMerchant

    DEKLARASI
    id_pesanan        : integer
    pesanan           : record {id_pesanan, status_pesanan, daftar_item}
    item_pesanan      : record {id_produk, jumlah}
    produk            : record {id_produk, stok}
    stok_cukup        : boolean
    pesan             : string

    DESKRIPSI
    { --- Langkah 1: Merchant memilih pesanan --- }
    INPUT(id_pesanan)
    pesanan <- AMBIL_PESANAN(id_pesanan)

    { --- Langkah 2: Validasi status pesanan --- }
    IF pesanan.status_pesanan != "Diteruskan ke WA" THEN
        OUTPUT("Pesanan ini sudah diproses sebelumnya")
        STOP
    END IF

    { --- Langkah 3: Cek ketersediaan stok semua item --- }
    stok_cukup <- TRUE
    FOR EACH item_pesanan IN pesanan.daftar_item DO
        produk <- AMBIL_PRODUK(item_pesanan.id_produk)
        IF produk.stok < item_pesanan.jumlah THEN
            stok_cukup <- FALSE
            BREAK
        END IF
    END FOR

    { --- Langkah 4: Stok tidak mencukupi --- }
    IF stok_cukup = FALSE THEN
        pesanan.status_pesanan <- "Batal"
        SIMPAN(pesanan)
        OUTPUT("Gagal konfirmasi: Stok produk tidak mencukupi")
        STOP
    END IF

    { --- Langkah 5: Stok mencukupi --- }
    MULAI_TRANSAKSI
    FOR EACH item_pesanan IN pesanan.daftar_item DO
        produk <- AMBIL_PRODUK(item_pesanan.id_produk)
        produk.stok <- produk.stok - item_pesanan.jumlah
        SIMPAN(produk)
    END FOR
    pesanan.status_pesanan <- "Dikonfirmasi Penjual"
    SIMPAN(pesanan)
    COMMIT_TRANSAKSI

    OUTPUT("Pesanan berhasil dikonfirmasi")
    SELESAI
## 3. Diagram Flowchart (Mermaid)

    
# Flowchart Proses Konfirmasi Pesanan Merchant

## Deskripsi
Flowchart ini menjelaskan proses merchant dalam menerima dan mengonfirmasi pesanan, memeriksa stok produk, memperbarui stok, serta menyimpan transaksi.

## Diagram Alur

```mermaid
flowchart TD
    A([Mulai]) --> B[/Input id_pesanan oleh Merchant/]
    B --> C[Ambil data pesanan]
    C --> D{status_pesanan = Diteruskan ke WA?}

    D -- Yes --> E([Output: Pesanan ini Sudah Diproses Sebelumnya])
    E --> Z([End])

    D -- No --> F[Periksa stok setiap item_pesanan]
    F --> G{Semua item: produk.stok >= item_pesanan.jumlah?}

    G -- No --> H[Status_Pesanan = "Batal"]
    H --> I([Output: Gagal konfirmasi, Stok Produk Tidak Mencukupi])
    I --> Z

    G -- Yes --> J[Mulai Transaksi]
    J --> K[Kurangi Produk.Stok sebanyak item_pesanan.Jumlah untuk setiap item]
    K --> L[Status_Pesanan = "Dikonfirmasi Penjual"]
    L --> M[Simpan Data dan Commit Transaksi]
    M --> N([Output: Pesanan Berhasil Dikonfirmasi])
    N --> Z
```

## Penjelasan Proses

  1. **Input ID Pesanan**
    Merchant memasukkan `id_pesanan`.

  2. **Ambil Data Pesanan**
   Sistem mengambil data pesanan berdasarkan ID yang dimasukkan.

3. **Periksa Status Pesanan**
   Sistem memeriksa apakah `status_pesanan` bernilai `"Diteruskan ke WA"`.
   - Yes: Sistem menampilkan pesan bahwa pesanan sudah diproses sebelumnya.
   - No: Sistem melanjutkan pemeriksaan stok setiap item pesanan.

4. **Periksa Stok Produk**
   Sistem memastikan stok setiap produk mencukupi jumlah yang dipesan.
   - No: Status pesanan diubah menjadi `"Batal"` dan sistem menampilkan pesan bahwa stok produk tidak mencukupi.
   - Yes: Sistem memulai transaksi.

5. **Kurangi Stok Produk**
   Sistem mengurangi stok setiap produk sesuai jumlah yang dipesan.

6. **Konfirmasi Pesanan**
   Status pesanan diubah menjadi `"Dikonfirmasi Penjual"`.

7. **Simpan Data dan Commit Transaksi**
   Sistem menyimpan perubahan data dan melakukan commit transaksi.

8. **Output Berhasil**
   Sistem menampilkan pesan bahwa pesanan berhasil dikonfirmasi.

## Catatan
Dokumen ini disusun berdasarkan alur pada PDF yang diberikan.

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
Berikut **Tabel Audit Konsistensi Silang** berdasarkan ERD yang kamu kirimkan. Karena ERD tersebut memiliki entitas MERCHANT, KATEGORI, PRODUK, PESANAN, dan ITEM_PESANAN, tabel audit ini disesuaikan dengan proses pemesanan produk pada sistem katalog UMKM.

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


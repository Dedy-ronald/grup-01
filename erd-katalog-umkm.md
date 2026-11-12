# Dokumentasi ERD Katalog UMKM (Bulan 1)

## 1. Diagram ERD (Mermaid)

```mermaid
erDiagram
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
```
## 2. Simulasi Data Transaksi Nyata
Skenario: Pada tanggal 12 November, Rina (WA: 081999888777) memesan 3 bungkus Keripik Tempe dengan harga Rp10.000 per bungkus dan 1 botol Sambal Roa dengan harga Rp25.000 dari Toko Dapur Minang.

1. Tabel PESANAN
id_pesanan (PK)	nama_pembeli	no_whatsapp	tanggal_pesanan	total_harga
PSN001	Rina	081999888777	12 November	Rp55.000

2. Tabel ITEM_PESANAN
id_item (PK)	id_pesanan (FK)	nama_produk	jumlah	harga_satuan	subtotal
ITM001	PSN001	Keripik Tempe	3	Rp10.000	Rp30.000
ITM002	PSN001	Sambal Roa	1	Rp25.000	Rp25.000

3. Perhitungan Total Pesanan
- Keripik Tempe: 3 × Rp10.000 = Rp30.000
- Sambal Roa: 1 × Rp25.000 = Rp25.000
Total pembayaran = Rp30.000 + Rp25.000 = Rp55.000.
## 3. Penjelasan Desain Skema
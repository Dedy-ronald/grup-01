# Tugas Mandiri 02b — Jembatan Kode: Fungsi Diskon & Ongkir

**Nama:** Aliffuddin Adilla Rafif

## 1. Kode JavaScript Sederhana:

```javascript
function hitungTotalBayar(totalBelanja, jarakKm) {
    // 1. Hitung Diskon
    let diskon = 0;

    if (totalBelanja >= 100000) {
        diskon = totalBelanja * 0.10;

        if (diskon > 20000) {
            diskon = 20000;
        }
    }

    // 2. Hitung Ongkir
    let ongkir = 0;

    if (jarakKm > 3) {
        let kelebihanKm = jarakKm - 3;
        ongkir = kelebihanKm * 2500;
    }

    // 3. Total Akhir
    let totalAkhir = totalBelanja - diskon + ongkir;

    return totalAkhir;
}

// Uji coba skenario B: belanja 150rb, jarak 5km
console.log("Total Skenario B:", hitungTotalBayar(150000, 5));

// Output: 140000
```

## 2. Refleksi Singkat:

Menerjemahkan pseudocode ke dalam JavaScript terasa lebih mudah karena saya sudah memahami langkah-langkah perhitungannya. Saya belajar menggunakan fungsi, variabel, dan kondisi if untuk menentukan diskon serta ongkir. Dengan begitu, saya bisa menghitung total pembayaran secara otomatis sesuai aturan yang sudah ditentukan.
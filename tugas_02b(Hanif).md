function hitungTotalBayar(totalBelanja, jarakKm) {
    // 1. Menghitung diskon
    let diskon = 0;

    if (totalBelanja >= 100000) {
        diskon = totalBelanja * 0.10;

        if (diskon > 20000) {
            diskon = 20000;
        } else {
            diskon = diskon;
        }
    } else {
        diskon = 0;
    }

    // 2. Menghitung ongkir
    let ongkir = 0;

    if (jarakKm > 3) {
        let kelebihanKm = jarakKm - 3;
        ongkir = kelebihanKm * 2500;
    } else {
        ongkir = 0;
    }

    // 3. Menghitung total pembayaran
    let totalAkhir = totalBelanja - diskon + ongkir;

    return totalAkhir;
}

// Pengujian Skenario B
console.log("Total Skenario B:", hitungTotalBayar(150000, 5));

// Output: Total Skenario B: 140000

console.log("Total Skenario A:", hitungTotalBayar(80000, 2));
console.log("Total Skenario B:", hitungTotalBayar(150000, 5));
console.log("Total Skenario C:", hitungTotalBayar(300000, 8));

Total Skenario A: 80000
Total Skenario B: 140000
Total Skenario C: 292500

## 2. Refleksi Singkat

Menurut saya, mengubah pseudocode menjadi JavaScript menjadi lebih mudah karena langkah-langkah perhitungannya sudah disusun terlebih dahulu. Saya belajar menggunakan fungsi, variabel, serta percabangan `if` dan `else` untuk menentukan diskon dan ongkir. Dengan melakukan pengujian, saya juga bisa mengetahui apakah hasil perhitungan sudah benar atau belum.

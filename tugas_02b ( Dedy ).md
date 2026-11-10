# Tugas Mandiri 02b — Jembatan Kode: Fungsi Diskon & Ongkir
Nama: Dedy

## 1. Kode JavaScript Sederhana

```javascript
function hitungTotalBayar(totalBelanja, jarakKm) {
  // 1. Hitung Diskon
  let diskon = 0;
  if (totalBelanja >= 100000) {
    diskon = totalBelanja * 0.10;
    if (diskon > 20000) {
      diskon = 20000;
    }
  } else {
    diskon = 0;
  }

  // 2. Hitung Ongkir
  let ongkir = 0;
  if (jarakKm <= 3) {
    ongkir = 0;
  } else {
    let kelebihanKm = jarakKm - 3;
    ongkir = kelebihanKm * 2500;
  }

  // 3. Hitung Total Akhir
  let totalAkhir = totalBelanja - diskon + ongkir;
  return totalAkhir;
}

// Uji coba ketiga skenario dari Dry Run Table
console.log("Total Skenario A (50rb, 2km):", hitungTotalBayar(50000, 2));
console.log("Total Skenario B (150rb, 5km):", hitungTotalBayar(150000, 5));
console.log("Total Skenario C (300rb, 1km):", hitungTotalBayar(300000, 1));
```

## 2. Hasil Output Console (`console.log`)

```text
Total Skenario A (50rb, 2km): 50000
Total Skenario B (150rb, 5km): 140000
Total Skenario C (300rb, 1km): 280000
```
*(Semua hasil perhitungan program cocok 100% dengan tabel Dry Run)*

## 3. Refleksi Singkat
Menerjemahkan *pseudocode* ke kode JavaScript terasa jauh lebih terarah karena alur percabangan `if-else` serta aturan batas maksimal diskon sudah terpetakan sejak awal. Saya tidak perlu menebak-nebak rumus di tengah penulisan kode, sehingga risiko kesalahan logika (*bug*) dapat ditekan.

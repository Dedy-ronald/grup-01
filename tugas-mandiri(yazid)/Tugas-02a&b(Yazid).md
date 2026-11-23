Tugas Mandiri 02b — Jembatan Kode: Fungsi Diskon & Ongkir

Nama: [Ahmad Yazid]

1. Kode JavaScript Sederhana:
javascript
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

// Uji coba skenario A: belanja 80rb, jarak 2km
console.log("Total Skenario A:", hitungTotalBayar(80000, 2));
// Output: 80000

// Uji coba skenario B: belanja 150rb, jarak 5km
console.log("Total Skenario B:", hitungTotalBayar(150000, 5));
// Output: 140000

// Uji coba skenario C: belanja 300rb, jarak 10km
console.log("Total Skenario C:", hitungTotalBayar(300000, 10));
// Output: 297500
2. Hasil Uji vs Dry Run Table:
Skenario	Total Belanja	Jarak	Diskon	Ongkir	Total Bayar (Dry Run)	Output Kode	Cocok?
A	Rp80.000	2 km	Rp0 (belanja < 100rb)	Rp0 (jarak ≤ 3 km)	Rp80.000	80000	Ya
B	Rp150.000	5 km	Rp15.000 (10%)	Rp5.000 (2 km × 2.500)	Rp140.000	140000	Ya
C	Rp300.000	10 km	Rp20.000 (10% = 30rb, dibatasi maks 20rb)	Rp17.500 (7 km × 2.500)	Rp297.500	297500	Ya

Skenario A menguji kondisi tanpa diskon dan tanpa ongkir. Skenario B menguji diskon biasa dan ongkir. Skenario C menguji batas maksimal diskon Rp20.000.

3. Refleksi Singkat:

[Tulis refleksimu sendiri dengan 2–3 kalimat: bagian mana yang paling mudah atau paling membingungkan saat menerjemahkan pseudocode ke JavaScript?]
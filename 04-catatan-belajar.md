# Catatan Belajar

1. **Planned vs unplanned.** Jika patching 120 menit ikut dihitung, SLA turun menjadi 99,19%. Pemisahan kategori sangat menentukan hasil.
2. **Penyebut rumus.** Jika planned juga dikurangkan dari total waktu (44.640 - 120 = 44.520), hasilnya 44.280/44.520 = 99,46%. Setelah pembulatan sama, tetapi definisi resmi tetap harus dicek di kontrak.
3. **Error budget.** 99,9% hanya memberi sekitar 44 menit per bulan.
4. **Pola insiden.** Insiden 1 = masalah ketahanan (redundansi). Insiden 3 = masalah kapasitas. Rekomendasi harus dipetakan ke akar masalah.
5. **Keterbatasan.** Ini studi kasus simulasi; log hanya 3 kejadian dan tidak mencakup degradasi parsial (lambat, bukan mati total).

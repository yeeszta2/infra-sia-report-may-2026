# Mathematical SLA Calculation

1. Total waktu = 31 x 24 x 60 = **44.640 menit**
2. Total downtime (unplanned saja) = 150 + 90 = **240 menit**
3. Uptime = 44.640 - 240 = **44.400 menit**
4. SLA % = 44.400 / 44.640 x 100% = 99,4624% = **99,46%**
5. Error budget = 0,1% x 44.640 = **44,64 menit**
6. Selisih = 240 - 44,64 = **195,36 menit** melebihi batas

**Hasil: NON-COMPLIANT** (99,46% < 99,90%).

Verifikasi: `python src/sla_calculator.py` dan `python -m unittest discover tests`.

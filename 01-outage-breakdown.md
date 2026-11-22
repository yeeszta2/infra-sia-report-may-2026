# Outage Breakdown

| # | Tanggal | Waktu (WIB) | Durasi | Kategori | Penyebab | Dihitung downtime? | Resolusi / catatan |
|---|---------|-------------|--------|----------|----------|--------------------|--------------------|
| 1 | 05 Mei | 10.00-12.30 | 150 mnt | Unplanned | Kerusakan hardware NIC | Ya | Penggantian NIC. Jam sibuk, tidak ada failover otomatis (single point of failure). |
| 2 | 15 Mei | 01.00-03.00 | 120 mnt | Planned | Security patching terjadwal | Tidak | Approved maintenance di jam trafik rendah. |
| 3 | 24 Mei | 20.15-21.45 | 90 mnt | Unplanned | Out of Memory akibat promo mendadak | Ya | Dipulihkan manual oleh tim on-call. Kapasitas tidak siap lonjakan. |

| Ringkasan | Nilai |
|-----------|-------|
| Total unplanned downtime | 150 + 90 = **240 menit** |
| Planned maintenance (dikecualikan) | 120 menit |
| MTTR | 240 / 2 = **120 menit/insiden** |

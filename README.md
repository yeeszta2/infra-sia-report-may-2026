# LAPORAN PENGUMPULAN TUGAS

**Weekly Assignment - Infrastructure SLA Reporting - IT Infrastructure & Security**

| | |
|---|---|
| Nama | belly |
| NIM | 123456 |
| Posisi | Intern - Information Technology (IT) |
| Institusi | University (Program Studi S1 Teknologi) |
| Tanggal Pengumpulan | 22 November 2026 |
| Topik | Infrastructure SLA Executive Report: Audit Ketersediaan Kluster Database Produksi Mei 2026 |
| GitHub Repository Link | https://github.com/yeeszta2/infra-sla-report-may-2026 |

---

## 1. Executive Summary

Pada Mei 2026, kluster database produksi mencatat **availability 99,46%**, di bawah target SLA **99,90%**. Status: **Non-Compliant**.

Terjadi 3 kejadian: 2 unplanned (kerusakan NIC dan Out of Memory saat promo) dengan total **240 menit downtime**, serta 1 planned maintenance (security patching) yang **tidak dihitung**. Budget downtime sebulan hanya **44,64 menit**, sehingga downtime aktual sekitar **5,4 kali** batas toleransi. Setiap insiden unplanned sudah melanggar SLA sendirian.

## 2. Outage Breakdown Table

| # | Tanggal | Durasi | Kategori | Penyebab | Dihitung? |
|---|---------|--------|----------|----------|-----------|
| 1 | 05 Mei, 10.00-12.30 | 150 mnt | Unplanned | Hardware NIC rusak | Ya |
| 2 | 15 Mei, 01.00-03.00 | 120 mnt | Planned | Security patching | Tidak |
| 3 | 24 Mei, 20.15-21.45 | 90 mnt | Unplanned | OOM akibat promo | Ya |

Unplanned = **240 menit**, planned (dikecualikan) = 120 menit. Detail: [docs/01-outage-breakdown.md](docs/01-outage-breakdown.md)

## 3. Mathematical SLA Calculation

```
Total waktu  = 31 x 24 x 60              = 44.640 menit
Downtime     = 150 + 90                  = 240 menit
Uptime       = 44.640 - 240              = 44.400 menit
SLA %        = 44.400 / 44.640 x 100%    = 99,4624% = 99,46%
Error budget = 0,1% x 44.640             = 44,64 menit
```

**Evaluasi: NON-COMPLIANT.** 99,46% < 99,90%, kelebihan downtime 195,36 menit.

**Implikasi:** 4 jam layanan tidak bisa diakses, satu di antaranya saat jam sibuk dan promo, sehingga transaksi gagal, reputasi turun, dan ada risiko penalti kontrak. Dua akar masalah (hardware tanpa redundansi dan kapasitas tanpa margin) bersifat sistemik dan bisa terulang. Detail: [docs/02-sla-calculation.md](docs/02-sla-calculation.md)

## 4. Management Recommendation

1. **Redundansi:** NIC teaming/bonding, jalur jaringan ganda, cluster dengan automatic failover (hilangkan single point of failure).
2. **Capacity Safety Margin:** headroom 30-40% di atas beban puncak, auto-scaling, rate limiting, load test sebelum promo.
3. **Koordinasi promo:** tim marketing memberi tahu infra minimal H-3.
4. **Monitoring dan MTTR:** alert proaktif (memori >80%, error NIC), runbook, self-healing, target MTTR < 30 menit.
5. **Error budget:** pantau 44,64 menit/bulan, bekukan perubahan non-esensial jika menipis.

Target bulan depan: downtime unplanned <= 44 menit. Detail: [docs/03-management-recommendation.md](docs/03-management-recommendation.md)

---

## Struktur Repository

```
infra-sla-report-may-2026/
├── README.md                  # laporan utama
├── data/incident_log.csv      # log insiden mentah
├── src/sla_calculator.py      # kalkulator SLA
├── tests/test_sla_calculator.py
└── docs/                      # rincian per bagian + catatan belajar
```

## Cara Verifikasi

```bash
python src/sla_calculator.py
python -m unittest discover tests
```

## Referensi

- Axelos (2019). *ITIL Foundation: ITIL 4 Edition*. TSO.
- Materi Telkomsel Academy, *Keeping the Service Alive: SRE & SOC* (2026).
- Telkomsel IT Infrastructure & Security Governance (2025). SOP Monthly SLA Calculation (simulasi).

# Management Recommendation

| Akar masalah | Rekomendasi taktis | Konsep |
|--------------|--------------------|--------|
| NIC rusak, layanan mati total | NIC teaming/bonding, jalur ganda ke switch berbeda, cluster dengan automatic failover | Redundansi hulu-hilir, hilangkan single point of failure |
| OOM saat promo | Capacity Safety Margin (headroom 30-40% di atas beban puncak historis), auto-scaling, rate limiting, load test sebelum promo | Capacity planning, scalability |
| Promo mendadak | Prosedur notifikasi kampanye ke tim infra minimal H-3 | Koordinasi bisnis-infra |
| Pemulihan lambat (MTTR 120 mnt) | Alert proaktif (memori >80%, error NIC), runbook, self-healing, target MTTR < 30 mnt | Monitoring = prevention; Detect-Analyze-Respond-Recover |
| Pengelolaan SLA | Pantau error budget (44,64 mnt/bulan) real-time; bekukan perubahan non-esensial jika budget menipis | SRE error budget |

**Target bulan depan:** downtime unplanned <= 44 menit (SLA >= 99,90%).

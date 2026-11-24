# Implementasi-Routing-OSPF-EIGRP-dengan-Redundansi-Jalur-dan-High-Availability
Project akhir semester 1 kelas 11-TJKT. Project mata pelajaran Cisco

# 🌐 Implementasi Routing OSPF-EIGRP dengan Redundansi Jalur & High Availability

Repositori ini berisi dokumentasi, skema perancangan, dan skrip konfigurasi untuk proyek jaringan komputer *enterprise* menggunakan perangkat Cisco. Proyek ini berfokus pada integrasi dua protokol routing yang berbeda (*Open Shortest Path First* dan *Enhanced Interior Gateway Routing Protocol*) dengan menerapkan redundansi jalur serta ketersediaan tinggi (*High Availability*) guna meminimalkan *downtime*.

---

## 🚀 Fitur Utama Proyek

* **Interoperabilitas Protokol (*Route Redistribution*):** Menggabungkan area OSPF (standar terbuka) dan domain EIGRP (proprietary Cisco) secara aman tanpa menyebabkan *routing loop*.
* **Redundansi Jalur (*Path Redundancy*):** Menyediakan jalur alternatif otomatis jika terjadi kegagalan pada jalur utama (*link failure*).
* **High Availability & Failover:** Menggunakan protokol *First Hop Redundancy* (seperti HSRP/VRRP) agar klien tetap memiliki *gateway* aktif meskipun router utama down.
* **Konvergensi Cepat:** Penyetelan *timer* routing untuk memastikan pemulihan jaringan terjadi dalam hitungan detik.

---

##📂 Struktur Repositori

├── topology/           # Berisi file Cisco Packet Tracer (.pkt) atau GNS3 / EVE-NG
├── configs/            # File teks berisi konfigurasi CLI tiap router dan switch
├── documentation/      # Proposal, laporan, dan dokumentasi lengkap proyek (.pdf / .docx)
└── README.md           # Dokumentasi proyek (file ini)

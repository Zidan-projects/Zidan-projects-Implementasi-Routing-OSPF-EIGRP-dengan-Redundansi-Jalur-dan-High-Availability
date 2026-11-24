PROJECT CISCO AKHIR SEMESTER 1 KELAS 11-TJKT

# 🌐 Implementasi Routing OSPF-EIGRP dengan Redundansi Jalur & High Availability
![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer%20%7C%20GNS3-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Routing](https://img.shields.io/badge/Protocol-OSPF%20%26%20EIGRP-success?style=for-the-badge)
![High Availability](https://img.shields.io/badge/Failover-HSRP%20Redundancy-orange?style=for-the-badge)

Repositori ini berisi dokumentasi, skema perancangan, dan skrip konfigurasi untuk proyek jaringan komputer *enterprise* menggunakan perangkat Cisco. Proyek ini berfokus pada integrasi dua protokol routing yang berbeda (*Open Shortest Path First* dan *Enhanced Interior Gateway Routing Protocol*) dengan menerapkan redundansi jalur serta ketersediaan tinggi (*High Availability*) guna meminimalkan *downtime*.

---

## 🛠️ Fitur & Teknologi yang Digunakan
* **OSPF Multi-Area / Single-Area:** Pertukaran rute berbasis *link-state* dengan optimasi *Router-ID* dan *Passive Interface*.
* **EIGRP :** Pertukaran rute cepat berbasis algoritma DUAL (*Diffusing Update Algorithm*) dengan dukungan *unequal-cost load balancing*.
* **Mutual Route Redistribution + Route-Map Tagging:** Pertukaran informasi rute dua arah antara OSPF dan EIGRP menggunakan penandaan rute (*route tagging*) untuk mencegah rute berputar kembali (*routing loop*).
* **HSRP (Hot Standby Router Protocol):** Virtualisasi *default gateway* sehingga perpindahan router utama (*Active*) ke cadangan (*Standby*) berjalan otomatis di bawah 3 detik.
* **EtherChannel (LACP) & Rapid-PVST+:** Agregasi tautan dan pencegahan *loop* pada lapisan *switching* (Layer 2).

---

## 🚀 Fitur Utama Proyek

* **Interoperabilitas Protokol (*Route Redistribution*):** Menggabungkan area OSPF (standar terbuka) dan domain EIGRP (proprietary Cisco) secara aman tanpa menyebabkan *routing loop*.
* **Redundansi Jalur (*Path Redundancy*):** Menyediakan jalur alternatif otomatis jika terjadi kegagalan pada jalur utama (*link failure*).
* **High Availability & Failover:** Menggunakan protokol *First Hop Redundancy* (seperti HSRP/VRRP) agar klien tetap memiliki *gateway* aktif meskipun router utama down.
* **Konvergensi Cepat:** Penyetelan *timer* routing untuk memastikan pemulihan jaringan terjadi dalam hitungan detik.

---

## 📂 Struktur Repositori

```text
├── 📁 topology/
│   └── topologi cisco.png            # Gambar diagram arsitektur jaringan
├── 📁 configs/
├── 📁 docs/
└── 📄 README.md                        # Dokumentasi utama repositori (file ini)
``

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

## 🛠️ Topologi Jaringan

*(Gambaran atau diagram topologi dapat diletakkan di sini)*
```text
[ Core Router OSPF ] <--- (Redistribution) ---> [ Core Router EIGRP ]
        |                                              |
   (Area 0)                                      (AS 100)
        |                                              |
[ Distribution / Access Switches + HSRP / FHRP Redundancy ]
        |
[ End-User / Client Subnets ]

PROJECT CISCO AKHIR SEMESTER 1 KELAS 11-TJKT

# 🌐 Implementasi Routing OSPF-EIGRP dengan Redundansi Jalur & High Availability

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
```

---
# 🌐 Implementasi Routing OSPF-EIGRP dengan Redundansi Jalur dan High Availability

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer%20%7C%20GNS3-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Routing](https://img.shields.io/badge/Protocol-OSPF%20%26%20EIGRP-success?style=for-the-badge)
![High Availability](https://img.shields.io/badge/Failover-HSRP%20Redundancy-orange?style=for-the-badge)

Repositori ini berisi rancangan arsitektur, skema pengalamatan IP, skrip konfigurasi perangkat, dan dokumentasi pengujian untuk proyek jaringan skala *enterprise* berbasis Cisco. Proyek ini menggabungkan dua protokol *dynamic routing* yang berbeda (**OSPF** dan **EIGRP**) serta menerapkan mekanisme **Path Redundancy** dan **High Availability (HSRP)** untuk menjamin konektivitas tanpa henti (*zero downtime*) saat terjadi kegagalan perangkat atau jalur fisik.

---

## 📋 Daftar Isi
1. [Latar Belakang & Tujuan](#-latar-belakang--tujuan)
2. [Fitur & Teknologi Utama](#-fitur--teknologi-utama)
3. [Topologi Jaringan](#-topologi-jaringan)
4. [Tabel Pengalamatan IP (IP Addressing)](#-tabel-pengalamatan-ip-ip-addressing)
5. [Konfigurasi CLI Perangkat](#-konfigurasi-cli-perangkat)
6. [Skenario & Hasil Pengujian](#-skenario--hasil-pengujian)
7. [Struktur Repositori](#-struktur-repositori)
8. [Tim Penyusun](#-tim-penyusun)

---

## 🎯 Latar Belakang & Tujuan
Dalam infrastruktur jaringan perusahaan yang berkembang, sering kali terdapat dua domain protokol *routing* berbeda—misalnya jaringan inti menggunakan **OSPF** (standar terbuka) dan jaringan cabang menggunakan **EIGRP** (khusus Cisco). Tanpa integrasi yang tepat serta jalur cadangan, kerusakan pada satu titik (*Single Point of Failure*) dapat melumpuhkan operasional.

**Tujuan Proyek:**
* Mengintegrasikan domain OSPF dan EIGRP menggunakan **Mutual Route Redistribution** yang aman dari *routing loop*.
* Membangun **Redundansi Jalur** antar-router inti dan distribusi menggunakan tautan ganda (*dual-homed*).
* Menerapkan **High Availability** pada sisi *gateway* pengguna menggunakan **HSRP (Hot Standby Router Protocol)** dengan fitur *preemption* dan *interface tracking*.

---

## 🛠️ Fitur & Teknologi Utama
* **OSPF (Area 0):** Pertukaran rute berbasis *link-state* pada jaringan inti dengan optimasi *Router-ID* dan *Passive Interface*.
* **EIGRP (AS 100):** Pertukaran rute cepat berbasis algoritma DUAL (*Diffusing Update Algorithm*) untuk segmen distribusi dan cabang.
* **Mutual Route Redistribution + Route-Map Tagging:** Pertukaran informasi rute dua arah antara OSPF dan EIGRP menggunakan penandaan rute (*route tagging* tag `90` dan `110`) untuk mencegah rute berputar kembali (*routing feedback/loop*).
* **HSRP (Hot Standby Router Protocol):** Virtualisasi *default gateway* sehingga perpindahan router utama (*Active*) ke cadangan (*Standby*) berjalan otomatis di bawah 3 detik.
* **Rapid-PVST+ & PortFast:** Konvergensi cepat dan pencegahan *loop* pada lapisan *switching* (Layer 2).

---

## 🗺️ Topologi Jaringan

```text
                    [ Domain OSPF - Area 0 ]
                         +------------+
                         |  R1-OSPF   | (Core OSPF - Lo0: 1.1.1.1)
                         +-----+------+
                              / \
            (10.10.12.0/30)  /   \  (10.10.13.0/30)
                            /     \
             +-------------+       +-------------+
             | R2-ASBR-1   |=======| R3-ASBR-2   |  <-- Mutual Redistribution
             | (HSRP Act)  |       | (HSRP Stby) |      (OSPF <---> EIGRP)
             +------+------+       +------+------+
                    |                     |
     (172.16.24.0/30)|                     |(172.16.35.0/30)
                    |                     |
             +------+------+       +------+------+
             |  R4-EIGRP   |       |  R5-EIGRP   |  <-- Domain EIGRP (AS 100)
             | (HSRP Act)  |       | (HSRP Stby) |
             +------+------+       +------+------+
                    \                     /
                     \                   /
              +---------------+ +---------------+
              | SW-Distribusi1| | SW-Distribusi2|
              |   (VLAN 10)   | |   (VLAN 20)   |
              +-------+-------+ +-------+-------+
                      |                 |
               [ PC Admin LAN ]  [ PC Staff LAN ]
               VIP: .10.254/24   VIP: .20.254/24
```

## 🔢 Tabel Pengalamatan IP (IP Addressing)

### 1. Perangkat Router (Layer 3)
| Nama Perangkat | Interface | Alamat IP | Subnet Mask | Prefix | Peran / Domain Routing |
| :--- | :--- | :--- | :--- | :---: | :--- |
| **R1-OSPF** | `GigabitEthernet0/0` | `10.10.12.1` | `255.255.255.252` | `/30` | Link ke R2-ASBR-1 (OSPF Area 0) |
| *(Core Router)* | `GigabitEthernet0/1` | `10.10.13.1` | `255.255.255.252` | `/30` | Link ke R3-ASBR-2 (OSPF Area 0) |
| | `Loopback0` | `1.1.1.1` | `255.255.255.255` | `/32` | Router-ID & Simulasi Server Pusat |
| **R2-ASBR-1** | `GigabitEthernet0/0` | `10.10.12.2` | `255.255.255.252` | `/30` | Link ke R1-OSPF (OSPF Area 0) |
| *(ASBR & HSRP Act)* | `GigabitEthernet0/1` | `172.16.24.1` | `255.255.255.252` | `/30` | Link ke R4-EIGRP (EIGRP AS 100) |
| | `GigabitEthernet0/2` | `192.168.10.252` | `255.255.255.0` | `/24` | LAN VLAN 10 (HSRP Priority 110) |
| | `Loopback0` | `2.2.2.2` | `255.255.255.255` | `/32` | Router-ID |
| **R3-ASBR-2** | `GigabitEthernet0/0` | `10.10.13.2` | `255.255.255.252` | `/30` | Link ke R1-OSPF (OSPF Area 0) |
| *(ASBR & HSRP Stby)*| `GigabitEthernet0/1` | `172.16.35.1` | `255.255.255.252` | `/30` | Link ke R5-EIGRP (EIGRP AS 100) |
| | `GigabitEthernet0/2` | `192.168.10.253` | `255.255.255.0` | `/24` | LAN VLAN 10 (HSRP Priority 100) |
| | `Loopback0` | `3.3.3.3` | `255.255.255.255` | `/32` | Router-ID |
| **R4-EIGRP** | `GigabitEthernet0/0` | `172.16.24.2` | `255.255.255.252` | `/30` | Link ke R2-ASBR-1 (EIGRP AS 100) |
| *(Branch Primary)* | `GigabitEthernet0/1` | `192.168.20.252` | `255.255.255.0` | `/24` | LAN VLAN 20 (HSRP Priority 110) |
| | `Loopback0` | `4.4.4.4` | `255.255.255.255` | `/32` | Router-ID |
| **R5-EIGRP** | `GigabitEthernet0/0` | `172.16.35.2` | `255.255.255.252` | `/30` | Link ke R3-ASBR-2 (EIGRP AS 100) |
| *(Branch Backup)* | `GigabitEthernet0/1` | `192.168.20.253` | `255.255.255.0` | `/24` | LAN VLAN 20 (HSRP Priority 100) |
| | `Loopback0` | `5.5.5.5` | `255.255.255.255` | `/32` | Router-ID |

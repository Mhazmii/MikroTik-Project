# Infrastruktur Hotspot Voucher MikroTik

![Status](https://img.shields.io/badge/Status-Berjalan-success)
![MikroTik](https://img.shields.io/badge/Platform-MikroTik-blue)
![Versi](https://img.shields.io/badge/Versi-1.0-orange)

## Tentang Proyek

Proyek ini merupakan implementasi jaringan hotspot voucher menggunakan dua perangkat MikroTik dengan konsep pemisahan tugas antara **Core Router** dan **Hotspot Router**.

Arsitektur ini dibuat agar pengelolaan jaringan menjadi lebih rapi, mudah dikembangkan, serta mendekati implementasi jaringan yang digunakan pada lingkungan profesional.

Pada proyek ini, **MikroTik RB760iGS** bertugas sebagai router utama yang menangani koneksi internet, routing, NAT, serta jaringan management.

Sedangkan **MikroTik RB951Ui-2HnD** difokuskan sebagai perangkat hotspot yang menangani jaringan pengguna, WiFi, captive portal, autentikasi voucher, dan pembatasan bandwidth.

---

## Tujuan Proyek

Proyek ini dibuat sebagai pembelajaran sekaligus simulasi implementasi hotspot pada skala kecil hingga menengah seperti:

- Area wisata
- Kebun atau lokasi outdoor
- Warung kopi
- Kafe
- Guest house
- UMKM
- Jaringan komunitas kecil

Beberapa tujuan utama dari proyek ini:

- Membangun arsitektur hotspot yang terpisah antara layanan inti dan layanan pengguna.
- Menerapkan sistem login menggunakan voucher hotspot MikroTik.
- Membatasi kecepatan internet setiap pengguna.
- Membatasi satu voucher untuk satu perangkat.
- Menyediakan dasar pengembangan untuk VLAN, monitoring, website internal, dan sistem manajemen voucher.

---

## Topologi Jaringan

```
                      INTERNET
                          |
                          |
                 Modem / ONT IndiHome
                   192.168.100.1
                          |
                          |
                    ether1 (WAN)
                          |
                    MikroTik RB760iGS
                      Core Router
                 WAN : 192.168.100.x
                 LAN : 172.20.1.1/24
                          |
                  ether5 (PoE Out)
                          |
                    ether1 (UPLINK)
                          |
                 MikroTik RB951Ui-2HnD
                    Hotspot Router
                 Management : 172.20.1.2
                          |
            --------------------------------
            |                              |
         LAN Client                    WLAN 2.4 GHz
                                          |
                                    KEBON-HOTSPOT
                                          |
                                   172.20.10.0/24
                                          |
                                   Pengguna Hotspot
```

---

## Perencanaan Alamat IP

### Jaringan Internet (WAN)

| Perangkat | Alamat |
|---|---|
| Modem IndiHome | 192.168.100.1 |
| RB760 WAN | DHCP Client (192.168.100.x) |

---

### Jaringan Management

Jaringan ini digunakan untuk mengakses dan mengelola perangkat jaringan.

| Perangkat | Alamat IP |
|---|---|
| RB760iGS | 172.20.1.1 |
| RB951Ui-2HnD | 172.20.1.2 |

---

### Jaringan Hotspot

Jaringan yang digunakan oleh pengguna WiFi.

| Parameter | Nilai |
|---|---|
| Network | 172.20.10.0/24 |
| Gateway | 172.20.10.1 |
| DHCP Pool | 172.20.10.100 - 172.20.10.254 |
| SSID | KEBON-HOTSPOT |

---

## Perangkat yang Digunakan

| Perangkat | Fungsi |
|---|---|
| MikroTik RB760iGS | Core Router |
| MikroTik RB951Ui-2HnD | Router Hotspot dan Access Point |
| Modem/ONT ISP | Sumber koneksi internet |
| Laptop | Konfigurasi dan monitoring |
| Smartphone/Client | Pengujian hotspot |

---

## Fitur yang Sudah Berjalan

### RB760iGS (Core Router)

- [x] Koneksi internet melalui DHCP Client
- [x] Routing jaringan
- [x] NAT Masquerade
- [x] DNS Forwarding
- [x] Jaringan management
- [x] PoE Out untuk RB951

### RB951Ui-2HnD (Hotspot Router)

- [x] Wireless Access Point
- [x] SSID KEBON-HOTSPOT
- [x] DHCP Server untuk pengguna hotspot
- [x] Captive Portal MikroTik
- [x] Sistem login voucher
- [x] Pembatasan bandwidth per pengguna

---

## Kebijakan Hotspot Saat Ini

Konfigurasi voucher yang digunakan saat ini:

| Parameter | Konfigurasi |
|---|---|
| Jenis Voucher | Harian |
| Durasi | 1 hari |
| Kecepatan | 2 Mbps Upload / 2 Mbps Download |
| Jumlah Perangkat | 1 perangkat per voucher |
| Sistem Login | Username dan password |
| Captive Portal | Aktif |

---

## Struktur Repository

```
mikrotik-hotspot-voucher/
│
├── README.md
│
├── docs/
│   ├── 01-gambaran-proyek.md
│   ├── 02-topologi-jaringan.md
│   ├── 03-perencanaan-ip-address.md
│   ├── 04-konfigurasi-rb760-core-router.md
│   ├── 05-konfigurasi-rb951-hotspot-router.md
│   ├── 06-konfigurasi-voucher-hotspot.md
│   ├── 07-keamanan-jaringan.md
│   ├── 08-troubleshooting.md
│   └── 09-pengembangan-selanjutnya.md
│
├── scripts/
│   ├── rb760-core.rsc
│   └── rb951-hotspot.rsc
│
├── backup/
│   ├── RB760-CORE.backup
│   └── RB951-HOTSPOT.backup
│
└── assets/
    ├── topologi/
    ├── screenshot-winbox/
    └── halaman-hotspot/
```

---

## Dokumentasi Konfigurasi

Setiap tahapan konfigurasi pada folder `docs` akan menyediakan dua metode:

### 1. Konfigurasi menggunakan Winbox

Berisi langkah konfigurasi menggunakan antarmuka grafis MikroTik.

Cocok untuk:
- Teknisi lapangan.
- Pemula yang baru belajar MikroTik.
- Dokumentasi visual.

### 2. Konfigurasi menggunakan Terminal (CLI)

Berisi perintah MikroTik RouterOS secara langsung.

Cocok untuk:
- Network Engineer.
- Deployment cepat.
- Pembuatan script `.rsc`.

---

## Status Pengembangan

### Versi 1.0 (Selesai)

- Core Router RB760iGS.
- Hotspot Router RB951Ui-2HnD.
- Jaringan management.
- WiFi hotspot.
- Captive portal.
- Voucher login.
- Limit bandwidth 2 Mbps.

### Pengembangan Berikutnya

- Firewall hardening.
- Pembatasan akses management.
- Isolasi pengguna hotspot.
- Integrasi Mikhmon.
- Otomatisasi pembuatan voucher.
- Hosting website internal.
- Port forwarding.
- Implementasi VLAN.
- Monitoring jaringan.

---

## Catatan

Proyek ini akan terus dikembangkan sebagai dokumentasi pembelajaran dan implementasi jaringan berbasis MikroTik. Seluruh konfigurasi yang tersedia dapat digunakan sebagai referensi untuk membangun sistem hotspot voucher dengan arsitektur yang lebih terstruktur.

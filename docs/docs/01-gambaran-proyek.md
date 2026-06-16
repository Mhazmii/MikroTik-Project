# Gambaran Proyek

## 1. Pendahuluan

Proyek ini merupakan implementasi sistem hotspot voucher berbasis MikroTik yang dirancang menggunakan arsitektur dua perangkat, yaitu **Core Router** dan **Hotspot Router**.

Tujuan utama dari desain ini adalah memisahkan layanan jaringan utama dengan layanan pengguna agar sistem lebih mudah dikelola, memiliki struktur yang lebih rapi, serta dapat dikembangkan di masa mendatang.

Dalam implementasi ini:

- MikroTik RB760iGS berperan sebagai Core Router.
- MikroTik RB951Ui-2HnD berperan sebagai Hotspot Router dan Access Point.

Walaupun menggunakan perangkat kelas rumahan dan skala kecil, desain jaringan dibuat mengikuti prinsip-prinsip dasar yang umum digunakan dalam implementasi jaringan profesional.

---

# 2. Latar Belakang

Pada implementasi hotspot sederhana, sering ditemukan satu perangkat router digunakan untuk menjalankan seluruh fungsi jaringan, seperti:

- Koneksi ke Internet.
- Routing.
- NAT.
- DHCP Server.
- Wireless Access Point.
- Captive Portal.
- Manajemen pengguna hotspot.
- Pembatasan bandwidth.

Pendekatan tersebut memang mudah dan cepat untuk diterapkan, namun memiliki beberapa kekurangan ketika jumlah pengguna dan kebutuhan jaringan mulai berkembang.

Beberapa kendala yang sering muncul:

- Konfigurasi menjadi kompleks karena semua layanan berada pada satu perangkat.
- Proses troubleshooting lebih sulit.
- Risiko gangguan lebih besar karena semua layanan bergantung pada satu perangkat.
- Sulit melakukan pengembangan seperti penambahan access point, VLAN, atau sistem monitoring.

Oleh karena itu, proyek ini menggunakan pendekatan pemisahan layanan dengan membagi tugas masing-masing perangkat.

---

# 3. Tujuan Proyek

Tujuan dari pembangunan infrastruktur jaringan ini adalah:

- Membangun sistem hotspot voucher yang terstruktur.
- Memisahkan layanan Core Network dan layanan pengguna.
- Menyediakan autentikasi pengguna menggunakan sistem hotspot MikroTik.
- Menerapkan pembatasan bandwidth per pengguna.
- Membatasi penggunaan satu voucher untuk satu perangkat.
- Menyediakan dasar untuk pengembangan sistem jaringan yang lebih besar.

---

# 4. Konsep Arsitektur Jaringan

Arsitektur yang digunakan dalam proyek ini adalah:

**Core Router + Dedicated Hotspot Router Architecture**

Konsep ini membagi tanggung jawab perangkat berdasarkan fungsi masing-masing.

---

## 4.1 Core Router (RB760iGS)

RB760iGS bertanggung jawab terhadap layanan utama jaringan.

Fungsi utama:

- Menghubungkan jaringan lokal ke ISP.
- Mengelola koneksi WAN.
- Melakukan proses routing.
- Menjalankan NAT (Network Address Translation).
- Menyediakan jaringan management.
- Menyediakan koneksi PoE menuju RB951.

RB760 tidak secara langsung menangani pengguna hotspot sehingga kinerja perangkat dapat lebih fokus terhadap fungsi jaringan inti.

---

## 4.2 Hotspot Router (RB951Ui-2HnD)

RB951Ui-2HnD bertanggung jawab terhadap jaringan pengguna.

Fungsi utama:

- Menyediakan layanan Wireless Access Point.
- Menyediakan jaringan hotspot khusus pengguna.
- Menjalankan Captive Portal MikroTik.
- Mengelola proses login menggunakan voucher.
- Menyediakan DHCP Server untuk pengguna hotspot.
- Melakukan pembatasan bandwidth setiap pengguna.

Pemisahan ini membuat pengelolaan pengguna menjadi lebih terfokus tanpa mengganggu layanan inti jaringan.

---

# 5. Kebutuhan Perangkat

Implementasi proyek menggunakan perangkat berikut:

| Perangkat | Fungsi |
|---|---|
| MikroTik RB760iGS | Core Router dan Gateway Internet |
| MikroTik RB951Ui-2HnD | Hotspot Router dan Access Point |
| Modem/ONT ISP | Sumber koneksi internet |
| Laptop | Konfigurasi dan administrasi jaringan |
| Smartphone/PC Client | Pengujian jaringan hotspot |

---

# 6. Ruang Lingkup Implementasi

Tahap implementasi versi 1.0 mencakup:

## Infrastruktur Dasar

- Koneksi internet dari ISP.
- Konfigurasi WAN.
- Konfigurasi NAT.
- Konfigurasi DNS.
- Pembuatan jaringan management.

## Infrastruktur Hotspot

- Pembuatan jaringan hotspot terpisah.
- Konfigurasi Wireless Access Point.
- Pembuatan DHCP Server hotspot.
- Implementasi Captive Portal.
- Pembuatan sistem login menggunakan voucher.

## Kebijakan Pengguna

Kebijakan pengguna yang diterapkan:

| Parameter | Konfigurasi |
|---|---|
| Durasi Voucher | 1 Hari |
| Kecepatan | 2 Mbps Upload dan Download |
| Shared User | 1 perangkat |
| Metode Login | Username dan Password |
| SSID | KEBON-HOTSPOT |

---

# 7. Batasan Sistem Saat Ini

Implementasi saat ini masih berada pada versi awal sehingga beberapa fitur belum diterapkan.

Fitur yang masih dalam tahap pengembangan:

- Firewall hardening.
- Pembatasan akses management dari WAN.
- Isolasi antar pengguna hotspot.
- Sistem monitoring jaringan.
- Integrasi Mikhmon untuk manajemen voucher.
- Website internal.
- Port forwarding.
- Implementasi VLAN.

---

# 8. Rencana Pengembangan

Pengembangan proyek direncanakan dalam beberapa tahap.

## Versi 1.1

Fokus pada keamanan jaringan:

- Konfigurasi firewall.
- Menutup akses Winbox dari jaringan WAN.
- Membatasi akses administrasi hanya dari jaringan management.
- Backup dan strategi pemulihan konfigurasi.

---

## Versi 1.2

Fokus pada manajemen pengguna:

- Integrasi Mikhmon.
- Pembuatan voucher otomatis.
- Cetak voucher.
- Monitoring pengguna aktif.

---

## Versi 2.0

Fokus pada peningkatan skala jaringan:

- Implementasi VLAN.
- Penambahan Access Point.
- Segmentasi jaringan berdasarkan kebutuhan.
- Implementasi server website.
- Sistem monitoring jaringan.
- Peningkatan keamanan jaringan.

---

# 9. Kesimpulan

Proyek ini menunjukkan bahwa perangkat MikroTik skala kecil tetap dapat digunakan untuk membangun infrastruktur jaringan dengan desain yang terstruktur.

Dengan memisahkan fungsi Core Router dan Hotspot Router, sistem menjadi lebih mudah dikelola, lebih mudah dikembangkan, dan memberikan dasar yang lebih baik untuk implementasi fitur jaringan di masa depan.

Dokumentasi ini akan terus diperbarui seiring dengan perkembangan konfigurasi dan penambahan fitur pada proyek ini.

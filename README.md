# MikroTik Hotspot Voucher Architecture

## Overview

This project demonstrates a small-scale professional hotspot infrastructure using two MikroTik devices:

- MikroTik RB760iGS as Core Router
- MikroTik RB951Ui-2HnD as Dedicated Hotspot Router

The architecture separates core routing and hotspot services to simplify management, improve security, and allow future scalability.

---

## Features

Current implementation:

- Internet Gateway
- DHCP Server
- NAT Masquerade
- Dedicated Hotspot Router
- WiFi Access Point
- Captive Portal
- Voucher Authentication
- 2 Mbps bandwidth limitation per user
- Single device login
- Daily voucher

---

## Architecture
Internet
|
IndiHome ONT
192.168.100.1
|
RB760iGS (Core Router)
WAN: 192.168.100.x
LAN: 172.20.1.1/24
|
RB951Ui-2HnD
Management: 172.20.1.2
|
WiFi KEBON-HOTSPOT
Gateway: 172.20.10.1/24
|
Hotspot Users

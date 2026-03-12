# Security Research: Vulnerability Assessment of Kipin.id Infrastructure

## Project Overview
Proyek ini mendokumentasikan proses independent security research dan vulnerability assessment terhadap infrastruktur publik milik Kipin.id. Fokus utama dari riset ini adalah untuk mengidentifikasi miskonfigurasi server dan paparan data sensitif yang dapat membahayakan integritas sistem.

Status: Reported (Responsible Disclosure)

---

## Tech Stack & Tooling
Dalam riset ini, digunakan berbagai alat standar industri untuk otomatisasi dan analisis manual:
* Targeting: httpx (Probing & service discovery)
* Fuzzing: ffuf (Directory & file discovery)
* Vulnerability Scanning: Nuclei (Template-based scanning)
* Analysis: Browser DevTools & Burp Suite (Traffic inspection & XHR analysis)
* Environment: Kali Linux on macOS (Apple Silicon via Virtual Machine)

---

## Methodology
Proses riset dilakukan mengikuti standar Penetration Testing Execution Standard (PTES):
1. Passive Reconnaissance: Mengumpulkan subdomain aktif dan informasi server.
2. Active Probing: Melakukan probing menggunakan httpx untuk memvalidasi layanan yang berjalan.
3. Directory Fuzzing: Menggunakan ffuf dengan wordlist common.txt untuk menemukan folder administratif.
4. Deep Analysis: Menganalisis respon XHR dan file konfigurasi yang terekspos secara manual.

---

## Key Findings

### 1. Exposed Administrative Interface (phpMyAdmin)
* Location: www.dashboard.kipin.id/phpmyadmin/
* Severity: High
* Description: Menemukan panel login database yang terekspos langsung ke internet. Hal ini meningkatkan risiko serangan credential stuffing atau brute force terhadap database pusat.

### 2. Configuration Disclosure (.htaccess)
* Location: www.dashboard.kipin.id/.htaccess
* Severity: Medium
* Description: File .htaccess dapat diakses secara publik, memberikan informasi mengenai aturan routing server dan konfigurasi internal lainnya.

### 3. Dangling Third-Party Integration
* Location: referral.kipin.id/admin
* Severity: Low
* Description: Menemukan integrasi GrowSurf yang tidak terurus (Campaign Deleted), namun kode frontend tetap mencoba memanggil API secara berulang. Ini menunjukkan kurangnya manajemen aset digital yang optimal.

---

## Responsible Disclosure
Keamanan data adalah prioritas utama. Semua temuan di atas telah dilaporkan kepada tim terkait melalui email formal pada Maret 2026. 

Disclaimer: Riset ini dilakukan semata-mata untuk tujuan edukasi dan membantu meningkatkan postur keamanan target. Tidak ada tindakan destruktif atau pengunduhan data sensitif yang dilakukan selama proses ini.

---

## About Me
Mahasiswa Universitas Semarang yang berfokus pada Web Development (Django/Laravel) dan Cybersecurity. Saat ini aktif mengeksplorasi integrasi AI (RAG) dan keamanan infrastruktur cloud.

---

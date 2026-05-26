# Automated Financial Reporting & Operations Simulation
Repository ini berisi simulasi lingkungan operasional bank tajirbgt yang dibangun di atas AWS. 
Proyek ini dirancang untuk mendemonstrasikan keahlian dalam mengelola infrastruktur cloud, 
database perbankan, otomasi data pipeline, serta penanganan insiden operasional sebagai L1/L2 Application Support Engineer.

## 🏗️ Cloud Infrastructure Architecture

Infrastruktur dasar dideploy secara manual melalui AWS Management Console dengan spesifikasi berikut:
* **Compute:** 1x AWS EC2 Instance (`t3.micro`) running Ubuntu Server 22.04 LTS.
* **Storage:** 1x AWS EBS Volume (gp3) untuk os & database lokal, serta 1x AWS S3 Bucket (`laporan-bank-tajirbgt-2026`) sebagai cold storage laporan harian.
* **Network & Security:** 1x Custom VPC dengan 1x Public Subnet, Internet Gateway, dan Security Group yang membuka Port 22 (SSH) dan Port 80 (HTTP).
* **IAM & Security Access:** 1x IAM Role (`EC2-To-S3-Upload-Role`) dengan policy `AmazonS3FullAccess` ditempelkan langsung ke EC2 untuk akses programmatic tanpa hardcoded credential.

Berikut adalah diagram alur operasional otomatisasi dan arsitektur sistem yang di-deploy di AWS:

![aws-ops-simulation-architecture](https://drive.google.com/file/d/10jruzk65Jjn3tsFGm7deZVHraJGoWh4j/view?usp=drive_link)

## 💾 Database State (PostgreSQL)

Di dalam server EC2, database bernama `mock_bank` telah dikonfigurasi dengan tabel `bank_transactions` yang menampung data tiruan untuk bahan simulasi insiden:

| Column Name | Data Type | Constraint |
| :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY |
| `account_id` | VARCHAR(50) | NOT NULL |
| `amount` | NUMERIC(15,2)| NOT NULL |
| `status` | VARCHAR(20) | NOT NULL (`SUCCESS` / `FAILED`) |
| `error_code` | VARCHAR(10) | NULLABLE |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP |

**Status Data Saat Ini:** 4 baris data awal berhasil dimasukkan (`INSERT 0 4`), mencakup transaksi sukses dan transaksi gagal dengan error code (`ERR_502` dan `TIMEOUT`).


## ⏳ Current Milestone
* [x] **Phase 1: Cloud Infrastructure Setup & Database Seeding** (Selesai)
* [ ] **Phase 2: Automation Script Development (`auto_reporting.py`)** (In Progress)
* [ ] **Phase 3: Application Support Incident Simulations & Playbook Documentation** (Planned)

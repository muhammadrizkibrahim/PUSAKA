<div align="center">

<img src="https://raw.githubusercontent.com/snipe/snipe-it/develop/public/img/logo-transparent.png" width="80" alt="PUSAKA Logo" />

# PUSAKA
### Pusat Kelola Barang Milik Negara

**Sistem Manajemen Barang Milik Negara berbasis [Snipe-IT](https://snipeitapp.com)**  
Diimplementasikan di **BPS Provinsi Kepulauan Riau**

[![Live App](https://img.shields.io/badge/Live%20App-pusaka.gurind.am-blue?style=flat-square&logo=googlechrome)](https://pusaka.gurind.am)
[![PHP](https://img.shields.io/badge/PHP-8.x-777BB4?style=flat-square&logo=php&logoColor=white)](https://php.net)
[![Laravel](https://img.shields.io/badge/Laravel-10.x-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://mysql.com)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=flat-square&logo=docker&logoColor=white)](https://docker.com)
[![Coolify](https://img.shields.io/badge/Deployed%20with-Coolify-6C3AC3?style=flat-square)](https://coolify.io)

</div>

---

## Tentang PUSAKA

**PUSAKA** (*Pusat Kelola Barang Milik Negara*) adalah sistem manajemen aset / Barang Milik Negara (BMN) yang dikembangkan dan disesuaikan untuk kebutuhan **BPS Provinsi Kepulauan Riau**. Sistem ini merupakan hasil replikasi dan kustomisasi dari aplikasi open-source [Snipe-IT](https://github.com/snipe/snipe-it), yang kemudian diadaptasi sesuai regulasi dan kebutuhan pengelolaan BMN di lingkungan instansi pemerintah.

Sistem ini memungkinkan petugas barang untuk mencatat, melacak, dan mengelola seluruh aset milik negara secara digital — mulai dari pengadaan, peminjaman, hingga penghapusan barang.

## Fitur Utama

- **Manajemen Aset** — Pencatatan lengkap aset BMN beserta detail, lokasi, dan kondisi barang
- **Pelacakan Status** — Monitoring status aset secara real-time (tersedia, dipinjam, dalam perbaikan, dll.)
- **Manajemen Pengguna** — Pengelolaan data pengguna/pegawai dan riwayat peminjaman
- **Kategori & Label** — Pengelompokan aset berdasarkan kategori, departemen, dan lokasi
- **Laporan & Ekspor** — Ekspor data aset ke format PDF dan Excel
- **Audit Log** — Riwayat lengkap setiap perubahan data aset
- **QR Code / Barcode** — Pelabelan aset dengan QR Code untuk pemindaian cepat
- **Kustomisasi Data** — Data disesuaikan dengan struktur organisasi dan kebutuhan BPS Provinsi Kepulauan Riau

## Tech Stack

### Aplikasi (Snipe-IT)
| Komponen | Teknologi |
|----------|-----------|
| Framework | Laravel (PHP) |
| Frontend | Bootstrap, jQuery |
| Database | MySQL 8.0 |
| Cache / Queue | Redis |
| Storage | Local / S3-compatible |
| Auth | Built-in (Session-based) |

### Infrastruktur & Deployment
| Komponen | Teknologi |
|----------|-----------|
| Kontainerisasi | Docker + Docker Compose |
| Platform Deploy | [Coolify](https://coolify.io) (self-hosted PaaS) |
| Server | VPS (Ubuntu) |
| Web Server | Nginx (reverse proxy) |
| SSL | Let's Encrypt (via Coolify) |
| Repository | GitHub |

## Arsitektur Deployment

```
Internet
    │
    ▼
[Cloudflare / DNS]
    │
    ▼
[VPS — Ubuntu]
    │
    ├── Coolify (Self-hosted PaaS)
    │       │
    │       ├── Nginx (Reverse Proxy + SSL)
    │       │
    │       └── Docker Compose
    │               ├── App Container  (PHP-FPM / Laravel)
    │               ├── MySQL Container
    │               └── Redis Container
    │
    └── pusaka.gurind.am
```

## Kustomisasi dari Snipe-IT

Berikut perubahan dan penyesuaian yang dilakukan dari Snipe-IT standar:

- **Data Lokasi** — Disesuaikan dengan struktur wilayah BPS Kepulauan Riau (provinsi, kabupaten/kota)
- **Kategori Aset** — Mengacu pada klasifikasi BMN sesuai PMK dan regulasi pemerintah
- **Perusahaan/Instansi** — Dikonfigurasi sesuai struktur organisasi BPS Provinsi Kepulauan Riau
- **Departemen/Bidang** — Disesuaikan dengan satuan kerja dan bidang di BPS Kepri
- **Supplier/Penyedia** — Data vendor dan rekanan pengadaan barang
- **Label & Branding** — Nama sistem, logo, dan tampilan disesuaikan menjadi PUSAKA
- **Field Kustom** — Penambahan field sesuai kebutuhan pelaporan BMN

## Cara Menjalankan Secara Lokal

### Prasyarat

- Docker & Docker Compose
- Git

### Langkah Instalasi

```bash
# Clone repositori ini
git clone https://github.com/<username>/<repo-name>.git
cd <repo-name>

# Salin file environment
cp .env.example .env

# Sesuaikan konfigurasi di .env
# (DB_DATABASE, DB_USERNAME, DB_PASSWORD, APP_URL, dll.)

# Jalankan dengan Docker Compose
docker compose up -d

# Generate application key
docker compose exec app php artisan key:generate

# Jalankan migrasi dan seeder
docker compose exec app php artisan migrate --seed

# (Opsional) Install dependensi manual
docker compose exec app composer install
docker compose exec app npm install && npm run dev
```

Akses aplikasi di `http://localhost` atau sesuai port yang dikonfigurasi.

## Deployment dengan Coolify

Proyek ini di-deploy menggunakan **Coolify** sebagai self-hosted PaaS di VPS kami.

1. Hubungkan repositori GitHub ini ke Coolify
2. Pilih metode deploy: **Docker Compose**
3. Atur environment variables sesuai kebutuhan
4. Coolify akan otomatis menangani:
   - Build image Docker
   - Provisioning SSL (Let's Encrypt)
   - Reverse proxy (Nginx/Traefik)
   - Restart otomatis saat push ke branch `main`

## Referensi

- [Snipe-IT Official](https://snipeitapp.com) — Aplikasi asal yang direplikasi
- [Snipe-IT GitHub](https://github.com/snipe/snipe-it) — Source code open-source
- [Snipe-IT Documentation](https://snipe-it.readme.io) — Dokumentasi lengkap
- [Coolify](https://coolify.io) — Platform deployment yang digunakan
- [BPS Kepulauan Riau](https://kepri.bps.go.id) — Instansi pengguna

## Lisensi

Aplikasi ini merupakan turunan dari [Snipe-IT](https://github.com/snipe/snipe-it) yang dilisensikan di bawah **AGPL-3.0**. Segala modifikasi dalam repositori ini mengikuti lisensi yang sama.

---

<div align="center">

Dikembangkan untuk **BPS Provinsi Kepulauan Riau**  
*Tanjungpinang, Kepulauan Riau — Indonesia*

</div>

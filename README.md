Pemrograman Berbasis Framework

DevOps & Deployment Engineer

✨ Deskripsi Singkat

Proyek ini adalah implementasi DevOps menggunakan Docker yang menggabungkan frontend (Laravel), backend (CodeIgniter 4), database (MySQL), dan NGINX sebagai reverse proxy. Semua bagian aplikasi dijalankan dalam container Docker terpisah, namun saling terhubung melalui jaringan internal yang sama.

⚡ Teknologi yang Digunakan

Docker: Platform container untuk menjalankan aplikasi

Laravel: Framework PHP untuk frontend

CodeIgniter 4 (CI4): Framework PHP untuk backend

MySQL: Sistem manajemen database relasional

NGINX: Web server dan reverse proxy

📂 Struktur Direktori

.
├── backend/            # Kode sumber backend (CI4)
│   ├── Dockerfile      # Instruksi build backend
│   └── .env            # Konfigurasi environment backend
├── frontend/           # Kode sumber frontend (Laravel)
│   ├── Dockerfile      # Instruksi build frontend
│   └── .env            # Konfigurasi environment frontend
├── mysql-init/         # Inisialisasi awal database
│   └── db.sql          # Skrip SQL (opsional)
├── nginx/              # Konfigurasi NGINX
│   └── nginx.conf      # Reverse proxy configuration
├── docker-compose.yml  # File utama untuk orkestrasi container
└── README.md           # Dokumentasi proyek

🚀 Langkah Eksekusi Proyek

1. Clone Repository

git clone https://github.com/AdimasPrawitAkbarSetiawan/Kelompok3_Framework.git
cd Kelompok3_Framework

2. Install Docker

Kunjungi Docker Desktop

Unduh & install untuk sistem operasi kamu (Windows/macOS)

Jalankan Docker Desktop dan pastikan statusnya running

3. Persiapkan Konfigurasi

Pastikan file berikut tersedia:

frontend/.env

backend/.env

frontend/Dockerfile

backend/Dockerfile

nginx/nginx.conf

4. Jalankan Docker Compose

docker-compose up --build

Atau di background:

docker-compose up -d --build

Docker akan:

Build image frontend dan backend

Menghubungkan ke database MySQL

Menyediakan akses ke aplikasi melalui NGINX

🌐 Akses Aplikasi

Frontend Laravel: http://localhost

PhpMyAdmin: http://localhost:8080

(Opsional) Dev Server Laravel Vite: http://localhost:3000

🛠️ DevOps Workflow dengan GitHub

GitHub digunakan untuk:

Menyimpan source code proyek

Berkolaborasi antar developer

Menyimpan dokumentasi seperti README ini

Cara Push Project ke GitHub:

git init
git remote add origin https://github.com/AdimasPrawitAkbarSetiawan/Kelompok3_Framework.git
git add .
git commit -m "Initial commit"
git push -u origin main

Setiap update:

git add .
git commit -m "Update commit"
git push

❓ Penjelasan Istilah

Docker: Alat untuk membuat dan menjalankan aplikasi dalam container

Container: Unit terisolasi tempat aplikasi berjalan

Dockerfile: File instruksi untuk membuat container image

.env: File konfigurasi environment

docker-compose.yml: File konfigurasi multi-container

NGINX: Server untuk mengarahkan traffic ke frontend/backend

💡 Tips & Catatan

Pastikan tidak ada port konflik seperti 80, 3306, atau 5173

Untuk memulai ulang dari awal:

docker-compose down
docker-compose up --build

Untuk melihat log container tertentu:

docker logs <nama-container>

📚 Dokumentasi Tambahan

Dokumentasi Docker

Dokumentasi Laravel

Dokumentasi CodeIgniter 4

✅ Dengan mengikuti panduan ini, Anda dapat menjalankan seluruh sistem aplikasi berbasis framework secara otomatis, rapi, dan konsisten. DevOps bukan hanya alat, tetapi cara kerja kolaboratif antara developer dan system engineer.

📦 GitHub Repository: AdimasPrawitAkbarSetiawan/Kelompok3_Framework


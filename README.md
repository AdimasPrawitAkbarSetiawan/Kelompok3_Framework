Pemrograman Berbasis Framework

DevOps & Deployment Engineer

✨ Deskripsi Singkat

Proyek ini adalah implementasi DevOps menggunakan Docker yang menggabungkan frontend (Laravel), backend (CodeIgniter 4), database (MySQL), dan NGINX sebagai reverse proxy. Semua bagian aplikasi dijalankan dalam container Docker terpisah, namun saling terhubung melalui jaringan internal yang sama.

⚡ Teknologi yang Digunakan

Docker: Untuk menjalankan semua bagian aplikasi dalam container

Laravel: Framework PHP untuk frontend

CodeIgniter 4 (CI4): Framework PHP untuk backend

MySQL: Sistem manajemen database

NGINX: Web server dan reverse proxy

📂 Struktur Direktori

.
├── backend/            # Folder berisi source code backend (CI4)
│   ├── Dockerfile      # Instruksi build container backend
│   └── .env          # Konfigurasi lingkungan backend
├── frontend/           # Folder berisi source code frontend (Laravel)
│   ├── Dockerfile      # Instruksi build container frontend
│   └── .env          # Konfigurasi lingkungan frontend
├── mysql-init/         # Inisialisasi awal untuk database
│   └── db.sql         # Skrip SQL (jika ada)
├── nginx/              # Konfigurasi untuk NGINX
│   └── nginx.conf    # Konfigurasi reverse proxy
├── docker-compose.yml  # File utama yang mengatur semua service
└── README.md         # Dokumentasi proyek

🚀 Langkah Eksekusi Proyek

1. Clone Repository

Clone seluruh struktur project ke dalam komputer lokal Anda:

# Clone repository utama
$ git clone https://github.com/AdimasPrawitAkbarSetiawan
$ cd <nama-folder kalian, disini folderku nama nya kelompok-3-PBF>

2. Install Docker

Jika belum memiliki Docker, ikuti langkah berikut:

Kunjungi https://www.docker.com/products/docker-desktop

Download dan install Docker Desktop (Windows/macOS)

Jalankan Docker Desktop dan pastikan statusnya running

3. Konfigurasi File

Pastikan struktur direktori Anda sesuai seperti yang dijelaskan di atas. Pastikan file berikut tersedia:

frontend/.env

backend/.env

frontend/Dockerfile

backend/Dockerfile

nginx/nginx.conf

4. Jalankan Docker Compose

Perintah ini akan membangun semua image dan menjalankan container:

docker-compose up --build

Jika ingin menjalankan di background:

docker-compose up -d --build

Docker akan secara otomatis:

Build backend (CI4) dan frontend (Laravel)

Menghubungkan ke database MySQL

Menyediakan akses melalui NGINX di port 80

📲 Akses Aplikasi

Setelah semua container berjalan, buka browser dan akses:

Frontend Laravel: http://localhost

PhpMyAdmin (opsional): http://localhost:8080

Jika menggunakan port dev Vite (opsional): http://localhost:3000

❓ Penjelasan Istilah

Docker: Alat untuk menjalankan aplikasi dalam "container" terisolasi agar bisa berjalan konsisten di mana pun.

Container: Seperti mesin virtual ringan, tempat aplikasi dijalankan tanpa tergantung OS komputer lokal.

Dockerfile: File berisi instruksi cara membangun container.

.env: File berisi pengaturan rahasia dan konfigurasi lingkungan.

docker-compose.yml: File yang mengatur seluruh service/container dalam satu sistem.

NGINX: Server yang bertugas sebagai perantara antara user dan aplikasi (reverse proxy).

🌟 Catatan Penting

Pastikan tidak ada port bentrok (misal 80, 3306, atau 5173 sudah dipakai program lain)

Jika ada perubahan pada source code atau konfigurasi, lakukan rebuild:

docker-compose down
docker-compose up --build

Untuk melihat log container:

docker logs <nama-container>

📄 Dokumentasi Tambahan

Kalau kalian baru mengenal DevOps atau Docker, disarankan membaca:

https://docs.docker.com/get-started/

https://laravel.com/docs

https://codeigniter.com/user_guide/

✅ Dengan mengikuti panduan ini, Kalian bisa menjalankan seluruh sistem aplikasi berbasis framework secara otomatis, rapi, dan konsisten. DevOps bukan sekadar tools, tapi cara kerja yang menyatukan developer dan sistem engineer dalam satu ekosistem produktif.

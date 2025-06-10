# Pemrograman Berbasis Framework

## DevOps & Deployment Engineer

---

## ✨ Deskripsi Singkat

Proyek ini adalah implementasi DevOps menggunakan Docker yang menggabungkan frontend (Laravel), backend (CodeIgniter 4), database (MySQL), dan NGINX sebagai reverse proxy. Semua bagian aplikasi dijalankan dalam container Docker terpisah, namun saling terhubung melalui jaringan internal yang sama.

---

## ⚡ Teknologi yang Digunakan

* **Docker**: Platform container untuk menjalankan aplikasi
* **Laravel**: Framework PHP untuk frontend
* **CodeIgniter 4 (CI4)**: Framework PHP untuk backend
* **MySQL**: Sistem manajemen database relasional
* **NGINX**: Web server dan reverse proxy

---

## 📂 Struktur Direktori

```
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
```

---

## 🚀 Langkah Eksekusi Proyek

### 1. Clone Repository

```bash
git clone https://github.com/AdimasPrawitAkbarSetiawan/Kelompok3_Framework.git
cd Kelompok3_Framework
```

### 2. Install Docker

1. Download Docker di link ini https://www.docker.com/products/docker-desktop
2. Unduh & install untuk sistem operasi kamu (Windows/macOS)
3. Jalankan Docker Desktop dan pastikan **statusnya running**

### 3. Persiapkan Konfigurasi

Pastikan file berikut tersedia:

* `frontend/.env`
* `backend/.env`
* `frontend/Dockerfile`
* `backend/Dockerfile`
* `nginx/nginx.conf`

### 4. Jalankan Docker Compose

```bash
docker-compose up --build
```

Atau di background:

```bash
docker-compose up -d --build
```

Docker akan:

* Build image frontend dan backend
* Menghubungkan ke database MySQL
* Menyediakan akses ke aplikasi melalui NGINX

---

## 🧱 Contoh Dockerfile

### Backend (CodeIgniter 4)

`backend/Dockerfile`

```Dockerfile
FROM php:8.2-fpm

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
    zip unzip git curl libpng-dev libjpeg-dev libfreetype6-dev libonig-dev libicu-dev \
    && docker-php-ext-install pdo pdo_mysql mbstring gd intl

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

COPY . .

RUN composer install --no-interaction --prefer-dist

RUN chown -R www-data:www-data /var/www/writable

EXPOSE 9001
CMD ["php-fpm"]
```

### Frontend (Laravel)

`frontend/Dockerfile`

```Dockerfile
FROM php:8.2-fpm

RUN apt-get update && apt-get install -y \
    git curl zip unzip libpng-dev libjpeg-dev libfreetype6-dev \
    libonig-dev libxml2-dev \
    && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY . .

RUN composer install --no-interaction --prefer-dist --optimize-autoloader

RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache

EXPOSE 9000
CMD ["php-fpm"]
```

---

## 🗂️ Contoh File docker-compose.yml

`docker-compose.yml`

```yaml
version: "3.8"

services:
  mysql:
    image: mysql:8
    ports:
      - "3307:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: app
      MYSQL_USER: user
      MYSQL_PASSWORD: secret
    volumes:
      - mysql-data:/var/lib/mysql

  frontend:
    build:
      context: ./frontend
    volumes:
      - ./frontend:/var/www
    depends_on:
      - mysql
    networks:
      - appnet

  backend:
    build:
      context: ./backend
    volumes:
      - ./backend:/var/www
    depends_on:
      - mysql
    networks:
      - appnet

  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - frontend
      - backend
    networks:
      - appnet

volumes:
  mysql-data:

networks:
  appnet:
    driver: bridge
```

---

## ⚙️ Konfigurasi NGINX

`nginx/nginx.conf`

```nginx
events {
    worker_connections 1024;
}

http {
    include mime.types;
    default_type application/octet-stream;
    sendfile on;
    keepalive_timeout 65;

    server {
        listen 80;
        index index.php index.html;
        server_name localhost;

        root /var/www/public;

        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
            include fastcgi_params;
            fastcgi_pass frontend:9000;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param DOCUMENT_ROOT $document_root;
        }

        location ~ /\.ht {
            deny all;
        }
    }
}
```

---

## 🌐 Akses Aplikasi

* **Frontend Laravel**: [http://localhost](http://localhost)
* **PhpMyAdmin** *(jika ditambahkan)*: [http://localhost:8080](http://localhost:8080)

---

## 🛠️ DevOps Workflow dengan GitHub

### Push Project ke GitHub:

```bash
git init
git remote add origin https://github.com/AdimasPrawitAkbarSetiawan/Kelompok3_Framework.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

Update:

```bash
git add .
git commit -m "Update commit"
git push
```

---

## ❓ Penjelasan Istilah

* **Docker**: Alat untuk membuat dan menjalankan aplikasi dalam container
* **Container**: Unit terisolasi tempat aplikasi berjalan
* **Dockerfile**: File instruksi untuk membuat container image
* **.env**: File konfigurasi environment
* **docker-compose.yml**: File konfigurasi multi-container
* **NGINX**: Server untuk mengarahkan traffic ke frontend/backend

---

## 💡 Tips & Catatan

* Pastikan tidak ada port konflik seperti 80, 3306, atau 5173
* Untuk memulai ulang dari awal:

```bash
docker-compose down
docker-compose up --build
```

* Untuk melihat log container:

```bash
docker logs <nama-container>
```

---

## 📚 Dokumentasi Tambahan

* [Dokumentasi Docker](https://docs.docker.com/get-started/)
* [Dokumentasi Laravel](https://laravel.com/docs)
* [Dokumentasi CodeIgniter 4](https://codeigniter.com/user_guide/)

---

✅ Dengan mengikuti panduan ini, Anda dapat menjalankan seluruh sistem aplikasi berbasis framework secara otomatis, rapi, dan konsisten. DevOps bukan hanya alat, tetapi cara kerja kolaboratif antara developer dan system engineer.

📦 GitHub Repository: [AdimasPrawitAkbarSetiawan/Kelompok3\_Framework](https://github.com/AdimasPrawitAkbarSetiawan/Kelompok3_Framework)

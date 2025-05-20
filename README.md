# bts-web2025
Project Web 2025  Laravel nextjs
Panduan Implementasi Website Laboratory Equipment
Timeline & Roadmap Pengembangan
Fase 0: Persiapan Environment (1 Minggu)
Hari	Kegiatan	Detail
1-2	Instalasi Tools	Laragon, Git, VS Code, PHP, Composer, Node.js
3	Setup GitHub	Membuat akun, repository, dan belajar basic Git
4-5	Setup Project Awal	Inisialisasi Laravel & Filament
6-7	Konfigurasi Database	Setup MySQL dan schema awal
Fase 1: Backend Development (4 Minggu)
Minggu	Kegiatan	Detail
1	Setup Admin Panel	Authentication, konfigurasi Filament
2	Manajemen Produk	CRUD produk dan kategori
3	RFQ & Testimonial	Form RFQ dan manajemen testimonial
4	Analytics & Settings	Integrasi analytics dan pengaturan tema
Fase 2: Frontend Development (3 Minggu)
Minggu	Kegiatan	Detail
1	Setup Next.js	Inisialisasi project dan konfigurasi Tailwind CSS
2	Halaman Utama & Katalog	Homepage, katalog produk dengan filter/search
3	Fitur Lanjutan	Perbandingan produk, form RFQ, multi-bahasa
Fase 3: Integrasi & Testing (2 Minggu)
Minggu	Kegiatan	Detail
1	Integrasi Backend-Frontend	API endpoints dan konsumsi data
2	Testing & Bug Fixing	Testing semua fitur dan perbaikan bugs
Fase 4: Deployment (1 Minggu)
Hari	Kegiatan	Detail
1-3	Deployment Backend	Upload ke Hostinger dan konfigurasi
4-6	Deployment Frontend	Static export Next.js dan upload
7	Final Testing	Testing di environment production
Panduan Step-by-Step
A. Persiapan Environment
1. Instalasi Laragon
Download Laragon Full dari situs resmi
Install dengan mengikuti wizard (terima semua default settings)
Setelah instalasi, buka Laragon dan klik "Start All"
Pastikan services Apache dan MySQL berjalan (indikator hijau)
2. Instalasi Git
Git sudah termasuk dalam Laragon, tapi bisa diupdate:
Klik kanan pada Laragon > Tools > Quick add > Git
Verifikasi instalasi: buka Terminal di Laragon, ketik:
git --version
3. Instalasi VS Code
Download VS Code dari situs resmi
Install dengan mengikuti wizard
Install extensions yang direkomendasikan:
PHP Intelephense
Laravel Blade formatter
Tailwind CSS IntelliSense
MySQL
GitLens
ESLint & Prettier
4. Setup GitHub dan Repository
Buat akun di GitHub
Install GitHub Desktop untuk kemudahan:
Download dari desktop.github.com
Buat repository baru:
Buka GitHub.com > klik '+' di kanan atas > New repository
Beri nama "lab-equipment-website"
Pilih "Public" atau "Private" sesuai kebutuhan
Klik "Create repository"
Clone repository ke lokal:
Di GitHub Desktop: File > Clone repository
Pilih repository yang baru dibuat
Pilih lokasi penyimpanan (sebaiknya di folder www/htdocs Laragon)
Klik "Clone"
B. Setup Backend (Laravel & Filament)
1. Instalasi Laravel
Buka Terminal Laragon (klik tombol Terminal)
Navigasi ke folder repository:
cd C:/laragon/www/lab-equipment-website
Buat project Laravel baru:
composer create-project laravel/laravel backend
Masuk ke folder backend:
cd backend
2. Konfigurasi Database
Buka Laragon, klik Menu > MySQL > HeidiSQL
Buat database baru: klik kanan di sidebar kiri > Create new > Database:
Beri nama "lab_equipment"
Character set: utf8mb4
Collation: utf8mb4_unicode_ci
Edit file .env di folder backend menggunakan VS Code:
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=lab_equipment
DB_USERNAME=root
DB_PASSWORD=
3. Instalasi Filament
Dalam terminal di folder backend:
composer require filament/filament:"^3.0" -W
Setup Filament:
php artisan filament:install --panels
Buat user admin pertama:
php artisan make:filament-user
Ikuti prompt untuk membuat user admin
4. Membuat Model & Resources
Membuat model Category:
php artisan make:model Category -m
Edit migration file di database/migrations/xxxx_create_categories_table.php:
php
Schema::create('categories', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('slug')->unique();
    $table->timestamps();
});
Buat Filament Resource untuk Category:
php artisan make:filament-resource Category
Ulangi langkah 1-3 untuk model Product dan tabel lainnya
5. Setup GitHub Workflow
Commit perubahan pertama:
Buka GitHub Desktop
Pastikan semua file terdeteksi (kecuali yang ada di .gitignore)
Tulis summary: "Initial Laravel & Filament setup"
Klik "Commit to main"
Klik "Push origin" untuk upload ke GitHub
C. Setup Frontend (Next.js)
1. Instalasi Next.js
Buka Terminal baru di Laragon
Navigasi ke folder repository:
cd C:/laragon/www/lab-equipment-website
Buat project Next.js:
npx create-next-app@latest frontend
Jawab pertanyaan setup:
Use TypeScript? Yes
Use ESLint? Yes
Use Tailwind CSS? Yes
Use src/ directory? Yes
Use App Router? Yes
Import alias? Terserah (biasanya @/*)
2. Setup Tailwind dan UI Components
Masuk ke direktori frontend:
cd frontend
Install dependencies tambahan:
npm install axios i18next react-i18next next-themes
3. Setup Multi-Language
Buat struktur folder untuk translasi:
mkdir -p src/i18n/locales
Buat file translasi dasar
4. Setup Dark/Light Mode
Konfigurasi provider tema di layout utama
D. Integrasi Backend-Frontend
1. Setup API Endpoints di Laravel
Buat API controllers untuk Products, Categories, dll
Setup routes di routes/api.php
2. Konsumsi API di Next.js
Setup axios instance dengan base URL API
Buat custom hooks untuk fetching data
E. Deployment
1. Export Static Next.js
Setup export di next.config.js:
js
const nextConfig = {
  output: 'export',
};
Build project:
npm run build
2. Upload ke Hostinger
Upload folder Laravel via FTP/File Manager
Upload folder out dari Next.js build
Setup subdomain atau domain untuk frontend
Tips untuk Pemula
Git Commands Dasar
bash
# Melihat status perubahan
git status

# Menambahkan semua file ke staging
git add .

# Commit perubahan
git commit -m "Pesan commit"

# Upload ke repository
git push

# Download perubahan terbaru
git pull

# Melihat history commit
git log
Workflow Development yang Disarankan
Mulai hari dengan git pull untuk mendapatkan perubahan terbaru
Kerjakan fitur atau perbaikan
Test lokally
Commit dan push perubahan di akhir hari
Jangan ragu untuk membuat branch terpisah untuk fitur eksperimental
Best Practices
Selalu backup database secara berkala
Gunakan .env untuk menyimpan konfigurasi sensitif
Jangan commit file besar atau binaries ke Git
Buat commit kecil dan sering dengan pesan yang jelas
Test secara menyeluruh sebelum deployment
Langkah Selanjutnya
Setelah berhasil setup environment dan mempelajari workflow dasar:

Pelajari lebih lanjut tentang Filament: Dokumentasi Filament
Pelajari Next.js: Dokumentasi Next.js
Eksplorasi referensi UI dari Labconco untuk inspirasi design
Tentukan struktur database final sebelum implementasi penuh
Semoga panduan ini membantu Anda sebagai pemula untuk memulai project development website laboratory equipment. Jangan ragu untuk mengajukan pertanyaan jika ada kesulitan di langkah manapun!


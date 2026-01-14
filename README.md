# 🏥 Sistem Antrian Klinik Online

Aplikasi web berbasis Laravel untuk mengelola antrian pasien klinik dengan sistem yang efisien, real-time, dan user-friendly.

## 👥 Kelompok

| Nama           | NIM        | Role                                |
| -------------- | ---------- | ----------------------------------- |
| M.Fauzul Abied | 2402510016 | Project Manager & Backend Developer |
| Siti Sa'diyah  | 2402510024 | Frontend Developer & UI/UX Designer |
| Nadiya Tri ramadhani          | 2402510012   | Date Administrator & Tester          |

## 📋 Deskripsi Project

Sistem Antrian Klinik Online adalah aplikasi web yang memudahkan pasien untuk mendaftar antrian secara online tanpa harus datang langsung ke klinik. Admin dapat mengelola antrian dengan efisien, memanggil pasien berikutnya secara otomatis, dan melacak status antrian secara real-time.
Ngepushnya numpang dilaptop temen saya yang bernama Dani Bahri.

## ✨ Fitur Unggulan

### 🎯 Fitur Utama

1. **Sistem Antrian Otomatis**

    - Nomor antrian otomatis per dokter per tanggal (mulai dari 1)
    - Pencegahan duplikasi antrian untuk dokter yang sama di tanggal yang sama
    - Maksimal 20 antrian per dokter per hari

2. **Validasi Jadwal Dokter**

    - Validasi otomatis tanggal kunjungan dengan jadwal praktek dokter
    - Notifikasi modal jika tanggal tidak sesuai jadwal dokter
    - Informasi jadwal praktek dokter (hari, jam, spesialisasi)

3. **Multi-Role Management**

    - **Admin**: Kelola antrian, dokter, poli, dan pasien
    - **User/Pasien**: Daftar antrian, lihat riwayat, batalkan antrian

4. **Thread-Safe Operations**

    - Database transaction dengan row-level locking
    - Pencegahan race condition saat concurrent registration
    - Atomic operations untuk update status antrian

5. **Filter & Search Advanced**
    - Filter berdasarkan tanggal, status, dan poli
    - Pencarian berdasarkan nama pasien
    - Statistik real-time per tanggal

### 🚀 Fitur Tambahan

-   **Dashboard Interaktif**: Statistik visual untuk admin dan pasien
-   **Responsive Design**: Tampilan optimal di desktop dan mobile
-   **Auto-Call Next Queue**: Tombol "Panggil Berikutnya" otomatis memanggil antrian terkecil
-   **Status Management**: WAITING → CALLED → DONE/CANCELED
-   **Queue History**: Riwayat antrian lengkap dengan filter dan pagination
-   **Profile Management**: Update profil dan password
-   **Real-time Notifications**: Alert toast untuk setiap aksi

## 🛠️ Teknologi yang Digunakan

### Backend

-   **Laravel 12.x** - PHP Framework
-   **PHP 8.2+** - Programming Language
-   **MySQL** - Database Management System
-   **Eloquent ORM** - Database Query Builder

### Frontend

-   **Blade Templates** - Template Engine
-   **Tailwind CSS** - Utility-First CSS Framework
-   **Preline UI** - UI Component Library
-   **JavaScript (Vanilla)** - Interactive Features

### Tools & Libraries

-   **Composer** - PHP Dependency Manager
-   **NPM/Vite** - Asset Bundling
-   **Laravel Pint** - Code Style Fixer
-   **Faker** - Test Data Generator

## 📦 Instalasi

### Prasyarat

-   PHP >= 8.2
-   Composer
-   MySQL/MariaDB
-   Node.js & NPM

### Langkah Instalasi

1. **Clone Repository**

    ```bash
    git clone https://github.com/danibahri/antrian-klinik.git
    cd antrian-klinik
    ```

2. **Install Dependencies**

    ```bash
    composer install
    npm install
    ```

3. **Setup Environment**

    ```bash
    cp .env.example .env
    php artisan key:generate
    ```

4. **Konfigurasi Database**

    Edit file `.env`:

    ```env
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=antrian_klinik
    DB_USERNAME=root
    DB_PASSWORD=
    ```

5. **Migrasi Database**

    ```bash
    php artisan migrate
    php artisan db:seed
    ```

6. **Build Assets**

    ```bash
    npm run build
    ```

7. **Jalankan Aplikasi**

    ```bash
    php artisan serve
    ```

    Aplikasi akan berjalan di `http://localhost:8000`

## 👤 Default User Credentials

Setelah seeding, gunakan kredensial berikut untuk login:

### Admin

-   **Email**: adminku@klinik.com
-   **Password**: password

### User/Pasien (jika ada seeder)

-   **Email**: user@gmail.com
-   **Password**: password

## 📱 Cara Penggunaan

### Untuk Pasien

1. **Registrasi Akun**

    - Klik "Daftar" di halaman login
    - Isi form: nama, email, telepon, tanggal lahir, alamat, password
    - Submit dan otomatis login

2. **Daftar Antrian**

    - Pilih Poli yang diinginkan
    - Pilih Dokter (lihat jadwal praktek)
    - Pilih tanggal kunjungan (sesuai jadwal dokter)
    - Isi keluhan (min. 10 karakter)
    - Submit untuk mendapat nomor antrian

3. **Kelola Antrian**
    - Lihat antrian aktif di dashboard
    - Batalkan antrian (jika status masih WAITING)
    - Lihat riwayat semua antrian

### Untuk Admin

1. **Kelola Antrian**

    - Lihat semua antrian di halaman "Kelola Antrian"
    - Filter berdasarkan tanggal, status, poli
    - Panggil antrian berikutnya otomatis
    - Panggil, selesaikan, atau batalkan antrian manual

2. **Kelola Master Data**
    - CRUD Dokter (nama, poli, jadwal, spesialisasi)
    - CRUD Poli (nama, deskripsi)
    - Lihat daftar pasien terdaftar

## 🗂️ Struktur Database

### Tabel Utama

-   **users**: Data user (admin & pasien)
-   **doctors**: Data dokter (nama, jadwal, spesialisasi)
-   **polis**: Data poli/klinik
-   **queues**: Data antrian dengan relasi ke users dan doctors

### Relasi

-   User `hasMany` Queue
-   Doctor `hasMany` Queue
-   Poli `hasMany` Doctor
-   Queue `belongsTo` User
-   Queue `belongsTo` Doctor

## 🔒 Keamanan

-   ✅ Password hashing dengan bcrypt
-   ✅ CSRF protection
-   ✅ XSS prevention
-   ✅ SQL injection prevention (Eloquent ORM)
-   ✅ Authentication middleware
-   ✅ Role-based access control
-   ✅ Database transaction locking

## 🐛 Bug Fixes & Improvements

### Recent Fixes (Jan 2026)

1. ✅ Fixed queue numbering race condition dengan database locking
2. ✅ Fixed ordering priority (queue_number first)
3. ✅ Fixed concurrent update conflicts dengan transactions
4. ✅ Fixed inconsistent date filtering
5. ✅ Added atomic operations untuk semua status updates

## 📄 License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

## 🤝 Kontribusi

Kontribusi, issues, dan feature requests sangat diterima!

1. Fork repository ini
2. Buat branch baru (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request

## 📞 Kontak

-   **Repository**: [https://github.com/serbag322-bit/UAS-Web-Based-Programming](https://github.com/danibahri/antrian-klinik)
-   **Email**: [fauzulabied.com]

---

**Dibuat dengan ❤️ untuk memudahkan pelayanan kesehatan**

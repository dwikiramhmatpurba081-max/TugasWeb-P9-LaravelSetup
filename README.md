# Tugas Rutin 9 — Setup Laravel

Project latihan Laravel 12 dengan tiga halaman Blade, data dinamis, model `Post`, migration, dan route parameter sebagai bonus.

## Persyaratan

- PHP 8.2 atau lebih baru dengan ekstensi yang dibutuhkan Laravel (termasuk `pdo_mysql`, `mbstring`, `openssl`, `fileinfo`, `tokenizer`, dan `xml`)
- Composer
- MySQL dan phpMyAdmin (contohnya dari XAMPP)

## Instalasi dan menjalankan

1. Jalankan MySQL dari XAMPP, lalu buka phpMyAdmin.
2. Buat database bernama `tugas_web_p9` dengan collation `utf8mb4_unicode_ci`.
3. Di terminal pada folder project, pasang dependency:

   ```powershell
   composer install
   ```

4. Jika file `.env` belum ada, salin konfigurasi contoh (file `.env` lokal yang disertakan dapat langsung dipakai):

   ```powershell
   Copy-Item .env.example .env
   ```

5. Periksa pengaturan `DB_HOST`, `DB_PORT`, `DB_DATABASE`, `DB_USERNAME`, dan `DB_PASSWORD` di `.env`. Nilai awal memakai konfigurasi MySQL XAMPP yang umum: `127.0.0.1:3306`, database `tugas_web_p9`, user `root`, dan password kosong.
6. Buat application key dan jalankan seluruh migration:

   ```powershell
   php artisan key:generate
   php artisan migrate
   ```

7. Jalankan server lokal:

   ```powershell
   php artisan serve
   ```

8. Buka <http://127.0.0.1:8000>. Untuk bukti tugas, ambil screenshot halaman tersebut saat server berjalan.

> Jika tabel cache/session gagal diakses, pastikan database telah dibuat dan jalankan `php artisan migrate` sebelum mencoba lagi.

## Halaman dan route

| URL | Isi |
| --- | --- |
| `/` | Beranda dengan daftar fitur dinamis dari controller |
| `/about` | Informasi project dengan daftar prinsip dinamis |
| `/contact` | Informasi kontak |
| `/hello/{nama}` | Bonus: sapaan dengan parameter nama, misalnya `/hello/Dewi` |

Seluruh halaman menggunakan Blade dan layout bersama di `resources/views/layouts/app.blade.php`. Styling memakai Tailwind CSS CDN sehingga tidak perlu proses build frontend.

## Controller, model, dan migration

- `app/Http/Controllers/PageController.php` mengirim data ke halaman Blade.
- `app/Models/Post.php` adalah model Eloquent untuk tabel `posts`.
- `database/migrations/2026_10_11_000000_create_posts_table.php` membuat tabel `posts`.

Pada project baru, perintah Artisan berikut menghasilkan controller dan model beserta migration. File hasil yang sesuai sudah tersedia di project ini:

```powershell
php artisan make:controller PageController
php artisan make:model Post -m
```

Jangan jalankan ulang perintah generator tersebut di project ini karena file-file hasilnya sudah ada.

## Pengujian

Setelah dependency terpasang, jalankan:

```powershell
php artisan test
```

Tes fitur memeriksa ketiga halaman utama, data dinamis, dan route sapaan.

## Struktur folder

```text
app/
  Http/Controllers/   Controller halaman
  Models/             Model Eloquent
bootstrap/             Bootstrap aplikasi Laravel
config/                Konfigurasi aplikasi dan database
database/
  migrations/          Skema database
public/                Entry point dan aset publik
resources/views/       Template Blade dan layout
routes/web.php         Definisi route web
storage/               Log dan file hasil runtime
tests/Feature/         Tes route dan halaman
```

## Repository tugas

Nama repository yang diminta: `TugasWeb-P9-LaravelSetup`.

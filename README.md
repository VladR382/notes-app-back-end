# Notes App Back-end

Ini adalah repositori untuk RESTful API yang dibangun dengan **Hapi**. Aplikasi ini memungkinkan pengguna untuk mendaftar, masuk, dan mengelola *notes* (catatan) pribadi mereka. Data disimpan dalam database **PostgreSQL** dan sistem autentikasi diamankan menggunakan **JSON Web Tokens (JWT)**.

## Fitur

  * **Manajemen Pengguna**:
      * **Registrasi Pengguna Baru**: Membuat akun pengguna baru dengan username, password (dienkripsi), dan nama lengkap.
      * **Login Pengguna**: Mengautentikasi pengguna dan memberikan *access token* serta *refresh token* (JWT).
      * **Refresh Token**: Memperbarui *access token* yang sudah kedaluwarsa tanpa perlu login kembali.
  * **Manajemen Catatan (CRUD)**:
      * **Tambah Catatan**: Membuat catatan baru yang terikat pada pengguna yang sedang login.
      * **Lihat Semua Catatan**: Mendapatkan daftar semua catatan milik pengguna yang sedang login.
      * **Lihat Detail Catatan**: Mendapatkan detail catatan berdasarkan ID, dengan verifikasi kepemilikan.
      * **Ubah Catatan**: Memperbarui catatan yang ada berdasarkan ID, dengan verifikasi kepemilikan.
      * **Hapus Catatan**: Menghapus catatan berdasarkan ID, dengan verifikasi kepemilikan.
  * **Keamanan & Validasi**:
      * **Otorisasi**: Pengguna hanya dapat mengakses dan memodifikasi catatan milik mereka sendiri.
      * **Validasi Input**: Memastikan semua data yang dikirim oleh klien sesuai dengan skema yang ditentukan menggunakan **Joi**.
      * **Penanganan Error**: Menggunakan *custom error* untuk memberikan respons yang jelas saat terjadi kesalahan pada permintaan klien atau server.

## Teknologi yang Digunakan

  * **[Hapi](https://hapi.dev/)**: Framework Node.js untuk membangun RESTful API.
  * **[PostgreSQL](https://www.postgresql.org/)**: Sistem manajemen basis data relasional sebagai penyimpan data.
  * **[@hapi/jwt](https://github.com/hapijs/jwt)**: Plugin Hapi untuk autentikasi menggunakan JSON Web Tokens.
  * **[bcrypt](https://www.npmjs.com/package/bcrypt)**: Pustaka untuk mengenkripsi dan memverifikasi password.
  * **[Joi](https://joi.dev/)**: Pustaka validasi skema objek.
  * **[nanoid](https://github.com/ai/nanoid)**: Pustaka untuk menghasilkan ID unik.
  * **[node-pg-migrate](https://github.com/salsita/node-pg-migrate)**: Alat untuk mengelola migrasi skema database.
  * **[ESLint](https://eslint.org/)**: Alat untuk menjaga konsistensi gaya penulisan kode.
  * **[Nodemon](https://nodemon.io/)**: Utilitas untuk me-restart server secara otomatis saat ada perubahan file.

## Struktur Proyek

```
.
├── migrations/         # File migrasi database
├── node_modules/
├── src/
│   ├── api/
│   │   ├── notes/        # Modul untuk fitur Notes
│   │   ├── users/        # Modul untuk fitur Users
│   │   └── authentications/ # Modul untuk fitur Authentications
│   ├── exceptions/       # Class error kustom
│   ├── services/
│   │   └── postgres/     # Logika bisnis (CRUD) dengan database PostgreSQL
│   ├── tokenize/
│   │   └── TokenManager.js # Logika pembuatan dan verifikasi JWT
│   ├── validator/        # Skema validasi Joi untuk setiap modul
│   └── server.js         # Inisialisasi dan konfigurasi server Hapi
├── .env                  # (Contoh) File konfigurasi environment
├── .gitignore
├── eslint.config.mjs
├── package-lock.json
└── package.json
```

## API Endpoints

Berikut adalah rute API yang tersedia:

| Metode | Path | Deskripsi | Memerlukan Autentikasi |
| :--- | :--- | :--- |:---:|
| `POST` | `/users` | Mendaftarkan pengguna baru. | Tidak |
| `POST`| `/authentications` | Login untuk mendapatkan token. | Tidak |
| `PUT`| `/authentications` | Memperbarui access token. | Tidak |
| `DELETE`| `/authentications` | Menghapus refresh token (logout). | Tidak |
| `POST` | `/notes` | Menambahkan catatan baru. | **Ya** |
| `GET` | `/notes` | Mendapatkan semua catatan milik pengguna. | **Ya** |
| `GET` | `/notes/{id}` | Mendapatkan detail catatan berdasarkan ID. | **Ya** |
| `PUT` | `/notes/{id}` | Mengubah catatan berdasarkan ID. | **Ya** |
| `DELETE`| `/notes/{id}`| Menghapus catatan berdasarkan ID. | **Ya** |

## Persiapan dan Instalasi

1.  **Clone repositori ini:**

    ```bash
    git clone https://github.com/vladr382/notes-app-back-end
    cd notes-app-back-end
    ```

2.  **Instal semua dependensi:**

    ```bash
    npm install
    ```

3.  **Konfigurasi Environment Variable:**
    Buat file `.env` di root proyek dan isi dengan konfigurasi database serta kunci untuk token JWT. Contoh:

    ```.env
    HOST=localhost
    PORT=5000

    # Konfigurasi Database PostgreSQL
    PGUSER=user
    PGPASSWORD=password
    PGDATABASE=notesdb
    PGHOST=localhost
    PGPORT=5432

    # Kunci JWT
    ACCESS_TOKEN_KEY=kunci_rahasia_access_token
    REFRESH_TOKEN_KEY=kunci_rahasia_refresh_token
    ACCESS_TOKEN_AGE=1800
    ```

4.  **Jalankan Migrasi Database:**
    Pastikan server PostgreSQL Anda berjalan. Kemudian, jalankan perintah berikut untuk membuat tabel-tabel yang dibutuhkan.

    ```bash
    npm run migrate up
    ```

## Menjalankan Aplikasi

Anda dapat menjalankan server dalam mode pengembangan atau produksi.

  * **Mode Pengembangan:**
    Perintah ini menggunakan `nodemon` untuk menjalankan server, yang akan otomatis me-restart jika ada perubahan file.

    ```bash
    npm run start:dev
    ```

  * **Mode Produksi:**

    ```bash
    npm run start:prod
    ```

Setelah server berjalan, API akan dapat diakses di `http://localhost:5000` (atau sesuai konfigurasi `.env` Anda).

## Linting

Untuk memeriksa kualitas dan konsistensi kode, jalankan perintah lint:

```bash
npm run lint
```
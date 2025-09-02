# Notes App Back End

Proyek latihan membuat aplikasi catatan sederhana menggunakan Node.js dan Hapi. Proyek ini mencakup fitur untuk mengelola catatan dan registrasi pengguna, dengan penyimpanan data menggunakan PostgreSQL.

## Fitur

  * **Manajemen Catatan**: Pengguna dapat membuat, melihat, memperbarui, dan menghapus catatan (CRUD).
  * **Manajemen Pengguna**: Pengguna dapat mendaftarkan akun baru dan mengambil data pengguna berdasarkan ID.
  * **Validasi Input**: Validasi data yang masuk menggunakan Joi untuk memastikan integritas data.
  * **Penanganan Kesalahan**: Implementasi penanganan kesalahan kustom untuk memberikan respons yang jelas saat terjadi error.
  * **Database PostgreSQL**: Menggunakan PostgreSQL untuk penyimpanan data yang persisten.

## Teknologi yang Digunakan

  * **Framework**: Hapi.js
  * **Database**: PostgreSQL
  * **Validator**: Joi
  * **Linter**: ESLint
  * **Password Hashing**: bcrypt
  * **Lainnya**: `node-pg-migrate`, `dotenv`, `nanoid`

## API Endpoints

Berikut adalah daftar endpoint API yang tersedia:

### Notes

| Method | Path          | Deskripsi                    |
| :----- | :------------ | :--------------------------- |
| `POST` | `/notes`      | Membuat catatan baru.        |
| `GET`  | `/notes`      | Mendapatkan semua catatan.     |
| `GET`  | `/notes/{id}` | Mendapatkan detail catatan.  |
| `PUT`  | `/notes/{id}` | Memperbarui catatan.         |
| `DELETE`| `/notes/{id}` | Menghapus catatan.           |

### Users

| Method | Path         | Deskripsi                       |
| :----- | :----------- | :------------------------------ |
| `POST` | `/users`     | Mendaftarkan pengguna baru.     |
| `GET`  | `/users/{id}`| Mendapatkan data pengguna.      |

## Instalasi dan Konfigurasi

1.  **Clone repository ini:**

    ```bash
    git clone <URL_REPOSITORY_ANDA>
    cd notes-app-back-end-add-user-regis
    ```

2.  **Instal semua dependency:**

    ```bash
    npm install
    ```

3.  **Konfigurasi Environment Variable:**
    Buat file `.env` di root direktori dan salin isi dari file `.env.example` (jika ada) atau isi dengan variabel berikut:

    ```env
    # Server configuration
    HOST=localhost
    PORT=5000

    # PostgreSQL configuration
    PGUSER=user
    PGPASSWORD=password
    PGDATABASE=notesapp
    PGHOST=localhost
    PGPORT=5432
    ```

    *Pastikan Anda memiliki database PostgreSQL yang berjalan dan sesuaikan kredensial di atas.*

4.  **Jalankan migrasi database:**
    Perintah ini akan membuat tabel `notes` dan `users` di database Anda.

    ```bash
    npm run migrate up
    ```

## Menjalankan Aplikasi

  * **Mode Development:**
    Menjalankan server dengan `nodemon` yang akan otomatis me-restart server setiap ada perubahan pada file.

    ```bash
    npm run start:dev
    ```

  * **Mode Production:**
    Menjalankan server untuk lingkungan produksi.

    ```bash
    npm run start:prod
    ```

Setelah server berjalan, Anda akan melihat pesan di konsol:
`Server berjalan pada http://localhost:5000`

# Notes App Back End

Ini adalah *back-end* untuk aplikasi catatan sederhana yang dibuat dengan Node.js dan Hapi.

-----

## Instalasi

1.  *Clone* repositori ini.
2.  Instal dependensi dengan menjalankan `npm install`.
3.  Buat berkas `.env` di direktori *root* dan tambahkan variabel lingkungan berikut:
    ```
    PORT=5000
    HOST=localhost
    PGUSER=...
    PGPASSWORD=...
    PGDATABASE=...
    PGHOST=...
    PGPORT=...
    ```
4.  Jalankan migrasi basis data dengan `npm run migrate`.

-----

## Menjalankan Aplikasi

  - Untuk mode pengembangan, gunakan `npm run start:dev`.
  - Untuk mode produksi, gunakan `npm run start:prod`.

-----

## *Endpoint* API

| Metode | Jalur | Deskripsi |
| --- | --- | --- |
| `POST` | `/notes` | Menambahkan catatan baru |
| `GET` | `/notes` | Mendapatkan semua catatan |
| `GET` | `/notes/{id}` | Mendapatkan catatan berdasarkan ID |
| `PUT` | `/notes/{id}` | Memperbarui catatan berdasarkan ID |
| `DELETE` | `/notes/{id}` | Menghapus catatan berdasarkan ID |

-----

## Teknologi yang Digunakan

  - **Hapi**: Kerangka kerja untuk membangun aplikasi web dan layanan.
  - **PostgreSQL**: Sistem basis data relasional.
  - **Joi**: Pustaka validasi data.
  - **nanoid**: Pembuat ID unik.
  - **dotenv**: Memuat variabel lingkungan dari berkas `.env`.
  - **ESLint**: Alat analisis kode statis untuk mengidentifikasi masalah dalam kode JavaScript.
  - **Nodemon**: Memantau perubahan dalam kode dan me-*restart* server secara otomatis.

-----

## Struktur Proyek

```
.
├── migrations
│   └── 1754807796666_create-table-notes.js
├── node_modules
├── src
│   ├── api
│   │   └── notes
│   │       ├── handler.js
│   │       ├── index.js
│   │       └── routes.js
│   ├── exceptions
│   │   ├── ClientError.js
│   │   ├── InvariantError.js
│   │   └── NotFoundError.js
│   ├── services
│   │   ├── inMemory
│   │   │   └── NotesService.js
│   │   └── postgres
│   │       └── NotesService.js
│   ├── utils
│   │   └── index.js
│   └── validator
│       └── notes
│           ├── index.js
│           └── schema.js
├── .gitignore
├── eslint.config.mjs
├── package-lock.json
├── package.json
└── README.md
```

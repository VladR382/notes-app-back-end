# Notes App Back-end (Versi Refactor)

Ini adalah repositori untuk RESTful API sederhana yang dibangun dengan **Hapi**. Aplikasi ini merupakan hasil refactor dari versi sebelumnya, dengan menerapkan arsitektur yang lebih modular untuk mengelola *notes* (catatan).

Aplikasi ini memungkinkan pengguna untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada catatan. Data catatan disimpan sementara di dalam memori (*in-memory*).

## Fitur

  * **Tambah Catatan Baru**: Membuat catatan baru dengan judul, isi, dan tag.
  * **Lihat Semua Catatan**: Mendapatkan daftar semua catatan yang telah disimpan.
  * **Lihat Detail Catatan**: Mendapatkan detail catatan berdasarkan ID uniknya.
  * **Ubah Catatan**: Memperbarui catatan yang ada berdasarkan ID-nya.
  * **Hapus Catatan**: Menghapus catatan berdasarkan ID-nya.
  * **Validasi Input**: Memastikan data yang dikirim oleh klien sesuai dengan skema yang ditentukan menggunakan **Joi**.
  * **Penanganan Error Terstruktur**: Menggunakan *custom error* untuk memberikan respons yang jelas dan informatif ketika terjadi kesalahan.

## Teknologi yang Digunakan

  * **[Hapi](https://hapi.dev/)**: Framework Node.js untuk membangun RESTful API yang andal dan dapat diskalakan.
  * **[Joi](https://joi.dev/)**: Pustaka validasi skema objek untuk memastikan integritas data.
  * **[nanoid](https://github.com/ai/nanoid)**: Pustaka untuk menghasilkan ID unik yang ringkas dan aman.
  * **[Nodemon](https://nodemon.io/)**: Utilitas untuk me-restart server secara otomatis saat ada perubahan file dalam mode pengembangan.
  * **[ESLint](https://eslint.org/)**: Alat untuk menganalisis dan menjaga konsistensi gaya penulisan kode.

## Struktur Proyek

Struktur proyek telah di-refactor untuk memisahkan setiap concern ke dalam modulnya masing-masing, membuatnya lebih mudah untuk dikelola dan dikembangkan.

```
.
├── node_modules/
├── src/
│   ├── api/
│   │   └── notes/
│   │       ├── index.js      # Plugin Hapi untuk notes
│   │       ├── handler.js      # Logika handler untuk setiap rute
│   │       └── routes.js       # Definisi rute-rute API notes
│   ├── exceptions/
│   │   ├── ClientError.js    # Class error kustom untuk kesalahan klien
│   │   ├── InvariantError.js # Error untuk kegagalan validasi
│   │   └── NotFoundError.js  # Error untuk sumber daya tidak ditemukan
│   ├── services/
│   │   └── inMemory/
│   │       └── NotesService.js # Logika bisnis (CRUD) untuk notes
│   ├── validator/
│   │   └── notes/
│   │       ├── index.js      # Validator untuk payload notes
│   │       └── schema.js       # Skema Joi untuk validasi
│   └── server.js           # Inisialisasi dan konfigurasi server Hapi
├── .gitignore
├── eslint.config.mjs       # Konfigurasi ESLint
├── package-lock.json
├── package.json
└── README.md
```

## API Endpoints

Berikut adalah rute API yang tersedia:

| Metode | Path          | Deskripsi                                |
| :----- | :------------ | :--------------------------------------- |
| `POST` | `/notes`      | Menambahkan catatan baru.                |
| `GET`  | `/notes`      | Mendapatkan semua catatan.               |
| `GET`  | `/notes/{id}` | Mendapatkan detail catatan berdasarkan ID. |
| `PUT`  | `/notes/{id}` | Mengubah catatan yang ada berdasarkan ID.|
| `DELETE`| `/notes/{id}`| Menghapus catatan berdasarkan ID.        |

### Contoh Request Body untuk `POST /notes` dan `PUT /notes/{id}`

```json
{
    "title": "Judul Catatan Baru",
    "body": "Isi dari catatan yang detail...",
    "tags": ["tutorial", "hapi"]
}
```

## Persiapan dan Instalasi

1.  **Clone repositori ini:**

    ```bash
    git clone https://github.com/vladr382/notes-app-back-end
    cd notes-app-back-end
    ```

2.  **Instal semua dependensi:**
    Gunakan `npm` untuk menginstal semua dependensi yang dibutuhkan yang tercantum dalam file `package.json`.

    ```bash
    npm install
    ```

## Menjalankan Aplikasi

Anda dapat menjalankan server dalam mode pengembangan atau produksi.

  * **Mode Pengembangan:**
    Perintah ini menggunakan `nodemon` untuk menjalankan server, yang akan secara otomatis me-restart ketika ada perubahan pada file.

    ```bash
    npm run start
    ```

  * **Mode Produksi:**
    Perintah ini menjalankan server dalam mode produksi, cocok untuk deployment.

    ```bash
    npm run start-prod
    ```

Setelah server berjalan, API akan dapat diakses di `http://localhost:5000`.

## Linting

Untuk memeriksa kualitas kode dan memastikan konsistensi, jalankan perintah lint:

```bash
npm run lint
```

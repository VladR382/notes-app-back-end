
# Notes App Back-end

Ini adalah repositori untuk back-end RESTful API sederhana yang dibangun dengan Hapi. Aplikasi ini memungkinkan pengguna untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada catatan. Data catatan disimpan dalam memori (in-memory).

## Fitur

* **Tambah Catatan Baru**: Membuat catatan baru dengan judul, tag, dan isi.
* **Lihat Semua Catatan**: Mendapatkan daftar semua catatan yang telah disimpan.
* **Lihat Detail Catatan**: Mendapatkan detail catatan berdasarkan ID uniknya.
* **Ubah Catatan**: Memperbarui catatan yang ada berdasarkan ID-nya.
* **Hapus Catatan**: Menghapus catatan berdasarkan ID-nya.

## Teknologi yang Digunakan

* **[Hapi](https://hapi.dev/)**: Framework Node.js untuk membangun RESTful API.
* **[Nodemon](https://nodemon.io/)**: Utilitas untuk me-restart server secara otomatis saat ada perubahan file dalam mode pengembangan.
* **[ESLint](https://eslint.org/)**: Alat untuk menganalisis dan menjaga konsistensi gaya penulisan kode.
* **[nanoid](https://github.com/ai/nanoid)**: Pustaka untuk menghasilkan ID unik yang aman untuk setiap catatan.

## Struktur Proyek

```
.
├── node_modules/
├── src/
│   ├── handler.js      # Logika bisnis untuk setiap rute
│   ├── notes.js        # Penyimpanan data catatan (in-memory array)
│   ├── routes.js       # Definisi rute-rute API
│   └── server.js       # Inisialisasi dan konfigurasi server Hapi
├── .gitignore
├── eslint.config.mjs   # Konfigurasi ESLint
├── package-lock.json
├── package.json
└── README.md
```

## API Endpoints

Berikut adalah rute API yang tersedia:

| Metode | Path | Deskripsi |
| :--- | :--- | :--- |
| `POST` | `/notes` | Menambahkan catatan baru. |
| `GET` | `/notes` | Mendapatkan semua catatan. |
| `GET` | `/notes/{id}` | Mendapatkan detail catatan berdasarkan ID. |
| `PUT` | `/notes/{id}` | Mengubah catatan yang ada berdasarkan ID. |
| `DELETE` | `/notes/{id}`| Menghapus catatan berdasarkan ID. |

### Contoh Request Body untuk `POST /notes`

```json
{
    "title": "Judul Catatan",
    "tags": ["tag1", "referensi"],
    "body": "Isi dari catatan..."
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
    Perintah ini menjalankan server dalam mode produksi.
    ```bash
    npm run start-prod
    ```

Setelah server berjalan, API akan dapat diakses di `http://localhost:5000`.

## Linting

Untuk memeriksa kualitas kode dan memastikan konsistensi, jalankan perintah lint:
```bash
npm run lint
```

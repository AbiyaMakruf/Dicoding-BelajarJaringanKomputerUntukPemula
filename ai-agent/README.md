# Dicoding - Belajar Fundamental Front-End Web Development

## Penilaian Proyek

Proyek ini merupakan submission akhir untuk kelas Dicoding **Belajar Fundamental Front-End Web Development** yang berhasil meraih predikat tertinggi **Bintang 5 (Skor Maksimal)** melalui pemenuhan seluruh kriteria wajib dan seluruh 4 kriteria opsional.

![Bukti Penilaian Bintang 5](readme/nilai.png)

[![JavaScript: ES6+](https://img.shields.io/badge/JavaScript-ES6%2B-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Webpack: 5.x](https://img.shields.io/badge/Webpack-5.x-8DD6F9?logo=webpack&logoColor=black)](https://webpack.js.org/)
[![Web Components](https://img.shields.io/badge/Web%20Components-Custom%20Elements-blue)](https://developer.mozilla.org/en-US/docs/Web/API/Web_components)
[![RESTful API: Dicoding V2](https://img.shields.io/badge/RESTful%20API-Dicoding%20v2-orange)](https://notes-api.dicoding.dev/v2)
[![SweetAlert2](https://img.shields.io/badge/UI%20Feedback-SweetAlert2-brightgreen)](https://sweetalert2.github.io/)
[![Anime.js](https://img.shields.io/badge/Animation-Anime.js-FF4B4B)](https://animejs.com/)
[![Prettier: Formatted](https://img.shields.io/badge/Code%20Style-Prettier-F7B93E?logo=prettier&logoColor=black)](https://prettier.io/)
[![Status: Bintang 5](<https://img.shields.io/badge/Rating-Bintang%205%20(Full%20Criteria)-success>)](#pemenuhan-kriteria-penilaian-bintang-5)

---

## Deskripsi Project

Proyek **Notes App (Integrasi RESTful API)** adalah aplikasi pencatatan modern berbasis _single-page application_ tanpa framework pihak ketiga (murni _Vanilla JavaScript_ dan _Web Components_ standar W3C). Aplikasi terhubung langsung secara real-time ke layanan server **Dicoding Notes API v2** ([https://notes-api.dicoding.dev/v2](https://notes-api.dicoding.dev/v2)) menggunakan **Fetch API** (`async/await`).

Seluruh modul dan aset JavaScript dibundel secara terstruktur menggunakan **Webpack** bersama modul pendukung seperti `html-webpack-plugin`, `css-loader`, `style-loader`, serta server pengembangan `webpack-dev-server`.

Aplikasi ini memenuhi seluruh kriteria wajib dan keempat kriteria opsional Dicoding:

1. **Kriteria Wajib 1 (Pertahankan Kriteria Sebelumnya):** Tata letak grid responsif dengan CSS Grid, formulir input catatan standar (`<input>` dan `<textarea>`), serta 5 implementasi Custom Elements Web Component (`<app-bar>`, `<note-form>`, `<note-item>`, `<loading-indicator>`, dan `<app-footer>`).
2. **Kriteria Wajib 2 (RESTful API sebagai Sumber Data):** Menghubungkan seluruh siklus hidup catatan ke Dicoding Notes API v2 untuk penambahan catatan baru, pembacaan daftar catatan aktif, dan penghapusan catatan tanpa menggunakan data lokal dumi.
3. **Kriteria Wajib 3 (Webpack Module Bundler):** Konfigurasi modular (`webpack.common.js`, `webpack.dev.js`, `webpack.prod.js`) dengan perintah `npm run start-dev` dan `npm run build`.
4. **Kriteria Wajib 4 (Fetch API):** Menggunakan native browser Fetch API secara asinkron dengan penanganan error respon status HTTP.
5. **Kriteria Wajib 5 (Indikator Loading):** Komponen custom `<loading-indicator>` dengan animasi pemintal (_spinner_) saat proses HTTP berlangsung.
6. **Kriteria Opsional 1 (Fitur Arsip Catatan):** Penuh dengan navigasi tab Catatan Aktif & Catatan Terarsip serta aksi arsip (`/notes/{id}/archive`) dan buka arsip (`/notes/{id}/unarchive`).
7. **Kriteria Opsional 2 (Feedback Error & Dialog Konfirmasi):** Notifikasi visual interaktif menggunakan library modern **SweetAlert2** untuk peringatan error jaringan, konfirmasi hapus permanen, dan toast sukses.
8. **Kriteria Opsional 3 (Efek Pergerakan Halus & Animasi):** Animasi halus berbasis **Anime.js** pada kemunculan kartu catatan (_stagger animation_), efek transisi tab, dan feedback penekanan tombol.
9. **Kriteria Opsional 4 (Prettier Code Formatter):** Konfigurasi standar `.prettierrc`, paket terdaftar di `devDependencies`, dan skrip otomatisasi `npm run format`.

---

## Daftar Isi

- [Struktur Repositori](#struktur-repositori)
- [Gambaran RESTful API & Endpoint](#gambaran-restful-api--endpoint)
- [Arsitektur dan Alur Aplikasi](#arsitektur-dan-alur-aplikasi)
- [Fitur Utama Aplikasi](#fitur-utama-aplikasi)
- [Pemenuhan Kriteria Penilaian (Bintang 5)](#pemenuhan-kriteria-penilaian-bintang-5)
- [Instalasi dan Setup](#instalasi-dan-setup)
- [Panduan Menjalankan Aplikasi](#panduan-menjalankan-aplikasi)
- [Ketentuan Berkas Submission](#ketentuan-berkas-submission)

---

## Struktur Repositori

```text
Dicoding-BelajarFundamentalFrontEndWebDevelopment/
├── .gitignore                         # Konfigurasi pengabaian berkas Git
├── .prettierrc                        # Konfigurasi aturan format kode Prettier
├── README.md                          # Dokumentasi lengkap proyek
├── package.json                       # Konfigurasi npm, dependensi, dan skrip runner
├── package-lock.json                  # Catatan versi dependensi terkunci
├── webpack.common.js                  # Konfigurasi dasar Webpack & HtmlWebpackPlugin
├── webpack.dev.js                     # Konfigurasi development & webpack-dev-server
├── webpack.prod.js                    # Konfigurasi produksi (minified bundle)
├── readme/
│   └── nilai.png                      # Bukti penilaian bintang 5 submission Dicoding
├── src/                               # Sumber kode utama aplikasi
│   ├── index.html                     # Templat HTML utama
│   ├── index.js                       # Titik masuk utama aplikasi & orkestrator state
│   ├── styles/
│   │   └── style.css                  # Desain CSS responsif, CSS Grid, & variabel tema
│   └── scripts/
│       ├── api/
│       │   └── notes-api.js           # Klien Fetch API untuk seluruh endpoint Notes API V2
│       ├── components/                # Implementasi Web Components (Custom Elements)
│       │   ├── app-bar.js             # Elemen kustom <app-bar> (Header & Search Bar)
│       │   ├── note-form.js           # Elemen kustom <note-form> (Form & Realtime Validation)
│       │   ├── note-item.js           # Elemen kustom <note-item> (Kartu Catatan & Aksi)
│       │   ├── loading-indicator.js   # Elemen kustom <loading-indicator> (Animasi Spinner)
│       │   └── app-footer.js          # Elemen kustom <app-footer> (Footer Informasi)
│       └── utils/
│           ├── alerts.js              # Utilitas feedback modal & toast SweetAlert2
│           └── animations.js          # Utilitas animasi halus dengan Anime.js
```

---

## Gambaran RESTful API & Endpoint

Aplikasi mengonsumsi API resmi Dicoding Notes V2 pada alamat dasar `https://notes-api.dicoding.dev/v2`:

| No  | Endpoint                | Metode HTTP | Deskripsi Fungsi                                       | Status Implementasi |
| :-: | :---------------------- | :---------: | :----------------------------------------------------- | :-----------------: |
|  1  | `/notes`                |    `GET`    | Mengambil seluruh daftar catatan aktif (non-archived)  |    **Terpasang**    |
|  2  | `/notes`                |   `POST`    | Menambahkan catatan baru dengan body `{ title, body }` |    **Terpasang**    |
|  3  | `/notes/archived`       |    `GET`    | Mengambil seluruh daftar catatan yang diarsipkan       |    **Terpasang**    |
|  4  | `/notes/{id}`           |    `GET`    | Mengambil detail satu catatan berdasarkan ID           |    **Tersedia**     |
|  5  | `/notes/{id}/archive`   |   `POST`    | Memindahkan catatan ke status arsip                    |    **Terpasang**    |
|  6  | `/notes/{id}/unarchive` |   `POST`    | Membatalkan status arsip catatan ke status aktif       |    **Terpasang**    |
|  7  | `/notes/{id}`           |  `DELETE`   | Menghapus catatan secara permanen dari server          |    **Terpasang**    |

---

## Arsitektur dan Alur Aplikasi

```mermaid
flowchart TD
    User([Pengguna]) <--> UI["Antarmuka Web Components\n(<app-bar>, <note-form>, <note-item>, <app-footer>)"]

    subgraph Client ["Client Logic (src/scripts/)"]
        UI -->|Event: note-create / archive / delete| Orchestrator["Main Orchestrator (src/index.js)"]
        Orchestrator -->|Trigger Loading| Loader["<loading-indicator> Component"]
        Orchestrator -->|Async HTTP Request| APIClient["API Service (notes-api.js)\nFetch API (async/await)"]
        APIClient -->|Success / Error Feedback| AlertService["SweetAlert2 Alerts (alerts.js)"]
        Orchestrator -->|Stagger & Entrance Transition| AnimService["Anime.js Engine (animations.js)"]
    end

    subgraph Backend ["Server Eksternal"]
        APIClient <-->|JSON Payload (v2)| CloudAPI["Dicoding Notes API\n(notes-api.dicoding.dev/v2)"]
    end
```

### 1. Manajemen Komponen (Web Components)

- Menerapkan arsitektur berbasis komponen mandiri tanpa framework.
- Memanfaatkan siklus hidup elemen kustom seperti `connectedCallback()` dan `attributeChangedCallback()`.
- Mendukung transmisi data melalui _Custom Attributes_ (`data-id`, `archived`) dan kustom event berbasis _CustomEvent_ (`note-create`, `note-archive-toggle`, `note-delete`, `search-query`).

### 2. Validasi Formulir Real-Time

- Input judul (`#note-title`) dan isi catatan (`#note-body`) dipantau secara langsung saat pengguna mengetik (`input` event).
- Dilengkapi dengan _Character Counter_ real-time (`0/100`).
- Tombol simpan dinonaktifkan (`disabled`) secara otomatis hingga data memenuhi batas minimal karakter yang ditentukan.
- Pesan kesalahan visual muncul di bawah masing-masing kolom masukan saat input tidak valid.

### 3. Indikator Loading & Feedback Interaktif

- Setiap interaksi jaringan (memuat data awal, menyimpan, mengubah status arsip, dan menghapus) memicu indikator pemuatan `<loading-indicator>`.
- Jika terjadi kegagalan jaringan atau server menolak request, pengguna diberikan notifikasi pesan galat informatif melalui **SweetAlert2**.
- Operasi penghapusan catatan dilengkapi modal konfirmasi pencegahan untuk menghindari penghapusan tidak disengaja.

---

## Fitur Utama Aplikasi

1. **Sinkronisasi Otomatis RESTful API:** Seluruh data catatan dikirim dan ditarik langsung dari server tanpa menggunakan penyimpanan data lokal dummy.
2. **Navigasi Kategori Catatan (Tab Aktif & Arsip):** Berpindah antara catatan aktif dan catatan yang telah diarsipkan secara mulus dengan indikator jumlah (_badge counter_).
3. **Pencarian Real-Time:** Filter pencarian instan pada bilah navigasi atas yang menyaring catatan berdasarkan kesesuaian judul maupun isi secara lokal dari data aktif.
4. **Layout Grid Responsif:** Penyusunan kartu catatan berbasis CSS Grid yang menyesuaikan layar perangkat dari ponsel cerdas, tablet, hingga monitor resolusi tinggi.
5. **Animasi Halus & Dinamis:** Efek masuk _staggered_ saat kartu catatan dimuat, transisi hover pada kartu catatan, dan efek visual responsif saat tombol di klik.
6. **Formulir Interaktif:** Proteksi validasi formulir instan dengan umpan balik visual yang ramah pengguna.

---

## Pemenuhan Kriteria Penilaian (Bintang 5)

| Kriteria                | Deskripsi Kriteria                                                                        | Implementasi pada Proyek                                                                                                                                                        |    Status     |
| :---------------------- | :---------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-----------: |
| **Kriteria Wajib 1**    | Pertahankan kriteria submission sebelumnya (form valid, CSS Grid layout, Web Components). | Memiliki form dengan judul & textarea body, CSS Grid layout pada `.grid-layout`, dan 5 Web Components (`app-bar`, `note-form`, `note-item`, `loading-indicator`, `app-footer`). | **Terpenuhi** |
| **Kriteria Wajib 2**    | Memanfaatkan RESTful API https://notes-api.dicoding.dev/v2 sebagai data utama.            | Terhubung penuh dengan endpoint API v2 (tambah, ambil, hapus catatan). Data lokal dumi telah dihilangkan.                                                                       | **Terpenuhi** |
| **Kriteria Wajib 3**    | Webpack sebagai module bundler (html-webpack-plugin, start-dev, build).                   | Dikonfigurasi dengan `webpack.common.js`, `webpack.dev.js`, `webpack.prod.js`, serta skrip `start-dev` dan `build`.                                                             | **Terpenuhi** |
| **Kriteria Wajib 4**    | Menggunakan Fetch API untuk interaksi asinkron.                                           | Seluruh request HTTP menggunakan `fetch()` natif dengan pola `async/await` di `src/scripts/api/notes-api.js`.                                                                   | **Terpenuhi** |
| **Kriteria Wajib 5**    | Memiliki indikator loading saat proses HTTP.                                              | Custom Element `<loading-indicator>` aktif saat memuat, membuat, mengarsipkan, dan menghapus catatan.                                                                           | **Terpenuhi** |
| **Kriteria Opsional 1** | Memiliki fitur arsip dan batal arsip catatan.                                             | Dilengkapi tombol arsip/aktifkan pada kartu serta tab filter Catatan Aktif & Catatan Terarsip.                                                                                  | **Terpenuhi** |
| **Kriteria Opsional 2** | Menampilkan feedback saat terjadi error.                                                  | Mengintegrasikan **SweetAlert2** untuk penanganan kegagalan jaringan, dialog konfirmasi hapus, dan toast sukses.                                                                | **Terpenuhi** |
| **Kriteria Opsional 3** | Memiliki efek pergerakan halus atau animasi.                                              | Mengintegrasikan **Anime.js** untuk transisi kemunculan kartu catatan (_stagger effect_), animasi tab, dan interaksi form.                                                      | **Terpenuhi** |
| **Kriteria Opsional 4** | Menerapkan Prettier sebagai Code Formatter.                                               | Memiliki berkas `.prettierrc`, dependensi `prettier` di `devDependencies`, dan skrip `npm run format`.                                                                          | **Terpenuhi** |

---

## Instalasi dan Setup

1. **Clone Repositori:**

   ```bash
   git clone https://github.com/AbiyaMakruf/Dicoding-BelajarFundamentalFrontEndWebDevelopment.git
   cd Dicoding-BelajarFundamentalFrontEndWebDevelopment
   ```

2. **Pasang Dependensi:**
   Pastikan Anda telah menginstal **Node.js** (versi 18 ke atas direkomendasikan):
   ```bash
   npm install
   ```

---

## Panduan Menjalankan Aplikasi

### 1. Mode Pengembangan (Development)

Jalankan server pengembangan lokal dengan fitur hot-reload:

```bash
npm run start-dev
```

Aplikasi akan aktif dan dapat diakses melalui peramban web pada alamat:
`http://localhost:9000/`

### 2. Membangun Berkas Distribusi (Production Build)

Lakukan kompilasi, optimasi, dan minifikasi seluruh berkas kode ke folder `dist/`:

```bash
npm run build
```

Berkas keluaran siap didistribusikan pada folder `dist/index.html` dan `dist/main.[contenthash].js`.

### 3. Merapikan Format Kode (Prettier Formatter)

Jalankan pemformatan kode di seluruh repositori:

```bash
npm run format
```

---

## Ketentuan Berkas Submission

Untuk pengumpulan berkas tugas ke platform Dicoding:

- Seluruh kode sumber, aset, dan konfigurasi Webpack berada di root proyek.
- Saat membuat arsip `notes-app.zip`, **jangan sertakan** direktori `node_modules` atau folder hasil kompilasi `dist` sesuai aturan submission Dicoding.

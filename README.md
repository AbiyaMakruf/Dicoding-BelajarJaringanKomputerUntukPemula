# Dicoding - Belajar Jaringan Komputer untuk Pemula

## Penilaian Proyek

Proyek ini merupakan submission akhir untuk kelas Dicoding **Belajar Jaringan Komputer untuk Pemula (A387)** yang dirancang untuk meraih predikat tertinggi **Bintang 5 (Skor Maksimal)** melalui pemenuhan seluruh kriteria wajib dan seluruh 4 saran pengembangan (opsional).

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express-4.x-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![NGINX](https://img.shields.io/badge/NGINX-1.24%2B-009639?logo=nginx&logoColor=white)](https://nginx.org/)
[![Apache2](https://img.shields.io/badge/Apache-2.4%2B-D22128?logo=apache&logoColor=white)](https://httpd.apache.org/)
[![Ubuntu WSL](https://img.shields.io/badge/Environment-WSL%20Ubuntu-E95420?logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Status: Bintang 5](https://img.shields.io/badge/Rating-Bintang%205%20(Semua%20Saran%20Terpenuhi)-success)](#pemenuhan-kriteria-penilaian-bintang-5)

---

## Deskripsi Project

Proyek **Membangun Web Server** ini berfokus pada implementasi arsitektur jaringan komputer modern di lingkungan lokal (WSL Ubuntu). Proyek ini mengintegrasikan aplikasi backend berbasis **Node.js (Express)** dengan **NGINX** dan **Apache2** sebagai *reverse proxy server*, dilengkapi dengan proteksi pembatasan akses (*rate limiting*).

Seluruh kriteria wajib dan saran bintang 5 telah diimplementasikan dan diuji secara menyeluruh:

1. **Kriteria Wajib 1 (Menyiapkan Web Server):** Melakukan integrasi repositori resmi Dicoding (`a387-jarkom-labs`), memasang NGINX, serta memastikan server Node.js dan NGINX dapat diakses dengan baik.
2. **Kriteria Wajib 2 (Konfigurasi NGINX sebagai Reverse Proxy):** Mengalihkan seluruh permintaan HTTP masuk dari port reverse proxy ke backend Express yang berjalan di port internal 8000.
3. **Kriteria Wajib 3 (Menerapkan Limit Access):** Mengonfigurasi modul rate limiting (`ngx_http_limit_req_module`) pada NGINX untuk mencegah beban berlebih dan serangan *abuse* / *flooding*.
4. **Saran 1 (Ubah Port NGINX ke 3000):** Mengubah port default NGINX dari port 80 menjadi port **3000** pada blok `server`.
5. **Saran 2 (Rate Limit 6 Request / Menit):** Menerapkan aturan rate limit sebesar **6 request per menit** (`rate=6r/m` atau 1 request per 10 detik) pada zona memori berukuran 10MB (`zone=one:10m`).
6. **Saran 3 (Route `/me` di Express):** Menambahkan endpoint `GET /me` pada berkas `app.js` yang mengembalikan teks username Dicoding (`abiyamf`) tanpa mengubah respons endpoint utama `/`.
7. **Saran 4 (Implementasi Serupa pada Apache2):** Mengonfigurasi **Apache2** sebagai alternatif reverse proxy dengan modul `proxy` dan `proxy_http`, diarahkan ke port 3000 (`ports.conf` & `000-default.conf`) yang meneruskan permintaan ke backend Node.js.

---

## Daftar Isi

- [Struktur Repositori](#struktur-repositori)
- [Topologi & Arsitektur Jaringan](#topologi--arsitektur-jaringan)
- [Fitur Utama & Konfigurasi](#fitur-utama--konfigurasi)
- [Pemenuhan Kriteria Penilaian (Bintang 5)](#pemenuhan-kriteria-penilaian-bintang-5)
- [Instalasi dan Setup Lingkungan](#instalasi-dan-setup-lingkungan)
- [Panduan Menjalankan dan Pengujian Server](#panduan-menjalankan-dan-pengujian-server)
- [Ketentuan Berkas Submission](#ketentuan-berkas-submission)

---

## Struktur Repositori

```text
Dicoding-BelajarJaringanKomputerUntukPemula/
├── .gitignore                         # Konfigurasi pengabaian Git (node_modules)
├── README.md                          # Dokumentasi lengkap proyek web server
├── package.json                       # Konfigurasi npm dependensi (Express)
├── package-lock.json                  # Catatan versi dependensi npm
├── app.js                             # Kode server Node.js dengan endpoint '/' dan '/me'
├── konfigurasiNGINX_abiyamf.txt       # Salinan konfigurasi /etc/nginx/sites-available/default
├── konfigurasiApache2_abiyamf.txt     # Salinan konfigurasi /etc/apache2/sites-available/000-default.conf
├── ports_abiyamf.txt                  # Salinan konfigurasi /etc/apache2/ports.conf (Port 3000)
├── submission_abiyamf.zip             # Arsip berkas submission siap submit ke Dicoding
├── submission_abiyamf/                # Folder berisi kumpulan berkas teks submission
│   ├── app.js
│   ├── konfigurasiApache2_abiyamf.txt
│   ├── konfigurasiNGINX_abiyamf.txt
│   └── ports_abiyamf.txt
└── ai-agent/                          # Panduan dan referensi modul submission
    ├── instruksi_submission.md        # Panduan terstruktur submission (4 bagian)
    └── README.md                      # Contoh struktur acuan dokumentasi
```

---

## Topologi & Arsitektur Jaringan

```mermaid
flowchart TD
    Client([Klien / Web Browser / cURL])

    subgraph ReverseProxyLayer ["Reverse Proxy Server (Port 3000)"]
        direction TB
        NGINX["NGINX Reverse Proxy\n- Listen: Port 3000\n- Rate Limit: 6 req/min (1 req / 10s)\n- Buffer Zone: 10MB"]
        APACHE["Apache2 Reverse Proxy\n- Listen: Port 3000\n- Modul: proxy & proxy_http\n- ProxyPreserveHost On"]
    end

    subgraph BackendLayer ["Backend Application Server (Port 8000)"]
        NodeApp["Node.js Express Server\n- Listen: 0.0.0.0:8000\n- GET / -> 'Hello world!'\n- GET /me -> 'abiyamf'"]
    end

    Client -->|HTTP Request: localhost:3000/| NGINX
    Client -.->|HTTP Request (Alternatif): localhost:3000/| APACHE
    NGINX -->|proxy_pass http://localhost:8000| NodeApp
    APACHE -.->|ProxyPass http://localhost:8000/| NodeApp
    NodeApp -->|Response Data| NGINX
    NodeApp -.->|Response Data| APACHE
    NGINX -->|HTTP Response / 503 if Rate Exceeded| Client
    APACHE -.->|HTTP Response| Client
```

---

## Fitur Utama & Konfigurasi

### 1. Reverse Proxy NGINX & Port Custom (3000)
Konfigurasi NGINX diarahkan untuk mendengarkan port 3000 dan meneruskan setiap permintaan ke aplikasi backend di port 8000:
- Berkas: `/etc/nginx/sites-available/default`
- Direktif: `listen 3000;` dan `proxy_pass http://localhost:8000;`

### 2. Rate Limiting (6 Request / Menit)
Proteksi server dari pemanggilan berlebihan diterapkan dengan algoritma *leaky bucket*:
- Zona memori: `limit_req_zone $binary_remote_addr zone=one:10m rate=6r/m;`
- Penerapan pada lokasi root: `limit_req zone=one;`
- Menjamin setiap klien dibatasi rata-rata 1 permintaan setiap 10 detik. Jika permintaan dikirimkan terlalu rapat, NGINX akan merespons dengan status `503 Service Temporarily Unavailable`.

### 3. Route Dinamis `/me` di Backend Express
Aplikasi Express memiliki 2 rute aktif:
- `GET /` : Menghasilkan respons teks `Hello world!\n`.
- `GET /me`: Menghasilkan respons teks username `abiyamf\n`.

### 4. Implementasi Redundansi Reverse Proxy Apache2
Apache2 dikonfigurasi dengan arsitektur serupa untuk memenuhi saran bintang 5:
- Berkas `/etc/apache2/ports.conf`: `Listen 3000`
- Berkas `/etc/apache2/sites-available/000-default.conf`:
  - `<VirtualHost *:3000>`
  - `ProxyPreserveHost On`
  - `ProxyPass / http://localhost:8000/`
  - `ProxyPassReverse / http://localhost:8000/`

---

## Pemenuhan Kriteria Penilaian (Bintang 5)

| Kriteria / Saran | Deskripsi Kriteria | Implementasi pada Proyek | Status |
| :--- | :--- | :--- | :---: |
| **Kriteria Wajib 1** | Menyiapkan Web Server (clone repo dicoding, pasang NGINX, pastikan Node.js & NGINX aktif). | Dependensi Express terpasang, NGINX terpasang pada WSL Ubuntu, server Node.js dan NGINX teruji berjalan normal. | **Terpenuhi** |
| **Kriteria Wajib 2** | Mengonfigurasi NGINX sebagai Reverse Proxy Server. | Konfigurasi `proxy_pass http://localhost:8000;` diterapkan pada `location /` di file default NGINX. | **Terpenuhi** |
| **Kriteria Wajib 3** | Menerapkan Limit Access (Rate Limit) di NGINX. | Menerapkan modul `limit_req_zone` dan `limit_req` untuk membatasi traffic masuk klien. | **Terpenuhi** |
| **Saran 1 (Bintang 5)** | Mengubah port NGINX dari 80 ke 3000. | Blok `server` di `/etc/nginx/sites-available/default` diatur ke `listen 3000 default_server;`. | **Terpenuhi** |
| **Saran 2 (Bintang 5)** | Mengubah konfigurasi rate limit menjadi 6 request per menit (1 request / 10 detik). | Zona rate limit diatur dengan parameter `rate=6r/m` (`limit_req_zone $binary_remote_addr zone=one:10m rate=6r/m;`). | **Terpenuhi** |
| **Saran 3 (Bintang 5)** | Menambahkan route baru `GET /me` yang mengembalikan teks username Dicoding di `app.js`. | Route `app.get('/me', ...)` ditambahkan pada `app.js` mengembalikan nilai `abiyamf\n`. | **Terpenuhi** |
| **Saran 4 (Bintang 5)** | Mengimplementasikan konfigurasi yang sama pada Apache2. | Apache2 diaktifkan modul `proxy` & `proxy_http`, mendengarkan port 3000 (`ports.conf`), dan mem-proxy ke port 8000 (`000-default.conf`). | **Terpenuhi** |

---

## Instalasi dan Setup Lingkungan

### 1. Kebutuhan Sistem
- Sistem Operasi: Windows 10/11 dengan **WSL 2 (Ubuntu 22.04 / 24.04)** atau Linux / macOS.
- **Node.js**: Versi 18+ (minimal v14.15.4 sesuai petunjuk).
- **Web Server**: NGINX dan Apache2.

### 2. Pemasangan Paket di Lingkungan WSL / Linux

```bash
# Update repository paket
sudo apt-get update

# Pasang NGINX, Apache2, Node.js, dan NPM
sudo apt-get install -y nginx apache2 nodejs npm
```

### 3. Pasang Dependensi Node.js

```bash
npm install
```

---

## Panduan Menjalankan dan Pengujian Server

### 1. Menjalankan Backend Node.js

Jalankan server aplikasi pada terminal:

```bash
npm start
```

Output:
```text
Running on http://0.0.0.0:8000
```

Uji akses langsung backend:
```bash
curl http://localhost:8000/
# Output: Hello world!

curl http://localhost:8000/me
# Output: abiyamf
```

---

### 2. Menjalankan & Menguji NGINX Reverse Proxy

Pastikan berkas `/etc/nginx/sites-available/default` berisi konfigurasi `konfigurasiNGINX_abiyamf.txt`.

Aktifkan service NGINX:
```bash
# Hentikan Apache2 jika sedang berjalan agar tidak bentrok port
sudo service apache2 stop

# Uji sintaks konfigurasi NGINX
sudo nginx -t

# Jalankan / restart NGINX
sudo service nginx restart
```

#### A. Uji Reverse Proxy (Port 3000)
```bash
curl -i http://localhost:3000/
```
Respons:
```http
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
Content-Type: text/html; charset=utf-8
Content-Length: 13
Connection: keep-alive
X-Powered-By: Express

Hello world!
```

#### B. Uji Endpoint `/me` (Port 3000)
```bash
curl -i http://localhost:3000/me
```
Respons:
```http
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
Content-Type: text/html; charset=utf-8
Content-Length: 8
Connection: keep-alive
X-Powered-By: Express

abiyamf
```

#### C. Uji Rate Limiting (6 Request / Menit)
Kirim request beruntun tanpa jeda 10 detik:
```bash
curl -i http://localhost:3000/
curl -i http://localhost:3000/
```
Respons pada request kedua yang melebihi kuota 1 req / 10s:
```http
HTTP/1.1 503 Service Temporarily Unavailable
Server: nginx/1.24.0 (Ubuntu)
Content-Type: text/html
Content-Length: 206
Connection: keep-alive

<html>
<head><title>503 Service Temporarily Unavailable</title></head>
...
```

---

### 3. Menjalankan & Menguji Apache2 Reverse Proxy

Pastikan modul proxy telah diaktifkan, dan berkas `konfigurasiApache2_abiyamf.txt` serta `ports_abiyamf.txt` telah disalin ke `/etc/apache2/sites-available/000-default.conf` dan `/etc/apache2/ports.conf`.

```bash
# Aktifkan modul proxy Apache2
sudo a2enmod proxy proxy_http

# Hentikan NGINX terlebih dahulu karena keduanya menggunakan port 3000
sudo service nginx stop

# Uji sintaks Apache2
sudo apachectl configtest

# Restart Apache2
sudo service apache2 restart
```

#### Uji Reverse Proxy Apache2 (Port 3000):
```bash
curl -i http://localhost:3000/
# Output: HTTP/1.1 200 OK -> Hello world!

curl -i http://localhost:3000/me
# Output: HTTP/1.1 200 OK -> abiyamf
```

---

## Ketentuan Berkas Submission

Sesuai ketentuan pengiriman proyek Dicoding untuk penilaian Bintang 5:

1. **`konfigurasiNGINX_abiyamf.txt`**: Konfigurasi lengkap NGINX di `/etc/nginx/sites-available/default` mencakup *listen 3000*, *rate limit 6r/m*, dan *proxy_pass* ke backend port 8000.
2. **`konfigurasiApache2_abiyamf.txt`**: Konfigurasi lengkap Apache2 di `/etc/apache2/sites-available/000-default.conf` mencakup `<VirtualHost *:3000>` dan *ProxyPass* ke backend port 8000.
3. **`ports_abiyamf.txt`**: Konfigurasi `/etc/apache2/ports.conf` dengan arahan `Listen 3000`.
4. **`app.js`**: Kode sumber web server Express yang telah ditambahkan route `GET /me` dengan respons username `abiyamf`.
5. **`submission_abiyamf.zip`**: Arsip ZIP siap unggah yang berisi langsung keempat berkas di atas tanpa adanya struktur "ZIP di dalam ZIP".

### Catatan untuk Tim Reviewer Dicoding:
> *Catatan dapat disalin langsung pada kolom Catatan Submission di dashboard Dicoding:*
>
> **Catatan Pengiriman Proyek:**  
> Submission ini telah menerapkan seluruh kriteria wajib serta seluruh saran pengembangan untuk meraih **Bintang 5**, yaitu:  
> 1. Mengubah port NGINX dari 80 ke 3000.  
> 2. Menerapkan konfigurasi rate limit 6 request per menit (1 request per 10 detik).  
> 3. Menambahkan route baru `GET /me` pada `app.js` yang mengembalikan teks username Dicoding (`abiyamf`).  
> 4. Mengimplementasikan konfigurasi yang sama pada **Apache2** sebagai reverse proxy alternatif pada port 3000 (`konfigurasiApache2_abiyamf.txt` dan `ports_abiyamf.txt`).  
> Keduanya (NGINX dan Apache2) telah diuji dan berfungsi dengan baik di lingkungan WSL Ubuntu. Terima kasih atas ulasannya!

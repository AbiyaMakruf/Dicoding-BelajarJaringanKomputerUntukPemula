# Instruksi Submission: Proyek Membangun Web Server

Dokumen ini berisi panduan dan instruksi lengkap pengerjaan submission akhir untuk kelas **Belajar Jaringan Komputer untuk Pemula**.

---

## 1. Pengantar

Selamat! Akhirnya Anda telah sampai di penghujung pembelajaran. Sejauh ini Anda sudah mempelajari berbagai topik mengenai jaringan komputer selama di kelas ini, di antaranya:
- Dasar-Dasar Jaringan Komputer
- Model Jaringan
- IP Address
- Domain Name System (DNS)
- Keamanan Jaringan
- Layanan Jaringan di AWS

Tentu Anda juga sudah mengerjakan seluruh latihan yang diberikan pada materi tersebut.

Untuk dapat lulus dari kelas ini, Anda harus mengerjakan tugas, yakni **membangun web server** sesuai kriteria yang ditentukan. Kemudian, Tim Reviewer akan memeriksa pekerjaan Anda serta memberikan review pada proyek yang Anda buat.

Pada modul *Layanan Jaringan di AWS*, Anda sudah mampu membangun web server dengan EC2 instance dan mengimplementasikan banyak hal di sana. Nah, kali ini Anda diminta untuk melakukan hal yang serupa, bedanya kini diimplementasikan pada **komputer pribadi Anda sendiri**. Jadi, Anda tidak wajib membuat kartu kredit/debit untuk daftar AWS.

- Bagi pengguna **Windows**, Anda dapat mengerjakan proyek akhir ini di **WSL dengan OS Ubuntu** seperti yang sudah dilakukan di beberapa modul sebelumnya.
- Bagi pengguna **Linux** atau **macOS**, Anda dapat mengerjakan langsung di aplikasi Terminal.

---

## 2. Kriteria

Terdapat **3 kriteria utama** yang harus dipenuhi dalam mengerjakan proyek akhir ini untuk lulus dari kelas:

### Kriteria 1: Menyiapkan Web Server
Langkah pertama yang perlu dilakukan dalam membangun web server adalah melakukan persiapan:
1. Melakukan cloning dari repositori GitHub yang sudah disediakan oleh Dicoding:  
   `https://github.com/dicodingacademy/a387-jarkom-labs.git`
2. Memasang NGINX di sistem operasi Anda.
3. Memastikan web server Node.js dan NGINX sama-sama bisa diakses dengan baik di browser/curl.

### Kriteria 2: Mengonfigurasi NGINX sebagai Reverse Proxy Server
Setelah Kriteria 1 berhasil dikerjakan:
1. Konfigurasikan NGINX yang sudah terinstal agar berfungsi sebagai **reverse proxy server**.
2. Hal ini bertujuan agar saat NGINX diakses melalui port web server NGINX, permintaan (*request*) dapat diteruskan ke web server backend (Node.js).

### Kriteria 3: Menerapkan Limit Access di NGINX
Setelah Kriteria 2 berhasil dikerjakan:
1. Konfigurasikan NGINX (*reverse proxy server*) untuk menerapkan **limit access** (*rate limit*) guna meningkatkan keamanan pada web server.
2. Untuk kriteria ini, Anda dapat menggunakan konfigurasi yang serupa dengan latihan di modul sebelumnya.

---

## 3. Penilaian

Submission Anda akan dinilai oleh Reviewer guna menentukan kebenaran submission yang dikerjakan. Supaya bisa lulus dari kelas ini, proyek web server Anda mesti memenuhi seluruh kriteria yang ada. Apabila ada ketentuan dalam kriteria yang belum terpenuhi, proyek akhir Anda akan ditolak.

Submission dinilai dengan skala bintang **1 - 5**. Untuk mendapatkan nilai tertinggi (**Bintang 5**), terapkan semua saran pengembangan berikut:

### Saran untuk Nilai Maksimal (Bintang 5)
1. **Mengubah port NGINX dari 80 ke 3000** (bukan port web server Node.js).
2. **Mengubah konfigurasi rate limit menjadi 6 request per menit** alias 1 request setiap 10 detik (`rate=6r/m`).
3. **Menambahkan route baru untuk endpoint `/me` dengan method GET** yang mengembalikan teks username Dicoding di berkas `app.js` (tidak perlu mengubah response di endpoint root `/`).
   - Contoh:
     - Request: `http://localhost:<port>/me`
     - Response: `<dicoding_username>`
4. **Mengimplementasikan konfigurasi yang sama pada Apache2** (sebagai reverse proxy alternatif/tambahan).

### Skala Penilaian Bintang
- **⭐ Bintang 1:** Semua ketentuan wajib terpenuhi, tetapi terdapat indikasi kecurangan dalam mengerjakan submission.
- **⭐⭐ Bintang 2:** Semua ketentuan wajib terpenuhi, tetapi berkas konfigurasi tidak rapi (spasi atau enter tidak sedap dipandang).
- **⭐⭐⭐ Bintang 3:** Semua ketentuan wajib terpenuhi, tetapi tidak menerapkan saran sama sekali.
- **⭐⭐⭐⭐ Bintang 4:** Semua ketentuan wajib terpenuhi dan menerapkan minimal 3 saran di atas.
- **⭐⭐⭐⭐⭐ Bintang 5:** Semua ketentuan wajib terpenuhi dan menerapkan **semua saran** di atas.

> **Catatan:** Jika submission Anda ditolak maka tidak ada penilaian. Kriteria penilaian bintang di atas hanya berlaku jika submission Anda lulus.

---

## 4. Lainnya

### Tips Pengerjaan
1. **Node.js & NPM:** Karena kode web server hasil clone memerlukan Node.js, pastikan Node.js dan NPM terinstal (dapat menggunakan NVM). Versi minimal Node.js adalah **v14.15.4**.
2. **Port Web Server Node.js:** Perhatikan port yang digunakan oleh Express pada berkas `app.js` (default: port 8000). Akses via `http://localhost:<port>/`.
3. **Penanganan Systemctl pada WSL:** Bila menemui pesan error `"System has not been booted with systemd as init system"`, gunakan perintah `service`. Contoh: `sudo service nginx status` atau `sudo service nginx restart`.
4. **Konflik Port 80 NGINX & Apache2:** Jika setelah memasang NGINX yang muncul adalah Apache2 Default Page, hentikan Apache2 dengan `sudo service apache2 stop`. Jika perlu hapus file default atau ganti nama file index (`mv /var/www/html/index.html /var/www/html/index.html_bkp`).
5. **Navigasi Terminal:** Gunakan `cd ..` untuk kembali ke folder sebelumnya.
6. **Melihat Username Akun Dicoding:**
   - Di navigasi atas Dicoding, klik foto profil > menu **Pengaturan**.
   - Salin teks pada kolom **Username** (misal: `abiyamf`).

### Ketentuan Berkas Submission
- **Bila menerapkan seluruh saran (NGINX + Apache2):**
  1. Salin konfigurasi NGINX pada `/etc/nginx/sites-available/default`, simpan sebagai `konfigurasiNGINX_<namaAnda>.txt`.
  2. Salin konfigurasi Apache2 pada `/etc/apache2/sites-available/000-default.conf`, simpan sebagai `konfigurasiApache2_<namaAnda>.txt`.
  3. Salin konfigurasi port Apache2 pada `/etc/apache2/ports.conf` (apabila menerapkan saran ubah port), simpan sebagai `ports_<namaAnda>.txt`.
  4. Lampirkan berkas `app.js` yang sudah diperbarui dengan route `/me`.
  5. Pada Apache2, tidak wajib menerapkan rate limit. Selain itu, tetap kerjakan sesuai kriteria.
- **Format Pengiriman:**
  - Seluruh berkas tersebut dimasukkan ke dalam satu folder, lalu dikompresi ke dalam bentuk **ZIP** (contoh: `submission.zip`).
  - **PENTING:** Pastikan tidak ada "ZIP di dalam ZIP".
  - Tuliskan pada kolom **Catatan Submission** bahwa Anda menggunakan NGINX dan Apache2 guna memudahkan proses review.

### Kriteria Penolakan Submission
Submission akan ditolak jika:
- Kriteria wajib tidak terpenuhi.
- Ketentuan berkas submission tidak terpenuhi.
- Berkas `.txt` tidak bisa dibuka, rusak, atau isinya sangat berantakan.
- Terdapat indikasi plagiasi atau kecurangan.

### Forum Diskusi
Jika mengalami kendala teknis atau pertanyaan, gunakan forum diskusi Dicoding:  
`https://www.dicoding.com/academies/387/discussions`

### Ketentuan Proses Review
- Tim Reviewer akan memeriksa submission dalam waktu maksimal 3 (tiga) hari kerja (tidak termasuk Sabtu, Minggu, dan hari libur nasional).
- Hindari melakukan submit berulang kali saat masih dalam antrean review.
- Hasil review akan diberitahukan melalui email serta halaman submission Dicoding.
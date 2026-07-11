# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel® Core™ i5-8250U @ 1.60 GHz 
  RAM     : 8 GB
  GPU     : Intel® UHD Graphics 620 
  Storage : TOSHIBA KSG60ZMV256G M.2 2280 SSD 256 GB
Software:
  OS        : Microsoft Windows 11 Pro Version 25H2 (Build 10.0.26200.8655)
  Runtime   : PHP 8.2.12
  Framework : Tidak menggunakan framework (PHP Native)


Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| PHP     | 8.2.12  | XAMPP  |       -       |
| Apache  | 2.4.58  | XAMPP  |       -       |
| MariaDB | 10.4.32 | XAMPP  |       -       |
| HTML    | HTML5   | W3C    |       -       |
| CSS     | CSS3    | W3C    |       -       |
| JavaScript | ECMAScript  | ECMA  |       -       |

Konfigurasi:
  Config file     : config/koneksi.php
  Random seed     : Tidak digunakan
  Hyperparameters : Tidak ada

Reproducibility Check:
  [X] Dependency terdokumentasi melalui spesifikasi environment
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [X] Config di version control (GitHub)
  [X] README awal telah disusun
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Intel® Core™ i5-8250U @ 1.60 GHz |
| RAM | 8 GB |
| GPU | Intel® UHD Graphics 620 |
| OS | Microsoft Windows 11 Pro Version 25H2 |
| Runtime | PHP 8.2.12 |
| Framework | PHP Native |
| Random Seed | Tidak digunakan |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| PHP | 8.2.12 | Menjalankan aplikasi web |
| Apache | 2.4.58 | Web server |
| MariaDB | 10.4.32 | Penyimpanan data arsip |
| HTML5 | HTML5 | Struktur halaman web |
| CSS3 | CSS3 | Tampilan antarmuka |
| JavaScript | ECMAScript | Interaksi sederhana pada halaman web |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | Tidak digunakan | Waktu pencarian dokumen | Belum dilakukan |
| 2 | Tidak digunakan | Waktu pencarian dokumen | Belum dilakukan |
| 3 | Tidak digunakan | Waktu pencarian dokumen | Belum dilakukan |

**Jika hasil berbeda, kemungkinan penyebab:**
Karena eksperimen belum dilaksanakan, belum dapat diketahui apakah terdapat perbedaan hasil antar-run. Secara teoritis, perbedaan waktu dapat disebabkan oleh beban komputer, proses di latar belakang, maupun koneksi database yang berubah selama pengujian.

**Checklist kontrol yang sudah diterapkan:**
- [ ] Random seed di-set di semua level
- [ ] Tidak ada background process yang mengganggu
- [ ] Cache dibersihkan antar-run
- [ ] Config file yang sama digunakan untuk semua run
---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Perbandingan Waktu Pencarian Dokumen Menggunakan Sistem Pengarsipan Manual dan Sistem Informasi Pengarsipan Digital Berbasis Web

## 1. Environment
CPU       : Intel® Core™ i5-8250U @ 1.60 GHz
RAM       : 8 GB
GPU       : Intel® UHD Graphics 620
OS        : Windows 11 Pro Version 25H2
Runtime   : PHP 8.2.12
Database  : MariaDB 10.4.32
Web Server: Apache 2.4.58

## 2. Installation
1. Install XAMPP.
2. Jalankan Apache dan MySQL.
3. Salin folder proyek ke direktori htdocs.
4. Import database ke phpMyAdmin.
5. Buka aplikasi melalui browser.

## 3. Data
Data berupa dokumen akademik Program Studi Sistem Informasi, seperti surat, laporan, dan arsip administrasi yang digunakan sebagai objek pengujian waktu pencarian dokumen.

## 4. Execution
1. Jalankan Apache dan MySQL.
2. Buka aplikasi melalui browser.
3. Lakukan pengujian pencarian dokumen pada sistem manual dan sistem informasi pengarsipan digital setelah implementasi selesai.
4. Catat waktu pencarian pada setiap percobaan.

## 5. Configuration
- File konfigurasi: `config/koneksi.php`
- Parameter utama:
  - Host : localhost
  - Database : database sistem pengarsipan
  - User : root
  - Password : disesuaikan dengan konfigurasi database

## 6. Expected Output
Output berupa waktu pencarian dokumen (dalam detik) pada sistem manual dan sistem pengarsipan digital. Hasil pengukuran kemudian dibandingkan untuk mengetahui apakah sistem pengarsipan digital mampu menurunkan waktu pencarian dokumen dibandingkan sistem manual.

```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [ ] Repeatability / [ ] Reproducibility / [X] Belum keduanya
**Komponen yang belum terdokumentasi:**
> # WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel® Core™ i5-8250U @ 1.60 GHz 
  RAM     : 8 GB
  GPU     : Intel® UHD Graphics 620 
  Storage : TOSHIBA KSG60ZMV256G M.2 2280 SSD 256 GB
Software:
  OS        : Microsoft Windows 11 Pro Version 25H2 (Build 10.0.26200.8655)
  Runtime   : PHP 8.2.12
  Framework : Tidak menggunakan framework (PHP Native)


Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| PHP     | 8.2.12  | XAMPP  |       -       |
| Apache  | 2.4.58  | XAMPP  |       -       |
| MariaDB | 10.4.32 | XAMPP  |       -       |
| HTML    | HTML5   | W3C    |       -       |
| CSS     | CSS3    | W3C    |       -       |
| JavaScript | ECMAScript  | ECMA  |       -       |

Konfigurasi:
  Config file     : config/koneksi.php
  Random seed     : Tidak digunakan
  Hyperparameters : Tidak ada

Reproducibility Check:
  [X] Dependency terdokumentasi melalui spesifikasi environment
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [X] Config di version control (GitHub)
  [X] README awal telah disusun
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Intel® Core™ i5-8250U @ 1.60 GHz |
| RAM | 8 GB |
| GPU | Intel® UHD Graphics 620 |
| OS | Microsoft Windows 11 Pro Version 25H2 |
| Runtime | PHP 8.2.12 |
| Framework | PHP Native |
| Random Seed | Tidak digunakan |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| PHP | 8.2.12 | Menjalankan aplikasi web |
| Apache | 2.4.58 | Web server |
| MariaDB | 10.4.32 | Penyimpanan data arsip |
| HTML5 | HTML5 | Struktur halaman web |
| CSS3 | CSS3 | Tampilan antarmuka |
| JavaScript | ECMAScript | Interaksi sederhana pada halaman web |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | Tidak digunakan | Waktu pencarian dokumen | Belum dilakukan |
| 2 | Tidak digunakan | Waktu pencarian dokumen | Belum dilakukan |
| 3 | Tidak digunakan | Waktu pencarian dokumen | Belum dilakukan |

**Jika hasil berbeda, kemungkinan penyebab:**
Karena eksperimen belum dilaksanakan, belum dapat diketahui apakah terdapat perbedaan hasil antar-run. Secara teoritis, perbedaan waktu dapat disebabkan oleh beban komputer, proses di latar belakang, maupun koneksi database yang berubah selama pengujian.

**Checklist kontrol yang sudah diterapkan:**
- [ ] Random seed di-set di semua level
- [ ] Tidak ada background process yang mengganggu
- [ ] Cache dibersihkan antar-run
- [ ] Config file yang sama digunakan untuk semua run
---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Perbandingan Waktu Pencarian Dokumen Menggunakan Sistem Pengarsipan Manual dan Sistem Informasi Pengarsipan Digital Berbasis Web

## 1. Environment
CPU       : Intel® Core™ i5-8250U @ 1.60 GHz
RAM       : 8 GB
GPU       : Intel® UHD Graphics 620
OS        : Windows 11 Pro Version 25H2
Runtime   : PHP 8.2.12
Database  : MariaDB 10.4.32
Web Server: Apache 2.4.58

## 2. Installation
1. Install XAMPP.
2. Jalankan Apache dan MySQL.
3. Salin folder proyek ke direktori htdocs.
4. Import database ke phpMyAdmin.
5. Buka aplikasi melalui browser.

## 3. Data
Data berupa dokumen akademik Program Studi Sistem Informasi, seperti surat, laporan, dan arsip administrasi yang digunakan sebagai objek pengujian waktu pencarian dokumen.

## 4. Execution
1. Jalankan Apache dan MySQL.
2. Buka aplikasi melalui browser.
3. Lakukan pengujian pencarian dokumen pada sistem manual dan sistem informasi pengarsipan digital setelah implementasi selesai.
4. Catat waktu pencarian pada setiap percobaan.

## 5. Configuration
- File konfigurasi: `config/koneksi.php`
- Parameter utama:
  - Host : localhost
  - Database : database sistem pengarsipan
  - User : root
  - Password : disesuaikan dengan konfigurasi database

## 6. Expected Output
Output berupa waktu pencarian dokumen (dalam detik) pada sistem manual dan sistem pengarsipan digital. Hasil pengukuran kemudian dibandingkan untuk mengetahui apakah sistem pengarsipan digital mampu menurunkan waktu pencarian dokumen dibandingkan sistem manual.

```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [ ] Repeatability / [ ] Reproducibility / [X] Belum keduanya
**Komponen yang belum terdokumentasi:**
> README telah disusun sebagai rancangan awal, namun implementasi sistem dan eksperimen belum dilakukan. Oleh karena itu dokumentasi hasil pengujian, struktur proyek, konfigurasi database, serta panduan reproduksi secara lengkap masih perlu disusun agar penelitian dapat direproduksi oleh peneliti lain.

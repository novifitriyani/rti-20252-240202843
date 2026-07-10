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
  Framework : PHP Native


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
  [X] Dependency terdokumentasi (requirements.txt / lock file)
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [X] Config di version control
  [ ] README instruksi reproduksi lengkap
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
| 1 | Tidak digunakan | Waktu pencarian dokumen | — |
| 2 | Tidak digunakan | Waktu pencarian dokumen | [X] Ya / [ ] Tidak |
| 3 | Tidak digunakan | Waktu pencarian dokumen | [X] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum non-repeatability:
> - **Thermal throttling** — CPU/GPU overheating pada run berturut-turut → clock speed turun → waktu eksekusi berubah
> - **Background process** — antivirus scan, update OS, atau cloud sync aktif saat run berlangsung
> - **Cache dari run sebelumnya** — hasil tersimpan di memori/disk sehingga run berikutnya tidak menjalankan komputasi penuh
> - **Random state tidak dikontrol di semua level** — Python seed di-set, tapi NumPy/PyTorch/TensorFlow punya seed independen

Perbedaan waktu dapat disebabkan oleh beban komputer yang berbeda, proses lain yang berjalan di latar belakang, atau koneksi ke database yang tidak stabil. 

**Checklist kontrol yang sudah diterapkan:**
- [ ] Random seed di-set di semua level
- [ ] Tidak ada background process yang mengganggu
- [ ] Cache dibersihkan antar-run
- [ ] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: ____________________

## 1. Environment
> (Salin spesifikasi dari Latihan 1)

## 2. Installation
> (Langkah instalasi, misal: "pip install -r requirements.txt")

## 3. Data
> (Deskripsi data: sumber, format, ukuran)

## 4. Execution
> (Command untuk menjalankan eksperimen)

## 5. Configuration
> (File config yang digunakan + parameter kunci)

## 6. Expected Output
> (Contoh output yang diharapkan + format)
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [ ] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> ___________________________________________________

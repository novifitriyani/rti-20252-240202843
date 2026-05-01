# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Sistem Informasi 
  Konteks  : Pengelolaan arsip dokumen akademik pada Program Studi sistem Informasi yang masih dilakukan secara manual 

System Context
  Input       : Data dokumen akademik, surat, laporan, dan arsip administrasi
  Process     : Input data dokumen, penyimpanan data ke database, pencarian dan pengelolaan arsip secara digital
  Output      : Arsip digital yang tersimpan rapi dan dapat diakses dengan mudah
  Outcome     : Pengelolaan dokumen menjadi lebih efektif dan meminimalkan risiko kehilangan data
  Constraints : Keterbatasan infrastruktur teknologi, kemampuan pengguna, dan kualitas input data
  Stakeholders: Admin program studi, dosen, mahasiswa, dan staf akademik

Fenomena → Problem
  Fenomena yang diamati             : Pengelolaan arsip dokumen di Program Studi Informasi masih dilakukan secara manual.
  Gejala (symptom) yang terukur     : Proses pencarian dokumen membutuhkan waktu lama dan berisiko terjadi kehilangan atau kerusakan dokumen.
  Masalah yang didiagnosis          : Belum adanya sistem informasi terintegrasi untuk pengelolaan arsip digital.
  Masalah riset (researchable)      : Bagaimana merancang dan mengimplentasikan sistem informasipengarsipan digital yang dapat membantu pengelolaan dan pencarian dokumen secara lebih efektif
  Variabel yang terukur             : Kecepatan pencarian dokumen, ketersediaan dokumen, fungsionalitas sistem, dan kemudahan penggunaan sistem

Problem Quality Check
  [x] Clarity — Apakah satu orang membaca akan paham?
  [x] Measurability — Apakah ada metrik kuantitatif?
  [x] Relevance — Apakah penting untuk domain?
  [x] Testability — Apakah bisa gagal?
  [x] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Pengelolaan arsip pada Program Studi Sistem Informasi masih dilakukan secara manual sehingga menyebabkan proses pencarian dokumen menjadi lambat serta meningkatkan risiko kehilangan atau kerusakan dokumen. Kondisi ini menunjukkan perlunya sistem informasi pengarsipan digital yang mampu membantu pengelolaan dokumen secara lebih terstruktur dan efisien.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Sistem Informasi Pengarsipan Digital

| Tahap | Hasil |
|-------|-------|
| Reality | Penngelolaan arsip dokumen asih dilakukan secara manual |
| Observed Issue (Symptom) | Pencarian dokumen lambat dan dokumen berisiko hilang |
| Diagnosed Problem (Root Cause) | Tidak adanya sistem pengarsipan digital terintegrasi |
| Researchable Problem | Bagaimana merancang sistem informasi pengarsipan digital yang efektif |
| Measurable Variable | Kecepatan pencarian, ketersediaan dokumen, kemudahan penggunaan |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Data dokumen akademik dan administrasi |
| Process | Penyimpanan, pengelolaan, dan pencarian dokumen digital |
| Output | Dokumen digital yang mudah diakses |
| Outcome | Efektivitas pengelolaan dokumen meningkat |
| Constraints | Infrastruktur, kemampuan pengguna, kualitas data |
| Stakeholders | Admin, dosen, mahasiswa, staf akademik |

**Komponen mana yang paling relevan dengan masalah riset?** Process

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Masalah dijelaskan secara spesifik dan mudah dipahami |
| Measurability | 4 | Variabel dapat diukur melalui penngujian sistem |
| Relevance | 5 | Relevan dengan kebutuhan digitalisasi arsip |
| Testability | 4 | Sistem dapat diuji melalui implementasi dan pengujian fungsional |
| Impact | 5 | Memberikan manfaat pada efisiensi pengelolaan dokumen |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Pengelolaan arsip dokumen secara manual pada Program Studi Sistem Informasi masih menimbulkan kendala berupa lambatnya proses pencarian dokumen dan tingginya risiko kehilangan data. Untuk mengatasi permasalahan tersebut, diperlukan sistem informasi pengarsipan digital berbasis web yang mampu membantu penyimpanan, pengelolaan, dan pencarian dokumen secara lebih efektif, tersetruktur dan mudah diakses oleh pengguna.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah yang biasa ditemui saat coding umumnya berfokus pada error teknis atau bug agar sistem dapat berjalan dengan benar. Sementara itu, masalah riset berfokus pada identifikasi gap atau permaslahan yang membutuhkan analisis sistematis dan pembuktian ilmiah. Pendekatan coding lebih menekankan solusi langsung sedangkan riset menuntut proses observasi, analisis, pengujian, dan validasi hasil.

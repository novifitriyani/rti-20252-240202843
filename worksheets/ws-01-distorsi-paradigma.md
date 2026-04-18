# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Novi Fitriyani
Tanggal          : 18 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah nilai akurasi tersebut dihitung menggunakan metrik evaluasi yang tepat dan relevan dengan tujuan penelitian, serta apakah terdapat metode pembanding (baseline) yang digunakan untuk memastikan bahwa peningkatan performa tersebut benar-benar signifikan dan bukan disebabakan oleh bias data, overfitting, atau kondisi eksperimen yang terbatas?
   - Data yang dibutuhkan untuk verifikasi: Diperlukan informasi mengenai dataset yang digunakan (termasuk ukuran, distribusi, dan keseimbangan data), prosedur eksperimen (train-test split atau cross validation), serta hasil perbandiangan dengan metode lain untuk memastikan validitas klaim performa.

2. Posisi paradigma:
   - Pendekatan: [x] Positivis  [ ] Interpretivis  [x] Design Science  [ ] Mixed
   - Alasan: Penelitian menggunakan pendekatan Design Science karena berfokus pada pembangunan artefak berupa sistem informasi untuk menyelesaikan masalah pengarsipan manual. Selain itu, terdapat positivis karena penelitian mengandung klaim peningkatan efisiensi yang secara implisit memerlukan pengujian objektif berbasis data. 

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Penelitian mengasumsikan bahwa digitalisasi sistem pengarsipan secara otomatis akan meningkatkan efisiensi, kecepatan, dan keamanan tanpa mempertimangkan faktor lain seperti kualitas data input, kesiapan pengguna, serta kompleksitas sistem yang dapat mempengaruhi hasil.
   - Sumber bias potensial: Bias dapat muncul karena penggunaan data yang hanya berasal dari satu program studi sehingga tidak representatif, serta tidak adanya perbandingan dengan sistem lain yang dapat menyebabkan bias konfirmasi terhadap klaim peningkatan performa.
   - Langkah mitigasi: Diperlukan pengujian pada lebih dari satu instansi atau lingkungan yang berbeda, penggunanaan metrik kuantitatif yang jelas (misalnya waktu pencarian dokumen sebelum dan sesudah sistem), serta perbandingan dengan metode atau sistem lain agar hasil penelitian lebih objektif, valid, dan dapat direplikasi.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Seluruh data eksperimen, termasuk data yang menunjukkan hasil yang kurang baik atau tidak sesuai harapan, tetap dipertahankan tanpa penghapusan, pemilihan selektif, maupun perubahan untuk memperkuat hasil penelitian
   - Batasan yang diakui sejak awal: Penelitian memiliki keterbatasan pada skala data yang kecil, ruang lingkup yang komprehensif, sehingga hasil penelitian belum dapat digenerelisasi secara luas tanpa validasi tambahan.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Rancang Bangun Sistem Informasi Pengarsipan digital (Studi Kasus: Program Studi Informasi)
> Penulis (Tahun): Astuti Rani Kariam, Kristianus Jago tute, dan Melky Radja (2024)
> Sumber/Link DOI: https://ejournal.catursakti.ac.id/index.php/simtek/article/view/798 

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | *Contoh: Kumpulkan log server 30 hari* | *Contoh: Hanya ambil jam sibuk* |
| Data → Processing | | |
| Processing → Analysis | | |
| Analysis → Inference | | |
| Inference → Knowledge | | |

**Distorsi paling besar di tahap:** ________________________

**Dua distorsi spesifik yang teridentifikasi:**
1. ___________________________________________________
2. ___________________________________________________

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | *Contoh: Laporkan kedua versi (dengan dan tanpa outlier)* |
| Transparansi | |
| Peer review | |

**Keputusan akhir dan justifikasi:**
> ___________________________________________________

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** ________________________________________

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | *Contoh: 4 — topik kuantitatif, cocok uji hipotesis* | *Contoh: 2 — topik tidak studi makna/konteks* | *Contoh: 5 — membangun artefak untuk uji klaim* |
| Jenis data yang dikumpulkan | *Metrik numerik, log eksperimen* | *Wawancara, observasi kualitatif* | *Hasil uji artefak, komparasi kinerja* |
| Limitasi paradigma | | | |

**Paradigma yang dipilih:** _____________________________
**Alasan:** ____________________________________________

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> ___________________________________________________
> ___________________________________________________

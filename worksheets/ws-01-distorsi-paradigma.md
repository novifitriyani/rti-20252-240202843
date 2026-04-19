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
Tanggal          : 19 April 2026

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
| Reality → Data | Mengamati masalah pengarsipan manual di Program Studi Sistem Informasi yang menyebabkan kesulitan pencarian dan kehilangan dokumen | Data hanya berasal dari satu institusi → tidak mewakili kondisi umum (sampling bias) |
| Data → Processing | Data arsip dikonversi ke sistem digital menggunakan database (PHP & MySQL) | Kesalahan input data (human error) dan tidak ada validasi kualitas data |
| Processing → Analysis | Sistem diuji menggunakan metode black box testing untuk memastikan fungsi berjalan | Pengujian hanya fungsional, tidak mengukur performa nyata (tidak ada metrik kuantitatif seperti waktu/akurasi)  |
| Analysis → Inference | Disimpulkan bahwa sistem meningkatkan efisiensi, kecepatan, dan kemudahan pengarsipan | Klaim tidak didukung perbandingan dengan sistem lain (tidak ada baseline → weak interface) |
| Inference → Knowledge | Pengetahuan yang dihasilkan: sistem digital lebih efektif dibanding sistem manual | Generelisasi terlalu luas, padahal hanya diuji pada satu studi kasus (external validity rendah) |

**Distorsi paling besar di tahap:** Analysis → Interface

**Dua distorsi spesifik yang teridentifikasi:**
1. Tidak adanya baseline pembanding sehingga klaim peningkatan efisiensi tidak dapat diverifikasi secara objektif.
2. Samppling bias karena data hanya berasal dari satu instansi sehingga hasil tidak dapat digeneralissai.

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Seluruh data, termauk outlier, harus tetap dilaporkan karena merupakan representasi kondisi nyata. Menghapus outlier hanya untuk memperoleh haisl signifikan termasuk manipulasi data (falsification) dan melanggar prinsip integritas ilmiah. Outlier tidak selalu kesalahan, tetapi bisa merepresentasikan fenomena penting sehingga tidak boleh dihapus tanpa alasan metodologis yang kuat. |
| Transparansi | Peneliti wajib melaporkan kedua hasil, yaitu dengan dan tanpa outlier, serta menjelaskan alasan jika dilakukan penghapusan. Transparansi diperlukan agar pembaca dapat menilai sendiri dampak outlier terhadap hasil dan menghindari praktik memilih data yang mendukung kesimpulan tertentu. |
| Peer review | Dalam proses peer review, penghapusan data tanpa justifikasi akan dianggap sebagai bias atau manipulasi. Reviewer dapat mempertanyakan validitas hasil dan menolak penelitian karena dianggap tidak merepresentasikan data secara objektif. Praktik membuang data tanpa analisis juga termasuk kesalahan umum yang harus dihindari dalam analisis data. |

**Keputusan akhir dan justifikasi:**
> Seluruh data termasuk outlier harus tetap dilaporkan sebagai hasil utama penelitian. Analisis tanpa outlier dapat disajikan sebagai analisis tambahan dengan penjelasan metodologis yang jelas. Keputusan ini diambil untuk menjaga integritas ilmiah, menghindari manipulasi data, serta memastikan bahwa hasil penelitian merepresentasikan kondisi sebenarnya dan dapat dipercaya.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Sistem Informasi Pengarsipan Digital untuk Meningkatkan Efisiensi Pengelolaan Dokumen

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 4 — terdapat klaim peningkatan efisiensi yang dapat diuji secara kuantitatif | 2 — tidak berfokus pada makna atau persepsi pengguna secara mendalam | 5 — fokus utama adalah membangun sistem sebagai solusi |
| Jenis data yang dikumpulkan | Metrik kinerja sistem, waktu pencarian dokumen, efisiensi | wawancara pengguna, persepsi terhadap sistem | Hasil implementasi sistem, pengujian fungsional, evaluasi sistem |
| Limitasi paradigma | Membutuhkan data kuantitatif yang kuat, namun dalam penelitian ini metrik belum lengkap | Tidak cocok karena penelitian tidak mengeksplorasi makna sosial secara mendalam | Fokus pada artefak dapat mengabaikan validitas ilmiah jika tidak disertai evaluasi yang kuat |

**Paradigma yang dipilih:** Design Science Research (dengan dukungan Positivis)
**Alasan:** Penelitian berfokus pada pembangunan artefak berupa sistem informasi untuk menyelesaikan masalah nyata (ciri utama Design Science), namun juga mengandung klaim peningkatan efisiensi yang secara implisit memerlukan pengujian objektif berbasis data (unsur Positivis)

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum memahami konsep Reesearch Trust Model, klaim seperti "95% akurat" cenderung diterima tanpa analisis mendalam. Setelah memahami rantai distorsi, muncul kebutuhan untuk mempertanyakan bagaimana data dikumpulkan, apakah terdapat bias dalam dataset, metode evaluasi yang digunaakan, keberadaan pembanding (baseline), serta apakah metrik yang digunakan benar-benar sesuai dengan klaim yang disampaikan. Fokus tidak lagi pada hasil akhir, tetapi pada proses yang menhasilkan hasil tersebut. 

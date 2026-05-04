# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat meningkatkan efektivitas pencarian dan pengelolaan dokumen dibandingkan sistem manual pada Program Studi Informasi?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
| Metode pengelolaan arsip | IV | Pendekatan pengarsipan | Manual vs Digital | Nominal | - | Identifikasi jenis sistem yang digunakan | Membedakan perlakuan eksperimen |
| Efektivitas pencarian dokumen | DV | Efisiensi pengelolaan dokumen | Waktu pencarian dokumen | ratio | Menit | Mengukur lama waktu menemukan dokumen | Langsung merepresentasikan efisiensi |
| Jenis dokumen | CV   | Kompleksitas pencarian | Dokumen akademik/administrasi | Nominal |        | - | Mengelompokkan tipe dokumen | Mengontrol variasi hasil |

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [x] Setiap langkah terdokumentasi
  [x] Tidak ada "lompatan logis"
  [x] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat meningkatkan efektivitas pencarian dan pengelolaan dokumen dibandingkan sistem manual?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Metode pengelolaan arsip | IV | Pendekatan pengarsipan | Manual vs Digital | Nominal | — |
| Efektivitas pencarian dokumen | DV | Efisiensi pengelolaan | Lama waktu pencarian dokumen | Ratio | Menit |
| Jenis dokumen | CV | Variasi dokumen | Akademik vs Administrasi | Nominal | - |

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 | Waktu pencarian dokumen secara langsung mengukur efisiensi sistem |
| Sensitive | 4 | Perbedaan kecil waktu masih dapat diamati |
| Feasible | 5 | Data mudah dikumpulkan melalui simulasi pencarian dokumen |

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Kemudahan penggunaan sistem (user satisfaction) sebagai pendukung untuk melihat pengalaman pengguna selain efisiensi waktu.

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika seluruh pengguna dapat menemukan dokumen dalam waktu yang sangat cepat, maka perbedaan performa antar sistem menjadi sulit dibedakan.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | *Apakah semua data point terkumpul?* | Ya, seluruh percobaan dicatat | Checklist pengumpulan data |
| Consistency | *Apakah ada kontradiksi internal?* | Tidak | Standarisasi prosedur pengukuran |
| Validity | *Apakah benar-benar mengukur yang dimaksud?* | Ya, waktu pencarian merepresentasikan efisiensi | Menggunakan prosedur pengukuran yang sama |
| Representativeness | *Apakah sampel mewakili populasi target?* | Cukup mewakili dokumen akademik | Menggunakan berbagai tipe dokumen |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti dapat melihat hasil yang paling menguntungkan sehingga mengurangi objektivitas penelitian. Berbeda dengan eksplorasi data yang sah, yaitu analisis tambahan yang dilakukan setelah eksperimen namun dilaporkan secara transparan sebagai exploratory analysis. 

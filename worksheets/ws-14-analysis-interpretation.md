# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
   |----------|------|-----|--------|-----|-----|---|
   | Pencarian Manual (ms) | 8710.50 | 6230.62 | 6852.5* | 3640 | 25390 | 10 (rata-rata per kata kunci) |
   | Pencarian Sistem (ms) | 17.58 | 41.40 | 2.12* | 1.00 | 134.50 | 10 (rata-rata per kata kunci) |

   *median dihitung dari 10 nilai rata-rata per kata kunci yang dipasangkan

2. Uji Hipotesis:
   Uji yang digunakan  : Paired t-test dan Wilcoxon signed-rank test (dijalankan keduanya karena n kecil, Wilcoxon sebagai validasi non-parametrik)
   Justifikasi          : Data berpasangan (setiap kata kunci diukur dengan metode manual DAN sistem pada dokumen yang sama), 2 grup, n=10 pasangan — tergolong sampel kecil sehingga uji non-parametrik (Wilcoxon) digunakan sebagai pelengkap paired t-test untuk mengantisipasi pelanggaran asumsi normalitas
   Hasil: p = 0.00169 (paired t-test), p = 0.00195 (Wilcoxon), effect size (Cohen's d) = 1.395
   CI 95%               : selisih rata-rata manual-sistem = [4234.96, 13150.88] ms (dihitung dari distribusi t untuk data berpasangan) — karena rentang ini tidak melewati 0, memperkuat kesimpulan bahwa perbedaan bukan kebetulan

3. Keputusan:
   [x] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : RQ penelitian mempertanyakan apakah sistem informasi pengarsipan digital dapat mempercepat pencarian dokumen dibanding manual. Hasil uji (p<0.01, d=1.395) mendukung H₁: pencarian melalui sistem secara signifikan lebih cepat dibanding pencarian manual
   Practical significance: Selain signifikan secara statistik, selisihnya juga signifikan secara praktis: rata-rata pencarian manual makan waktu ±8.7 detik, sedangkan sistem hanya ±0.018 detik — percepatan sekitar 99.8%. Ini bukan sekadar perbedaan kecil yang "signifikan di atas kertas", tapi perbedaan yang akan benar-benar terasa oleh pengguna sehari-hari
   Perbandingan literatur: Hasil ini konsisten dengan premis umum di bidang sistem informasi bahwa pencarian berbasis indeks/database (dengan query terstruktur) jauh lebih efisien dibanding penelusuran linear manual pada arsip fisik/tidak terstruktur — sejalan dengan tujuan awal penelitian yang disebutkan di WS-01/WS-02 (mengganti proses pencarian manual yang lambat)

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   | Statistical | n hanya 10 pasangan (per kata kunci), bukan per dokumen individual | Power statistik terbatas, estimasi effect size bisa kurang stabil | Tambah jumlah kata kunci/dokumen uji pada replikasi berikutnya (idealnya n≥30) |
   | Internal validity | Peneliti yang sama menjalankan kedua metode (manual & sistem), berpotensi bias familiaritas (lebih hafal lokasi dokumen saat sesi kedua) | Durasi manual/sistem bisa under/overestimate | Acak urutan pengujian (manual dulu vs sistem dulu) pada sesi berikutnya, atau libatkan orang lain sebagai penguji manual |
   | Construct validity | Simulasi arsip manual (folder komputer) tidak 100% merepresentasikan arsip fisik kertas sungguhan | Waktu pencarian manual riil (fisik) bisa jadi berbeda (mungkin lebih lambat) dari simulasi ini | Disebutkan eksplisit sebagai keterbatasan simulasi di bab metode, bukan diklaim sebagai arsip fisik asli |
   | External validity | Data diuji oleh 1 orang (peneliti sendiri), bukan banyak pengguna | Hasil belum tentu representatif untuk pengguna umum dengan kemampuan/kebiasaan pencarian berbeda | Rekomendasi pengujian lanjutan dengan responden tambahan disebutkan sebagai future work

6. Failure Analysis (jika H₀ tidak ditolak):
   Tidak berlaku — H₀ ditolak (hasil signifikan mendukung hipotesis penelitian)
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 2 (Pencarian Manual vs Pencarian Sistem) |
| Apakah data berpasangan (paired)? | Ya — setiap kata kunci diuji dengan kedua metode (manual dan sistem) pada dokumen yang setara, sehingga tiap kata kunci punya sepasang nilai yang saling berhubungan |
| Apakah distribusi normal? (uji normalitas) | Tidak dapat dipastikan normal — n sampel kecil (10 pasangan) dan data durasi cenderung right-skewed (ada beberapa nilai jauh lebih tinggi dari yang lain, terutama pada data sistem yang punya outlier 134.5 ms untuk kata kunci "tugas") |
| **Uji yang dipilih:** | Paired t-test, divalidasi ulang dengan Wilcoxon signed-rank test (non-parametrik) |
| **Justifikasi:** | Karena data berpasangan dan n kecil dengan distribusi yang tidak pasti normal, paired t-test dipakai sebagai uji utama namun didampingi Wilcoxon sebagai pengecekan silang yang tidak mengasumsikan normalitas — kedua uji menghasilkan kesimpulan yang konsisten (p<0.01) sehingga hasil dianggap robust |

**Effect size yang akan dilaporkan:** [x] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

Menggunakan data riil dari eksperimen sendiri (bukan data contoh Model A/B):

**Data:**
| Skenario | Durasi (mean ± std, ms) | n |
|----------|-------------------------|---|
| Pencarian Manual | 8710.50 ± 6230.62 | 10 |
| Pencarian Sistem | 17.58 ± 41.40 | 10 |

p = 0.00169 (paired t-test), Cohen's d = 1.395, CI 95% selisih = [4234.96, 13150.88] ms

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | p = 0.00169 < 0.05 (bahkan < 0.01) → signifikan secara statistik, kemungkinan hasil ini terjadi karena kebetulan sangat kecil |
| Effect size | d = 1.395 → tergolong **Large** (>0.8), artinya perbedaan antara pencarian manual dan sistem bukan cuma signifikan secara statistik tapi juga besar secara magnitude |
| Practical significance | Selisih rata-rata ±8.7 detik per pencarian jelas terasa nyata bagi pengguna — pada skala penggunaan sehari-hari (misal staf yang mencari dokumen puluhan kali per hari), akumulasi waktu yang dihemat menjadi sangat signifikan secara praktis, bukan cuma "signifikan di atas kertas" |
| Hubungan ke RQ | Hasil ini menjawab langsung RQ penelitian: sistem informasi pengarsipan digital terbukti secara statistik mempercepat proses pencarian dokumen dibanding metode manual |
| Perbandingan literatur | Sejalan dengan premis umum bahwa pencarian terindeks (database dengan query LIKE/index) jauh mengungguli linear search manual pada koleksi dokumen yang tidak terstruktur — konsisten dengan justifikasi awal penelitian di WS-01/WS-02 |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Bukan gagal total — p=0.12 berarti hipotesis tidak terdukung secara statistik pada α=0.05, tapi ini tetap temuan yang sah dan bisa jadi kontribusi (menunjukkan metode baru tidak selalu lebih baik dari baseline) |
| Kemungkinan penyebab? | Selisih F1 hanya 1.5 poin (83.2 vs 84.7) — kemungkinan metode baru memang tidak memberikan peningkatan performa yang berarti pada skenario ini, atau ukuran sampel terlalu kecil untuk mendeteksi perbedaan sekecil itu (power statistik rendah) |
| Boundary condition? | Bisa jadi metode baru hanya unggul pada kondisi tertentu (misal dataset besar atau kasus yang lebih kompleks) yang tidak tercakup dalam skenario pengujian ini — perlu dicek apakah performa berbeda pada subset data yang berbeda |
| Insight yang bisa diambil? | Kalau metode baru punya kompleksitas/biaya komputasi lebih tinggi tapi hasilnya tidak berbeda signifikan dari baseline, ini justru insight penting: baseline yang lebih sederhana mungkin lebih efisien dipakai, kecuali metode baru punya keunggulan lain (misal interpretability atau kecepatan) di luar metrik F1 |
| Apakah layak dilaporkan? Mengapa? | Ya — hasil non-signifikan tetap layak dilaporkan apa adanya, bukan disembunyikan atau "dicari-cari" sudut lain sampai signifikan (p-hacking). Melaporkan hasil ini membantu peneliti lain tidak mengulang eksperimen yang serupa tanpa hasil berbeda |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Ukuran sampel tidak disebutkan secara eksplisit dalam skenario, kemungkinan kecil | Power test rendah, sulit mendeteksi efek kecil meskipun sebenarnya ada |
| Construct validity | F1-score sebagai satu-satunya metrik mungkin tidak menangkap seluruh aspek performa (mis. kecepatan, robustness) | Kesimpulan "tidak ada perbedaan" bisa jadi hanya berlaku untuk metrik F1, bukan performa keseluruhan |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Sebelum mengerjakan worksheet ini, saya cenderung menganggap "failure" (hipotesis tidak terdukung) sebagai kegagalan penelitian yang harus dihindari atau ditutupi. Tapi dari Latihan 3, saya sadar bahwa hasil non-signifikan yang dilaporkan jujur dan dianalisis mendalam (kenapa tidak signifikan, boundary condition apa yang mungkin berlaku) justru lebih bernilai dibanding hasil signifikan tanpa analisis lanjutan sama sekali.
>
> Ini juga membuat saya lebih hati-hati menilai hasil penelitian saya sendiri — meskipun hasil saya kebetulan signifikan (p=0.00169, d=1.395 untuk perbandingan manual vs sistem), saya tetap perlu melaporkan keterbatasannya secara jujur (n kecil, potensi bias familiaritas, simulasi arsip yang belum 100% merepresentasikan kondisi fisik) daripada hanya menonjolkan angka p-value yang kecil. Failure analysis mengajarkan saya bahwa kredibilitas penelitian bukan ditentukan oleh "berhasil atau gagal", tapi oleh seberapa jujur dan mendalam proses analisisnya — baik hasilnya mendukung hipotesis maupun tidak.

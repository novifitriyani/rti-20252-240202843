# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat menurunkan waktu pencarian dokumen dibandingkan sistem manual pada dokumen akademik Program Studi Sistem Informasi?
Hypothesis        :
- H₀: Tidak terdapat perbedaan signifikan waktu pencarian dokumen antara sistem manual dan sistem pengarsipan digital
- H₁: Terdapat penurunan waktu pencarian dokumen pada sistem pengarsipan digital dibandingkan sistem manual
Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Sistem manual pengarsipan | Manual | Dataset dokumen akademik sama, jumlah & jenis sama, seed/urutan sama |
| Treatment | Sistem informasi pengarsipan digital berbasis web | Digital | Dataset dokumen akademik sama, preprocessing sama, lingkungan pengujian sama |

Fairness Checklist:
  [x] Dataset identik 
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    | User familiarity (bias karena sudah terbiasa dengan sistem digital) | Gunakan prosedur uji berulang dan randomisasi urutan pengujian |
| External    | Dataset hanya dari satu program studi | Perluasan dataset ke instansi lain jika penelitian lanjutan |
| Construct   | Waktu pencarian tidak sepenuhnya merepresentasikan “efisiensi” | Tambahkan metrik pendukung seperti success rate pencarian |
| Conclusion  | Jumlah sampel terlalu kecil | Gunakan repeated trials (beberapa kali percobaan) |

Statistical Plan:
  Uji statistik   : Paired t-test
  Justifikasi      : Membandingkan dua kondisi (manual vs digital) pada dataset yang sama
  Alpha            : 0.05
  Effect size min  : Penurunan waktu 20% dianggap signifikan secara praktis
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat menurunkan waktu pencarian dokumen dibandingkan sistem manual?

**Tipe eksperimen:** [x] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Sistem manual pengarsipan  | Manual | Dataset sama, urutan dokumen sama, environment sama |
| Treatment | Sistem pengarsipan digital | Digital | Dataset sama, preprocessing sama, environment sama |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ | Mengunakan dokumen arsip yang sama |
| Preprocessing setara | ✅ | Format data sama sebelum pengujian |
| Tuning effort setara | ✅ | Tidak ada optimasi khusus salah atau sistem |
| Environment identik | ✅ | Hardware dan software sama |
| Metrik evaluasi sama | ✅ | Waktu pencarian (detik) |

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya?

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Bias pengguna karena familiar dengan sistem digital | Randomisasi urutan uji + training singkat |
| External | Data hanya dari satu institusi | Perlu ekspansi dataset di penelitian lanjutan |
| Construct | Efisiensi tidak hanya diukur dari waktu | Tambahkan metrik tambahan (succes rate) |
| Conclusion | Sampel uji terlalu sedikit | Gunakan repeated measurement (beberapa percobaan) |

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena dataset penelitian hanya berasal dari satu program studi sistem informasi, sehingga hasil penelitian belum tentu dapat digeneralisasi ke institusi atau lingkungan lain dengan karakteristik dokumen yang berbeda 

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah baseline yang digunakan relevan dan benar-benar mewakili metode pemanding yang umum digunakan?
2. Apakah dataset, preprocessing, dan environment pengujian dibuat sama untuk semua metode?
3. Apakah hasil perbandingan diuji menggunakan metrik dan uji statistik yang valid?

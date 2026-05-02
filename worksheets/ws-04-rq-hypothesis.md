# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Belum terdapat evaluasi performa kuantitatif pada sistem informasi pengarsipan digital dalam meningkatkan efektivitas pengelolaan dan pencarian dokumen

Research Question:
  Tipe         : [ ] Comparison  [x] Improvement  [ ] Exploratory
  Formulasi    : Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat meningkatkan efektivitas pencarian dan pengelolaan dokumen dibandingkan sistem manual pada Program Studi Sistem Informasi?
  Variabel IV  : Metode pengelolaan arsip (manual vs sistem digital berbasis web)
  Variabel DV  : Efektifitas pengelolaan dan pencarian dokumen
  Metrik       : Waktu pencarian dokumen, tingkat ketersedian dokumen, dan kemudahan penggunaan sistem
  Dataset      : Dokumen akademik dan administrasi Program Studi Sistem Informasi
  Baseline     : Sistem pengarsipan manual

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [x] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Diperoleh bukti empiris mengenai pengaruh implementasi sistem informasi pengarsipan digital terhadap efektivitas pencarian dan pengelolaan dokumen.
  Jenis kontribusi        : [x] Improvement  [ ] Comparison  [ ] Novel approach
  Gap yang diisi          : Kurangnya evaluasi performa kuantitatif pada sistem pengarsipan digital.

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan pada efektivitas pencarian dan pengelolaan dokumen antara sistem pengarsipan manual dan sistem informasi pengarsipan digital berbasis web.
  H₁ : Terdapat perbedaan signifikan pada efektivitas pencarian dan pengelolaan dokumen antara sistem pengarsipan manual dan sistem informasi pengarsipan digital berbasis web.
  Threshold              : Penurunan waktu pencarian dokumen minimal 20%
  Justifikasi threshold  : Penuruna sebesar 20% dianggap cukup signifikan untuk menunjukkan peningkatan efisiensi operasional.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Belum ada evaluasi performa kuantitatif sistem pengarsipan digital

**RQ versi pertama (tulis bebas):**
> Apakah sistem informasi pengarsipan digital dapat meningkatkan efektivitas pengelolaan dokumen?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | Ya | Sistem manual vs sistem digital berbasis web |
| Metrik terukur | Ya | Waktu pencarian, ketersediaan dokumen |
| Baseline | Ya | Sistem manual |
| Dataset/konteks | Ya | Dokumen akademik Program Studi Informasi |

**Tipe RQ:** [ ] Comparison / [x] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat meningkatkan efektivitas pencarian dan pengelolaan dokumen dibandingkan sistem manual pada Program Studi Sistem Informasi?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak terdapat perbedaan signifikan efektivitas antara sistem manual dan sistem digital |
| H₁ | Terdapat perbedaan signifikan efektivitas antara sistem manual dan sistem digital |
| Metrik | Waktu pencarian dokumen, ketersediaan dokumen |
| Threshold | Penurunan waktu pencarian ≥ 20% |
| Justifikasi threshold |Menunjukkan peningkatan efisiensi yang terukur |

**Apakah hipotesis ini falsifiable?** [x] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika hasil pengujian menunjukkan sistem digital tidak menghasilkan peningkatan efektivitas atau penurunan waktu pencarian kurang dari treshold yang ditetapkan.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah sistem pengarsipan digital meningkatkan efektivitas dibanding sistem manual |
| Variable (IV) | Metode pengelolaan arsip (manual vs digital) |
| Variable (DV) | Efektivitas pengelolaan dokumen |
| Metric | Waktu pencarian, ketersediaan dokumen |
| Data source | Dokumen akademik Program Studi Sistem Informasi |
| Analysis method | Perbndingan sebelum-sesudah dan evaluasi sistem|

**Apakah rantai lengkap?** [ ] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi?

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Rancang Bangun Sistem Informasi Pengarsipan Digital (Studi Kasus: Program Studi informasi)
**RQ yang diekstrak:** Apakah sistem informasi pengarsipan digital dapat meningkatkan efektivitas pengelolaan dokumen akademik?
**Komponen yang hilang:** Metrik kuantitatif dan evaluasi performa yang lebih terukur

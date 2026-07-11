# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : Log pencarian sistem (log_pencarian), diekspor dari menu Laporan Pencarian, 11 Juli 2026
Jumlah data awal  : 59 baris (kolom: Kata Kunci, Durasi (ms), Waktu Pencarian)

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 0 dari 59 (0%) | Tidak ada tindakan | Tidak ada nilai kosong di kolom manapun |
| Duplikat| 5 baris (3 baris "surat tugas" identik pukul 15:38:16, 2 baris "dokumen administrasi" identik pukul 15:32:00) | Dipertahankan (tidak dihapus) | Bukan duplikat entri data, melainkan pengguna benar-benar melakukan klik pencarian berulang dalam detik yang sama (double-click / uji ulang manual) — merepresentasikan aktivitas nyata, bukan kesalahan pencatatan |
| Error   | 6 baris dengan variasi kapitalisasi ("PROPOSAL", "PROPOSALL", "Dokumen Administrasi", "TUGAS", "Proposal PKM GFT") dan 2 baris typo ("lapran") | Normalisasi teks: lowercase + koreksi typo ("lapran"→"laporan", "proposall"→"proposal") | Variasi ini murni human input error saat mengetik kata kunci pencarian, bukan representasi kata kunci yang berbeda secara substantif — perlu digabung agar agregasi per-kata-kunci di WS-12/WS-14 akurat |

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
| Text normalization | Kata Kunci | `.lower().strip()` lalu koreksi 2 typo manual | Menyamakan kata kunci yang secara substantif sama tapi ditulis beda kapitalisasi/typo |
| Parsing datetime | Waktu Pencarian | String → datetime object | Diperlukan untuk analisis kronologis (WS-12 Latihan 2, deteksi pola cold-start) |

Normalization:
  Metode    : Tidak dilakukan normalisasi numerik (min-max/z-score/robust scaling) pada kolom Durasi (ms)
  Alasan    : Data akan dianalisis dalam satuan aslinya (ms) karena tujuan penelitian adalah membandingkan durasi absolut pencarian manual vs sistem — normalisasi ke rentang [0,1] justru menghilangkan makna praktis dari angka tersebut
  Parameter : (tidak berlaku — tidak ada normalisasi numerik yang diterapkan)

Leakage Check:
  [x] Parameter normalisasi dari training set saja (tidak berlaku, tidak ada split training/test pada data ini — seluruh data deskriptif)
  [x] Tidak ada informasi test set dalam preprocessing (tidak berlaku, penelitian ini bersifat deskriptif/komparatif, bukan predictive modeling dengan train-test split)
  [x] Cross-validation dilakukan setelah split (tidak berlaku untuk konteks ini)

Jumlah data akhir : 59 baris (tidak ada baris dihapus, hanya teks kata kunci dinormalisasi)
Script tersedia   : [ ] Ya → path: ____ | [x] Belum — analisis dilakukan langsung dengan pandas secara interaktif, belum disimpan sebagai script terpisah di repository
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing di semua kolom | 0 dari 59 (0%) | Tidak ada tindakan | Tidak ditemukan sel kosong |
| Duplikat baris identik ("surat tugas" 3×, "dokumen administrasi" 2×, timestamp sama persis) | 5 dari 59 (8.5%) | Dipertahankan | Merepresentasikan aktivitas klik pencarian berulang yang nyata terjadi (bukan kesalahan pencatatan sistem), sehingga menghapusnya justru mendistorsi data aktivitas asli |
| Inkonsistensi kapitalisasi & typo pada kata kunci ("PROPOSAL", "PROPOSALL", "TUGAS", "Dokumen Administrasi", "lapran") | 8 dari 59 (13.6%) | Normalisasi teks (lowercase + koreksi typo) | Kata kunci yang secara substantif sama harus digabung agar tidak dihitung sebagai kategori terpisah saat agregasi |

**Jumlah data sebelum cleaning:** 59
**Jumlah data setelah cleaning:** 59
**Persentase data yang hilang/berubah:** 0% hilang, 13.6% mengalami perubahan teks (normalisasi kata kunci, bukan penghapusan data)

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| Durasi (ms) | 1 – 268 ms | Right-skewed (median 1, mean 8.95, jauh lebih tinggi dari median karena outlier) | Ya (268 ms, 83 ms, 48 ms, dst — 10 dari 59 di atas batas IQR) | Tidak perlu normalisasi numerik | Analisis bertujuan membandingkan durasi absolut (ms) antara pencarian manual vs sistem — mengubah ke skala [0,1] atau z-score justru menghilangkan makna praktis "berapa detik/ms sebenarnya" yang dibutuhkan pembaca skripsi |
| Kata Kunci (teks) | — | — | — | Text normalization (lowercase + koreksi typo) | Bukan normalisasi numerik, tapi diperlukan supaya agregasi per-kata-kunci tidak pecah karena variasi penulisan |

**Apakah normalisasi diperlukan?** [ ] Ya / [x] Tidak
**Justifikasi:**
> Normalisasi numerik (min-max/z-score/robust scaling) tidak diperlukan karena metode analisis yang direncanakan (WS-14) adalah perbandingan deskriptif dan uji statistik sederhana (mis. uji-t) antara durasi manual vs sistem, bukan model machine learning berbasis jarak (distance-based) yang sensitif terhadap skala fitur. Mengubah durasi ke skala lain hanya akan mempersulit interpretasi hasil bagi pembaca. Yang diperlukan hanya normalisasi teks pada kolom kata kunci, bukan normalisasi numerik pada kolom durasi.

**Leakage check:**
- [x] Parameter dihitung dari training set saja — tidak berlaku, penelitian ini tidak menggunakan train-test split (bukan predictive modeling)
- [x] Normalisasi diterapkan setelah train-test split — tidak berlaku untuk alasan yang sama

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: Log pencarian sistem pengarsipan digital (log_pencarian), diekspor 11 Juli 2026
2. Data awal: 59 records, 3 features (Kata Kunci, Durasi (ms), Waktu Pencarian)
3. Cleaning:
   - Missing values: 0 kasus, metode: tidak diperlukan tindakan
   - Duplikat: 5 kasus (baris identik), tindakan: dipertahankan (merepresentasikan aktivitas nyata, bukan error pencatatan)
   - Error: 8 kasus (variasi kapitalisasi & typo kata kunci), tindakan: normalisasi teks (lowercase + koreksi typo)
4. Transformation: Text normalization pada kolom Kata Kunci (lowercase + strip + koreksi 2 typo); parsing kolom Waktu Pencarian dari string ke datetime untuk analisis kronologis
5. Normalisasi: Tidak dilakukan (metode), parameter dari — (kolom Durasi (ms) dianalisis dalam satuan asli karena tujuan penelitian butuh nilai absolut, bukan model berbasis jarak)
6. Data akhir: 59 records, 3 features (jumlah tidak berubah, hanya nilai teks pada 1 kolom dinormalisasi)
7. Leakage check: [x] Lulus / [ ] Ada masalah — tidak berlaku ketat karena tidak ada train-test split dalam desain penelitian ini (data digunakan seluruhnya untuk analisis deskriptif/komparatif)
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Sejujurnya, sebelum mengerjakan worksheet ini saya cenderung berpikir "data numerik = harus dinormalisasi" karena itu yang biasa saya lakukan di tugas-tugas machine learning sebelumnya. Tapi setelah memeriksa data durasi pencarian ini, saya sadar normalisasi di sini justru tidak diperlukan — bahkan bisa jadi bentuk over-preprocessing. Tujuan analisis saya adalah membandingkan angka durasi yang bermakna secara praktis (berapa milidetik sebenarnya, bukan skor relatif 0–1), dan metode analisisnya bukan model machine learning berbasis jarak yang butuh skala seragam.
>
> Risiko over-preprocessing yang paling nyata di kasus saya: kalau saya paksa normalisasi min-max pada kolom Durasi (ms), outlier 268 ms akan menekan semua nilai lain mendekati 0, sehingga perbedaan yang sebenarnya bermakna (mis. 1 ms vs 18 ms) jadi kelihatan nyaris sama di skala [0,1] — padahal itu perbedaan 18×. Preprocessing yang "terlihat rapi" seperti ini justru bisa menyembunyikan pola asli yang ingin saya tunjukkan di WS-14, sesuai jebakan kognitif "lebih banyak preprocessing = lebih bersih = lebih baik" yang disebutkan di materi.

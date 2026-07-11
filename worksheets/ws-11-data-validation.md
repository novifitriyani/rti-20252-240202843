# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua skenario tercakup (skenario sistem)
  [x] Jumlah run sesuai rencana
  [x] Tidak ada file output hilang
  Missing: 0 dari 59 data points (data sistem). Data manual: 0 dari rencana — belum dilaksanakan.

Format Consistency:
  [x] Semua file format sama (CSV/JSON/...)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [x] Nilai dalam range masuk akal
  [x] Tidak ada waktu negatif
  [ ] Metrik 0–100%, tidak di luar range (tidak berlaku — metrik berupa durasi ms, bukan persentase)
  Anomali ditemukan: 10 dari 59 data (17%) di atas batas atas IQR (3.5 ms), tertinggi 268 ms — pola cold-start di awal sesi

Cross-Validation:
  [ ] Run identik → hasil mendekati (belum bisa diverifikasi, data manual pembanding belum ada)
  [x] Trend konsisten dengan ekspektasi teori (durasi rendah & stabil setelah cold-start awal sesi)

Keputusan:
  [ ] Data siap analisis
  [x] Perlu cleaning (normalisasi kapitalisasi & typo kata kunci)
  [x] Perlu re-run (skenario: pengumpulan data pencarian manual sebagai pembanding)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Pencarian via sistem (log otomatis) | 59 | 59 | 0 | — (seluruh log tercatat otomatis oleh sistem, tidak ada proses input manual yang bisa gagal) |
| Pencarian manual (folder/arsip fisik) | 0 | 0 | 0 | Belum dilaksanakan — direncanakan pada tahap eksperimen berikutnya sebagai pembanding |

**Total expected:** 59 (data sistem) | **Total actual:** 59 | **Missing:** 0

**Keputusan untuk data missing:**
> Untuk data pencarian sistem, tidak ada data yang hilang karena seluruh pencarian yang dilakukan melalui form pencarian otomatis tercatat ke tabel `log_pencarian` (durasi diukur dengan `microtime()` di sisi server, tanpa campur tangan pencatatan manual). Data pembanding manual belum dikumpulkan dan akan dilakukan pada tahap eksekusi selanjutnya sebelum masuk ke analisis akhir (WS-14).

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

Data diambil dari 59 log pencarian sistem (kolom `Durasi (ms)`), diekspor dari menu Laporan Pencarian pada tanggal 11 Juli 2026. Karena datanya lebih dari 5 baris, ditampilkan ringkasannya:

| Statistik | Nilai |
|-----------|-------|
| n | 59 |
| Min | 1 ms |
| Q1 | 1 ms |
| Median | 1 ms |
| Q3 | 2 ms |
| Max | 268 ms |
| Mean | 8.95 ms |

**Deteksi outlier:**
- Q1 = 1 ms | Q3 = 2 ms | IQR = 1 ms
- Batas bawah (Q1 - 1.5×IQR) = -0.5 ms (tidak relevan, durasi tidak mungkin negatif)
- Batas atas (Q3 + 1.5×IQR) = 3.5 ms
- Outlier terdeteksi: 10 dari 59 data (durasi 4–268 ms), yang paling ekstrem: 268 ms (keyword "tugas"), 83 ms ("surat keputusan"), 48 ms & 20 ms (keduanya "proposal"), 18 ms ("formulir")

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| Run keyword "tugas" (21:06:07) | 268 ms | Kemungkinan ini pencarian pertama setelah jeda lama (idle) — koneksi database perlu inisialisasi ulang (cold start), atau query LIKE tanpa index menyisir seluruh 100 baris tabel saat MySQL belum melakukan cache query | Dipertahankan sebagai data valid, tapi dicatat sebagai anomali cold-start; direkomendasikan menambah kolom index pada `judul`/`nomor_dokumen` agar query lebih stabil |
| Run keyword "surat keputusan" (14:24:01) | 83 ms | Kemungkinan sama: pencarian pertama di sesi baru (14:07–14:25 adalah rentang awal pengujian), belum ada query cache dari MySQL | Dipertahankan, dicatat sebagai bagian dari pola cold-start di awal sesi |
| Run keyword "proposal" (21:27:09 & 21:27:30) | 48 ms & 20 ms | Dua pencarian berurutan di sesi malam (21:2x), kemungkinan server sempat idle sebelum sesi ini dimulai | Dipertahankan; termasuk pola cold-start per sesi, bukan bug sistem |
| Run keyword "formulir" (21:26:40) | 18 ms | Pencarian pertama di sesi 21:2x, konsisten dengan pola cold-start yang sama | Dipertahankan dengan catatan yang sama |

**Catatan pola (Contextual/Pattern anomaly):** Secara observasi, outlier besar (>18 ms) cenderung muncul di **awal setiap sesi pengujian baru** (mis. awal jam 14:07, awal jam 21:06), sedangkan pencarian berikutnya dalam sesi yang sama turun ke 1–2 ms. Pola waktunya sendiri adalah **fakta yang bisa dicek langsung dari timestamp**. Namun, penyebabnya — diduga efek cold-start koneksi/cache database — **masih berupa hipotesis, belum diverifikasi**. Kemungkinan penyebab lain (mis. beban proses lain di server saat itu) belum bisa disingkirkan tanpa pengujian tambahan (mis. mengulang pengukuran beberapa kali atau memeriksa log server pada jam-jam tersebut).

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul (59 dari 59 log pencarian sistem tercatat; data pembanding manual belum dikumpulkan dan akan menyusul sebagai eksperimen terpisah)
**2. Format:** [X] Konsisten / [ ] Ada inkonsistensi — Namun ditemukan **inkonsistensi kapitalisasi & typo pada kata kunci** (bukan pada format datanya): "proposal" vs "PROPOSAL" vs "PROPOSALL", "laporan" vs "lapran" — ini memengaruhi analisis per-keyword di WS-12/WS-14 kalau tidak dinormalisasi terlebih dahulu
**3. Range check (anomali):** 10 dari 59 data (17%) berada di atas batas atas IQR (3.5 ms), dengan nilai tertinggi 268 ms. Semua nilai durasi tetap positif dan masuk akal (tidak ada durasi negatif atau nol)
**4. Logic check:** [X] Parameter sesuai plan / [ ] Ada ketidaksesuaian — Kolom durasi terisi otomatis oleh sistem (`microtime()`), kolom keyword dan timestamp konsisten dengan aktivitas pencarian yang dilakukan peneliti sendiri (self-testing) sesuai rencana WS-09/WS-10

**Kesimpulan:** [ ] Data siap analisis / [X] Perlu tindakan: (1) normalisasi teks kata kunci (lowercase + perbaikan typo) sebelum agregasi per-kategori, (2) kumpulkan data pembanding manual sebelum masuk ke analisis akhir WS-14, (3) outlier cold-start dipertahankan tapi didokumentasikan sebagai temuan, bukan dihapus

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> "Data yang benar" berarti nilainya sesuai kondisi sebenarnya saat direkam — misalnya durasi 268 ms memang benar-benar terukur oleh sistem, bukan angka salah ketik. Tapi "data yang dipercaya" lebih dari itu: peneliti sudah memverifikasi bahwa data itu lengkap, konsisten formatnya, masuk akal rentangnya, dan anomalinya sudah diinvestigasi (bukan diabaikan). Data pencarian sistem yang saya kumpulkan itu "benar" secara teknis (memang tercatat otomatis oleh `microtime()`), tapi baru bisa "dipercaya" setelah saya cek: ada outlier 268 ms yang harus dijelaskan penyebabnya (cold-start), dan ada inkonsistensi penulisan kata kunci (PROPOSAL vs proposal vs PROPOSALL) yang bisa mendistorsi hasil kalau langsung dianalisis tanpa dibersihkan dulu. Validasi formal tetap diperlukan meskipun data dikumpulkan otomatis karena otomatisasi hanya menjamin proses pencatatannya konsisten — bukan menjamin datanya representatif, bebas anomali, atau siap dianalisis secara statistik.

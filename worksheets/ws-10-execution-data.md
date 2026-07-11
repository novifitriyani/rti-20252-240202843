# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned | - | - |
| 2 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned | - | - |
| 3 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned | - | - |
| 4 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned | - | - |
| 5 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned | - | - |


Jumlah runs per skenario : 5
Total runs               : 5

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : Belum tersedia
  Skenario  : Perbandingan sistem manual dan sistem informasi pengarsipan digital
  Input     : Dokumen uji yang akan dicari pada sistem manual dan sistem informasi pengarsipan digital
  Output    : Waktu pencarian dokumen (detik)
  Anomali   : Belum diketahui
  Catatan   : Eksperimen akan dilakukan setelah implementasi sistem selesai.
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | Perbandingan sistem manual dan digital | Tidak digunakan | Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned |
| 2 | Perbandingan sistem manual dan digital | Tidak digunakan | Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned |
| 3 | Perbandingan sistem manual dan digital | Tidak digunakan |   Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned |
| 4 | Perbandingan sistem manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned |
| 5 | Perbandingan sistem manual dan digital | Tidak digunakan |  Dokumen uji yang sama, komputer yang sama, browser yang sama, dan kondisi lingkungan pengujian yang sama | Planned |

**Total skenario:** 1
**Run per skenario:** 5
**Total run keseluruhan:** 5

**Keterangan:**
Eksperimen direncanakan dilakukan sebanyak lima kali menggunakan prosedur yang sama untuk memperoleh data waktu pencarian yang lebih konsisten. Setiap run menggunakan dokumen uji, perangkat, browser, dan kondisi lingkungan pengujian yang sama agar hasil yang diperoleh dapat dibandingkan secara konsisten. Penelitian ini tidak menggunakan algoritma yang bersifat acak sehingga random seed tidak digunakan.

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | run-001 |
| Timestamp | Tanggal dan waktu pelaksanaan eksperimen |
| Skenario | Perbandingan pencarian dokumen pada sistem manual dan sistem informasi pengarsipan digital |
| Operator | Peneliti |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | Tidak digunakan |
| Code version | Belum tersedia (implementasi website belum dibuat) |
| Runtime | PHP 8.2.12 |
| Database | MariaDB 10.4.32|
| Web Server | Apache 2.4.58 |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Waktu pencarian sistem manual | float | ≥ 0 detik |
| Waktu pencarian sistem digital | float | ≥ 0 detik |
| Selisih waktu pencarian | float | ≥ 0 detik |

**Format output:** [X] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Sistem tidak dapat dijalankan | Dokumentasikan penyebab, perbaiki masalah, kemudian ulangi pengujian |
| Hasil ekstrem | Waktu pencarian jauh lebih lama dibandingkan run lainnya | Periksa kondisi komputer, pastikan tidak ada proses lain yang memengaruhi pengujian, dokumentasikan penyebabnya, kemudian ulangi pengujian. |
| Waktu eksekusi anomali | Komputer sedang menjalankan aplikasi lain | Dokumentasikan kondisi pengujian, tutup aplikasi lain yang berjalan di latar belakang, kemudian ulangi pengujian |
| Inkonsistensi dengan run lain | Hasil pengujian berbeda cukup jauh | Periksa konfigurasi sistem, prosedur pengujian, dokumentasikan penyebab perbedaan hasil, kemudian lakukan pengujian ulang apabila diperlukan. |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Saya belum pernah melakukan penelitian yang mengharuskan pelaksanaan eksperimen secara berulang dan pencatatan data secara sistematis. Sebelumnya saya hanya menyelesaikan tugas berdasarkan hasil satu kali percobaan.

**Yang akan dilakukan berbeda:**
> Pada penelitian ini saya akan menyusun rencana eksperimen terlebih dahulu, melakukan pengujian beberapa kali sesuai prosedur, serta mendokumentasikan setiap hasil pengujian agar data yang diperoleh lebih valid dan dapat dianalisis dengan baik.

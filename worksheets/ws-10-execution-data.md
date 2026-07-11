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
| 1 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan | 1 dokumen | Planned | - | hasil_run1.csv |
| 2 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan | 5 dokumen | Planned | - | hasil_run2.csv |
| 3 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan | 10 dokumen | Planned | - | hasil_run3.csv |
| 4 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan | 20 dokumen | Planned | - | hasil_run4.csv |
| 5 | Perbandingan pencarian dokumen manual dan digital | Tidak digunakan | 50 dokumen | Planned | - | hasil_run5.csv |


Jumlah runs per skenario : 5
Total runs               : 5

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : Belum tersedia
  Skenario  : Perbandingan sistem manual dan sistem informasi pengarsipan digital
  Input     : Jumlah dokumen yang dicari
  Output    : Waktu pencarian dokumen (detik)
  Anomali   : Belum diketahui
  Catatan   : Eksperimen akan dilakukan setelah implementasi sistem selesai.
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | Perbandingan sistem manual dan digital | Tidak digunakan | 1 dokumen | Planned |
| 2 | Perbandingan sistem manual dan digital | Tidak digunakan | 5 dokumen | Planned |
| 3 | Perbandingan sistem manual dan digital | Tidak digunakan | 10 dokumen| Planned |
| 4 | Perbandingan sistem manual dan digital | Tidak digunakan | 20 dokumen| Planned |
| 5 | Perbandingan sistem manual dan digital | Tidak digunakan | 50 dokumen| Planned |

**Total skenario:** 1
**Run per skenario:** 5
**Total run keseluruhan:** 5

**Keterangan:**
Eksperimen direncanakan dilakukan sebanyak lima kali menggunakan prosedur yang sama untuk memperoleh data waktu pencarian yang lebih konsisten. Setiap run menggunakan jumlah dokumen sesuai skenario pengujian. Penelitian ini tidak menggunakan algoritma yang bersifat acak sehingga random seed tidak digunakan.

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
| Code version | GitHub Repository (akan diperbarui setelah implementasi) |
| Runtime | PHP 8.2.12 |
| Database | MariaDB 10.4.32|
| Web Server | Apache 2.4.58 |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Waktu pencarian sistem manual | float | ≥ 0 detik |
| Waktu pencarian sistem digital | float | ≥ 0 detik |
| Selisih waktu pencarian | float | ≥ 0 detik |

**Format output:** [X] CSV / [ ] JSON / [X] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Apache atau MariaDB berhenti saat pengujian | Dokumentasikan penyebab, jalankan kembali layanan, kemudian ulangi pengujian |
| Hasil ekstrem | Waktu pencarian jauh lebih lama dibandingkan run lainnya | Periksa beban CPU, penggunaan memori, dan aplikasi yang sedang berjalan. |
| Waktu eksekusi anomali | Komputer mengalami lag atau penggunaan CPU tinggi | Tutup aplikasi lain, kemudian lakukan pengujian ulang |
| Inkonsistensi dengan run lain | Hasil pengujian berbeda cukup jauh | Periksa konfigurasi aplikasi dan database, kemudian ulangi pengujian dengan kondisi yang sama |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Saya belum pernah melakukan penelitian yang mengharuskan pelaksanaan eksperimen secara berulang dan pencatatan data secara sistematis. Sebelumnya saya hanya menyelesaikan tugas berdasarkan hasil satu kali percobaan.

**Yang akan dilakukan berbeda:**
> Pada penelitian ini saya akan menyusun rencana eksperimen terlebih dahulu, melakukan pengujian beberapa kali sesuai prosedur, serta mendokumentasikan setiap hasil pengujian agar data yang diperoleh lebih valid dan dapat dianalisis dengan baik.

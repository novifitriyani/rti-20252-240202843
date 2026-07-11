# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah sistem informasi pengarsipan digital dapat mempercepat proses pencarian dokumen dibandingkan dengan pencarian manual?
Metrik Utama      : Durasi pencarian (ms) per kata kunci, diukur otomatis oleh sistem menggunakan microtime()

Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| Pencarian via sistem (seluruh kata kunci) | 8.95 ± 36.51 ms | — | 59 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Bar chart per kata kunci (mean ± std) | Kata kunci mana yang butuh waktu pencarian lebih lama | Mean durasi per kata kunci |
| 2 | Line chart kronologis (15 pencarian terakhir) | Tren durasi dari waktu ke waktu, terlihat pola cold-start | Durasi per pencarian (urut waktu) |

Bias Check:
  [x] Y-axis mulai dari 0 (atau dijustifikasi)
  [x] Error bar/CI ditampilkan (std ditampilkan di tabel)
  [x] Semua data disertakan (tidak cherry-picked) — termasuk outlier 268 ms
  [x] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| dokumen administrasi | 1.67 ± 1.61 ms | min 1 / max 6 ms | 12 |
| surat tugas | 1.91 ± 1.51 ms | min 1 / max 6 ms | 11 |
| proposal | 8.20 ± 15.15 ms | min 1 / max 48 ms | 10 |
| laporan | 2.33 ± 3.27 ms | min 1 / max 9 ms | 6 |
| surat keputusan | 17.60 ± 36.56 ms | min 1 / max 83 ms | 5 |
| formulir | 5.75 ± 8.22 ms | min 1 / max 18 ms | 4 |
| panduan | 1.33 ± 0.58 ms | min 1 / max 2 ms | 3 |
| tugas | 134.50 ± 188.80 ms | min 1 / max 268 ms | 2 |
| **Keseluruhan (semua kata kunci)** | **8.95 ± 36.51 ms** | **min 1 / max 268 ms** | **59** |

*Catatan: kata kunci sudah dinormalisasi (lowercase, typo "lapran"→"laporan" dan "proposall"→"proposal" digabung) agar agregasi akurat. Kata kunci dengan n=1 ("001", "proposal pkm gft") dan "berita acara", "surat" (n=2) tidak ditampilkan terpisah karena sampel terlalu kecil untuk dihitung std.*

**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± std (bukan single number)
- [x] Diurutkan berdasarkan metrik utama (jumlah sampel, dari terbanyak)
- [x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Bar chart mean durasi per kata kunci | Kata kunci "surat keputusan" dan "tugas" punya rata-rata durasi jauh lebih tinggi (didorong outlier), sedangkan "dokumen administrasi" & "surat tugas" paling stabil rendah | Mean durasi per kata kunci dari tabel Latihan 1 |
| 2 | Line chart kronologis 15 pencarian terakhir | Durasi tinggi cenderung muncul di pencarian pertama tiap sesi, lalu turun & stabil — pola cold-start, bukan acak | Durasi per pencarian, diurutkan berdasarkan waktu |
| 3 | Box plot per kata kunci (untuk kata kunci dengan n≥5) | Menampilkan sebaran & outlier tiap kata kunci sekaligus, lebih jujur dibanding hanya mean karena std sangat besar pada beberapa kata kunci | Seluruh nilai durasi per kata kunci (dokumen administrasi, surat tugas, proposal, laporan, surat keputusan) |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Ya — A terlihat 2× B padahal beda 0.4% |
| Apakah error bar ditampilkan? | Tidak — tidak ada informasi std/variabilitas, padahal skenario tidak menyebutkan jumlah run (n), sehingga pembaca tidak tahu apakah selisih 0.4% ini konsisten atau kebetulan |
| Apakah semua kondisi ditampilkan? | Tidak jelas — hanya dua metode dibandingkan tanpa baseline, dan tidak disebutkan apakah ada kondisi/skenario lain yang tidak ditampilkan |
| Apa solusinya? | Set Y-axis mulai dari 0%, tambahkan error bar (std/CI) dan cantumkan n, serta sertakan seluruh kondisi yang diuji tanpa menyembunyikan hasil yang kurang mendukung |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [ ] Semua bias check lulus
- [x] Ada yang perlu diperbaiki: Grafik bar chart mean per kata kunci (grafik #1) berisiko menyesatkan jika ditampilkan tanpa error bar, karena std pada "surat keputusan" dan "tugas" sangat besar (36.56 dan 188.80) — nilai mean-nya sendiri kurang representatif tanpa disertai sebaran datanya. Solusi: sertakan error bar pada grafik #1, atau prioritaskan box plot (grafik #3) sebagai visual utama untuk kata kunci dengan sampel kecil dan variabilitas tinggi.

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik saling melengkapi, bukan saling menggantikan. Tabel memberi angka presisi (mean, std, n) yang bisa dikutip ulang dan diverifikasi, tapi sulit langsung terlihat polanya — misalnya dari tabel Latihan 1 saja, tidak langsung kelihatan bahwa outlier "surat keputusan" dan "tugas" itu terjadi di awal sesi pengujian. Grafik (terutama line chart kronologis) langsung menunjukkan pola cold-start itu secara visual, tapi tanpa tabel, saya tidak bisa tahu angka pastinya (268 ms, bukan "sekitar 250-an"). Kalau cuma pakai salah satu, saya berisiko kehilangan presisi (kalau cuma grafik) atau kehilangan insight pola (kalau cuma tabel).
>
> Saya belum pernah sengaja membuat grafik yang menyesatkan, tapi setelah mengerjakan Latihan 3 saya sadar hampir membuat kesalahan serupa: rencana awal saya di Latihan 2 hanya bar chart mean per kata kunci tanpa error bar. Kalau itu langsung dipakai, pembaca bisa mengira "surat keputusan" konsisten lambat (17.60 ms), padahal std-nya 36.56 — artinya datanya sangat bervariasi (kadang 1 ms, kadang 83 ms) dan mean saja menyembunyikan itu. Ini pas dengan poin "Missing error bar" di materi — mean tanpa variabilitas bisa membuat kesimpulan yang secara teknis benar tapi menyesatkan secara kontekstual.

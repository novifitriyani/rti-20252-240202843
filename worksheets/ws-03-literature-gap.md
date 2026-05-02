# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Sistem Informasi Pengarsipan Digital untuk Pengelolaan Dokumen Akademik
Database   : Google Scholar
Query      : Sistem informasi pengarsipan digital 
Tahun      : 2021-2025
Hasil awal : 15 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Karim et al. | 2024 | Web-based archive information system | Dokumen akademik Program Studi SI | mempermudah pengelolaan dan pencarian arsip | Tidak ada evaluasi kuantitatif performa |
| Hudawi et al. | 2022 | Framework Codelgniter | Arsip dokumen organisasi | Sistem mempermudah penyimpanan arsip | Implementasi terbatas pada satu instasi |
| Marlena & Solikin | 2025 | Sistem arsib digital berbasis web | Dokumen PT Kereta Api Indonesia | Pengelolaan asrip lebih efektif | Belum membahas usability pengguna |
| Ente et al. | 2023 | OCR berbasis web |Dokumen hasil scan | Mempermudah pencarian dokumen digital | Bergantung kualitas sacan dokumen|
| Sahal & Winardi | 2021 | Sistem pengarsipan digital | Arsip administrasi | Mendukung digitalisasi dokumen | Security System belum optimal |

Pola yang ditemukan:
  Metode dominan     : Sistem informasi pengarsian berbasis web dengan database terintegrasi
  Dataset umum       : Dokumen akademik, administrasi, surat dan arsip organisasi
  Limitasi berulang  : Evaluasi sistem masih dominan black box/fungsional, Implementasi hanya pada satu institusi, Belum banyak evaluai usability dan security.

GAP IDENTIFICATION

Gap 1: [Jenis: Performance Gap]
  Deskripsi    : Sebagian besar penelitian berfokus pada implementasi sistem tanpa evaluasi performa yang terukur.
  Bukti        : Mayoritas paper hanya menguji fungsi tanpa pengukuran kuantitatif seperti kecepatan pencarian dokumen.
  Signifikansi : Sulit membuktikan efektivitas sistem secara objektif 

Gap 2: [Jenis: Context Gap]
  Deskripsi    : Penelitian umumnya diuji hanya pada satu organisasi atau institusi
  Bukti        : Seluruh paper menggunakan studi kasus tunggal
  Signifikansi : Hasil sulit digeneralisasi ke lingkungan berbeda

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| Sistem pengarsipan manual | Pembanding kondisi sebelum digitalisasi | Masih digunakan di banyak institusi | Karim et al., 2024 |
| Sistem pengarsipan web sederhana| Menyelesaikan asalah serupa | Banyak digunakan dalam penelitan sejenis| Hudawi et al., 2022|
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Sistem Informasi Pengarsipan Digital
**Query pencarian:** Sitem informasi pengarsipan digital
**Database:** Google Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Karim et al. | 2024 | Web-based archive system | Dokumen akademik  | Mempermudah arsip digital | Tidak ada evaluasi kuantitatif |
| 2 | Hudawi et al. | 2022 | Codelgniterb framework | Arsip organisasi | Pengelolaan lebih efisien | Single situation |
| 3 | Marlena & Solikin | 2025 | Web digital archive | dokumen perusahaan | Efektivitas meningkat | Belum usability analysis |
| 4 | Ente et al. | 2023 | OCR web-based archive | Scan dokumen | Search lebih mudah | Bergantung kualitas scan |
| 5 | Sahal & Winardi | 2021 | Digital archiving system | Arsip administrasi | Mendukung digitalisai dokumen | Sistem keamanan belum optimal |

**Pola yang terlihat — Metode dominan:** Sistem informasi pengarsipan berbasis web dengan database terintegrasi
**Limitasi yang berulang:** Kurangnya evaluasi kuantitatif performa, usability, dan security system

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [x] Ya / [ ] Tidak | Belum ada evaluasi performa kuantitatif sistem pengarsipan digital |
| Method Gap | [ ] Ya / [ ] Tidak | - |
| Data Gap | [ ] Ya / [ ] Tidak | - |
| Context Gap | [x] Ya / [ ] Tidak | Studi masih terbatas pada satu institusi |

**Gap utama yang dipilih:** Performance Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena sebagian besar penelitian hanya membangun sistem tanpa membuktikan secara terukur bahwa sistem benar-benar meningkatkan efektivitas penglolaan dokumen. 

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Sistem manual | Karena sistem manual adalah kondisi awal sebelum ada digitalisasi arsip | Masih banyak yang menggunakan pengarsipan manual | Bukan | Karim et al., 2024 |
| 2 | Web archive system sederhana | Karena sama-sama menyelesaikan masalah pengarsipan digital berbasis web | Banyak penelitian serupa menggunakan model web archive system sederhana (CRUD dokumen, database, search) | Bukan | Hudawi et al., 2022|

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [x] Tidak
> Justifikasi: Baseline dipilih karena relevan dengan masalah yang sama dan mewakili praktik umum pada pengelolaan arsip dokumen  

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Klaim "belum ada yang meneliti ini" tidak cukup tanpa bukti pencarian literatur. Research gap yang valid harus dibuktikan melalui pencarian sistematis, analisis beberapa paper, serta identifikasi pola keterbatasan yang konsisten.

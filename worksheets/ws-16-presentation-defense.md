# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:
  Total slides   : 9 (7 konten + title + closing)
  Time per slide : ~1.5-2 min
  Total time     : 15 menit

Slide Outline:
| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
| 1 | Title       | Judul + logo sistem | 30s   |
| 2 | Problem     | Ilustrasi arsip manual berantakan | 2min  |
| 3 | Gap + RQ    | Pertanyaan penelitian | 2min  |
| 4 | Method      | Diagram alur sistem & desain eksperimen | 2min |
| 5 | Result (tabel) | Tabel statistik deskriptif manual vs sistem | 2min |
| 6 | Result (grafik) | Bar chart & line chart durasi pencarian | 2min |
| 7 | Interpretasi | Effect size & practical significance | 2min |
| 8 | Limitasi & future work | Poin-poin limitasi | 1.5min |
| 9 | Kesimpulan | Ringkasan kontribusi | 1min |

Anticipatory Defense Matrix:
| Kategori | Pertanyaan Potensial | Jawaban (CER) |
|----------|---------------------|---------------|
| Problem  | Mengapa masalah pencarian dokumen manual ini penting diteliti? | Claim: Pencarian manual menghambat efisiensi kerja administratif. Evidence: Data menunjukkan rata-rata 8.7 detik per pencarian manual, dan itu terus berulang setiap staf mencari dokumen. Reasoning: Akumulasi waktu ini signifikan dalam skala penggunaan harian sebuah instansi |
| Gap      | Bukankah sudah banyak sistem arsip digital yang ada? | Claim: Banyak sistem arsip digital ada, tapi jarang yang disertai bukti kuantitatif kecepatan pencarian dibanding manual secara terukur. Evidence: Penelitian ini justru berfokus pada pengukuran (paired t-test, effect size), bukan hanya pengembangan sistem. Reasoning: Kontribusi utamanya bukan "sistemnya baru", tapi "buktinya terukur secara ilmiah" |
| Method   | Mengapa hanya 10 kata kunci yang diuji, bukan semua 100 dokumen satu-satu? | Claim: 10 kata kunci mewakili seluruh 8 kategori dokumen yang ada di sistem. Evidence: Kata kunci yang dipilih mencakup semua kategori (Proposal, Laporan, SK, dst) dengan jumlah dokumen representatif di tiap kategori. Reasoning: Constraint waktu penelitian membuat sampling per-kategori lebih efisien dibanding menguji seluruh 100 dokumen individual, sambil tetap menjaga keterwakilan |
| Results  | Kenapa durasi sistem untuk kata kunci "tugas" mencapai 134.5 ms, jauh di atas kata kunci lain? | Claim: Ini outlier yang sudah diinvestigasi di WS-11. Evidence: Nilai tertinggi (268 ms) terjadi di awal sesi pengujian, konsisten dengan pola cold-start koneksi database. Reasoning: Pola ini didokumentasikan sebagai dugaan (belum diverifikasi definitif), bukan diabaikan begitu saja — transparansi ini justru memperkuat kredibilitas analisis |
| Generalization | Apakah hasil ini berlaku untuk instansi dengan jumlah dokumen jauh lebih banyak (misal 10.000 dokumen)? | Claim: Berpotensi tetap signifikan lebih cepat, tapi belum diverifikasi langsung. Evidence: Penelitian ini hanya diuji pada skala 100 dokumen. Reasoning: Disebutkan eksplisit sebagai limitasi (external validity) di Discussion — pengujian skala besar direkomendasikan sebagai future work |

Latihan:
  Latihan 1: [belum dilaksanakan] — isi setelah kamu latihan presentasi sendiri dengan stopwatch
  Latihan 2: [belum dilaksanakan] — isi setelah latihan kedua
  Latihan 3: [belum dilaksanakan] — isi setelah simulasi Q&A dengan teman/kolega (lihat Latihan 3 di bawah)
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | *Contoh: Judul + konteks — rekomendasi vs kepuasan* | *Title slide, gambar sistem* | *1 min* |
| 2 | *Contoh: Problem — RMSE tinggi tapi satisfaction rendah (45/100)* | *Bar chart: satisfaction vs RMSE per sistem* | *2 min* |
| 3 | *Contoh: Gap + RQ — belum ada CF+context untuk satisfaction* | *Tabel gap literatur* | *1.5 min* |
| 4 | Method overview — desain eksperimen paired-comparison manual vs sistem pada 100 dokumen | Diagram alur: arsip manual → sistem → pengukuran durasi | 2 min |
| 5 | Key result (tabel) — statistik deskriptif kedua metode | Tabel mean±std manual (8710.5±6230.6 ms) vs sistem (17.58±41.40 ms) | 2 min |
| 6 | Key result (grafik) — visualisasi durasi per kata kunci & pola kronologis | Bar chart mean±std, line chart 15 pencarian terakhir | 2 min |
| 7 | Interpretasi — signifikansi statistik & praktis | Ringkasan p=0.00169, d=1.395 (large effect), percepatan 99.8% | 2 min |
| 8 | Limitasi & future work — n kecil, bias familiaritas, simulasi arsip | Poin bullet ringkas | 1.5 min |
| 9 | Kesimpulan — sistem terbukti signifikan lebih cepat, kontribusi & rekomendasi lanjutan | Ringkasan 1 kalimat + call-to-action | 1 min |

**Total waktu estimasi:** 15 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | *Problem* | *Contoh: Mengapa fokus kepuasan, bukan akurasi?* | *Akurasi tinggi tidak menjamin kepuasan* | *Survey: 45/100 satisfaction meski RMSE 0.87* | *Gap antara metrik teknis dan pengalaman pengguna* |
| 2 | *Method* | *Contoh: Mengapa hanya 3 dataset?* | *3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy* | *Tabel karakteristik dataset di Bab Method* | *Generalisasi perlu validasi lanjut — tercatat sebagai limitasi* |
| 3 | Method | Kenapa data manual dan sistem tidak dikumpulkan bersamaan dari awal? | Urutan pengumpulan tidak memengaruhi validitas selama keduanya ada sebelum kesimpulan ditarik | Sistem diuji fungsional (black box testing) terlebih dahulu untuk memastikan validitasnya sebagai pembanding, baru data performa dikumpulkan | Membandingkan ke sistem yang belum tervalidasi fungsinya berisiko menghasilkan data yang tidak bermakna |
| 4 | Results | Apakah selisih 8.7 detik vs 0.018 detik ini reliable mengingat n hanya 10 pasangan? | Ya, karena diuji dengan 2 metode statistik berbeda yang hasilnya konsisten | Paired t-test (p=0.00169) dan Wilcoxon non-parametrik (p=0.00195) menghasilkan kesimpulan yang sama | Konsistensi antar 2 uji dengan asumsi berbeda memperkuat keandalan hasil meski n kecil |
| 5 | Generalization | Apakah sistem ini bisa diterapkan di instansi lain di luar konteks skripsi ini? | Berpotensi bisa, dengan penyesuaian | Sistem dibangun dengan struktur generik (kategori, dokumen, pencarian) yang tidak spesifik ke satu instansi | Perlu pengujian ulang di konteks nyata sebelum klaim generalisasi dibuat — disebutkan sebagai future work, bukan klaim final |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

> **Catatan pengerjaan:** Bagian ini sengaja belum diisi karena membutuhkan interaksi nyata dengan teman/kolega yang bertanya spontan — tujuannya melatih respons refleksmu sendiri, bukan jawaban yang sudah disiapkan (beda dengan Latihan 2 yang memang untuk persiapan). Gunakan Anticipatory Defense Matrix di Template A.16 sebagai modal jawaban, tapi biarkan pertanyaan temanmu benar-benar spontan.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|| *1* | *Contoh: "Mengapa tidak membandingkan dengan metode Y?"* | *Contoh: "Karena Y memerlukan dataset labeled yang tidak tersedia. Disebutkan sebagai limitasi di halaman X."* | *[✓] Direct [✓] Data-based [✓] Honest* || 1 | (isi setelah simulasi Q&A) | | [ ] Direct [ ] Data-based [ ] Honest |
| 2 | (isi setelah simulasi Q&A) | | [ ] Direct [ ] Data-based [ ] Honest |
| 3 | (isi setelah simulasi Q&A) | | [ ] Direct [ ] Data-based [ ] Honest |

**Pertanyaan yang paling sulit dijawab:**
> (isi setelah simulasi Q&A dilakukan)

**Apa yang perlu disiapkan lebih baik:**
> (isi setelah simulasi Q&A dilakukan)

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Bagian yang paling mengubah cara berpikir saya adalah WS-11 (Data Validation) dan WS-14 (Failure Analysis) — dua-duanya mengajarkan bahwa data "otomatis tercatat oleh sistem" tidak otomatis berarti "siap dianalisis". Saya sempat berasumsi kalau data sudah keluar dari sistem, ya tinggal dipakai. Ternyata perlu dicek dulu (missing, duplikat, inkonsistensi, outlier), dan bahkan setelah itu, hasil signifikan sekalipun tetap harus dilaporkan bersama keterbatasannya secara jujur, bukan hanya dipoles jadi kelihatan sempurna.

**Yang akan selalu diterapkan:**
> Kebiasaan memisahkan dengan jelas antara "fakta yang teramati" dan "dugaan/interpretasi atas fakta itu" (seperti pada kasus outlier cold-start di WS-11) — supaya klaim yang saya buat di laporan manapun ke depannya tidak melebihi apa yang benar-benar didukung oleh data, dan supaya saya bisa mempertahankan setiap klaim itu dengan jujur kalau ditanya lebih lanjut (prinsip CER: Claim-Evidence-Reasoning dari WS-16 ini).

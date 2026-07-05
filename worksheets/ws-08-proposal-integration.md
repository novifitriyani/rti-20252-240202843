# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread** (benang merah):
```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```
Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [X] Problem → Gap: masalah terdokumentasi di literatur
  [X] Gap → RQ: pertanyaan menjawab gap spesifik
  [X] RQ → Hypothesis: hipotesis memprediksi jawaban
  [X] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [X] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [X] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [X] Istilah sama di semua bagian
  [X] Variabel di RQ = variabel di hipotesis = metrik di desain
  [X] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [X] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [X] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [X] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [X] Proposal mengakui kemungkinan H0 tidak ditolak (honest uncertainty)
  [X] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria     | 1 (Lemah)                                        | 2 (Cukup)                                     | 3 (Baik)                                           | Skor |
|------------- |--------------------------------------------------|-----------------------------------------------|----------------------------------------------------|------|
| Koherensi    | >2 koneksi vertikal terputus                     | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas        | 3 |
| Specificity  | Variabel/metrik masih abstrak, tidak ada angka   | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas   | 3 |
| Feasibility  | Timeline >6 bulan tanpa memperhitungkan sumber   | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail | 3 |
| Rigor        | Baseline tidak jelas atau straw man              | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap   | 3 |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Pengelolaan arsip masih dilakukan secara manual sehingga proses pencarian dokumen kurang efisien, membutuhkan waktu lebih lama, dan berisiko kehilangan data. |
| Gap | WS-03 | Sebagian besar penelitian hanya berfokus pada implementasi sistem dan pengujian fungsional, belum melakukan evaluasi performa kuantitatif serta masih terbatas pada satu institusi. |
| RQ | WS-04 | Apakah implementasi sistem informasi pengarsipan digital berbasis web dapat menurunkan waktu pencarian dokumen dibandingkan sistem manual pada dokumen akademik Program Studi Sistem Informasi? |
| Hipotesis | WS-04 | H₁: Sistem informasi pengarsipan digital berbasis web dapat menurunkan waktu pencarian dokumen dibandingkan sistem manual. |
| Variabel & Metrik | WS-05 | IV = metode pengelolaan arsip (manual vs digital); DV = waktu pencarian dokumen (detik); CV = jenis dokumen akademik; metrik utama adalah waktu pencarian dokumen. |
| Sistem | WS-06 | Sistem berbasis web yang menyediakan fitur unggah, penyimpanan, dan pencarian dokumen untuk mengukur waktu pencarian secara konsisten. |
| Desain Eksperimen | WS-07 | Comparison Study antara sistem manual dan sistem digital menggunakan dataset yang sama, metrik waktu pencarian, serta uji statistik Paired t-test. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✅ | Masalah pengelolaan arsip manual diperkuat oleh hasil literature review yang menunjukkan masih minim evaluasi performa sistem. |
| Gap → RQ | ✅ | RQ secara langsung menjawab gap dengan menguji penurunan waktu pencarian dokumen. |
| RQ → Hypothesis | ✅ | H₁ memprediksi bahwa sistem digital memberikan waktu pencarian yang lebih cepat dibandingkan sistem manual. |
| Hypothesis → Metric | ✅ | Hipotesis diuji menggunakan metrik waktu pencarian dokumen (detik). |
| Metric → System | ✅ | Sistem mencatat dan menghasilkan data waktu pencarian dokumen sebagai hasil pengukuran. |
| System → Experiment | ✅ | Sistem digunakan sebagai media eksperimen untuk membandingkan metode manual dan digital. |

**Koneksi mana yang paling lemah?** Tidak ada koneksi yang lemah karena seluruh komponen sudah saling mendukung.
**Bagaimana cara memperkuatnya?**
> Menambah jumlah dataset serta memperluas objek penelitian ke beberapa institusi agar hasil penelitian lebih dapat digenerelisasikan.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [X] Ya / [ ] Tidak
---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Problem, gap, RQ, hipotesis, variabel, sistem, dan eksperimen saling terhubung dengan baik. |
| Specificity | 3 | Variabel, metrik, threshold, dan metode pengukuran telah ditentukan secara jelas. |
| Feasibility | 3 | Penelitian realistis dilakukan dalam waktu skripsi dengan sumber daya yang tersedia. |
| Rigor | 3 | Baseline, metode eksperimen, serta uji statistik telah ditentukan berdasarkan hasil kajian literatur. |

**Skor total:** 12 / 12

**Apakah proposal siap untuk fase eksekusi?** [X] Ya / [ ] Belum
---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** Menentukan variabel penelitian dan metrik pengukuran karena sudah mengacu pada Research Question yang telah dirumuskan.  
**Bagian tersulit:** Mengidentifikasi research gap dari literatur karena harus membandingkan beberapa penelitian dan menemukan kekurangan yang benar-benar didukung bukti.
**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, saya akan melakukan pencarian literatur secara lebih sistematis sejak awal dan menyusun referensi berdasarkan tema agar proses identifikasi research gap menjadi lebih mudah dan terstruktur.

# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Sistem Informasi Pengarsipan Digital Berbasis Web untuk Mempercepat Pencarian Dokumen Akademik dan Administrasi
Target  : [ ] Jurnal  [ ] Konferensi  [x] Laporan (Skripsi/Tugas Akhir)

Section Check:
  [x] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [x] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [x] Related Work — concept-centric, gap positioning
  [x] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [x] Results — tabel + grafik + observasi (tanpa interpretasi)
  [x] Discussion — interpretasi, perbandingan, implikasi, limitation
  [x] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [x] RQ di Introduction = RQ di Method = RQ di Conclusion
  [x] Variabel di Method = variabel di Results
  [x] Klaim di Discussion didukung data di Results
  [x] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [x] Clarity — mudah dipahami tanpa re-read
  [x] Precision — tidak ada istilah ambigu
  [x] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Pencarian dokumen akademik/administrasi secara manual memakan waktu lama dan tidak efisien. Penelitian ini membangun sistem informasi pengarsipan digital berbasis web (PHP native, MariaDB) dan mengujinya dibandingkan pencarian manual. Hasil menunjukkan sistem 99.8% lebih cepat (rata-rata 0.018 detik vs 8.7 detik), signifikan secara statistik (p=0.00169, Cohen's d=1.395). | 200-250 |
| Introduction | Konteks: pencarian dokumen manual di arsip fisik/tidak terstruktur memakan waktu dan rentan human error. Gap: belum ada sistem pengarsipan sederhana yang teruji secara kuantitatif kecepatan pencariannya untuk skala kecil-menengah (instansi pendidikan). RQ: apakah sistem pengarsipan digital dapat mempercepat pencarian dokumen dibanding manual secara signifikan? | 500-700 |
| Related Work | Membahas penelitian terdahulu tentang sistem manajemen dokumen/arsip digital, perbandingan metode pencarian terindeks vs manual, serta studi tentang efisiensi sistem informasi berbasis web di lingkungan akademik — memposisikan gap bahwa penelitian ini fokus pada pengukuran kuantitatif waktu pencarian dengan data primer, bukan sekadar studi kelayakan | 700-1000 |
| Method | Desain: eksperimen paired-comparison (manual vs sistem) pada 100 dokumen di 8 kategori. Variabel: metode pencarian (IV), durasi pencarian dalam ms/detik (DV). Setup: PHP native, MariaDB, Apache (XAMPP); data manual dikumpulkan via simulasi arsip tidak terstruktur, data sistem dicatat otomatis via microtime(). Prosedur: black box testing fungsional, lalu pengujian performa dengan 10 kata kunci yang sama untuk kedua metode | 800-1200 |
| Results | Tabel statistik deskriptif (mean, std, n) kedua skenario; hasil paired t-test dan Wilcoxon (p<0.01); effect size (d=1.395); grafik bar chart & line chart durasi per kata kunci — dilaporkan objektif tanpa interpretasi | 500-800 |
| Discussion | Interpretasi: hasil mendukung H1, sistem signifikan lebih cepat baik secara statistik maupun praktis. Perbandingan dengan literatur pencarian terindeks vs linear search. Limitation: n kecil (10 pasangan), potensi bias familiaritas peneliti tunggal, simulasi arsip manual belum representasi fisik penuh | 600-900 |
| Conclusion | Menjawab RQ: sistem terbukti mempercepat pencarian dokumen ±99.8% dibanding manual. Kontribusi: sistem pengarsipan siap pakai + bukti kuantitatif efisiensinya. Future work: pengujian dengan responden tambahan, data manual arsip fisik sungguhan, index database untuk optimasi lanjutan | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| *Contoh: RQ1* | *✓* | *✓* | *✓* | *✓* | *✓* |
| *Contoh: Metrik-X* | *✗ ←* | *✗ ←* | *✓* | *✗ ←* | *✗ ←* |
| RQ1 (sistem lebih cepat dari manual?) | ✓ | ✓ | ✓ | ✓ | ✓ |
| RQ2 (belum ada, hanya 1 RQ utama pada penelitian ini) | — | — | — | — | — |
| Metrik utama (durasi pencarian ms/detik) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel IV (metode pencarian: manual/sistem) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel DV (durasi pencarian) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Klaim/kontribusi (sistem signifikan lebih cepat) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Limitasi (n kecil, bias familiaritas, simulasi arsip) | ✗ ← | ✗ ← | ✗ | ✓ | ✓ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Limitasi penelitian (ukuran sampel kecil, potensi bias familiaritas, simulasi arsip manual) hanya muncul di Discussion dan Conclusion, tapi tidak disinggung sama sekali di Introduction atau Method. Idealnya, Method setidaknya menyebutkan desain eksperimen sudah mempertimbangkan keterbatasan ini (misal kenapa n=10 pasangan dipakai, kenapa arsip manual disimulasikan bukan fisik asli) supaya pembaca tidak kaget saat sampai ke Discussion.

**Tindakan perbaikan:**
> Tambahkan 1-2 kalimat di bagian akhir Method yang menyebutkan constraint desain penelitian (skala waktu terbatas, jumlah kata kunci uji, alasan simulasi arsip manual) sehingga limitasi yang dibahas lebih detail di Discussion terasa sebagai kelanjutan yang sudah diantisipasi, bukan kelemahan yang baru disadari belakangan.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> Sistem yang dibuat menunjukkan performa yang bagus dalam pencarian dokumen. Berdasarkan hasil pengujian, pencarian dengan sistem jauh lebih cepat dibandingkan cara manual. Hal ini membuktikan bahwa sistem yang dikembangkan berhasil dan work dengan baik untuk mengatasi masalah pencarian dokumen yang ada sebelumnya.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Kalimat pertama "performa yang bagus" ambigu — bagus dalam hal apa? Kecepatan? Akurasi? Kemudahan pakai? Kalimat kedua "jauh lebih cepat" juga tidak diberi angka, jadi pembaca tidak tahu seberapa jauh | Ganti dengan angka konkret: "durasi pencarian rata-rata turun dari 8.7 detik (manual) menjadi 0.018 detik (sistem)" |
| Precision | "berhasil dan work dengan baik" adalah istilah informal dan tidak presisi — tidak menyebutkan kriteria keberhasilan apa yang dipakai (signifikansi statistik? threshold tertentu?). Kata "work" juga bahasa gaul, tidak sesuai bahasa ilmiah | Ganti dengan: "hasil pengujian statistik menunjukkan perbedaan yang signifikan (p=0.00169, Cohen's d=1.395)" |
| Conciseness | Kalimat ketiga mengulang informasi yang sudah tersirat di kalimat kedua ("membuktikan sistem berhasil" adalah restatement dari "jauh lebih cepat"), menambah panjang tanpa menambah informasi baru | Gabungkan kalimat kedua & ketiga menjadi satu kalimat yang langsung menyatakan hasil beserta signifikansinya |

**Paragraf setelah perbaikan:**
> Hasil pengujian menunjukkan durasi pencarian dokumen menggunakan sistem (rata-rata 0.018 detik) secara signifikan lebih cepat dibandingkan pencarian manual (rata-rata 8.7 detik), dengan uji paired t-test menghasilkan p=0.00169 dan effect size besar (Cohen's d=1.395). Temuan ini mendukung hipotesis bahwa sistem informasi pengarsipan digital dapat mempercepat proses pencarian dokumen secara signifikan, baik secara statistik maupun praktis.

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis "tentang" riset berarti sekadar melaporkan apa yang dilakukan secara berurutan — seperti diary ("saya membuat sistem, lalu saya uji, hasilnya bagus"). Menulis sebagai "argumen" berarti setiap bagian saling mendukung satu klaim utama dan menjawab pertanyaan yang dipicu bagian sebelumnya — dari masalah (pencarian manual lambat) ke gap (belum ada bukti kuantitatif untuk sistem skala kecil) ke RQ ke metode yang dirancang khusus menjawab RQ itu ke hasil yang langsung relevan ke RQ ke kesimpulan yang menutup argumen. Latihan 1 (outline) membuat saya sadar bahwa Method saya harus ditulis supaya jelas terhubung ke RQ, bukan cuma daftar teknologi yang dipakai.
>
> Urutan penulisan Method → Discussion → Introduction awalnya terasa aneh (biasanya saya nulis Introduction dulu), tapi setelah dipikir ulang ini masuk akal: saya baru benar-benar tahu apa yang "layak dijanjikan" di Introduction setelah tahu apa yang sungguh saya temukan di Results dan Discussion. Kalau Introduction ditulis duluan sebelum eksperimen selesai, ada risiko saya menjanjikan sesuatu yang ternyata tidak konsisten dengan temuan aktual (seperti masalah "RQ2 hilang di Discussion" pada contoh consistency matrix di atas) — menulis Introduction terakhir justru membuat argumen jadi lebih koheren dan jujur terhadap data.

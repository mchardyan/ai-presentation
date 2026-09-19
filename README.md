# ai-presentation
Claude Skill to Create Powerpoint Presentation Specialized for Thesis Defense (Sidang Skripsi) or Pitch Deck Proposal (Optimized for Claude Free, 8-10 slides)

# Specialized for Bahasa Indonesia/Indonesian User
Skill ini bukan pengganti skill `pptx` bawaan, melainkan lapisan **konten dan strategi** di atasnya. `pptx` yang menangani mesin render (pptxgenjs, layout, validasi file), sedangkan `ai-presentation` yang menentukan apa isi tiap slide, urutan bagian, jumlah slide, sumber data yang boleh dipakai, dan gaya desain.

## Kapan Skill Ini Terpicu

Otomatis dipakai Claude saat pengguna:
- Melampirkan naskah skripsi atau dokumen lain dan minta dirangkum jadi slide
- Minta dibuatkan pitch deck
- Minta dibuatkan presentasi produk
- Minta dibuatkan PPT/deck/slide/bahan sidang/bahan presentasi dalam bentuk apa pun

Tidak perlu menyebut kata ".pptx" secara eksplisit — cukup minta "buatkan slide dari skripsi ini" atau "buatkan pitch deck untuk startup saya".

## Tiga Mode Presentasi

| Mode | Struktur |
|---|---|
| **Skripsi (Sidang)** | Urutan tetap: Judul → Latar Belakang → Rumusan Masalah → Tujuan → Tinjauan Pustaka → Metode → Hasil → Pembahasan → Kesimpulan → Saran |
| **Presentasi Produk** | Alur umum ke detail: Judul → Masalah → Solusi → Fitur → Detail Teknis → Use Case → Perbandingan → Roadmap → Penutup |
| **Pitch Deck** | Naratif investor: Judul → Masalah → Solusi → Produk → Ukuran Pasar → Model Bisnis → Traksi → Kompetisi → Go-to-Market → Tim → Proyeksi → Ask |

Mode Skripsi urutannya kaku (tidak boleh diacak). Mode Produk dan Pitch Deck lebih fleksibel mengikuti brief pengguna.

## Aturan Sumber Data (Paling Ketat)

- **File skripsi**: hanya boleh pakai data, teori, dan kutipan yang sudah ada di dalam dokumen. Tidak menambah sumber luar apa pun kecuali diminta eksplisit oleh pengguna.
- **Produk & Pitch Deck**: boleh riset tambahan lewat web search, tapi seperlunya saja (misalnya ukuran pasar atau data kompetitor).
- **Semua sumber wajib bisa ditelusuri asal-usulnya.** Sumber yang tidak bisa dipastikan benar-benar ada tidak boleh dipakai sama sekali — lebih baik data lebih sedikit tapi valid.
- Estimasi harus ditandai jelas sebagai estimasi, tidak boleh disamarkan sebagai data resmi.
- Sumber data di pitch deck dicantumkan sebagai catatan kecil di slide atau di catatan bicara.

## Format Tiap Slide

Setiap slide punya dua lapis konten yang dipisah:
1. **Isi visual di slide** — judul singkat (maks ±8 kata) dan poin-poin padat yang dibaca audiens
2. **Narasi bicara** — kalimat penjelas lengkap di speaker notes (`addNotes`), sebagai panduan presenter saat bicara, tidak ditumpuk ke badan slide

## Layout & Kepadatan

- Sebagian besar slide isi memakai 2-3 kolom sejajar (bukan bullet list panjang ke bawah), dengan pola bervariasi antar slide: dua kolom teks, tiga kolom kartu, kolom tidak simetris, atau grid 2x2/2x3
- Minimal 8 slide, tanpa batas atas kaku — jumlah mengikuti kebutuhan isi
- Prioritas memadatkan isi lewat kolom daripada memecah ke banyak slide tipis, tanpa mengorbankan keterbacaan (body 12-16pt, margin minimal 0,5")

## Desain Minimalis

- Palet warna brand asli (dicari via web search) untuk produk/perusahaan yang sudah punya identitas visual; untuk skripsi atau topik tanpa brand, pilih dari palet di skill `pptx` sesuai nuansa topik
- Satu warna dominan (60-70%), maksimal satu aksen tajam, tanpa garis/strip dekoratif di tepi slide atau kartu
- Satu motif visual konsisten di semua slide

## QA Wajib Sebelum File Diserahkan

File final **tidak boleh** diserahkan selama masih ada:
- Elemen desain yang saling menimpa (teks menembus bentuk, kotak teks bertabrakan, ikon tertutup elemen lain)
- Bidang/shape yang saling bertumpuk (kartu, kotak warna, gambar, blok kolom berjarak < 0,3" atau saling menutup)
- Teks terpotong/meluap, kontras rendah, margin < 0,5", atau kolom tidak sejajar

Proses QA: render ke gambar per slide → cek satu per satu → perbaiki → render ulang slide yang berubah → ulangi sampai bersih → jalankan `markitdown` (cek isi) dan `validate.py` (cek keutuhan file) dari skill `pptx`.

## Dependensi

Skill ini bergantung pada skill `pptx` bawaan (pptxgenjs, markitdown, LibreOffice, validate.py) sebagai mesin pembuatan file. Pastikan skill `pptx` tersedia di sesi yang sama.

## Struktur File

```
ai-presentation/
├── SKILL.md   (instruksi lengkap yang dibaca Claude)
└── README.md  (dokumen ini, untuk referensi manusia)
```

---
name: ai-presentation
description: Membuat presentasi PowerPoint (.pptx) profesional, padat, dan siap pakai untuk sidang skripsi, pitch deck, presentasi produk, dan kebutuhan presentasi formal lainnya. Gunakan skill ini setiap kali pengguna melampirkan naskah skripsi atau dokumen lain dan meminta dirangkum jadi slide, meminta dibuatkan pitch deck, presentasi produk, atau PPT dalam bentuk apa pun (deck, slide, bahan sidang, bahan presentasi). Tidak perlu menyebut kata ".pptx" secara eksplisit. Skill ini mengatur struktur konten sesuai jenis presentasi (skripsi mulai Latar Belakang sampai Saran, produk dari umum ke detail, pitch deck naratif investor dengan data pendukung yang benar-benar terverifikasi), kepadatan slide (layout 2 sampai 3 kolom, compact, minimal 8 slide), skema warna minimalis, narasi bicara per slide, dan pengecekan desain sebelum file diserahkan. Pembuatan file .pptx-nya sendiri memakai skill pptx bawaan (pptxgenjs) sebagai mesin render.
---

# AI Presentation (Skripsi / Produk / Pitch Deck)

Skill ini adalah lapisan konten dan strategi presentasi di atas skill `pptx` bawaan. Skill `pptx` menangani detail teknis pptxgenjs (layout, gotcha, validasi file). Skill ini menentukan apa yang masuk ke tiap slide, urutan slide, berapa banyak slide, sumber data yang boleh dipakai, dan arahan desain supaya hasilnya langsung layak pakai tanpa banyak edit manual.

Selalu baca `/mnt/skills/public/pptx/SKILL.md` sebelum menulis kode pptxgenjs. Skill ini tidak menggantikan panduan teknis di sana. Soal warna hex, chart native, font aman, sampai QA visual, semua tetap ikuti skill `pptx`.

## Alur Kerja

1. **Kenali sumber dan jenis presentasi.** Jika pengguna melampirkan file (skripsi, brief produk, business plan), baca dulu isinya secara menyeluruh sebelum menyusun slide. Jangan menebak isi bab dari judul filenya saja. Tentukan salah satu dari tiga mode di bawah (Skripsi, Produk, atau Pitch Deck). Kalau ambigu, tanyakan singkat ke pengguna, jangan menebak sendiri di tengah proses.
2. **Rangkum per bagian sumber**, bukan per kalimat. Ambil argumen inti, data kunci, dan temuan penting tiap bab atau bagian. Buang detail yang tidak akan diucapkan saat presentasi.
3. **Tentukan boleh tidaknya menambah sumber luar** dengan aturan di [Aturan Sumber](#aturan-sumber) di bawah sebelum mencari data tambahan apa pun.
4. **Susun kerangka slide** sesuai struktur mode yang berlaku, tentukan jumlah slide total (lihat [Kepadatan dan Jumlah Slide](#kepadatan-dan-jumlah-slide)).
5. **Tulis isi tiap slide**, judul pendek, poin-poin visual di slide, dan narasi bicara terpisah (lihat [Format Tiap Slide](#format-tiap-slide)).
6. **Tentukan palet warna** (lihat [Desain Minimalis](#desain-minimalis-dan-warna)) sebelum mulai coding.
7. **Bangun file** dengan pptxgenjs mengikuti gotcha di skill `pptx`. Gunakan pola kolom di [Layout Kolom](#layout-kolom-2-sampai-3) untuk sebagian besar slide isi.
8. **QA wajib termasuk cek overlap** (lihat [QA Sebelum Menyerahkan File](#qa-sebelum-menyerahkan-file)). Jangan pernah menyerahkan file final selama masih ada elemen atau bidang yang bertumpuk.
9. Simpan ke `/mnt/user-data/outputs/` dan sajikan filenya ke pengguna.

## Aturan Sumber

Ini aturan yang paling ketat di skill ini, jangan dilanggar demi terlihat lebih meyakinkan atau lebih lengkap.

- **Kalau file yang dilampirkan adalah naskah skripsi**, cukup gunakan data, teori, kutipan, dan angka yang sudah ada di dalam dokumen itu. Jangan menambahkan sumber luar apa pun (jurnal lain, statistik lembaga, berita) kecuali pengguna secara eksplisit meminta ditambahkan. Tugas skill di sini adalah merangkum, bukan memperkaya isi skripsi dengan sumber baru yang belum pernah diuji dosen pembimbing.
- **Untuk mode Produk dan Pitch Deck**, boleh mencari data pendukung lewat web search, tapi hanya seperlunya untuk mengisi bagian yang memang butuh data eksternal (misalnya ukuran pasar atau perbandingan kompetitor). Jangan menambahkan sumber luar untuk bagian yang isinya sudah cukup dari brief pengguna sendiri.
- **Setiap sumber yang mau dipakai harus diverifikasi dulu asal usulnya.** Kalau tidak bisa dipastikan sumber itu benar-benar ada dan datang dari lembaga, situs, atau publikasi yang bisa ditelusuri (bukan hasil karangan atau sitasi yang terdengar meyakinkan tapi tidak bisa ditemukan linknya), sumber itu tidak boleh dipakai sama sekali. Lebih baik slide memuat lebih sedikit data yang benar daripada data lengkap yang tidak bisa dipertanggungjawabkan.
- Kalau data yang dibutuhkan tidak ditemukan dari sumber yang bisa diverifikasi, sampaikan itu ke pengguna dan tanyakan apakah mau memakai estimasi yang ditandai jelas sebagai estimasi, atau melewati bagian itu. Jangan pernah menyamarkan estimasi sebagai data resmi.
- Untuk data yang dipakai di pitch deck, cantumkan sumbernya sebagai catatan kecil di slide atau di catatan bicara, contohnya "Sumber, nama lembaga, tahun".

## Tiga Mode Presentasi

### 1. Skripsi (Sidang)

Urutan slide tetap, tidak boleh diacak atau dihilangkan bagiannya kecuali pengguna secara eksplisit minta dipangkas.

1. **Judul**, judul skripsi, nama, NIM, program studi, pembimbing (jika ada di naskah)
2. **Latar Belakang**, masalah atau fenomena yang mendasari penelitian, kenapa penting
3. **Rumusan Masalah**, pertanyaan penelitian, ditulis ringkas dan tajam
4. **Tujuan Penelitian**
5. **Tinjauan Pustaka**, teori dan konsep kunci serta penelitian terdahulu yang relevan, bukan seluruh bab 2
6. **Metode Penelitian**, pendekatan, populasi atau sampel atau informan, teknik pengumpulan dan analisis data
7. **Hasil Penelitian**, temuan utama, gunakan tabel atau grafik dari data skripsi jika ada
8. **Pembahasan**, interpretasi hasil dikaitkan ke teori dan rumusan masalah
9. **Kesimpulan**
10. **Saran**, untuk penelitian lanjutan dan atau praktis

Boleh menggabungkan Kesimpulan dan Saran jadi satu slide bila keduanya singkat. Boleh memecah Hasil atau Pembahasan jadi dua slide bila datanya banyak, itu tidak melanggar urutan, hanya menambah slide di dalam bagian yang sama.

### 2. Presentasi Produk

Alur sistematis, dari umum ke detail, biasanya:

1. Judul atau nama produk
2. Masalah yang dijawab (konteks umum)
3. Solusi atau gambaran produk secara umum
4. Fitur utama (breakdown, mulai mengerucut)
5. Detail teknis dan spesifikasi tiap fitur unggulan
6. Use case atau skenario penggunaan konkret
7. Perbandingan dengan alternatif (jika relevan)
8. Roadmap atau langkah selanjutnya
9. Penutup atau call to action

Sesuaikan jumlah dan urutan persis dengan brief pengguna. Kerangka ini adalah default, bukan aturan kaku seperti mode Skripsi.

### 3. Pitch Deck

Naratif sistematis dan detail, ditujukan ke investor:

1. Judul dan tagline satu kalimat
2. Masalah, didukung data pasar nyata
3. Solusi
4. Produk atau demo singkat
5. Ukuran pasar (TAM, SAM, SOM), wajib bersumber, jangan mengarang angka
6. Model bisnis, cara menghasilkan uang
7. Traksi (metrik, milestone, pilot, LOI) jika tersedia dari pengguna
8. Kompetisi dan keunggulan kompetitif
9. Go to market strategy
10. Tim
11. Proyeksi finansial ringkas
12. Ask (dana yang diminta) dan rencana penggunaan dana

Semua data eksternal di bagian ini tunduk pada [Aturan Sumber](#aturan-sumber) di atas.

## Format Tiap Slide

Setiap slide isi (bukan judul atau penutup) punya dua lapis konten yang dipisah, jangan dicampur.

1. **Isi visual di slide**, judul slide singkat dan menarik (maksimal kira-kira delapan kata, bukan kalimat lengkap), lalu poin-poin padat berupa frasa singkat, angka, atau kalimat pendek. Ini yang dibaca audiens.
2. **Narasi bicara**, kalimat penjelas yang lebih lengkap tentang apa yang diucapkan presenter saat slide itu tampil. Taruh ini di speaker notes lewat `slide.addNotes("...")` (lihat skill `pptx`), bukan sebagai teks tambahan di badan slide, supaya slide tetap bersih tapi pengguna tetap punya panduan bicara saat membuka Presenter View. Tulis narasi ini mengalir seperti orang bicara di depan penguji atau audiens, bukan mengulang persis poin-poin di slide.

Judul slide tidak boleh generik. "Latar Belakang" polos boleh dipakai untuk skripsi karena memang nama bagian formal, tapi untuk produk dan pitch deck judul harus mencerminkan isi, misalnya "Pasar Senilai Rp2,1 Triliun dan Terus Tumbuh" alih-alih "Ukuran Pasar".

## Layout Kolom (2 sampai 3)

Sebagian besar slide isi memakai dua atau tiga kolom sejajar, bukan satu blok bullet panjang ke bawah. Ini yang membuat slide terasa padat tapi tetap rapi dan mengurangi jumlah slide yang dibutuhkan.

Pola yang bisa dipakai bergantian antar slide (jangan pakai pola yang sama di semua slide):
- **Dua kolom teks sejajar**, misalnya Rumusan Masalah di kiri dan Tujuan di kanan, atau Sebelum dan Sesudah, atau Kelebihan dan Kelemahan.
- **Tiga kolom kartu pendek**, tiap kolom berisi ikon atau angka kecil di atas, judul mini bold, dua sampai tiga baris penjelasan. Cocok untuk fitur produk, tahapan metode, atau tiga temuan utama.
- **Dua kolom tidak simetris**, teks di satu sisi (sekitar 60 persen lebar), tabel, grafik, atau gambar di sisi lain (sekitar 40 persen), atau sebaliknya.
- **Grid 2x2 atau 2x3** untuk kombinasi tabel data dan penjelasan.

Bangun kolom dengan beberapa `addText` atau `addShape` yang koordinat x-nya dihitung eksplisit (bagi lebar slide dikurangi margin dan jarak antar kolom, lalu dibagi jumlah kolom). Jangan andalkan tabel pptxgenjs untuk tata letak kolom teks bebas, pakai `addTable` hanya untuk data tabular sungguhan.

## Kepadatan dan Jumlah Slide

- Minimal delapan slide, tapi tidak ada batas atas kaku. Jumlah mengikuti kebutuhan isi sumber. Untuk skripsi dengan lima bab yang wajar, umumnya jatuh di sekitar sepuluh sampai empat belas slide karena mengikuti struktur wajib di atas.
- Prioritaskan memadatkan isi ke dalam satu slide lewat layout kolom di atas daripada memecah jadi banyak slide tipis. Satu slide boleh memuat tiga sampai enam poin per kolom asal ukuran font dan margin tetap mengikuti batas aman di skill `pptx` (body 14 sampai 16pt, margin minimal 0,5 inci). Kepadatan tinggi tidak boleh mengorbankan keterbacaan atau menyebabkan teks terpotong. Kalau isi sungguh tidak muat tanpa memperkecil font di bawah ambang aman, pecah jadi slide lanjutan, jangan dipaksakan.
- Body text boleh sedikit lebih kecil dari rentang default (turun ke 12 sampai 13pt) khusus untuk slide berdensitas tinggi seperti Tinjauan Pustaka atau Hasil, tapi tetap jaga kontras dan jarak antar blok minimal 0,3 inci.

## Desain Minimalis dan Warna

- Kalau presentasi produk atau pitch deck untuk brand atau perusahaan yang sudah punya identitas visual nyata, cari tahu dulu warna resminya (web search logo atau brand guideline perusahaan tersebut) dan pakai itu sebagai palet utama.
- Kalau tidak ada brand spesifik (termasuk untuk skripsi), pilih satu palet dari tabel palet di skill `pptx` (bagian Design Ideas, Color Palettes) yang paling sesuai nuansa topik. Misalnya topik riset komunikasi atau media bisa cocok dengan palet biru gelap tenang atau charcoal minimal, topik bisnis yang enerjik bisa pakai palet dengan aksen tajam.
- Prinsip minimalis yang wajib dipegang, satu warna dominan (60 sampai 70 persen), maksimal satu warna aksen tajam, background putih atau warna gelap solid (hindari krem atau beige default), tidak ada garis aksen di bawah judul, tidak ada strip warna dekoratif di tepi slide atau kartu. Cukup gunakan whitespace, kartu dengan tint lembut, atau bayangan tipis untuk memisahkan blok.
- Konsisten pakai satu motif visual di semua slide, misalnya ikon selalu dalam lingkaran berwarna, atau garis pembatas kolom dengan gaya sama. Jangan ganti gaya kartu tiap slide.

## QA Sebelum Menyerahkan File

Ini langkah yang tidak boleh dilewati. File final tidak boleh diserahkan ke pengguna kalau salah satu masalah di bawah masih ditemukan.

1. Render presentasi ke gambar per slide (ikuti cara di skill `pptx`, bagian Converting to Images) dan periksa satu per satu.
2. **Cek elemen desain yang saling menimpa (overlap).** Perhatikan teks yang menembus bentuk atau gambar, dua kotak teks yang bertabrakan, ikon yang tertutup elemen lain, atau garis yang memotong tulisan. Kalau ditemukan, perbaiki koordinat atau ukuran elemen yang bermasalah sebelum lanjut.
3. **Cek bidang atau shape yang saling bertumpuk (overlapping).** Ini termasuk kartu, kotak warna, gambar, dan blok kolom yang jaraknya kurang dari 0,3 inci atau posisinya saling menutup sebagian. Kalau ditemukan, geser atau kecilkan bidang yang bertumpuk sampai semua elemen punya ruang sendiri.
4. Cek juga hal standar dari skill `pptx`, teks yang terpotong atau meluap dari kotaknya, kontras rendah, margin kurang dari 0,5 inci dari tepi slide, dan kolom yang tidak sejajar.
5. Kalau ada perbaikan, render ulang hanya slide yang diubah dan periksa lagi sampai bersih.
6. Jalankan `markitdown` untuk cek isi (tidak ada placeholder atau teks generik yang tersisa) dan `scripts/office/validate.py` untuk cek keutuhan file.
7. Baru setelah semua langkah di atas bersih, simpan file final dan sajikan ke pengguna.

## Ringkasan ke Pengguna

Sebelum menutup, sampaikan ke pengguna secara singkat, jumlah slide akhir, mode yang dipakai, palet warna yang dipilih beserta alasan singkatnya, dan apakah ada sumber eksternal yang ditambahkan atau tidak (khusus untuk file skripsi, tegaskan kalau seluruh isi hanya berasal dari dokumen yang dilampirkan).

# data analyst competititon
# Data Analyst Competition 2025

Project analisis sentimen komentar/review pengguna terhadap enam aplikasi AI chatbot: **GPT, Claude, Gemini, DeepSeek, Grok, dan Perplexity**.

## Struktur Folder

```
Data-Analyst/
└── sort/
    ├── cleaning.r              # Pembersihan data (missing value, duplikat, standarisasi teks)
    ├── sort.r                  # Sorting data, deteksi bahasa, dan klasifikasi sentimen
    ├── finalization             # Output akhir hasil sorting (sort_sample)
    └── tempCodeRunnerFile.r     # File draft/scratch dari proses eksplorasi awal
```

## Alur Kerja

1. **Load Data** — Membaca `sample_submission.csv` beserta data `Test/` dan `Train/` untuk masing-masing model AI (gpt, claude, gemini, deepseek, grok, perplexity), lalu digabungkan ke dalam list `df_test` dan `df_train`.

2. **Cleaning (`cleaning.r`)**
   - Cek struktur/tipe data (`str()`)
   - Cek dan hapus *missing value* (`na.omit`)
   - Cek dan hitung data duplikat
   - Standarisasi teks (`trimws()` pada kolom `Comment`)
   - Buang baris dengan bahasa yang gagal terdeteksi (`Language == NA`)

3. **Sorting & Klasifikasi (`sort.r`)**
   - Sorting data berdasarkan `Sentiment`, serta berdasarkan `At` (tanggal) dan `AppVersion`
   - Deteksi bahasa komentar menggunakan package `cld3`
   - Tokenisasi komentar (`tidytext::unnest_tokens`) dan analisis sentimen dengan leksikon **Bing**, ditambah leksikon kustom untuk kata non-Inggris (`badiya`, `achcha`, `ভালো`)
   - Klasifikasi tiap komentar menjadi **positif / negatif / netral** berdasarkan proporsi kata positif dan negatif (`prop_pos >= 0.3` → positif, `prop_neg >= 0.3` → negatif, selain itu netral)

## Package R yang Digunakan

| Package | Kegunaan |
|---|---|
| `readr` | Membaca file CSV |
| `dplyr` | Manipulasi data |
| `tidyverse` | Kumpulan tools data wrangling |
| `tidytext` | Tokenisasi teks & analisis sentimen |
| `cld3` | Deteksi bahasa otomatis |

## Cara Menjalankan

1. Sesuaikan path file CSV (saat ini masih menunjuk ke direktori lokal `C:/Users/.../Downloads/data-analysis-competition-2025/...`) dengan lokasi data di perangkat Anda.
2. Install package yang dibutuhkan:
   ```r
   install.packages(c("readr", "cld3", "dplyr", "tidytext", "tidyverse"))
   ```
3. Jalankan `cleaning.r` terlebih dahulu untuk membersihkan data, lalu `sort.r` untuk sorting, deteksi bahasa, dan klasifikasi sentimen.

## Catatan

- File `tempCodeRunnerFile.r` merupakan hasil eksperimen sementara dan berisi duplikasi logika dari `cleaning.r` serta `sort.r` — bisa diabaikan atau dihapus jika tidak diperlukan lagi.
- Path dataset saat ini masih hardcoded ke direktori lokal salah satu anggota tim; sebaiknya diganti dengan path relatif agar script portable.

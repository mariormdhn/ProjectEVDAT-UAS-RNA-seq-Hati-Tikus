# Analisis Eksplorasi Data RNA-seq Hati Tikus (*Mus musculus*)
### Dataset GEO GSE326527 — Infeksi Murine Norovirus CR6

> **Mata Kuliah:** Analisis Eksplorasi dan Visualisasi Data  
> **Program Studi:** Bioinformatika — Institut Pertanian Bogor (IPB University)

---

## Anggota Kelompok

| No | Nama |
|:--:|:-----|
| 1  | Mario Ilham Ramadhan |
| 2  | Rakazaki Putra Hendrawan |
| 3  | Tri Setyo Agus Wibowo |
| 4  | M Haedar Rafli A |

---

## 📌 Deskripsi Proyek

Proyek ini melakukan **analisis eksplorasi dan visualisasi data** pada dataset RNA-seq publik dari NCBI GEO (**GSE326527**). Dataset ini berisi data ekspresi gen dari jaringan hati (*liver*) tikus *Mus musculus* yang terinfeksi **murine norovirus strain CR6** selama **5 hari pasca infeksi (5 dpi)**.

Tujuan utama analisis adalah mengeksplorasi apakah terdapat **perbedaan pola ekspresi gen global** antara dua kelompok eksperimen:

- **STAT1Het** — tikus heterozygous (STAT1 masih fungsional, digunakan sebagai kontrol)
- **STAT1KO** — tikus knockout (STAT1 tidak aktif / dihilangkan)

**STAT1** (*Signal Transducer and Activator of Transcription 1*) adalah protein kunci dalam jalur pensinyalan interferon yang berperan penting dalam respons imun terhadap infeksi virus.

---

## 📁 Struktur Repository

```
.
├── ProjectUAS.Rmd                  # Skrip analisis utama (R Markdown)
├── ProjectUAS.html                 # Output HTML hasil knit (opsional)
├── GSE326527_expression_data.csv   # Dataset ekspresi gen (unduh dari GEO)
└── README.md                       # Dokumentasi proyek ini
```

> ⚠️ **Catatan:** File `GSE326527_expression_data.csv` tidak disertakan dalam repository karena ukurannya. Lihat bagian [Cara Mendapatkan Data](#-cara-mendapatkan-data) di bawah.

---

## 🧪 Desain Eksperimen

| Parameter | Detail |
|:----------|:-------|
| Organisme | *Mus musculus* (tikus rumah) |
| Jaringan | Liver (hati) |
| Perlakuan | Infeksi murine norovirus strain CR6 |
| Waktu pengamatan | 5 hari pasca infeksi (5 dpi) |
| Jumlah sampel | 10 total (5 Het + 5 KO) |
| Platform | RNA-seq |

---

## 🔬 Tahapan Analisis

```
1. Data Loading & Cleaning
   ├── Penanganan missing gene symbols
   ├── Seleksi kolom sampel liver
   └── Filter gen ekspresi rendah (mean ≤ 10)

2. Eksplorasi Data
   └── Statistik deskriptif per sampel

3. Visualisasi Distribusi
   ├── Boxplot raw counts
   └── Histogram raw counts per sampel

4. Transformasi Log2 [log2(x+1)]
   ├── Boxplot post-transformasi
   └── Histogram post-transformasi

5. Analisis Korelasi
   ├── Matriks korelasi Pearson
   └── Correlation heatmap

6. Seleksi Top Variable Genes
   └── 20 gen dengan variansi tertinggi

7. Principal Component Analysis (PCA)
   ├── Scree plot
   ├── Score plot (PC1 vs PC2)
   └── PCA dengan confidence ellipse 95%

8. Hierarchical Clustering
   └── Dendrogram (Euclidean + Ward.D2)

9. Heatmap
   └── Top 20 variable genes (row z-score)
```

---

## ⚙️ Requirements

### Package yang Dibutuhkan

```r
install.packages(c(
  "readr",
  "dplyr",
  "tidyr",
  "tibble",
  "ggplot2",
  "corrplot",
  "pheatmap",
  "RColorBrewer",
  "factoextra"
))
```

---

## 📥 Cara Mendapatkan Data

1. Kunjungi halaman dataset di NCBI GEO:  
   👉 https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE326527

2. Unduh file ekspresi gen (biasanya berformat `.csv` atau `.txt.gz`)

3. Simpan file dengan nama `GSE326527_expression_data.csv` di direktori yang sama dengan `ProjectUAS.Rmd`

---

## 📊 Ringkasan Hasil

| Analisis | Temuan Utama |
|:---------|:-------------|
| **Kualitas Data** | Tidak ada missing value; detection rate konsisten antar sampel |
| **Distribusi** | Data mentah *right-skewed*; transformasi log2 berhasil menormalkan distribusi |
| **Korelasi** | Korelasi Pearson antar sampel satu kelompok sangat tinggi (replikasi baik) |
| **PCA** | PC1 menangkap variansi terbesar; terdapat pemisahan kelompok Het vs KO |
| **Clustering** | Dendrogram mengelompokkan sampel konsisten dengan label kelompok |
| **Heatmap** | 20 gen tervariabel menunjukkan pola ekspresi berbeda antar kelompok |

**Kesimpulan:** Terdapat perbedaan pola ekspresi gen global yang konsisten antara kelompok **STAT1Het** dan **STAT1KO**, mengindikasikan peran penting STAT1 dalam memodulasi respons transkriptomik hati tikus terhadap infeksi murine norovirus.

---

## 📚 Referensi

- **Dataset:** GSE326527 — NCBI Gene Expression Omnibus (GEO)  
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE326527

---

<div align="center">
  <sub>Institut Pertanian Bogor (IPB University) · Program Studi Bioinformatika · 2026</sub>
</div>

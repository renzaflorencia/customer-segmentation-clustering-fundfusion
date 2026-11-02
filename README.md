# FundFusion Customer Segmentation (Clustering Analysis)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F79A3E?style=flat&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)

---

## 📌 Business Overview & Problem Statement

**FundFusion** adalah lembaga penyedia layanan keuangan yang menghadapi tantangan dalam menentukan strategi pemasaran produk perbankan yang tepat. Saat ini, perusahaan **belum memiliki strategi yang terarah** untuk menawarkan jenis produk keuangan (seperti Deposito, Kartu Kredit, Kredit Rumah, Kredit Kendaraan, dan Dana Tunai) yang sesuai dengan segmen calon nasabah.

Ketiadaan segmentasi ini berpotensi menurunkan efisiensi kampanye pemasaran dan tingkat konversi akuisisi nasabah baru maupun *cross-selling*.

---

## 🎯 Objectives

- **Segmentasi Nasabah:** Membangun model machine learning berbasis *unsupervised learning* (Clustering) untuk mengelompokkan pola kepemilikan produk berdasarkan profil demografi dan finansial nasabah.
- **Evaluasi Model:** Mencapai kualitas klaster yang optimal yang diukur melalui parameter evaluasi dengan target nilai **Silhouette Score > 0.7**.
- **Rekomendasi Strategis:** Mengidentifikasi karakteristik unik tiap segmen guna mendukung tim pemasaran (*Telemarketing*) dalam melakukan penawaran produk yang lebih personal dan relevan.

---

## 📊 Dataset Description

Dataset memuat **28,129 data nasabah** dengan 18 fitur yang mencakup informasi demografi, jalur akuisisi, lama menjadi nasabah (*vintage*), serta kepemilikan produk finansial.

### Data Dictionary

| Nama Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `GCIF` | Object / String | ID Unik Nasabah |
| `Area` | Categorical | Wilayah domisili nasabah (Jakarta, Bandung, Surabaya, Solo, Jogja, Bogor) |
| `Jalur_Pembukaan` | Categorical | Saluran pembukaan akun (Telemarketing, Aplikasi Digital, Cabang, Internet Banking) |
| `Vintage` | Categorical | Durasi menjadi nasabah (`< 1 Tahun`, `2 - 3 Tahun`, `> 4 Tahun`) |
| `Usia` | Numerical | Usia nasabah (dalam tahun) |
| `Jenis_Kelamin` | Categorical | Jenis kelamin (`Laki-laki`, `Perempuan`) |
| `Status_Perkawinan` | Categorical | Status pernikahan (`Belum Menikah`, `Menikah`, `Cerai`, `Janda/Duda`) |
| `Jumlah_Anak` | Numerical | Jumlah tanggungan anak |
| `Pendidikan` | Categorical | Tingkat pendidikan terakhir |
| `Produk_Tabungan` | Binary (0/1) | Indikator kepemilikan produk Tabungan |
| `Produk_Deposito` | Binary (0/1) | Indikator kepemilikan produk Deposito |
| `Produk_Kartu_Kredit` | Binary (0/1) | Indikator kepemilikan produk Kartu Kredit |
| `Produk_Kredit_Rumah` | Binary (0/1) | Indikator kepemilikan produk KPR |
| `Produk_Kredit_Kendaraan` | Binary (0/1) | Indikator kepemilikan produk Kredit Kendaraan |
| `Produk_Kredit_Dana_Tunai` | Binary (0/1) | Indikator kepemilikan produk Pinjaman Dana Tunai |
| `Total_Kepemilikan_Produk`| Numerical | Total kombinasi produk yang dimiliki nasabah |
| `Pendapatan_Tahunan` | Numerical | Estimasi pendapatan tahunan nasabah |
| `Total_Relationship_Balance`| Numerical | Total saldo hubungan perbankan nasabah |

---

## 🛠️ Data Preprocessing & Methodology

Metodologi pengerjaan yang diterapkan dalam *notebook* ini meliputi:

1. **Exploratory Data Analysis (EDA):**
   - Agregasi statistik deskriptif berdasarkan `Area`, `Vintage`, `Jalur_Pembukaan`, dan `Status_Perkawinan`.
   - Analisis distribusi demografi terhadap rata-rata penyerapan produk.

2. **Data Cleaning:**
   - Handling missing values (`Usia` memiliki ~4,045 nilai hilang yang ditangani dengan `dropna()`).
   - Deteksi dan penanganan *outlier* pada fitur numerik kontinu (`Usia`, `Pendapatan_Tahunan`, `Total_Relationship_Balance`) menggunakan pendekatan **Z-score** ($\vert{}Z\vert{} < 3$).

3. **Data Filtering & Subseting:**
   - Memfokuskan analisis khusus pada segmen nasabah akuisisi channel **Telemarketing** (sebanyak 8,653 sampel).

4. **Feature Engineering & Transformation:**
   - **One-Hot Encoding** pada variabel kategorikal (`Area`, `Jenis_Kelamin`, `Status_Perkawinan`, `Pendidikan`, `Vintage`).
   - **Feature Scaling** menggunakan `StandardScaler` untuk menyamakan skala pada variabel numerik.
   - **Multicollinearity Check:** Menghapus fitur berkolerasi tinggi ($r > 0.7$) guna menghindari redundansi pada pemodelan klaster.

5. **Experimental Dataset Splitting:**
   - **Experiment 0:** Seluruh fitur gabungan (Demografi + Finansial).
   - **Experiment 1:** Sub-kumpulan fitur Demografi saja.
   - **Experiment 2:** Sub-kumpulan fitur Kepemilikan Produk & Finansial saja.

---

## 🚀 How to Run

### Prerequisites
Pastikan pustaka Python berikut telah terinstal pada lingkungan kerja Anda:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn

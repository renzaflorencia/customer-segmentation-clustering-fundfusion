🏦 Customer Segmentation & Clustering for FundFusion

Proyek ini bertujuan untuk membantu bank **FundFusion** dalam merumuskan strategi penawaran produk yang tepat sasaran kepada calon nasabah melalui pendekatan *Unsupervised Learning* (Clustering) berdasarkan profil demografi dan finansial nasabah.

## Project Overview
- **Problem Statement:** Belum memiliki strategi yang tepat dalam menawarkan jenis produk yang sesuai dengan segmen nasabah.
- **Objective:** Membangun model *clustering* berdasarkan demografi dan kepemilikan produk layanan FundFusion dengan *Silhouette Score* yang optimal (> 0.7).
- **Dataset:** Berisi data demografi nasabah, jalur pembukaan akun, *vintage*, status perkawinan, pendapatan tahunan, hingga total kepemilikan produk.

## Tech Stack & Libraries
- **Language:** Python
- **Libraries:** Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn, SciPy

## Workflow / Tahapan Proyek
1. Data Cleaning & Preprocessing (Penanganan Missing Values & Outlier)
2. Data Filtering (Eksplorasi Jalur Pembukaan *Telemarketing*)
3. Feature Selection & Encoding (One-Hot Encoding untuk variabel kategorikal)
4. Standardisasi Data Numerik (`StandardScaler`)
5. Pengecekan Multikolinearitas (Korelasi antar fitur)
6. Model Clustering & Evaluasi

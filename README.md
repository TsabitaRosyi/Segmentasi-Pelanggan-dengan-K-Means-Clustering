# 📊 Segmentasi Pelanggan dengan K-Means Clustering
### Analisis Data Event Telkomsel Branch Surabaya Menggunakan Python

Proyek **Customer Segmentation menggunakan algoritma K-Means Clustering** untuk mengelompokkan pelanggan berdasarkan kontribusi omzet dan rasio aktivitas pelanggan. Analisis dilakukan menggunakan data event Telkomsel dengan tujuan mengidentifikasi karakteristik setiap segmen serta menghasilkan rekomendasi strategi pemasaran yang lebih efektif dan efisien.


---

## 🎯 Latar Belakang

Setiap wilayah operasional Telkomsel memiliki karakteristik pelanggan dan kontribusi bisnis yang berbeda. Perbedaan tersebut dapat dilihat dari tingkat aktivitas pelanggan serta besarnya omzet yang dihasilkan.

Pemahaman terhadap karakteristik tersebut diperlukan agar perusahaan dapat menentukan sasaran pasar dan strategi pemasaran yang lebih tepat.

Melalui proyek ini, dilakukan segmentasi pelanggan menggunakan algoritma **K-Means Clustering** dengan memanfaatkan dua variabel utama, yaitu:

- **Omzet Total (`OMSET TOTAL`)**: Menggambarkan kontribusi omzet yang dihasilkan.
- **Active Ratio (`ACTIVE RATIO`)**: Menggambarkan tingkat aktivitas pelanggan berdasarkan perbandingan jumlah pelanggan aktif terhadap total pelanggan.

Hasil clustering kemudian dianalisis untuk mengidentifikasi karakteristik setiap segmen dan menyusun rekomendasi strategi pemasaran berdasarkan kebutuhan masing-masing kelompok.

## 🎯 Tujuan Proyek

1. Mengidentifikasi karakteristik pelanggan berdasarkan kontribusi omzet dan tingkat aktivitas.
2. Mengelompokkan data pelanggan menggunakan algoritma K-Means Clustering.
3. Menentukan jumlah cluster optimal menggunakan Elbow Method.
4. Mengevaluasi kualitas hasil clustering menggunakan Silhouette Score dan Pseudo F-Statistic.
5. Mengidentifikasi potensi pasar berdasarkan wilayah operasional.
6. Menyusun rekomendasi strategi pemasaran yang sesuai dengan karakteristik setiap segmen.

---

## 📂 Dataset

Dataset yang digunakan merupakan data event Telkomsel yang mencakup beberapa wilayah operasional, yaitu Bali Nusra, Jawa Tengah-DIY, dan Jawa Timur.

**Informasi Dataset:**

| Keterangan | Detail |
|---|---|
| Nama File | `output_EVENTS_alls.csv` |
| Lokasi File | `data/output_EVENTS_alls.csv` |
| Format | CSV |
| Delimiter | Semicolon (`;`) |
| Jumlah Data | 1.071 baris |
| Cakupan Wilayah | Bali Nusra, Jateng-DIY, dan Jatim |

**Variabel dalam Dataset**

Dataset memiliki beberapa variabel yang berkaitan dengan informasi geografis, aktivitas pelanggan, dan performa bisnis.

| Kategori | Variabel |
|---|---|
| Geografis | `AREA`, `REGIONAL`, `BRANCH`, `CLUSTER`, `CITY` |
| Aktivitas Pelanggan | `DS TOTAL`, `DS ACTIVE`, `DS RATIO (%)` |
| Omzet | `OMSET TOTAL`, `OMSET DATA`, `OMSET DIGITAL`, `OMSET RECHARGE` |
| Aktivitas Event | `PLAN/ACTUAL POI`, `PLAN/ACTUAL EVENT`, `ACTUAL CALL (%)` |
| Aktivitas Penjualan | `SALES`, `OTA`, `SALES ORBIT`, `VF`, `TRX DIGITAL` |

**Variabel Utama untuk Clustering**

Dua variabel yang digunakan dalam proses pembentukan cluster adalah:

1. `OMSET TOTAL`
   - Mengukur total kontribusi omzet.
   - Digunakan untuk mengidentifikasi kelompok dengan kontribusi omzet rendah maupun tinggi.

2. `ACTIVE RATIO`
   - Mengukur tingkat aktivitas pelanggan.
   - Dihitung menggunakan perbandingan jumlah pelanggan aktif terhadap jumlah total pelanggan.

Rumus perhitungan:

```python
ACTIVE RATIO = DS ACTIVE / DS TOTAL
```

Variabel tersebut digunakan untuk membentuk segmentasi berdasarkan kombinasi tingkat aktivitas pelanggan dan kontribusi omzet.

---

## ⚙️ Metodologi dan Workflow

Proyek ini dilakukan melalui beberapa tahapan analisis data sebagai berikut.

### 1. Data Loading dan Data Preprocessing

Tahap awal dilakukan dengan membaca dataset dan mempersiapkan data sebelum proses analisis.

Proses yang dilakukan:
- Membaca dataset CSV menggunakan delimiter `;`.
- Menghapus kolom yang tidak diperlukan, yaitu `OMSET TOTAL.1`.
- Menangani missing values dengan mengganti nilai NaN menjadi 0.
- Menghapus data duplikat.
- Membuat variabel baru `ACTIVE RATIO` berdasarkan perbandingan `DS ACTIVE` dan `DS TOTAL`.

### 2. Outlier Detection dan Handling

Dilakukan identifikasi nilai ekstrem yang berpotensi memengaruhi hasil clustering.

Metode yang digunakan:
- **Interquartile Range (IQR)** untuk mendeteksi outlier.
- **Winsorization** untuk menangani nilai ekstrem dengan membatasi nilai berdasarkan batas tertentu.

Tahapan ini bertujuan mengurangi pengaruh nilai ekstrem terhadap proses pembentukan cluster.

### 3. Exploratory Data Analysis (EDA)

Analisis eksploratif dilakukan untuk memahami karakteristik dan distribusi data berdasarkan wilayah operasional.

Analisis meliputi:
- Distribusi data berdasarkan regional.
- Distribusi data berdasarkan branch.
- Distribusi data berdasarkan cluster wilayah.
- Eksplorasi hubungan antara omzet total dan rasio aktivitas pelanggan.

### 4. Data Standardization

Sebelum proses clustering, variabel yang digunakan perlu memiliki skala yang sebanding.

Metode yang digunakan adalah **StandardScaler** dari Scikit-learn.

Variabel yang distandarisasi:
- `OMSET TOTAL`
- `ACTIVE RATIO`

Standardisasi dilakukan agar perbedaan skala antarvariabel tidak mendominasi perhitungan jarak dalam algoritma K-Means.

### 5. K-Means Clustering

Algoritma **K-Means Clustering** digunakan untuk mengelompokkan data berdasarkan kemiripan karakteristik.

Tahapan:
- Menentukan kandidat jumlah cluster menggunakan Elbow Method.
- Membentuk model K-Means dengan jumlah cluster terpilih.
- Melakukan pengelompokan berdasarkan variabel yang telah distandarisasi.
- Menambahkan label cluster pada setiap observasi.
- Mengidentifikasi centroid dan karakteristik masing-masing cluster.

### 6. Clustering Evaluation

Evaluasi dilakukan untuk mengetahui kualitas hasil pengelompokan.

Metrik evaluasi yang digunakan:
- Silhouette Score.
- Pseudo F-Statistic.

### 7. Customer Segmentation dan Marketing Strategy

Tahap akhir dilakukan dengan menganalisis profil setiap cluster berdasarkan rata-rata omzet dan rasio aktivitas pelanggan.

Hasil segmentasi digunakan sebagai dasar penyusunan rekomendasi strategi pemasaran untuk setiap kelompok.

---

## 📈 Hasil Analisis

### 1. Penentuan Jumlah Cluster — Elbow Method

Elbow Method digunakan untuk menentukan jumlah cluster yang optimal berdasarkan perubahan nilai Within-Cluster Sum of Squares (WCSS).

Berdasarkan hasil analisis, jumlah cluster yang digunakan adalah **3 cluster (k = 3)**.

<img width="859" height="547" alt="image" src="https://github.com/user-attachments/assets/6c686791-5213-4058-b745-3d7eef6270ee" />

### 2. Visualisasi Hasil Clustering

Visualisasi clustering digunakan untuk memperlihatkan distribusi data berdasarkan dua variabel utama, yaitu omzet total dan active ratio, serta posisi centroid masing-masing cluster.

<img width="846" height="547" alt="image" src="https://github.com/user-attachments/assets/4a91b49c-1a16-434a-86a5-bb325c673607" />

### 3. Profil Hasil Segmentasi Pelanggan

Berdasarkan hasil clustering, diperoleh tiga kelompok pelanggan dengan karakteristik yang berbeda.

| Cluster | Jumlah Data | Rata-rata Omzet Total | Rata-rata Active Ratio | Karakteristik |
|---|---:|---:|---:|---|
| 0 | 654 | ± Rp7,13 juta | 0,14 | Omzet rendah dan aktivitas rendah |
| 1 | 227 | ± Rp41,64 juta | 0,20 | Omzet tinggi (segmen premium) |
| 2 | 182 | ± Rp9,52 juta | 0,33 | Aktivitas tinggi, omzet rendah–menengah |
| **Total** | **1.063** | - | - | - |

**Interpretasi Setiap Cluster:**

- **Cluster 0 — Low Activity, Low Revenue**

  Kelompok dengan jumlah data terbesar. Memiliki tingkat aktivitas pelanggan dan kontribusi omzet yang relatif rendah. Segmen ini berpotensi menjadi target program peningkatan aktivitas dan reaktivasi pelanggan.

- **Cluster 1 — High Revenue / Premium Segment**

  Kelompok dengan rata-rata omzet tertinggi. Segmen ini menunjukkan kontribusi bisnis yang besar sehingga perlu dipertahankan melalui program loyalitas dan peningkatan kualitas layanan.

- **Cluster 2 — High Activity, Moderate Revenue**

  Kelompok dengan rasio aktivitas tertinggi, tetapi rata-rata omzet masih berada di bawah segmen premium. Segmen ini memiliki potensi untuk dikembangkan melalui penawaran produk dan program promosi yang mendorong peningkatan transaksi.

---

## 📊 Evaluasi Model

Evaluasi dilakukan untuk mengukur kualitas hasil segmentasi menggunakan metrik Silhouette Score dan Pseudo F-Statistic.

**Hasil Evaluasi:**

| Metrik | Hasil |
|---|---:|
| Jumlah Cluster | 3 |
| Silhouette Score | **0,5079** |

**Interpretasi Silhouette Score**

Silhouette Score sebesar **0,5079** menunjukkan bahwa hasil pengelompokan memiliki tingkat pemisahan dan kekompakan cluster yang cukup baik.

Nilai ini mengindikasikan bahwa data dalam setiap cluster relatif memiliki kemiripan karakteristik dan dapat dibedakan dari cluster lainnya.

---

## 💡 Rekomendasi Strategi Pemasaran

Hasil segmentasi dapat digunakan sebagai dasar untuk menentukan pendekatan pemasaran yang berbeda pada setiap kelompok pelanggan.

| Segmen | Karakteristik | Rekomendasi Strategi |
|---|---|---|
| Cluster 0 | Omzet rendah, aktivitas rendah | Reaktivasi melalui program promosi, penawaran produk yang relevan, dan pendekatan pemasaran untuk meningkatkan aktivitas pelanggan. |
| Cluster 1 | Omzet tinggi (premium) | Retensi pelanggan melalui program loyalitas, peningkatan kualitas layanan, serta penawaran eksklusif. |
| Cluster 2 | Aktivitas tinggi, omzet rendah–menengah | Penawaran khusus dan promosi produk untuk mendorong peningkatan transaksi serta kontribusi omzet. |

**Implikasi Bisnis**

Melalui segmentasi ini, perusahaan dapat:

1. Memprioritaskan program pemasaran berdasarkan karakteristik setiap segmen.
2. Mengidentifikasi wilayah dengan potensi peningkatan aktivitas pelanggan.
3. Mempertahankan pelanggan dengan kontribusi omzet tinggi.
4. Mengoptimalkan alokasi sumber daya pemasaran.
5. Menentukan pendekatan promosi yang lebih relevan berdasarkan kondisi masing-masing segmen.

---

## 🛠️ Teknologi dan Tools

Berikut teknologi dan library yang digunakan dalam proyek ini:

| Teknologi / Library | Penggunaan |
|---|---|
| Python | Bahasa pemrograman utama |
| Pandas | Data manipulation dan preprocessing |
| NumPy | Komputasi numerik |
| Scikit-learn | StandardScaler, K-Means, dan evaluasi clustering |
| SciPy | Analisis statistik dan pengolahan data |
| Matplotlib | Visualisasi data |
| Seaborn | Visualisasi statistik |
| Jupyter Notebook | Lingkungan pengembangan dan analisis |

---

## 📁 Struktur Repositori

Berikut struktur direktori proyek:

```text
.
├── data/
│   └── output_EVENTS_alls.csv
│
├── notebooks/
│   └── segmentasi_pelanggan_kmeans.ipynb
│
│
├── docs/
│   └── laporan_segmentasi_pelanggan.pdf
│
└── README.md
```

**Keterangan:**

- `data/` — Menyimpan dataset yang digunakan dalam analisis.
- `notebooks/` — Menyimpan Jupyter Notebook yang berisi tahapan preprocessing, EDA, clustering, dan evaluasi model.
- `docs/` — Menyimpan laporan lengkap proyek dalam format PDF.
- `README.md` — Dokumentasi utama proyek.

---

## 🚀 Cara Menjalankan Proyek

### 1. Clone Repository

```bash
git clone https://github.com/<username>/<nama-repository>.git
```

### 2. Masuk ke Direktori Proyek

```bash
cd <nama-repository>
```

### 3. Install Dependencies

Pastikan Python sudah terinstal, kemudian jalankan:

```bash
pip install -r requirements.txt
```

### 4. Jalankan Jupyter Notebook

```bash
jupyter notebook notebooks/segmentasi_pelanggan_kmeans.ipynb
```

### 5. Jalankan Analisis

Buka notebook dan jalankan setiap cell secara berurutan mulai dari tahap import library, data preprocessing, EDA, standardisasi, clustering, hingga evaluasi dan interpretasi hasil.

**Catatan:** Jalankan notebook dari direktori proyek atau sesuaikan working directory agar path dataset dapat terbaca dengan benar.

---

## 📌 Kesimpulan

Proyek ini menerapkan algoritma **K-Means Clustering** untuk melakukan segmentasi pelanggan berdasarkan dua indikator utama, yaitu kontribusi omzet total dan rasio aktivitas pelanggan.

Berdasarkan hasil analisis, diperoleh tiga segmen pelanggan dengan karakteristik berbeda:

1. Pelanggan dengan tingkat aktivitas dan omzet rendah.
2. Pelanggan dengan kontribusi omzet tinggi atau segmen premium.
3. Pelanggan dengan aktivitas tinggi tetapi kontribusi omzet relatif lebih rendah.

Dengan nilai **Silhouette Score sebesar 0,5079**, hasil clustering menunjukkan pemisahan kelompok yang cukup baik.

Hasil segmentasi ini dapat menjadi salah satu dasar pendukung pengambilan keputusan bisnis, khususnya dalam menentukan prioritas pemasaran, meningkatkan aktivitas pelanggan, mempertahankan pelanggan potensial, dan mengoptimalkan kontribusi omzet.

---

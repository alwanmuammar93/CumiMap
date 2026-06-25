# 🦑 CumiMap — Prediksi Zona Penangkapan Cumi-Cumi

Model Machine Learning untuk memprediksi zona potensial penangkapan cumi-cumi berdasarkan data oseanografi, dikembangkan sebagai proyek akademik di **Politeknik Negeri Ujung Pandang (PNUP)**.

---

## 📌 Deskripsi

CumiMap mengklasifikasikan wilayah laut ke dalam tiga zona tangkapan (**Tinggi / Sedang / Rendah**) menggunakan pendekatan unsupervised clustering (K-Means) dan supervised classification (Decision Tree + Random Forest).

---

## ⚙️ Teknologi

| Komponen | Detail |
|---|---|
| Bahasa | Python 3 |
| Platform | Google Colab |
| Clustering | K-Means (K=3) |
| Klasifikasi | Decision Tree + Random Forest |
| Library | scikit-learn, pandas, numpy, matplotlib, joblib |

---

## 🌊 Fitur Input (Oseanografi)

| Fitur | Keterangan |
|---|---|
| `latitude`, `longitude` | Koordinat lokasi tangkapan |
| `suhu_permukaan` | Suhu permukaan laut (°C) |
| `salinitas` | Kadar garam air laut |
| `kecepatan_arus` | Kecepatan arus laut (m/s) |
| `arah_arus` | Arah arus (derajat) |
| `klorofil_a` | Konsentrasi klorofil-a (mg/m³) |
| `tinggi_gelombang` | Tinggi gelombang laut (m) |
| `jam_tangkap` | Jam operasi penangkapan |
| `fase_bulan` | Fase bulan saat penangkapan |
| `hasil_tangkapan_kg` | Hasil tangkapan (kg) — basis label zona |

---

## 🔄 Alur Pipeline

```
Dataset CSV
    ↓
Step 1 : Load & Validasi Dataset
    ↓
Step 2 : Preprocessing & Feature Engineering
         (Clamp fisik → IQR capping → Encoding siklikal → RobustScaler + MinMaxScaler)
    ↓
Step 3 : K-Means Clustering (K=3) → Label Zona Tinggi / Sedang / Rendah
    ↓
Step 4 : Decision Tree → Seleksi Fitur Penting (threshold importance ≥ 0.05)
    ↓
Step 5 : Random Forest → Training & Evaluasi (class_weight='balanced')
    ↓
Step 6 : Export CSV hasil prediksi + Download model (.pkl)
```

---

## 📂 Output Model

| File | Keterangan |
|---|---|
| `cumimap_rf_model.pkl` | Model Random Forest |
| `cumimap_robust_scaler.pkl` | RobustScaler (fit pada train set) |
| `cumimap_scaler.pkl` | MinMaxScaler (fit pada train set) |
| `cumimap_kmeans.pkl` | Model K-Means clustering |
| `cumimap_hasil_prediksi.csv` | Hasil prediksi seluruh data |

---

## 🚀 Cara Menjalankan

1. Buka file di **Google Colab**:
   [https://colab.research.google.com](https://colab.research.google.com)

2. Upload file `modul_cumi_map 1.py` atau buka langsung notebook-nya

3. Jalankan setiap step secara berurutan (Step 1 → Step 6)

4. Saat Step 1 berjalan, upload file CSV dataset kamu

> ⚠️ **Catatan:** Project ini menggunakan `google.colab` library sehingga hanya bisa dijalankan di lingkungan Google Colab, bukan di PC lokal secara langsung.

---

## 📋 Format Dataset CSV

Pastikan file CSV kamu memiliki kolom berikut:

```
latitude, longitude, jam_tangkap, fase_bulan,
suhu_permukaan, salinitas, kecepatan_arus, arah_arus,
klorofil_a, tinggi_gelombang, hasil_tangkapan_kg
```

---

## 👤 Author

**Alwan Muammar** — Mahasiswa Politeknik Negeri Ujung Pandang (PNUP)  
GitHub: [@alwanmuammar93](https://github.com/alwanmuammar93)

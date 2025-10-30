# uts-machine-learning

## Struktur proyek
```
polynomial-property-prediction/
├── generated_dataset.csv
├── best_property_model.pkl
├── feature_scaler.pkl
├── model.ipynb                # Notebook utama (Colab)
├── requirements.txt
├── README.md
└── WRITTEN_ANALYSIS.md
```

## Jalankan proyek

### Install dependencies

```
pip install -r requirements.txt
```

### Jalankan di Google Colab / Jupyter:
- Buka model.ipynb
- Jalankan semua cell secara berurutan

### Membuat prediksi baru
Gunakan fungsi `predict_price(lt, lb, kt, umur, jarak)`

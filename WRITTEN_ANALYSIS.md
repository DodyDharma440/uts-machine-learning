# Written Analysis

## Excecutive summary hasil
Model polynomial regression berhasil dibangun untuk memprediksi harga properti berdasarkan generated dataset sebanyak 300 sampel. Setelah pelatihan dan evaluasi menyeluruh terhadap 35 model (berbagai kombinasi degree dan jenis regularisasi), model Lasso Regression dengan degree 5 dan alpha=1 terpilih sebagai model dengan R² test tertinggi (0.9674). Namun, model ini menunjukkan potensi overfitting. Model Linear Regression degree 2 memberikan keseimbangan terbaik antara akurasi dan kestabilan. Dengan Cross-Validation, model Ridge degree 2, alpha=1 terpilih sebagai model terbaik secara keseluruhan.

## Insight dari EDA
- Dataset memiliki hubungan non-linear yang jelas antara fitur seperti luas_bangunan dan harga, terlihat dari scatter plot yang melengkung.
- Korelasi antar fitur cukup realistis, misalnya luas_bangunan dan harga memiliki korelasi positif tinggi, sedangkan jarak_pusat dan harga memiliki korelasi negatif.
- Distribusi fitur dan target umumnya normal, tanpa missing values.
- Outlier dalam harga relatif sedikit dan tidak signifikan memengaruhi model.

## Perbandingan performa model
Dari tabel results_df, berikut adalah ringkasan performa beberapa model utama berdasarkan Test R² (tertinggi ke terendah)

| Degree | Model   | Alpha | Test R²   | Test RMSE | Catatan                                             |
|--------|---------|-------|-----------|-----------|-----------------------------------------------------|
| 5      | Lasso   | 1     | 0.9674    | 70.66     | R² Tertinggi, tapi Train RMSE = 46.14 → Overfitting |
| 4      | Lasso   | 1     | 0.9667    | 71.34     | -                                                   |
| 3      | Ridge   | 1     | 0.9665    | 71.58     | -                                                   |
| 2      | Ridge   | 1     | 0.9643    | 73.86     | Keseimbangan Bagus                                  |
| 2      | Linear  | N/A   | 0.9640    | 74.22     | -                                                   |
| 1      | Lasso   | 10    | 0.8656    | 143.38    | Underfitting                                        |
| 5      | Linear  | N/A   | -1.3414   | 598.43    | Sangat Overfit                                      |

- Degree 1: Performa rendah, underfitting.
- Degree 2 & 3: Performa tinggi dan stabil, optimal.
- Degree 4 & 5: R² tinggi, tetapi gap besar antara train dan test RMSE, menunjukkan overfitting, terutama pada model Linear.
- Lasso (terutama degree 5) mampu mencapai R² tertinggi, tetapi rentan overfit. Ridge lebih stabil.

## Rekomendasi degree polynominal terbaik
Degree 2 atau 3. Alasannya adalah sebagai berikut.
- Memberikan R² tinggi (0.964 - 0.967) tanpa overfitting yang parah.
- Jumlah fitur polynomial masih terkendali.
- Performa test set konsisten dan bagus.
- Degree 2 lebih sederhana dan lebih mudah diinterpretasikan.

## Rekomendasi regularization method terbaik
Ridge Regression (alpha = 1). Alasannya adalah:
- Menunjukkan kestabilan yang lebih baik dibandingkan Linear dan Lasso pada degree tinggi.
- Hasil Cross-Validation menunjukkan model Ridge degree 2, alpha=1 sebagai model terbaik secara keseluruhan (Mean R2 CV: 0.9609).
- Tidak menghilangkan fitur secara agresif seperti Lasso, yang mungkin mengorbankan informasi.

## Limitasi model
- Data yang sintetis atau rekayasa tidak merepresentasikan kompleksitas data dunia nyata.
- Overfitting pada degree tinggi seperti pada model dengan degree 4 dan 5 sangat sensitif terhadap noise dalam data pelatihan.
- Fitur terbatas yang tidak mempertimbangkan faktor-faktor lain seperti lokasi spesifik, fasilitas, atau tren pasar.
- Metode regresi linear tidak mampu menangkap pola kompleks yang mungkin lebih baik ditangani oleh model non-linear.

## Saran improvement
- Gunakan dataset real.
- Menambahkan fitur geografis atau kategori.
- Mencoba model non-linear lain seperti Random Forest.


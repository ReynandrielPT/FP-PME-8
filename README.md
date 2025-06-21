# Determinasi dan Penerapan Model Machine Learning untuk Deteksi Dini Tingkat Kecemasan Berbasis Gaya Hidup
## Final Project Machine Learning Kelas E Kelompok 8

| NRP         | Nama                             |
| ----------- | -------------------------------- |
| 5025231030  | I Gusti Ngurah Arya Sudewa       |
| 5025231087  | Justin Chow                      |
| 5025231113  | Reynandriel Pramas Thandya       |

## 📌 Tentang Proyek

Proyek ini mengatasi peningkatan signifikan gangguan kecemasan yang sering dikaitkan dengan tekanan akademik, tuntutan pekerjaan, dan paparan media sosial. Meskipun korelasi antara faktor gaya hidup (seperti kualitas tidur, aktivitas fisik, dan pola makan) dengan kesehatan mental telah banyak didokumentasikan, penerapan *machine learning* untuk deteksi dini, khususnya dalam konteks Indonesia, masih sangat terbatas.

Penelitian ini menyajikan perbandingan komprehensif dari sepuluh algoritma *machine learning* yang berbeda untuk memprediksi tingkat kecemasan berdasarkan kebiasaan gaya hidup. Tujuan utamanya adalah untuk mengidentifikasi kombinasi algoritma dan teknik penyeimbangan data yang paling efektif untuk menciptakan model deteksi dini kecemasan yang andal.

Hasil penelitian menunjukkan bahwa model *ensemble* berbasis pohon, khususnya **Random Forest**, yang dipadukan dengan teknik **Random Oversampling (ROS)**, memberikan performa tertinggi dengan mencapai **Akurasi 0,87** dan **Macro F1-Score 0,87**. Temuan ini menekankan pentingnya penanganan data yang tidak seimbang untuk membangun model prediksi yang akurat dalam bidang kesehatan mental.

## ✨ Fitur Utama & Rumusan Masalah

Proyek ini dirancang untuk menjawab beberapa pertanyaan berikut:

1.  **Performa Model Terbaik:** Di antara sepuluh model *machine learning* yang diuji, manakah yang menunjukkan performa terbaik dalam memprediksi kategori tingkat kecemasan berdasarkan data gaya hidup? 
2.  **Dampak Penyeimbangan Data:** Bagaimana dampak signifikan dari penerapan teknik penanganan data tidak seimbang (Random Oversampling, SMOTE, dan tanpa penyeimbangan) terhadap metrik evaluasi seperti Akurasi dan F1-Score? 
3.  **Kombinasi Optimal:** Manakah kombinasi spesifik antara model algoritma dan teknik penyeimbangan data yang menghasilkan solusi paling optimal dan dapat diandalkan untuk deteksi dini kecemasan? 

## 🛠️ Metodologi

Eksperimen ini disusun untuk mengevaluasi berbagai model dan strategi pra-pemrosesan secara sistematis.

### Dataset

* **Sumber:** Penelitian ini menggunakan dataset "Mental Health and Lifestyle Habits 2019-2024" dari Kaggle.
* **Fitur:** Dataset ini berisi 18 variabel demografis dan gaya hidup, termasuk `Age` (Usia), `Occupation` (Pekerjaan), `Sleep Hours` (Jam Tidur), `Physical Activity` (Aktivitas Fisik), `Caffeine Intake` (Asupan Kafein), `Family History of Anxiety` (Riwayat Kecemasan Keluarga), dan `Diet Quality` (Kualitas Diet).
* **Variabel Target:** Skor `Anxiety_Level` asli (dengan rentang 1-10) diubah menjadi lima kategori berbeda: `Very Low`, `Low`, `Medium`, `High`, dan `Very High` untuk membingkai masalah sebagai tugas klasifikasi multikelas.

### Model yang Dievaluasi

Sepuluh algoritma *supervised learning* dilatih dan dievaluasi:
1.  Decision Tree 
2.  Random Forest 
3.  K-Nearest Neighbors (KNN) 
4.  Logistic Regression 
5.  Gaussian Naive Bayes 
6.  Support Vector Machine (SVM) 
7.  Artificial Neural Network (ANN) 
8.  CatBoost 
9.  XGBoost 
10. LightGBM 

### Desain Eksperimen

Eksperimen ini dirancang untuk mengevaluasi performa berbagai model secara sistematis dengan langkah-langkah berikut:

#### 1. Pra-pemrosesan Data
Langkah-langkah pembersihan dan persiapan data yang dilakukan adalah sebagai berikut:
* **Imputasi *Missing Values*:** Nilai yang hilang diisi menggunakan rata-rata (*mean*) untuk fitur numerik dan modus (*mode*) untuk fitur kategorikal.
* ***Encoding* Fitur Kategorikal:** Fitur non-numerik (misalnya, 'Gender', 'Occupation') diubah menjadi angka menggunakan `LabelEncoder`.
* **Standardisasi Fitur Numerik:** Seluruh fitur numerik diskalakan menggunakan `StandardScaler` untuk menyamakan rentang nilainya, yang penting untuk beberapa model seperti SVM dan Regresi Logistik.

#### 2. Pembagian Data
Data dibagi menjadi **80% set pelatihan** dan **20% set pengujian**. Pembagian ini dilakukan secara **stratifikasi** berdasarkan kelas target untuk memastikan distribusi kelas yang proporsional di kedua set. Penggunaan `random_state=42` memastikan bahwa hasil eksperimen ini dapat direproduksi kembali.

#### 3. Strategi Penyeimbangan Kelas
Untuk mengatasi potensi bias akibat ketidakseimbangan kelas, tiga skenario berbeda dievaluasi **hanya pada data pelatihan**:
* **Tanpa Balancing (`None`):** Model dilatih pada data asli sebagai *baseline* untuk perbandingan.
* **Random Over-Sampling (`ROS`):** Sampel dari kelas-kelas minoritas diduplikasi secara acak untuk menyeimbangkan distribusi data.
* **SMOTE:** Sampel sintetis baru dibuat untuk kelas-kelas minoritas. Teknik ini bertujuan untuk menciptakan batas keputusan yang lebih jelas dan robus antar kelas.

### Metrik Evaluasi

Kinerja model dinilai menggunakan metrik berikut:
* **Akurasi:** Proporsi prediksi yang benar dari total sampel.
* **Macro F1-Score:** Rata-rata F1-Score dari setiap kelas tanpa pembobotan, yang sangat penting untuk mengevaluasi kinerja pada dataset yang tidak seimbang.
* **Confusion Matrix:** Untuk menganalisis kinerja model dan pola kesalahan pada setiap kelas secara kualitatif.

## 📊 Hasil

### Ringkasan Performa

* **Tanpa Penyeimbangan:** Berlawanan dengan ekspektasi umum, model-model yang dilatih pada data asli yang tidak seimbang justru menunjukkan kinerja terbaik. Model seperti Regresi Logistik dan Gaussian Naive Bayes mampu mencapai skor Akurasi dan Macro F1 yang solid, menunjukkan bahwa data asli sudah cukup informatif.

* **Dengan Penyeimbangan:** Penerapan teknik *oversampling* (ROS dan SMOTE) secara konsisten terbukti kontra-produktif. Hampir semua model, termasuk model *ensemble* berbasis pohon (Random Forest, XGBoost, CatBoost, LightGBM), mengalami penurunan kinerja. Hal ini mengindikasikan bahwa penambahan sampel sintetis atau duplikat justru memperkenalkan *noise* dan merusak pola yang ada.

* **Fenomena Koreksi Berlebih:** Analisis *confusion matrix* menunjukkan bahwa penurunan performa ini seringkali disebabkan oleh fenomena 'koreksi berlebih' (*overcorrection*), di mana usaha untuk memperbaiki bias pada kelas minoritas justru menciptakan kebingungan baru yang signifikan pada kelas mayoritas.

### Model Pemenang

Kombinasi yang paling efektif adalah **Regresi Logistik** yang **tanpa menggunakan metode balancing**.

* **Akurasi:** **0,64**
* **Macro F1-Score:** **0,63**

Konfigurasi ini menunjukkan kemampuan superior dalam memanfaatkan struktur data asli tanpa distorsi dari teknik *oversampling*. Kinerjanya yang tinggi menegaskan bahwa pada dataset ini, pemilihan model yang tepat lebih krusial daripada modifikasi distribusi data itu sendiri.

## 🚀 Kesimpulan

Penelitian ini menegaskan bahwa strategi penanganan data harus dievaluasi secara cermat untuk setiap kasus dan tidak bisa digeneralisasi. Kesimpulan utamanya adalah bahwa untuk dataset ini, **penanganan ketidakseimbangan kelas dengan metode *oversampling* justru menjadi bumerang**. Upaya menyeimbangkan data secara artifisial terbukti merusak kinerja model yang pada dasarnya sudah solid.

Model **Regresi Logistik pada data asli** muncul sebagai solusi dengan performa puncak, mencapai akurasi 0,64 dan Macro F1-Score 0,63, membuktikan bahwa memahami dan memercayai data asli terkadang lebih efektif daripada menerapkan teknik penyeimbangan secara membabi buta.

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

1.  **Pra-pemrosesan Data:**
    * Nilai yang hilang (missing values) diimputasi menggunakan rata-rata (mean) untuk fitur numerik dan modus (mode) untuk fitur kategorikal.
    * Fitur kategorikal diubah menjadi format numerik menggunakan `LabelEncoder`.
    * Fitur numerik distandardisasi menggunakan `StandardScaler`.
2.  **Pembagian Data:** Data dibagi menjadi 80% set pelatihan dan 20% set pengujian, dengan menggunakan `random_state=42` untuk memastikan reproduktifitas.
3.  **Strategi Penyeimbangan Kelas:** Untuk mengatasi sifat kelas target yang tidak seimbang, tiga skenario diuji pada data pelatihan:
    * **None (Tanpa Penyeimbangan):** Tidak ada teknik penyeimbangan yang diterapkan (menjadi *baseline*).
    * **Random Over-Sampling (ROS):** Kelas minoritas di-sampling ulang dengan menduplikasi sampel yang ada.
    * **SMOTE (Synthetic Minority Over-sampling Technique):** Sampel sintetis baru dibuat untuk kelas minoritas guna menciptakan batas keputusan yang lebih kuat.

### Metrik Evaluasi

Kinerja model dinilai menggunakan metrik berikut:
* **Akurasi:** Proporsi prediksi yang benar dari total sampel.
* **Macro F1-Score:** Rata-rata F1-Score dari setiap kelas tanpa pembobotan, yang sangat penting untuk mengevaluasi kinerja pada dataset yang tidak seimbang.
* **Confusion Matrix:** Untuk menganalisis kinerja model dan pola kesalahan pada setiap kelas secara kualitatif.

## 📊 Hasil

### Ringkasan Performa

* **Tanpa Penyeimbangan:** Sebagian besar model menunjukkan kinerja yang buruk pada data asli yang tidak seimbang. Model-model tersebut menunjukkan bias yang kuat terhadap kelas mayoritas dan gagal mengidentifikasi kelas minoritas seperti "High" dan "Very High" dengan benar. Contohnya, model SVM dasar sama sekali tidak dapat mengidentifikasi sebagian besar kelas, menghasilkan Macro F1-Score hanya 0,27.
* **Dengan Penyeimbangan:** Penerapan ROS dan SMOTE secara dramatis meningkatkan kinerja model *ensemble* berbasis pohon (Random Forest, XGBoost, CatBoost, LightGBM) dan KNN. Skor Macro F1 mereka melonjak dari kisaran 0,50-0,60 menjadi di atas 0,80.
* **Keterbatasan Model:** Model yang lebih sederhana seperti Regresi Logistik dan Gaussian Naive Bayes, serta ANN dan SVM (dengan konfigurasi saat ini), tidak mengalami peningkatan signifikan dan bahkan cenderung menurun kinerjanya. Hal ini menunjukkan bahwa keterbatasan fundamental dari model-model tersebut menjadi penghambat kinerja yang lebih besar daripada masalah ketidakseimbangan kelas itu sendiri.

### Model Pemenang

Kombinasi yang paling efektif adalah **Random Forest** yang dipasangkan dengan **Random Over-Sampling (ROS)**.

* **Akurasi:** **0,87** 
* **Macro F1-Score:** **0,87** 

Konfigurasi ini menunjukkan kemampuan superior dalam mengklasifikasikan sampel di kelima tingkat kecemasan dengan benar, membuktikan kekuatan dari penggabungan metode *ensemble* yang dirancang untuk mengurangi *overfitting* dengan teknik penyeimbangan data yang representatif.

## 🚀 Kesimpulan

Penelitian ini menegaskan bahwa *machine learning*, jika diimplementasikan dengan benar, memiliki potensi besar untuk deteksi dini kecemasan berdasarkan faktor gaya hidup. Kesimpulan utamanya adalah bahwa **penanganan ketidakseimbangan kelas bukan hanya sebuah rekomendasi, tetapi sebuah keharusan** untuk membangun model yang andal. Tanpanya, kinerja model cenderung rendah dan tidak stabil, terutama pada metrik Macro F1-Score.

Model *ensemble* berbasis pohon secara konsisten mendominasi, dengan kombinasi **Random Forest + ROS** muncul sebagai solusi dengan performa puncak, mencapai akurasi 0,87 dan Macro F1-Score 0,87.

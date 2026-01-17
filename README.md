# Analisis Prediksi Kelelahan Mental Mahasiswa dengan Augmentasi Data Sintetis

##  Gambaran Umum (Overview)

Proyek ini bertujuan untuk memprediksi tingkat kelelahan mental pada mahasiswa berdasarkan pola tidur dan penggunaan perangkat digital. 

Tantangan utama dalam penelitian ini adalah keterbatasan jumlah data primer (kuesioner asli). Oleh karena itu, sistem ini menerapkan teknik **Data Augmentation** menggunakan *Rule-Based Synthetic Data Generator* (Pembangkit Data Sintetis Berbasis Aturan) untuk meningkatkan performa model Machine Learning.

Model yang digunakan adalah **Random Forest Classifier** yang dioptimalkan menggunakan *Grid Search Cross-Validation*.

---

##  Fitur Utama

1.  **Generator Data Cerdas (Smart Data Generator):**
    * Tidak sekadar mengacak data (*random choice*), melainkan menanamkan logika kausalitas.
    * Menggunakan variabel bayangan `stress_score` untuk memastikan korelasi antara fitur (kebiasaan) dan target (kesehatan mental).
    * *Contoh Logika:* Jika durasi tidur < 5 jam, maka probabilitas menjawab skor kelelahan mental tinggi akan meningkat.

2.  **Hybrid Dataset Merging:**
    * Menggabungkan Data Asli (dari Google Form/CSV) dengan Data Sintetis secara mulus.
    * Harmonisasi nama kolom dan format data otomatis.

3.  **Machine Learning Pipeline:**
    * **Preprocessing:** Mapping data ordinal, Encoding data nominal, dan penanganan *missing values*.
    * **Modelling:** Random Forest dengan tuning hyperparameter (`n_estimators`, `max_depth`, dll).
    * **Threshold Tuning:** Mencari batas probabilitas terbaik (bukan sekadar 0.5) untuk memaksimalkan akurasi.

---

##  Logika Generator Data (Synthetic Logic)

Agar data buatan valid secara statistik untuk pelatihan model, digunakan logika berikut:

1.  **Faktor Pemicu Stres (Input):**
    * Tidur kurang dari 5 jam = `Score +3`
    * Kualitas tidur "Buruk" = `Score +3`
    * Screen time > 8 jam = `Score +2`
2.  **Probabilitas Jawaban Kuesioner (Output):**
    * Jika **Stress Score Tinggi (≥5)**: Mahasiswa buatan cenderung menjawab skala **3 atau 4** (Setuju/Sangat Setuju) pada pertanyaan lelah mental.
    * Jika **Stress Score Rendah (≤2)**: Mahasiswa buatan cenderung menjawab skala **0 atau 1**.

---

##  Prasyarat (Requirements)

Pastikan pustaka Python berikut sudah terinstal:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn

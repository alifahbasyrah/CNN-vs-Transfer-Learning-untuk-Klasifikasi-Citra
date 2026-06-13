				CNN vs Transfer Learning untuk Klasifikasi Citra

 Deskripsi Proyek
Proyek eksperimen ini bertujuan untuk memenuhi Tugas Individu mata kuliah Pembelajaran Mesin / Deep Learning. Fokus eksperimen adalah melakukan klasifikasi citra dua kelas (biner) menggunakan dua pendekatan arsitektur yang berbeda, yaitu CNN from Scratch (membangun model sendiri dari nol) dan Transfer Learning (menggunakan pretrained model MobileNetV2).

Eksperimen ini mengevaluasi secara objektif kelebihan dan kelemahan dari kedua pendekatan tersebut berdasarkan metrik kuantitatif, analisis data, visualisasi hasil, serta skenario penempatan dalam konteks penggunaan nyata di dunia industri.


Ketentuan Dataset
Sesuai dengan syarat instruksi tugas, pengondisian dataset diatur sebagai berikut:
* Eksperimen 1 (CNN from Scratch): Menggunakan subset biner dari dataset CIFAR-10.
* Eksperimen 2 (Transfer Learning): Menggunakan dataset biner Cats vs Dogs.
* Pembagian Data (Data Splitting):
  - Data Training: 70% 
  - Data Validation: 15%
  - Data Testing: 15%



Desain Arsitektur & Strategi Eksperimen

A. Eksperimen 1: CNN from Scratch
Model kustom dirancang secara sistematis dengan struktur bertahap menggunakan komponen-komponen utama:
* Feature Extractor Layer: Terdiri dari pasangan lapisan Conv2D, lapisan penstabil BatchNormalization, pereduksi dimensi spasial MaxPooling2D, serta regulasi Dropout untuk mencegah overfitting dini.
* Classifier Layer: Lapisan Flatten untuk mengubah peta fitur menjadi vektor tunggal, diikuti Dense Layer, lapisan penahan BatchNormalization, regulasi ketat Dropout, dan lapisan output Dense (1 neuron) beraktivasi Sigmoid untuk menghasilkan probabilitas klasifikasi biner.
* Konfigurasi: Optimizer Adam (Learning Rate = 0.001), ukuran batch sebesar 32, dilatih penuh selama 20 epoch.

B. Eksperimen 2: Transfer Learning (MobileNetV2)
* Pretrained Model: Dipilih MobileNetV2 atas pertimbangan efisiensi komputasi yang tinggi dan arsitekturnya yang ringan.
* Strategi Implementasi: Menerapkan strategi Feature Extraction murni. Seluruh lapisan bawaan dasar MobileNetV2 dibekukan secara total (trainable = False).
* Top Classifier: Di atas model dasar dipasang lapisan GlobalAveragePooling2D, diikuti penahan interaksi Dropout(0.2), dan diakhiri lapisan keluaran tunggal Dense beraktivasi Sigmoid. Dilatih selama 10 epoch.


Ringkasan Hasil Eksperimen (Perbandingan Model)

Berikut adalah tabel matriks perbandingan objektif dari hasil akhir pengujian kedua model:

| Aspek Perbandingan | CNN from Scratch | Transfer Learning (MobileNetV2) |
| :--- | :---: | :---: |
| Akurasi Training | 84.63% | 54.20% |
| Akurasi Validation | 72.50% | 55.60% |
| Akurasi Testing | 72.10% | 55.10% |
| Loss Training | 0.3449 | 0.6836 |
| Loss Validation | 0.5565 | 0.6820 |
| Waktu Training | ~1 detik / epoch | ~2 detik / epoch |
| Jumlah Parameter | 544.385 (Dapat dilatih) | 1.281 (Hanya Classifier) |
| Risiko Overfitting | Tinggi | Sangat Rendah (Underfitting Struktural) |
| Kemudahan Implementasi | Sedang | Sangat Mudah |
| Kesesuaian dengan Dataset | Sangat Sesuai | Tidak Sesuai (Resolusi terlalu kecil) |

Catatan Analisis: Keberhasilan model CNN from scratch membuktikan kesesuaian filter konvolusi kustom terhadap citra resolusi mikro (32x32 piksel). Sebaliknya, MobileNetV2 mengalami kendala struktural akibat hilangnya peta informasi spasial berharga saat gambar sekecil itu mengalir ke lapisan awal ekstraktor tanpa adanya proses peningkatan skala.

---

## Struktur Repositori GitHub
Struktur direktori berkas proyek dikelola secara ketat mengikuti ketentuan baku tugas:

project-cnn-vs-transfer-learning/
├── link_dataset.txt
├── notebook/
│   └── cnn_vs_transfer_learning.ipynb
├── report/
│   ├── laporan.pdf
│   └── laporan_eksperimen.tex
├── README.md
└── requirements.txt

Cara Menjalankan Proyek di Perangkat Lokal

 1. Pemasangan Dependensi Pustaka
Buka terminal/command prompt dan ketik perintah berikut untuk menginstal pustaka wajib:
pip install tensorflow numpy scikit-learn matplotlib jupyter

2. Kloning Repositori Proyek
Unduh repositori kerja ini ke mesin lokal Anda menggunakan perintah Git:
git clone https://github.com/username-anda/project-cnn-vs-transfer-learning.git

3. Eksekusi Notebook Eksperimen
Jalankan lingkungan kerja Jupyter Notebook untuk melihat hasil pengujian:
jupyter notebook notebook/cnn_vs_transfer_learning.ipynb


Proyek ini diselesaikan secara mandiri oleh Mahasiswa sebagai bentuk pemenuhan komponen tugas akademis dan dokumentasi riset terapan.
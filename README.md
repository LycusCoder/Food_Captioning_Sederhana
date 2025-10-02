# Food Captioning Sederhana (MM-Food-100k)

Proyek penelitian ini bertujuan untuk membangun model Multi-Label Classification berbasis CNN (EfficientNet) yang dapat memprediksi bahan-bahan (`ingredients`) dari gambar makanan.

---

## 🚀 Commit Pertama: Data Inspection & Environment Setup

### 1. Environment Setup

Proyek ini menggunakan Python 3.10 dan dikelola dengan `pip` untuk memastikan reproduktifitas di berbagai *platform* (Windows/Linux/Mac).

- **Environment Manager:** Conda (digunakan untuk isolasi).
- **Package Manager:** Pip (Semua dependensi tercantum di `requirements.txt`).
- **Instalasi:** Cukup aktifkan *environment* Conda Anda, lalu jalankan:
  ```bash
  pip install -r requirements.txt
  ```

### 2. Tahap Eksplorasi Data (EDA)

Semua eksplorasi data terdapat di `backend/Cek_data-food.ipynb`.

  - **Dataset:** `MM-Food-100k.csv` (100.000 data).
  - **Inspeksi Kualitas:**
      - Terdapat **99,998** data pada kolom `dish_name` (2 data *missing*).
      - Terdapat **98,642** data pada kolom `cooking_method` (1,358 data *missing*).
  - **Fitur Kunci:** Kolom `image_url` (input) dan `ingredients` (multi-label output).
  - **Interaksi:** Notebook dilengkapi dengan UI interaktif (`ipywidgets`) untuk memvisualisasikan data gambar dan label secara *real-time* (Selesai).

### 3. Tahap Preprocessing & Modeling (WIP)

File: `backend/Food_Captioning_Training.ipynb`

  - **Tujuan:** Mengubah data mentah menjadi format yang dapat dilatih model CNN.
  - **Preprocessing Teks:**
      - Kolom `ingredients` berhasil dikonversi dari *string* JSON menjadi *list* Python.
      - Implementasi `MultiLabelBinarizer` dari `scikit-learn` untuk mengubah `ingredients` menjadi vektor biner ($Y$).
  - **Preprocessing Gambar (WIP):**
      - Skema `ImageDataGenerator` Keras sudah disiapkan untuk *resizing* (ke **224x224**) dan **augmentasi** data *training*.
  - **Model Arsitektur:**
      - **Backbone:** EfficientNetB0 (Pre-trained on ImageNet).
      - **Head:** Multi-Label Classification Head dengan aktivasi **Sigmoid** dan *loss function* **Binary Crossentropy**.

-----

## 🚧 Known Issues (Masalah yang Diketahui)

1.  **Image Loading:** Gambar belum diunduh secara lokal. Langkah selanjutnya adalah menyiapkan *script* pengunduhan gambar (dari `image_url`) agar dapat diakses oleh `ImageDataGenerator`.
2.  **Model Loading Error:** Terdapat `ValueError: Shape mismatch` saat meload bobot `EfficientNetB0` dengan `input_tensor` kustom. Ini akan diatasi dengan penyesuaian *input layer* lebih lanjut atau mencoba versi TensorFlow/Keras yang berbeda.

<!-- end list -->


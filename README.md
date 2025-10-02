# Food Captioning Sederhana (MM-Food-100k)

Proyek ini adalah implementasi **Multi-Label Classification** menggunakan *Convolutional Neural Network* (CNN) untuk memprediksi daftar bahan (`ingredients`) dari sebuah gambar masakan. Kami memanfaatkan arsitektur **EfficientNetB0** sebagai *feature extractor*.

-----

## 👥 Tim Pengembang

| Nama | NIM | Kontak |
| :--- | :--- | :--- |
| **Muhammad Affif** | 24225045 | [affif@nourivex.tech](mailto:affif@nourivex.tech) |
| **Muhamad Fahren Andrean Rangkuti** | 23215030 | [kevinkaslana002@gmail.com](mailto:kevinkaslana002@gmail.com) |
| **Putri Areka Sandra** | 23215007 | [putriareka312@gmail.com](mailto:mailto:putriareka312@gmail.com) |

-----

## 🚀 Commit Pertama: Initial Setup & Data Inspection

### 1\. Environment Setup

Proyek ini dibangun di atas Python 3.10 dan dikelola menggunakan **Conda** untuk isolasi *environment* dan **Pip** untuk manajemen paket, menjamin reproduktifitas pada *platform* Windows, Linux, dan macOS.

Untuk memulai, aktifkan *environment* yang sudah dibuat (`penelitian`), lalu instal semua dependensi:

```bash
conda activate penelitian
pip install -r requirements.txt
```

-----

### 2\. Tahap Eksplorasi Data (EDA)

Analisis awal data dilakukan di *Jupyter Notebook*: `backend/Cek_data-food.ipynb`.

  - **Dataset:** **MM-Food-100k.csv** (Total **100.000** observasi).
  - **Fitur Kunci:**
      - **Input ($\mathbf{X}$):** `image_url`
      - **Output ($\mathbf{Y}$):** `ingredients` (Multi-Label).
  - **Inspeksi Kualitas Data (Missing Values):**
      - Kolom `dish_name`: Terdapat 2 data *missing* (99,998 data *non-null*).
      - Kolom `cooking_method`: Terdapat 1,358 data *missing* (98,642 data *non-null*).
  - **Keunggulan Notebook:** Dilengkapi dengan **UI interaktif (`ipywidgets`)** untuk visualisasi *real-time* gambar dan atribut data.

-----

### 3\. Tahap Preprocessing & Modeling (Work In Progress)

Pekerjaan pada tahapan *training* berpusat pada *Notebook*: `backend/Food_Captioning_Training.ipynb`.

#### Preprocessing Teks (Label)

  - Kolom `ingredients` berhasil dikonversi dari format *string* JSON menjadi *list* Python.
  - Dilakukan **Multi-Label Binarization** menggunakan `MultiLabelBinarizer` dari `scikit-learn` untuk menghasilkan vektor biner $Y$.

#### Preprocessing Gambar

  - Skema *image data generator* Keras telah disiapkan untuk **Image Resizing** (ke **224x224**) dan **Data Augmentation** pada *training set*.

#### Model Arsitektur

  - **Backbone CNN:** EfficientNetB0 (Menggunakan *pre-trained weights* dari ImageNet).
  - **Classification Head (Custom):**
      - Aktivasi *output*: **Sigmoid** (Wajib untuk Multi-Label).
      - *Loss function*: **Binary Crossentropy** (Wajib untuk Multi-Label).

-----

## 🚧 Known Issues & Next Steps

| Kategori | Masalah | Rencana Tindak Lanjut |
| :--- | :--- | :--- |
| **Data I/O** | Gambar belum diunduh secara lokal (saat ini masih berupa URL). | Menyiapkan *script* pengunduhan gambar (dari `image_url`) agar dapat diakses oleh `ImageDataGenerator` Keras. |
| **Modeling** | Terjadi `ValueError: Shape mismatch` saat meload bobot `EfficientNetB0`. | Mengatasi konflik *input layer* dengan **`tf.keras.layers.Input`** eksplisit atau menyesuaikan versi TensorFlow/Keras. |


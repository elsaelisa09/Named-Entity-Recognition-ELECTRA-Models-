# Named Entity Recognition (NER) using IndoELECTRA

Project ini bertujuan untuk membangun model **Named Entity Recognition (NER)** untuk Bahasa Indonesia. Model ini dilatih untuk mendeteksi dan mengklasifikasikan entitas bernama (seperti nama orang, lokasi, dan organisasi) dalam teks menggunakan arsitektur deep learning state-of-the-art.

## 🧠 Model Architecture

Project ini menggunakan arsitektur **ELECTRA** (*Efficiently Learning an Encoder that Classifies Token Replacements Accurately*).

Berbeda dengan BERT yang menggunakan *Masked Language Modeling* (menebak kata yang hilang), ELECTRA menggunakan pendekatan **Replaced Token Detection**. Model ini melatih dua jaringan (Generator dan Discriminator) di mana Discriminator bertugas mendeteksi apakah sebuah token adalah token asli atau token yang telah diganti oleh Generator. Pendekatan ini terbukti lebih efisien dan efektif secara komputasi.

* **Paper Resmi:** [ELECTRA: Pre-training Text Encoders as Discriminators Rather Than Generators (Clark et al., 2020)](https://arxiv.org/abs/2003.10555)

### Pretrained Model
Untuk implementasi ini, kami menggunakan model pretrained yang telah dilatih khusus pada korpus Bahasa Indonesia:
* **Model Name:** `ChristopherA08/IndoELECTRA`
* **Source:** [Hugging Face Hub](https://huggingface.co/ChristopherA08/IndoELECTRA)

## 📂 Dataset: SINGGALANG

Dataset yang digunakan dalam eksperimen ini adalah **SINGGALANG**.

* **Deskripsi:** Dataset ini dibuat secara otomatis (*automatically labeled*) menggunakan metode *distant supervision*. Label dihasilkan dengan mereferensikan *expanded DBpedia* dari MDEE_Gazetteer.
* **Jumlah Data:** Terdiri dari sekitar 48,957 kalimat.
* **Sumber Dataset:** [SINGGALANG Repository](https://github.com/ialfina/ner-dataset-modified-dee/blob/master/singgalang/SINGGALANG.tsv)

### Label Entitas
Dataset ini mencakup tiga label entitas utama (selain label `O` untuk *Outside*):

1.  **PER (Person):** Nama orang atau individu.
2.  **LOC (Location):** Nama lokasi geografis, tempat, kota, atau negara.
3.  **ORG (Organization):** Nama perusahaan, institusi, atau organisasi.

*Format pelabelan umumnya menggunakan skema IOB (Inside-Outside-Beginning), misal: `B-PER`, `I-PER`, `B-LOC`, dll.*

## 📊 Training Results

Berikut adalah hasil pelatihan model selama 12 Epoch.
*Catatan: Akurasi (Accuracy) yang tinggi diimbangi dengan F1-Score yang moderat adalah hal yang wajar pada dataset NER yang tidak seimbang (didominasi oleh label 'O').*

| Epoch | Training Loss | Validation Loss | Accuracy | F1 Score |
| :---: | :---: | :---: | :---: | :---: |
| 1 | 1.8259 | 1.3823 | 0.6874 | 0.1827 |
| 2 | 0.9283 | 0.6946 | 0.7824 | 0.3221 |
| 3 | 0.6596 | 0.6241 | 0.7904 | 0.3354 |
| 4 | 0.5981 | 0.5897 | 0.7936 | 0.3459 |
| 5 | 0.5690 | 0.5797 | 0.7993 | 0.3500 |
| 6 | 0.5410 | 0.5624 | 0.8020 | 0.3597 |
| 7 | 0.5267 | 0.5535 | 0.8011 | 0.3580 |
| 8 | 0.5152 | 0.5501 | 0.8056 | 0.3650 |
| 9 | 0.5074 | 0.5470 | 0.8069 | 0.3669 |
| 10 | 0.5018 | 0.5452 | 0.8055 | 0.3638 |
| 11 | 0.5009 | 0.5432 | 0.8087 | **0.3692** |
| 12 | 0.4976 | 0.5435 | 0.8086 | 0.3689 |

## ⚙️ Requirements

* Python 3.x
* PyTorch
* Transformers (Hugging Face)
* Scikit-learn
* Pandas & Numpy

---
*Citation for Dataset:*
*Alfina et al. (2017). DBpedia of MDEE_Gazetteer.*
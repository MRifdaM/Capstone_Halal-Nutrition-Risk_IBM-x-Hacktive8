# Analisis Risiko Gizi dan Bahan Ambigu pada Produk Pangan
### Studi Kasus Menggunakan Data Open Food Facts dan Klasifikasi AI (IBM Granite)

---

## 📜 Gambaran Umum Proyek (Project Overview)
Proyek ini bertujuan untuk membangun "peta risiko" produk pangan dengan menganalisis dataset Open Food Facts yang berisi jutaan produk. Fokus utama analisis adalah pada dua aspek krusial bagi konsumen modern: **risiko gizi** (kandungan gula, garam, dan lemak jenuh yang tinggi) dan **transparansi bahan** (kejelasan sumber komposisi yang relevan untuk pantangan makanan seperti halal, vegan, dll.).

Karena keterbatasan data pada pasar spesifik, analisis ini mengambil pendekatan studi kasus pada sampel data global yang didominasi oleh pasar Barat (AS & Prancis). Proyek ini memanfaatkan model AI (IBM Granite) untuk melakukan klasifikasi dan peringkasan, mengubah data mentah yang kompleks menjadi *insight* yang dapat ditindaklanjuti bagi produsen dan konsumen.

---

## 📊 Tautan & Penjelasan Dataset

* **Tautan Sumber Data Mentah:** [Open Food Facts - Product Database di Hugging Face](https://huggingface.co/datasets/openfoodfacts/product-database)

Dataset Open Food Facts adalah database produk makanan terbesar di dunia yang bersifat *open-source* dan *crowdsourced*, berisi lebih dari 3 juta data produk. Mengingat ukurannya yang sangat besar (beberapa Gigabyte), metodologi **streaming dan sampling** diterapkan untuk mendapatkan sampel data yang representatif.

**Raw dataset yang disertakan di repositori ini (`openfoodfacts_sample.csv`) adalah hasil pengambilan 100.000 baris pertama dari sumber data mentah tersebut.** Pendekatan ini memungkinkan analisis yang efisien tanpa kehilangan keragaman data secara signifikan, namun tetap dapat dijalankan di lingkungan dengan sumber daya terbatas seperti Google Colab.

---

## 💡 Wawasan & Temuan Kunci (Insight & Findings)
Analisis pada 100.000 sampel produk menghasilkan beberapa temuan kunci yang signifikan:

1.  **Krisis Ganda: Risiko Gula & Lemak Jenuh yang Tinggi**
    * Hampir sepertiga dari produk yang dianalisis memiliki kandungan **Gula Tinggi (27%)** dan **Lemak Jenuh Tinggi (30%)**. Ini mengindikasikan adanya masalah kesehatan yang sistemik pada produk pangan olahan.
    * Di sisi lain, risiko garam jauh lebih terkendali, dengan mayoritas produk (70%) berada di kategori Rendah.

2.  **Mayoritas Bahan Bersifat Ambigu**
    * Lebih dari separuh produk **(55.2%)** diklasifikasikan memiliki bahan yang **ambigu**, di mana sumbernya (hewani/nabati) tidak dijelaskan secara eksplisit pada label.
    * Masalah ini paling parah terjadi pada kategori produk olahan kompleks seperti **Desserts (89.2% ambigu)** dan **Snacks (82.8% ambigu)**.

3.  **Episentrum Masalah: Kategori Makanan Ringan & Manis**
    * Kategori seperti **"Confectioneries"** dan **"Biscuits & Cakes"** adalah "zona merah" mutlak, di mana **lebih dari 90%** produknya memiliki risiko gula **TINGGI**.
    * Terdapat korelasi kuat antara produk tinggi gula dengan produk yang memiliki bahan ambigu, menunjukkan bahwa produk yang paling tidak sehat juga yang paling tidak transparan.

---

## 🤖 Penjelasan Dukungan AI (AI Support Explanation)

Penggunaan model AI **IBM Granite** (`ibm-granite/granite-3.3-8b-instruct`) sangat fundamental dan digunakan dalam dua kapasitas krusial:

1.  **AI untuk Klasifikasi**: Model AI menganalisis ribuan daftar komposisi produk (`ingredients_text`) yang tidak terstruktur untuk mengklasifikasikan status kejelasan bahan menjadi `ambiguous` atau `clear`. Tugas ini mustahil dilakukan secara manual dalam skala besar dan menunjukkan kemampuan AI dalam memahami konteks bahasa alami pada data yang kompleks.

2.  **AI untuk Summarisasi**: Setelah data kuantitatif (persentase, statistik) dihitung, model AI digunakan untuk mensintesis temuan-temuan tersebut menjadi sebuah ringkasan naratif yang koheren, lengkap dengan draf *insight* dan rekomendasi. Ini secara signifikan mempercepat proses analisis dan pengambilan kesimpulan strategis dari hasil visualisasi.

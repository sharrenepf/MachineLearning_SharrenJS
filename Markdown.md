
# Tugas Praktikum 1 Bagian 1 No 3 & Bagian 2

---

## Bagian 1 — Library yang Digunakan

### 1. PyPREP

PyPREP adalah implementasi Python dari **PREP pipeline** (*Preprocessing Pipeline*) yang dirancang untuk prapemrosesan standar sinyal EEG. Library ini dibangun di atas MNE-Python.

Fungsi utama:

- **Penghapusan derau jala-jala listrik** (*line noise*) pada frekuensi 50/60 Hz beserta harmoniknya.
- **Robust referencing**, yaitu estimasi *average reference* yang tidak terkontaminasi kanal rusak, dilakukan secara iteratif.
- **Deteksi kanal bermasalah** (*bad channels*) melalui beberapa kriteria: kanal datar (*flat*), deviasi amplitudo ekstrem, korelasi rendah antar kanal tetangga, rasio derau frekuensi tinggi, dan prediksi RANSAC.
- **Interpolasi kanal rusak** menggunakan interpolasi bola (*spherical spline*).

---

### 2. SciPy

SciPy adalah library komputasi ilmiah yang menyediakan algoritma numerik di atas struktur data NumPy. 
---

### 3. Weights & Biases (`wandb`)

`wandb` adalah platform *experiment tracking* dan MLOps untuk mencatat, memvisualisasikan, dan membandingkan proses pelatihan model pembelajaran mesin.

Fungsi utama:

- **Pencatatan metrik** pelatihan dan validasi secara *real-time* (loss, akurasi, F1, learning rate) dalam bentuk dasbor daring.
- **Pencatatan konfigurasi** (*hyperparameter*), versi kode, versi dataset, dan spesifikasi perangkat keras untuk setiap eksperimen.
- **Sweeps**: pencarian hiperparameter otomatis dengan strategi *grid*, *random*, atau optimasi Bayesian.
- **Artifacts**: pemversian dataset, *checkpoint* model, dan keluaran, lengkap dengan jejak silsilah (*lineage*).
- **Model Registry**: pengelolaan siklus hidup model dari eksperimen hingga tahap produksi.
- **Reports**: penyusunan laporan yang dapat dibagikan dan pemantauan konsumsi sumber daya (GPU, memori, daya).

Kegunaan dalam penelitian: menjamin **reproducibility** dan **auditability**. Seluruh eksperimen tercatat sehingga hasil yang dilaporkan dapat ditelusuri kembali ke konfigurasi yang tepat.
---

### 4. pyECG

`pyECG` adalah library Python untuk **pembacaan dan representasi data elektrokardiogram (EKG)** beserta anotasinya.

Fungsi utama:

- Membaca berkas rekaman EKG dari format standar, khususnya **ISHNE** dan format **WFDB/PhysioNet** (misalnya basis data MIT-BIH Arrhythmia).
- Menyediakan struktur data terpadu (`ECGRecord`, `Signal`, `Time`, `Annotation`) sehingga rekaman dari format berbeda dapat diperlakukan secara seragam.
- Mengelola anotasi detak (label jenis denyut, posisi sampel) yang menjadi *ground truth* pada tugas klasifikasi aritmia.
- Mengakses metadata rekaman: frekuensi cuplik, jumlah dan nama sadapan, serta durasi.
---

## Bagian 2 — Aspek Etika, Hukum, dan Lingkungan

### 2.1 Contoh Pelanggaran Etika dan Hukum dalam Penggunaan Kecerdasan Buatan

#### a. Pengumpulan data biometrik tanpa persetujuan (kasus Clearview AI)

Clearview AI membangun basis data pengenalan wajah dengan mengambil (*scraping*) miliaran foto dari media sosial dan situs publik tanpa persetujuan pemilik wajah, lalu menjual aksesnya kepada aparat penegak hukum dan pihak swasta. Otoritas perlindungan data di Italia, Prancis, Yunani, Inggris, Australia, dan Belanda menyatakan praktik ini melanggar hukum perlindungan data dan menjatuhkan sanksi administratif bernilai jutaan euro.

Pelanggaran yang terjadi: pemrosesan data biometrik tanpa dasar hukum yang sah, ketiadaan *informed consent*, dan pengabaian hak subjek data untuk mengakses serta menghapus datanya. Dalam kerangka Indonesia, praktik serupa bertentangan dengan UU No. 27 Tahun 2022 tentang Pelindungan Data Pribadi, yang mengategorikan data biometrik sebagai data pribadi bersifat spesifik dan mewajibkan persetujuan eksplisit.

#### b. Diskriminasi algoritmik (sistem rekrutmen Amazon dan algoritma COMPAS)

Amazon menghentikan sistem penyaringan pelamar berbasis AI setelah ditemukan bahwa model tersebut secara sistematis menurunkan peringkat CV yang memuat indikator gender perempuan. Penyebabnya adalah data latih berupa riwayat rekrutmen sepuluh tahun terakhir yang didominasi pelamar laki-laki, sehingga bias historis direproduksi oleh model. Pada ranah peradilan, investigasi ProPublica terhadap algoritma COMPAS yang digunakan untuk memprediksi risiko residivisme di Amerika Serikat menemukan bahwa terdakwa kulit hitam lebih sering diberi label "berisiko tinggi" secara keliru dibandingkan terdakwa kulit putih.

Pelanggaran yang terjadi: diskriminasi tidak langsung, ketiadaan transparansi dan *explainability*, serta absennya mekanisme koreksi bagi pihak yang dirugikan.

#### c. Deepfake untuk penipuan finansial

Pada awal 2024, seorang staf keuangan perusahaan rekayasa Arup di Hong Kong mentransfer dana sekitar 25 juta dolar AS setelah mengikuti rapat video yang seluruh pesertanya, termasuk sosok "CFO", merupakan rekaan *deepfake*. Kasus ini menunjukkan penyalahgunaan AI generatif untuk pemalsuan identitas dan penipuan terorganisasi. Dalam hukum Indonesia, perbuatan ini dapat dijerat dengan UU ITE (manipulasi informasi elektronik dan penipuan daring) serta KUHP tentang penipuan.

#### d. Pelanggaran hak cipta pada data pelatihan

Sejumlah gugatan diajukan oleh penulis, penerbit, dan perusahaan media terhadap pengembang model generatif atas penggunaan karya berhak cipta sebagai data latih tanpa lisensi. Isu utamanya adalah batas doktrin *fair use* dan hak ekonomi pencipta.

#### e. Kerangka regulasi sebagai respons

Uni Eropa mengesahkan **EU AI Act** (Regulation (EU) 2024/1689) yang mengklasifikasikan sistem AI berdasarkan tingkat risiko dan melarang praktik seperti *social scoring* oleh negara serta identifikasi biometrik jarak jauh secara *real-time* di ruang publik (dengan pengecualian terbatas). Indonesia menerbitkan Surat Edaran Menkominfo No. 9 Tahun 2023 tentang Etika Kecerdasan Artifisial sebagai pedoman, meskipun sifatnya belum mengikat secara hukum.

**Referensi Bagian 2.1**

1. Angwin, J., Larson, J., Mattu, S., & Kirchner, L. (2016, 23 Mei). *Machine bias*. ProPublica. https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing
2. Dastin, J. (2018, 11 Oktober). *Amazon scraps secret AI recruiting tool that showed bias against women*. Reuters. https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G
3. Garante per la protezione dei dati personali. (2022). *Facial recognition: the Italian SA fines Clearview AI EUR 20 million*. https://www.garanteprivacy.it/
4. Autoriteit Persoonsgegevens. (2024). *Dutch DPA imposes a fine on Clearview because of illegal data collection for facial recognition*. https://www.autoriteitpersoonsgegevens.nl/en
5. European Parliament & Council. (2024). *Regulation (EU) 2024/1689 (Artificial Intelligence Act)*. https://eur-lex.europa.eu/eli/reg/2024/1689/oj
6. Republik Indonesia. (2022). *Undang-Undang No. 27 Tahun 2022 tentang Pelindungan Data Pribadi*.
7. Kementerian Komunikasi dan Informatika RI. (2023). *Surat Edaran No. 9 Tahun 2023 tentang Etika Kecerdasan Artifisial*.
8. Chen, H. (2024, 4 Februari). *Finance worker pays out $25 million after video call with deepfake "chief financial officer"*. CNN. https://www.cnn.com/2024/02/04/asia/deepfake-cfo-scam-hong-kong-intl-hnk

---

### 2.2 Dampak Energi dan Lingkungan serta Upaya Mitigasinya

#### a. Gambaran dampak

**Konsumsi energi pelatihan model.** Strubell dkk. (2019) memperkirakan bahwa pelatihan satu model Transformer besar disertai *neural architecture search* menghasilkan emisi setara ±284 ton CO₂, atau kira-kira lima kali emisi seumur hidup sebuah mobil penumpang di Amerika Serikat. Patterson dkk. (2021) melaporkan pelatihan GPT-3 mengonsumsi sekitar 1.287 MWh listrik dengan emisi ±552 ton CO₂e.

**Konsumsi energi inferensi.** Beban energi tidak berhenti pada pelatihan. Ketika sebuah model dilayani ke jutaan pengguna, akumulasi energi inferensi pada akhirnya melampaui energi pelatihannya.

**Beban pada jaringan listrik.** International Energy Agency (2024) memperkirakan konsumsi listrik pusat data global mencapai sekitar 460 TWh pada 2022 dan berpotensi meningkat menjadi 620–1.050 TWh pada 2026, dengan AI sebagai salah satu pendorong utama.

**Jejak air.** Li dkk. (2023) memperkirakan pelatihan GPT-3 di pusat data AS mengonsumsi sekitar 700.000 liter air bersih untuk pendinginan isu yang signifikan pada wilayah yang mengalami tekanan ketersediaan air.

**Limbah elektronik.** Siklus pergantian GPU dan akselerator yang cepat menambah volume limbah elektronik beserta persoalan penambangan mineral kritis di hulu.

#### b. Upaya mitigasi

**Tingkat teknis (dapat dilakukan peneliti individu)**

1. **Gunakan kembali model terlatih.** *Fine-tuning* atau *transfer learning* dari *checkpoint* yang sudah ada memangkas biaya komputasi secara drastis dibandingkan pelatihan dari awal.
2. **Kompresi model.** Kuantisasi (FP32 → INT8), *pruning*, dan *knowledge distillation* menurunkan kebutuhan komputasi saat inferensi tanpa penurunan akurasi yang berarti.
3. **Pilih arsitektur yang proporsional.** Untuk data tabular atau sinyal fisiologis berskala sedang, model klasik atau CNN ringan sering kali setara dengan arsitektur besar dengan biaya jauh lebih rendah.
4. **Hentikan pelatihan lebih awal.** *Early stopping* dan pencarian hiperparameter yang efisien (optimasi Bayesian, Hyperband) mencegah pemborosan siklus komputasi. Fitur *Sweeps* pada `wandb` mendukung strategi ini.
5. **Ukur dan laporkan.** Gunakan `codecarbon` atau ML CO₂ Impact Calculator untuk mencatat konsumsi energi dan estimasi emisi, lalu cantumkan dalam publikasi.

**Tingkat infrastruktur dan kebijakan**

6. **Pilih lokasi dan waktu komputasi berdasarkan intensitas karbon.** Menjalankan pelatihan di wilayah dengan bauran energi terbarukan tinggi, atau pada jam ketika intensitas karbon jaringan rendah (*carbon-aware scheduling*), dapat menurunkan emisi hingga satu orde besaran tanpa mengubah kode.
7. **Tingkatkan efisiensi pusat data.** Perbaikan *Power Usage Effectiveness* (PUE), pendinginan cair, dan pemanfaatan panas buangan.
8. **Transparansi wajib.** Regulasi yang mewajibkan pengungkapan konsumsi energi dan emisi model — sebagaimana diamanatkan sebagian dalam EU AI Act untuk model *general-purpose* — memungkinkan perbandingan yang jujur antarpengembang.

#### c. Pendapat Saya

Menurut saya, masalahnya bukan pada teknologi AI nya, tapi pada kebiasaan kita menganggap "lebih besar berarti lebih bagus". Model yang lebih besar dianggap lebih hebat, jadi semua orang berlomba membuat model besar. Padahal model besar butuh listrik besar juga.

Ada tiga hal yang menurut saya bisa dilakukan:

Catat dulu pemakaian energinya. Kalau tidak pernah diukur, kita tidak akan tahu seberapa boros. Sama seperti kita tidak bisa hemat uang kalau tidak pernah mencatat pengeluaran. Jurnal ilmiah sebaiknya mulai mewajibkan penulis mencantumkan angka ini.
Hargai model yang hemat, bukan cuma yang akurat. Kalau ada dua model dengan akurasi hampir sama, yang lebih hemat listrik seharusnya dianggap lebih baik. Sekarang penilaiannya masih fokus ke akurasi saja.
Pakai ulang model yang sudah ada. Melatih model dari nol itu mahal dan boros. Kalau sudah ada model yang bisa disesuaikan, lebih baik pakai itu.

**Referensi Bagian 2.2**

1. Strubell, E., Ganesh, A., & McCallum, A. (2019). Energy and policy considerations for deep learning in NLP. *Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics*, 3645–3650. https://doi.org/10.18653/v1/P19-1355
2. Patterson, D., Gonzalez, J., Le, Q., Liang, C., Munguia, L.-M., Rothchild, D., So, D., Texier, M., & Dean, J. (2021). *Carbon emissions and large neural network training*. arXiv:2104.10350. https://arxiv.org/abs/2104.10350
3. Luccioni, A. S., Viguier, S., & Ligozat, A.-L. (2023). Estimating the carbon footprint of BLOOM, a 176B parameter language model. *Journal of Machine Learning Research*, 24(253), 1–15.
4. Li, P., Yang, J., Islam, M. A., & Ren, S. (2023). *Making AI less "thirsty": Uncovering and addressing the secret water footprint of AI models*. arXiv:2304.03271. https://arxiv.org/abs/2304.03271
5. International Energy Agency. (2024). *Electricity 2024: Analysis and forecast to 2026*. https://www.iea.org/reports/electricity-2024
6. Lacoste, A., Luccioni, A., Schmidt, V., & Dandres, T. (2019). *Quantifying the carbon emissions of machine learning*. arXiv:1910.09700. https://arxiv.org/abs/1910.09700
7. Schwartz, R., Dodge, J., Smith, N. A., & Etzioni, O. (2020). Green AI. *Communications of the ACM*, 63(12), 54–63. https://doi.org/10.1145/3381831
8. CodeCarbon. (2024). *CodeCarbon: Track and reduce CO₂ emissions from your computing*. https://codecarbon.io

---
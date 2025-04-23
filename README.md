# autoencoder
membuat convolutional autoencoder yang belajar dari pasangan gambar:

Input: Gambar manga grayscale (1 channel)

Output: Gambar manga berwarna (RGB, 3 channel)

#Tools:

google collab/jupiter notebook

Python

TensorFlow/Keras

OpenCV atau PIL untuk preprocessing gambar


Keuntungan menyediakan dataset BW dan Color (paired data):
🎯 Supervised Learning = Pembelajaran Lebih Terarah
Model tahu apa yang harus dihasilkan karena diberikan contoh nyata:

Input: gambar BW

Target: gambar Color

Ini membuat training lebih akurat dan efisien, karena model belajar secara langsung hubungan antara piksel BW → RGB.

🧠 Model Belajar Transfer Warna Secara Kontekstual
Misalnya:

Rambut karakter A selalu merah

Seragam selalu biru

Kalau hanya diberikan BW tanpa target warna, model nggak tahu bahwa bagian tertentu harus punya warna tertentu.

🎨 Menghindari Warna Acak / Tidak Realistis
Tanpa target warna, autoencoder bisa:

Menghasilkan warna yang salah (rambut hijau, langit pink)

Merata-ratakan warna sehingga hasilnya pucat atau buram

🔍 Evaluasi Hasil Jadi Objektif
Dengan data color sebagai label, hitung metrik evaluasi:

MSE (Mean Squared Error)

SSIM (Structural Similarity)

PSNR (Peak Signal-to-Noise Ratio)
![image](https://github.com/user-attachments/assets/e590f108-1054-4cad-9e68-399ef7ce1aa8)


![image](https://github.com/user-attachments/assets/00e14878-a582-40fd-a919-42202f5a52c8)

Penyebab Hasil "Gagal" / Buram
Dataset Tidak Berpasangan
→ Model tidak belajar "hubungan" langsung antara gambar hitam putih dan versi berwarnanya.

Dataset Terlalu Sedikit
→ Hanya 20 gambar BW dan 20 berwarna → ini sangat kecil untuk deep learning, apalagi pewarnaan.

Model Terlalu Sederhana
→ Arsitektur autoencoder terlalu dangkal. Gambar seperti manga butuh representasi fitur kompleks.

Warna Target Tidak Konsisten
→ Jika gambar color random dan tidak satu tema/karakter, model bingung memberi warna yang konsisten.

✅ Cara Memperbaiki dan Meningkatkan Kualitas Pewarnaan
1. Gunakan Dataset Pasangan (BW & Color)
Idealnya 1 gambar BW memiliki pasangan tepatnya yang sudah diwarnai.

Kalau tidak ada, bisa pakai pendekatan self-supervised: konversi color ke BW lalu latih model menebak warna aslinya.

2. Perbanyak Dataset
20 gambar itu sangat terbatas.

Target awal yang ideal: 500–1000 pasangan BW & Color.

3. Tingkatkan Arsitektur Model
Contoh peningkatan:

Tambahkan lebih banyak conv layer.

Gunakan BatchNormalization, Dropout, atau bahkan skip connection seperti di U-Net.

Bisa juga eksplor Conditional GAN seperti pix2pix (hasil lebih realistis).

4. Gunakan Warna Input Sebagai Petunjuk
Bisa tambahkan sedikit warna acuan pada input (misal user warnai sebagian gambar), atau gunakan teknik "hints" seperti di scribble colorization.


solusi yang saya ambil

Ubah pipeline jadi self-supervised:

Ambil hanya gambar berwarna

Convert ke grayscale

Latih model dari grayscale → prediksi warna aslinya
dan hasil dibawah ini 

![image](https://github.com/user-attachments/assets/94708cca-9c63-48d6-8eb7-cc5f8d65df18)
![image](https://github.com/user-attachments/assets/41f705e2-f373-46fe-bcd4-39314153ba28)

solusi selanjutnya

Ganti Arsitektur ke U-Net 
U-Net sangat efektif untuk:

Melestarikan detail struktur (outline manga)

Menghasilkan pewarnaan lebih tajam

Bekerja baik meskipun dataset kecil (relatif)

![image](https://github.com/user-attachments/assets/416eb539-4042-4af6-9817-b0b4edc9489b)
![image](https://github.com/user-attachments/assets/0b1a3263-9bb9-4698-9016-a3451f7d6576)


hasilnya masih gagal dan dapat disimpulkan alasannya
Dataset masih kecil

Model masih sederhana

belum ada pengenalan objek

pasangan dataset yang tidak sesuai(keterbatasan dataset dan kualitasnya yang buruk)

epoch terlalu kecil

layer terlalu sedikit

dan sebagainya

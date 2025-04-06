# SisOp-2025
#Nama : Hafizh Hamas Muntazar
#NRP : 3124500060
#Kelas :D3 IT B
# Sistem Operasi

## 1.1 Tiga Tujuan Utama Sistem Operasi  
1. **Manajemen Sumber Daya:** Mengalokasikan CPU, memori, dan perangkat I/O secara efisien.  
2. **Antarmuka Pengguna & Kemudahan:** Memberikan cara bagi pengguna dan aplikasi untuk berinteraksi dengan perangkat keras.  
3. **Kontrol & Keamanan:** Mengatur eksekusi proses, menjaga keamanan, dan memastikan akses yang adil ke sumber daya.  

## 1.2 Kapan Sistem Operasi "Membuang" Sumber Daya?  
Sistem operasi mungkin menggunakan sumber daya secara tidak efisien untuk meningkatkan **pengalaman pengguna, keamanan, atau stabilitas**. Contohnya:  
- **GUI (Graphical User Interface)** lebih berat, tetapi meningkatkan kemudahan penggunaan.  
- **Virtualisasi dan Redundansi** meningkatkan keamanan dan keandalan.  
- **Sistem time-sharing** memastikan keadilan akses CPU meskipun efisiensi penggunaan CPU berkurang.  

Penggunaan ini bukan pemborosan karena memberikan manfaat lebih besar.  

## 1.3 Kesulitan Utama dalam Menulis OS untuk Lingkungan Real-Time  
Sistem operasi real-time harus memenuhi **batas waktu yang ketat**. Tantangannya:  
- **Penjadwalan yang dapat diprediksi** untuk memenuhi tenggat waktu.  
- **Penanganan interrupt yang efisien** tanpa overhead berlebihan.  
- **Menghindari perebutan sumber daya** yang dapat menyebabkan keterlambatan.  

## 1.4 Haruskah OS Menyertakan Aplikasi seperti Browser dan Email?  
### **Ya:**  
- Integrasi meningkatkan **kinerja dan keamanan** (misalnya, sandboxing aplikasi).  
- Menyediakan **pengalaman pengguna yang konsisten** di berbagai perangkat.  
- Mengurangi **kompleksitas instalasi** untuk pengguna awam.  

### **Tidak:**  
- Melanggar **prinsip modularitas** (OS harus mengelola perangkat keras, bukan menyediakan aplikasi).  
- Menyebabkan **bloatware dan risiko keamanan** (aplikasi bawaan sulit dihapus).  
- Mengurangi **kebebasan pengguna** dalam memilih aplikasi mereka sendiri.  

## 1.5 Mode Kernel vs. Mode User sebagai Bentuk Keamanan  
- **Mode Kernel:** Akses penuh ke perangkat keras dan memori, digunakan oleh OS.  
- **Mode User:** Akses terbatas untuk mencegah program merusak sistem.  
- Ini mencegah aplikasi biasa memodifikasi sistem secara langsung, meningkatkan keamanan.  

## 1.6 Instruksi yang Harus Menjadi Privileged  
**Privileged (Harus dalam Mode Kernel):**  
- **(a)** Mengatur nilai timer  
- **(c)** Menghapus memori  
- **(e)** Mematikan interrupt  
- **(f)** Memodifikasi tabel status perangkat  
- **(g)** Beralih dari mode user ke mode kernel  
- **(h)** Mengakses perangkat I/O  

**Non-Privileged (Dapat Digunakan di Mode User):**  
- **(b)** Membaca jam  
- **(d)** Mengeluarkan instruksi trap (untuk beralih ke mode kernel dengan aman)  

## 1.7 Masalah dalam Melindungi OS dengan Partisi Memori Tetap  
1. **Tidak Fleksibel:** Jika OS memerlukan lebih banyak memori, tidak bisa diperluas.  
2. **Sulit Diperbarui:** OS tidak dapat memperbarui atau mengubah dirinya sendiri.  

## 1.8 Penggunaan Mode CPU Tambahan  
1. **Tingkat Privilege Berbeda:** Misalnya, Mode User, Supervisor, dan Hypervisor untuk virtualisasi.  
2. **Isolasi Proses:** Mode terpisah untuk aplikasi, layanan sistem, dan firmware.  

## 1.9 Penggunaan Timer untuk Menghitung Waktu Saat Ini  
- OS mengatur **interrupt timer** yang dipicu pada interval tetap.  
- **Handler interrupt** menambahkan penghitung waktu.  
- Waktu sistem dihitung berdasarkan interval yang telah berlalu sejak sistem menyala.  

## 1.10 Manfaat dan Masalah Cache  
**Manfaat:**  
1. **Akses Data Lebih Cepat:** Mengurangi latensi dengan menyimpan data yang sering digunakan.  
2. **Mengurangi Beban Memori Utama:** Menghindari keterlambatan karena akses memori yang lambat.  

**Masalah yang Diatasi:**  
- Meningkatkan kinerja CPU dengan mengurangi akses ke memori yang lebih lambat.  

**Masalah yang Ditimbulkan:**  
- **Masalah Koherensi:** Data dalam beberapa cache bisa menjadi usang.  
- **Kompleksitas Tambahan:** Manajemen cache membutuhkan algoritma tambahan.  

---

*Dokumen ini berisi jawaban atas pertanyaan sistem operasi terkait konsep dasar, keamanan, dan efisiensi dalam manajemen sumber daya komputer.*  


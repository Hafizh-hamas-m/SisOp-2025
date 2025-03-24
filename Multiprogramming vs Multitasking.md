# SisOp-2025
#Nama : Hafizh Hamas Muntazar
#NRP : 3124500060
#Kelas :D3 IT B
## 1. Perbedaan Multiprogramming vs Multitasking
Multiprogramming:  
Teknik di mana beberapa program disimpan di memori utama secara bersamaan dan prosesor mengeksekusi program secara bergantian. Tujuannya adalah memaksimalkan penggunaan CPU dengan mengurangi waktu idle (menganggur).  

Multitasking:  
Kemampuan sistem operasi untuk menjalankan beberapa tugas (proses) secara bersamaan. Ada dua jenis multitasking:  

- Preemptive: OS mengatur waktu CPU untuk setiap proses (contoh: Windows, Linux).  
- Cooperative: Proses mengatur waktu sendiri untuk berhenti dan memberi giliran ke proses lain (contoh: MS-DOS lama).  

## 2. Fungsi Sistem Operasi (OS)
Manajemen Proses: Mengatur proses yang berjalan di sistem.  
Manajemen Memori: Mengatur penggunaan RAM oleh berbagai aplikasi.  
Manajemen File: Menyediakan struktur dan akses terhadap file di penyimpanan.  
Manajemen Perangkat (I/O): Mengatur komunikasi antara perangkat keras (printer, keyboard, dll.) dan perangkat lunak.  
Keamanan dan Proteksi: Melindungi data dan akses dari pengguna atau program yang tidak sah.  
Antarmuka Pengguna (UI): Memberikan tampilan grafis (GUI) atau baris perintah (CLI) agar pengguna dapat berinteraksi dengan komputer.  

## 3. Virtualisasi Container
Pengertian:  
Teknologi yang memungkinkan isolasi aplikasi dan dependensinya dalam lingkungan yang ringan (container). Container berjalan di atas kernel OS yang sama tetapi memiliki sistem file, pustaka, dan konfigurasi sendiri.  

Keuntungan:  
- Lebih ringan dibandingkan virtual machine (VM).  
- Cepat dalam pembuatan dan eksekusi.  
- Portabilitas tinggi di berbagai lingkungan (dev, staging, production).  

Contoh Teknologi:  
Docker, Kubernetes.

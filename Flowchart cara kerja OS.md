#Nama : Hafizh Hamas Muntazar
#NRP : 3124500060
#Kelas :D3 IT B
## 📊 Flowchart:

flowchart 
    A(Mulai: Power On) --> B(POST: Cek Hardware)
    B --> C{POST Berhasil?}
    C --> |Ya| D(Load BIOS/UEFI)
    C --> |Tidak| X(Error: Beep/Kode Kesalahan)
    D --> E(Boot Loader: Cari & Muat OS)
    E --> F(Load Kernel ke Memori)
    F --> G(Initialize Kernel & Hardware)
    G --> H(Tampilkan Antarmuka Login)
    H --> I{User Login?}
    I --> |Ya| J(User Session: OS Siap Digunakan)
    I --> |Tidak| H
    J --> K{Shutdown?}
    K --> |Ya| L(Tutup Semua Proses)
    L --> M(Simpan Data & Status Sistem)
    M --> N(Matikan Sistem)
    K --> |Tidak| J

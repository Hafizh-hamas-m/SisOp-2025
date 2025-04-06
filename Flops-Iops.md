# Laporan Pengujian FLOPS dan IOPS pada WSL 2

## 📌 Identitas
- **Nama**: [Nama Mahasiswa]  
- **NIM**: [Nomor Induk Mahasiswa]  
- **Mata Kuliah**: [Nama Mata Kuliah]  
- **Dosen**: [Nama Dosen]

---

## 1. Pendahuluan

Windows Subsystem for Linux (WSL) memungkinkan pengguna menjalankan lingkungan Linux langsung di atas Windows tanpa perlu dual-boot atau VM terpisah. Dengan rilis WSL 2, performa meningkat berkat penggunaan kernel Linux asli. Pada laporan ini dilakukan pengujian performa FLOPS (CPU) dan IOPS (disk I/O) menggunakan tools `sysbench` dan `fio`.

---

## 2. Lingkungan Pengujian

| Komponen        | Spesifikasi                   |
|-----------------|-------------------------------|
| OS              | Windows 11 + WSL 2            |
| Distro Linux    | Ubuntu 20.04 (WSL)            |
| CPU             | Intel Core i7-1165G7 @ 2.80GHz|
| RAM             | 16 GB                         |
| Penyimpanan     | SSD NVMe                      |

---

## 3. Pengujian FLOPS (CPU) - `sysbench`

### 🔧 Perintah:
```bash
sysbench cpu --cpu-max-prime=20000 run
```

### 📊 Hasil:
```
CPU speed:
    events per second:   464.77

General statistics:
    total time:                          10.0011s
    total number of events:              4648

Latency (ms):
         min:                                  2.08
         avg:                                  2.15
         max:                                  2.91
```

### ✅ Analisis:
Nilai `events per second` sebesar **464.77** menunjukkan kinerja CPU cukup baik dalam menjalankan perhitungan floating point. Latensi rata-rata rendah dan stabil.

---

## 4. Pengujian IOPS (Disk) - `fio`

### 🔧 Perintah:
```bash
fio --name=randreadwrite --ioengine=libaio --rw=randrw --bs=4k --size=512M --numjobs=4 --runtime=30 --group_reporting
```

### 📊 Hasil:
```
read: IOPS=5274, BW=20.6MiB/s
write: IOPS=5218, BW=20.4MiB/s
```

### ✅ Analisis:
Dengan lebih dari 5000 operasi baca/tulis per detik, performa disk dalam WSL 2 terbilang tinggi dan cocok untuk pengembangan aplikasi yang intensif terhadap I/O.

---

## 5. Kesimpulan

Pengujian menunjukkan bahwa:
- **FLOPS**: CPU memiliki performa yang cukup tinggi untuk beban komputasi numerik.
- **IOPS**: Sistem I/O dalam WSL 2 sangat responsif dan efisien.
- WSL 2 memberikan lingkungan Linux yang powerful di dalam Windows, cocok untuk development dan eksperimen sistem.

---

📝 *Catatan*: Laporan ini menggunakan simulasi dan hasil uji standar. Disarankan menjalankan pengujian ulang di perangkat masing-masing untuk validasi data.

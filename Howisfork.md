#Nama : Hafizh Hamas Muntazar
#NRP : 3124500060
#Kelas :D3 IT B
# 🚀 Pemahaman dan Contoh `fork()` di Bahasa C

Dokumentasi ini menjelaskan cara kerja `fork()` dalam bahasa C untuk membuat proses anak (child process) dari proses induk (parent process), lengkap dengan contoh kode dan penjelasan langkah-langkahnya.

---

## 🔁 Apa itu `fork()`?

`fork()` adalah **system call** pada sistem operasi berbasis UNIX/Linux yang digunakan untuk **menduplikasi (menggandakan) proses** yang sedang berjalan.

- Proses yang memanggil `fork()` disebut **parent process**.
- Proses hasil duplikasi disebut **child process**.
- Kedua proses akan berjalan **secara paralel** setelah `fork()` dipanggil.

---

## 💡 Nilai Kembalian `fork()`

| Nilai dari `fork()` | Keterangan                                 |
|---------------------|--------------------------------------------|
| `0`                 | Kode ini dijalankan oleh **child process** |
| `> 0`               | Kode ini dijalankan oleh **parent process**, dan nilainya adalah PID dari child |
| `< 0`               | Terjadi **error** saat membuat proses baru |

---

## 📂 Contoh Program Dasar `fork()`

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork(); // Membuat proses baru

    if (pid < 0) {
        // Gagal membuat child
        printf("Fork gagal!\n");
    } else if (pid == 0) {
        // Ini dijalankan oleh proses anak
        printf("Ini proses anak. PID = %d\n", getpid());
    } else {
        // Ini dijalankan oleh proses induk
        printf("Ini proses induk. PID = %d, PID anak = %d\n", getpid(), pid);
    }

    return 0;
}

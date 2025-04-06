#Nama : Hafizh Hamas Muntazar
#NRP : 3124500060
#Kelas :D3 IT B
# Cetak 1 2 3 Secara Berurutan Menggunakan `pthread` (C Language)

Program ini menggunakan tiga thread untuk mencetak angka `1`, `2`, dan `3` secara bergiliran dan terus-menerus. Sinkronisasi dilakukan menggunakan `pthread_mutex_t` dan `pthread_cond_t`.

## 💡 Penjelasan

- Setiap thread mencetak satu angka (1, 2, atau 3).
- Gunakan mutex (`lock`) untuk mencegah kondisi balapan (race condition).
- Gunakan `condition variable` (`cond`) untuk mengatur giliran setiap thread.
- Variabel global `done` digunakan sebagai penanda giliran thread.

Urutan cetak yang dihasilkan adalah:

```
1 2 3 1 2 3 1 2 3 ...
```

## 🧵 Implementasi Kode

```c
#include <stdio.h>
#include <pthread.h>

// Inisialisasi variabel kondisi dan mutex
pthread_cond_t cond[3] = {
    PTHREAD_COND_INITIALIZER,
    PTHREAD_COND_INITIALIZER,
    PTHREAD_COND_INITIALIZER
};
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;

int done = 1; // Menentukan giliran thread yang boleh print

void *print_number(void *arg) {
    int num = *(int *)arg;

    while (1) {
        pthread_mutex_lock(&lock);

        while (done != num) {
            pthread_cond_wait(&cond[num - 1], &lock);
        }

        // Mencetak angka
        printf("%d ", num);
        fflush(stdout); // Memastikan output langsung muncul di layar

        // Menentukan thread selanjutnya
        done = num % 3 + 1;
        pthread_cond_signal(&cond[done - 1]);

        pthread_mutex_unlock(&lock);
    }

    return NULL;
}

int main() {
    pthread_t threads[3];
    int nums[3] = {1, 2, 3};

    for (int i = 0; i < 3; i++) {
        pthread_create(&threads[i], NULL, print_number, &nums[i]);
    }

    // Menjaga program tetap berjalan
    while (1);

    return 0;
}
```

## ⚙️ Cara Kompilasi dan Jalankan

Gunakan `gcc` dan sertakan flag `-pthread` saat kompilasi:

```bash
gcc -o cetak123 main.c -pthread
./cetak123
```

## 📝 Catatan

- Program ini akan berjalan terus-menerus. Gunakan `Ctrl + C` untuk menghentikannya.
- Kode menggunakan `fflush(stdout)` untuk memastikan output tampil real-time, terutama saat dijalankan di IDE atau terminal dengan buffer output.

## 📚 Referensi

- Dokumentasi pthread: https://man7.org/linux/man-pages/man7/pthreads.7.html
- Tugas Thread Nomor 3-4 (Referensi Indonesia)

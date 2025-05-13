# Tugas 6 Sistem Operasi  
**Topik: Thread 3, Eksperimen Forking, Soal Nomor 3 & 4 (Referensi Bahasa Indonesia)**

**Nama:** Firas Rasendriya Athaillah  
**NRP:** 3124500042  
**Kelas:** D3 IT B
**Dosen:** Dr. Ferry Astika Saputra, S.T., M.Sc  

**PROGRAM STUDI D3 TEKNIK INFORMATIKA**  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)**  
**TAHUN 2024**

---

## 1. Kompilasi Thread 3

### Kode Program dan Langkah Eksekusi

```c
#include <stdio.h>
#include <pthread.h>

pthread_cond_t cond1 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond2 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond3 = PTHREAD_COND_INITIALIZER;
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
int done = 1;

void *foo(void *arg) {
    int thread_num = *(int *)arg;
    while (1) {
        pthread_mutex_lock(&lock);
        while (done != thread_num) {
            if (thread_num == 1) {
                pthread_cond_wait(&cond1, &lock);
            } else if (thread_num == 2) {
                pthread_cond_wait(&cond2, &lock);
            } else {
                pthread_cond_wait(&cond3, &lock);
            }
        }
        printf("%d ", thread_num);
        fflush(stdout);

        if (done == 3) {
            done = 1;
            pthread_cond_signal(&cond1);
        } else if (done == 1) {
            done = 2;
            pthread_cond_signal(&cond2);
        } else if (done == 2) {
            done = 3;
            pthread_cond_signal(&cond3);
        }
        pthread_mutex_unlock(&lock);
    }
    return NULL;
}

int main() {
    pthread_t tid1, tid2, tid3;
    int n1 = 1, n2 = 2, n3 = 3;
    pthread_create(&tid1, NULL, foo, &n1);
    pthread_create(&tid2, NULL, foo, &n2);
    pthread_create(&tid3, NULL, foo, &n3);

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);
    pthread_join(tid3, NULL);
    return 0;
}
```

### Langkah Eksekusi

1. Buka terminal di sistem Linux  
2. Jalankan perintah `nano print_123.c`  
3. Salin kode di atas dan tempelkan ke dalam file  
4. Simpan file dengan `CTRL + O`, tekan Enter, lalu keluar dengan `CTRL + X`  
5. Kompilasi menggunakan: `gcc -pthread print_123.c -o print_123`  
6. Jalankan program dengan: `./print_123`

### Hasil Output

```
1 2 3 1 2 3 ...
```

(Program akan terus mencetak hingga dihentikan secara manual dengan `CTRL + C`)

### Penjelasan Program

- Variabel `done` menentukan giliran thread yang mencetak angka.
- Tiga kondisi (`cond1`, `cond2`, `cond3`) digunakan untuk mengontrol aktivasi tiap thread secara bergiliran.
- `mutex` memastikan hanya satu thread yang bisa memodifikasi variabel `done` dalam satu waktu.

Fungsi `foo` dijalankan oleh tiap thread, menerima parameter identifikasi thread (1, 2, atau 3). Setelah mencetak angka, thread tersebut akan mengubah giliran ke thread berikutnya dan memberi sinyal untuk membangunkannya.

---

## 2. Eksperimen Forking

### Definisi Forking

Forking adalah metode dalam sistem operasi yang digunakan untuk membuat salinan proses yang sedang berjalan. Proses ini menciptakan *child process* yang identik dengan *parent process*, menggunakan sistem call `fork()`.

### Contoh Kode

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("Fork gagal");
        return 1;
    } else if (pid == 0) {
        printf("Ini adalah proses anak dengan PID %d\n", getpid());
    } else {
        printf("Ini adalah proses induk dengan PID %d dan anak dengan PID %d\n", getpid(), pid);
    }

    return 0;
}
```

### Penjelasan

- `fork()` memisahkan proses menjadi dua: induk dan anak.
- Jika hasilnya negatif, berarti fork gagal.
- Jika hasilnya nol, berarti proses anak yang sedang berjalan.
- Jika lebih dari nol, maka itu adalah proses induk yang menerima PID anak.

---

## Soal Nomor 3

### Pertanyaan:
**Apa keuntungan menggunakan ukuran time quantum yang berbeda pada tiap level dalam antrian multilevel?**

### Jawaban:

1. **Penyesuaian terhadap Jenis Proses**
   - Proses ringan/interaktif cocok dengan time quantum kecil untuk respons cepat.
   - Proses berat/CPU-bound memerlukan time quantum lebih besar agar efisien.

2. **Efisiensi Kinerja Sistem**
   - Mengurangi overhead akibat terlalu sering berpindah konteks.

3. **Meningkatkan Responsivitas dan Throughput**
   - Proses singkat bisa diselesaikan lebih cepat tanpa menghalangi proses lainnya.

4. **Keadilan dan Dinamika Prioritas (Multilevel Feedback Queue)**
   - Proses dapat berpindah level berdasarkan perilakunya: proses berat bisa turun, proses cepat bisa naik.

---

## Soal Nomor 4

### Tabel Proses

| Proses | Burst Time | Prioritas |
|--------|------------|-----------|
| P1     | 10         | 3         |
| P2     | 1          | 1         |
| P3     | 2          | 3         |
| P4     | 1          | 4         |
| P5     | 5          | 2         |

### A. FCFS (First Come First Serve)

Asumsi urutan masuk: P1 â†’ P2 â†’ P3 â†’ P4 â†’ P5

**Gantt Chart:**

```
P1 | P2 | P3 | P4 | P5
0   10  11  13  14  19
```

---

### B. SJF (Shortest Job First â€“ Nonpreemptive)

Urut berdasarkan durasi terpendek: P2 â†’ P4 â†’ P3 â†’ P5 â†’ P1

**Gantt Chart:**

```
P2 | P4 | P3 | P5 | P1
0    1   2    4    9   19
```

---

### C. Prioritas Nonpreemptive

Urutan berdasar prioritas (angka lebih kecil lebih prioritas): P2 â†’ P5 â†’ P1 â†’ P3 â†’ P4

**Gantt Chart:**

```
P2 | P5 | P1 | P3 | P4
0    1    6   16   18  19
```

---

### D. Round Robin (Quantum = 2)

Urutan awal: P1 (10), P2 (1), P3 (2), P4 (1), P5 (5)

**Gantt Chart:**

```
P1 | P2 | P3 | P4 | P5 | P1 | P5 | P1 | P5 | P1 | P1
0    2    3    5    6    8   10  12  13  15  17  19
```

---

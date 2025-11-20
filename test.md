### queue.h
```cpp
/* queue.h - Definisi Struktur Data */
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

#define MAX 5 // Kapasitas maksimal antrean adalah 5 elemen

typedef int infotype; // Tipe data yang disimpan adalah integer

struct Queue {
    infotype info[MAX]; // Array statis penyimpan data
    int head;           // Indeks penunjuk elemen pertama (yang akan dilayani)
    int tail;           // Indeks penunjuk elemen terakhir (data baru masuk)
};

// Deklarasi fungsi (Prototype)
void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x); // Menambah data
void dequeue(Queue &Q);             // Menghapus data
void printInfo(Queue Q);            // Menampilkan isi

#endif
```

### queuealt1.cpp
```cpp
/**
 * FILE: queue.cpp
 * METODE: Alternatif 1 (Geser saat Dequeue)
 * PENJELASAN: 
 * - Head selalu dianggap berada di posisi awal (indeks 0).
 * - Ketika satu elemen keluar, elemen-elemen di belakangnya digeser maju.
 */

#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1; // Menandakan antrean kosong
    Q.tail = -1; // Menandakan antrean kosong
}

bool isEmptyQueue(Queue Q) {
    // Kosong jika kedua pointer masih di -1
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    // Penuh jika ekor (tail) sudah mencapai batas maksimum array
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "queue penuh, tidak bisa menambah data" << endl;
    } else {
        // Jika antrean awalnya kosong, set head ke 0 agar valid
        if (isEmptyQueue(Q)) {
            Q.head = 0;
        }
        // 1. Majukan tail ke slot kosong berikutnya
        Q.tail++;
        // 2. Masukkan data ke posisi tail
        Q.info[Q.tail] = x;
    }
}

void dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "queue kosong" << endl;
    } else {
        // KASUS KHUSUS: Jika tinggal 1 elemen
        if (Q.head == Q.tail) {
            // Kembalikan ke status inisialisasi (kosong)
            createQueue(Q);
        } else {
            // LOGIKA GESER (SHIFTING):
            // Karena orang paling depan (indeks 0) keluar, semua orang
            // di belakangnya (indeks 1 s/d tail) harus maju satu langkah ke depan.
            // Ini adalah operasi yang 'berat' jika datanya banyak.
            for (int i = Q.head; i < Q.tail; i++) {
                // Salin data dari indeks [i+1] ke [i]
                Q.info[i] = Q.info[i + 1]; 
            }
            // Karena semua sudah maju, posisi ekor (tail) mundur satu langkah
            Q.tail--;
        }
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " \t " << Q.tail << " \t | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
    } else {
        // Cetak dari head sampai tail
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
        cout << endl;
    }
}
```

### queuealt2.cpp
```cpp
/**
 * FILE: queue2.cpp
 * METODE: Alternatif 2 (Head Bergerak & Geser saat Enqueue)
 * PENJELASAN:
 * - Head bergerak ke kanan saat dequeue (tidak ada geser langsung).
 * - Data baru digeser ulang ke indeks 0 HANYA jika tail mentok tapi head > 0.
 */

#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    // Cukup cek head = -1
    return (Q.head == -1);
}

bool isFullQueue(Queue Q) {
    // Definisi penuh sementara: Ekor sudah mentok di ujung array.
    // (Walaupun mungkin di depan (head) masih ada tempat kosong bekas dequeue)
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    // Cek apakah ekor sudah mentok di ujung array
    if (isFullQueue(Q)) {
        // CEK APAKAH INI "PENUH BENERAN" ATAU "PENUH SEMU"?
        // Jika head > 0, berarti ada ruang kosong di depan bekas dequeue.
        if (Q.head > 0) {
            // --- PROSES GESER (SHIFTING) ---
            // Pindahkan semua data yang masih valid (dari head s/d tail)
            // kembali ke posisi awal array (mulai indeks 0).
            for (int i = Q.head; i <= Q.tail; i++) {
                // Geser elemen ke kiri sejauh nilai 'head'
                // Saat i = 2: info[2 - 2] diisi info[2] -> info[0] = A. (Posisi 0 diisi A)
                Q.info[i - Q.head] = Q.info[i];
            }
            
            // Koreksi posisi indeks setelah penggeseran
            Q.tail = Q.tail - Q.head; // Tail mundur
            Q.head = 0;               // Head kembali ke 0
            
            // Setelah digeser dan dirapikan, barulah masukkan data baru
            Q.tail++;
            Q.info[Q.tail] = x;
        } else {
            // Jika head == 0 dan tail == MAX-1, berarti antrean benar-benar penuh.
            cout << "queue kosong, tidak bisa menambah data" << endl; 
            // Catatan: Pesan error di atas typo dari file asli, seharusnya "queue penuh"
        }
    } else {
        // KONDISI NORMAL (Belum mentok ujung)
        if (isEmptyQueue(Q)) {
            Q.head = 0;
        }
        Q.tail++;
        Q.info[Q.tail] = x;
    }
}

void dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "queue kosong" << endl;
    } else {
        // Jika tinggal 1 elemen
        if (Q.head == Q.tail) {
            createQueue(Q);
        } else {
            // Cukup majukan head. 
            // Data lama tidak dihapus/digeser, hanya indeks head yang "lari" menjauh.
            // Ini meninggalkan ruang kosong di indeks-indeks awal.
            Q.head++;
        }
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " \t " << Q.tail << " \t | ";
    
    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
    } else {
        // Loop hanya mencetak dari Head saat ini sampai Tail saat ini
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
        cout << endl;
    }
}
```

### queuealt3.cpp
```cpp
/* queue3.cpp - Implementasi Circular Queue (Tanpa Pergeseran) */
#include "queue.h"

// Inisialisasi Queue awal
void createQueue(Queue &Q) {
    Q.head = -1; // Menandakan antrean kosong
    Q.tail = -1; // Menandakan antrean kosong
}

// Cek apakah kosong
bool isEmptyQueue(Queue Q) {
    // Kosong jika head masih -1
    return (Q.head == -1);
}

// Cek apakah penuh (LOGIKA CIRCULAR)
bool isFullQueue(Queue Q) {
    // Queue penuh jika posisi setelah tail (secara melingkar) adalah head.
    // Rumus: (tail + 1) % MAX == head
    // Contoh: MAX=5. Tail di 4, Head di 0. (4+1)%5 = 0. Maka Penuh.
    return ((Q.tail + 1) % MAX == Q.head);
}

// Memasukkan data (Enqueue)
void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        // Jika penuh, tolak data
        cout << "queue penuh, tidak bisa menambah data" << endl;
    } else {
        // Jika antrean awalnya kosong total, set head ke 0
        if (isEmptyQueue(Q)) {
            Q.head = 0;
        }
        
        // Majukan tail secara melingkar (Circular).
        // Jika tail di indeks 4, (4+1)%5 = 0. Tail balik ke depan.
        // tail = 3 (3 + 1) = 4 % 5 = 4 maka tail = 4 (indeks 4)
        Q.tail = (Q.tail + 1) % MAX;
        
        // maka data yang baru dimasukan akan mengisi indeks 4 yang dan menjadi tail
        Q.info[Q.tail] = x;
    }
}

// Mengeluarkan data (Dequeue)
void dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "queue kosong" << endl;
    } else {
        // Kondisi jika antrean tinggal 1 elemen
        if (Q.head == Q.tail) {
            // Reset kembali ke status kosong awal (-1)
            createQueue(Q);
        } else {
            // Majukan head secara melingkar.
            // Head bergerak mengejar Tail.
            Q.head = (Q.head + 1) % MAX;
        }
    }
}

// Menampilkan status Queue
void printInfo(Queue Q) {
    // Tampilkan posisi indeks Head dan Tail saat ini
    cout << Q.head << " \t " << Q.tail << " \t | ";
    
    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
    } else {
        int i = Q.head;
        // Loop menggunakan while karena indeks berputar (bukan i++ biasa)
        while (true) {
            cout << Q.info[i] << " ";
            
            // Jika i sudah mencapai tail, berarti semua data sudah dicetak
            if (i == Q.tail) {
                break;
            }
            
            // Pindah ke elemen berikutnya secara melingkar
            i = (i + 1) % MAX;
        }
        cout << endl;
    }
}
```

### main.cpp
```cpp
/* main.cpp - Driver Code */
#include <iostream>
#include "queue.h"

using namespace std;

int main() {
    Queue Q;
    
    // Header tabel output
    cout << "H \t T \t | Queue info" << endl;
    cout << "----------------------------------" << endl;

    // 1. Inisialisasi
    createQueue(Q);
    printInfo(Q); // Output: -1 -1 | empty queue

    // 2. Masuk 5
    enqueue(Q, 5);
    printInfo(Q); // Output: 0 0 | 5

    // 3. Masuk 2
    enqueue(Q, 2);
    printInfo(Q); // Output: 0 1 | 5 2

    // 4. Masuk 7
    enqueue(Q, 7);
    printInfo(Q); // Output: 0 2 | 5 2 7

    // 5. Keluar satu (5 keluar)
    dequeue(Q);
    printInfo(Q); // Output: 1 2 | 2 7  <-- Perhatikan Head maju ke indeks 1

    // 6. Masuk 4
    enqueue(Q, 4);
    printInfo(Q); // Output: 1 3 | 2 7 4

    // 7. Keluar satu (2 keluar)
    dequeue(Q);
    printInfo(Q); // Output: 2 3 | 7 4

    // 8. Keluar satu (7 keluar)
    dequeue(Q);
    printInfo(Q); // Output: 3 3 | 4

    // 9. Keluar satu (4 keluar - habis)
    dequeue(Q);
    printInfo(Q); // Output: -1 -1 | empty queue

    return 0;
}

```

#### yey


# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA)</h1>
<p align="center">MOHAMMAD REYHAN ARETHA FATIN - 103112400078</p>

## Dasar Teori
Singly Linked List adalah struktur data yang terdiri dari kumpulan elemen (struct elmlist)  yang saling terhubung menggunakan pointer. Setiap elemen memiliki dua bagian: infotype (didefinisikan sebagai int ) untuk menyimpan data, dan pointer next yang menunjuk ke elemen berikutnya. List itu sendiri memiliki penanda awal bernama first, dan list dianggap kosong jika first bernilai Nil (atau NULL). Salah satu operasi dasar yang ditekankan dalam modul adalah searching (pencarian), yang didefinisikan sebagai proses mengunjungi setiap node secara berurutan dan berhenti ketika node yang dicari telah ditemukan. Operasi pencarian ini sangat penting karena menjadi fondasi untuk mempermudah implementasi operasi lain seperti insertAfter dan deleteAfter.

Metode pencarian yang dijelaskan ini mengunjungi setiap node satu per satu dari awal secara formal dikenal sebagai Linear Search (Pencarian Linier) atau Sequential Search (Pencarian Berurutan). Keunggulan utamanya adalah kesederhanaan implementasi dan fakta bahwa data list tidak perlu diurutkan terlebih dahulu. Namun, kelemahannya terletak pada efisiensi waktu. Dalam skenario terburuk, algoritma ini harus mengunjungi seluruh $n$ elemen, sehingga memiliki kompleksitas waktu O(n).

Sebagai perbandingan, terdapat algoritma Binary Search (Pencarian Biner) yang jauh lebih efisien dengan kompleksitas waktu O(log n). Algoritma ini bekerja dengan membagi kumpulan data menjadi dua bagian secara berulang dan hanya melanjutkan pencarian di separuh bagian yang relevan. Akan tetapi, binary search memiliki syarat mutlak: data harus sudah dalam keadaan terurut (sorted) dan struktur datanya harus mendukung random access (kemampuan mengakses elemen mana pun secara langsung, seperti array). Karena singly linked list tidak mendukung random access untuk mencapai node ke-i, kita harus selalu mulai dari first maka binary search tidak dapat diimplementasikan secara efisien pada struktur data ini.

## Guided

### Guided 1
```c++

```

> Output
> 
> ![Screenshot bagian x](OUTPUT/guided1.png)

Bagian pencarian data pada program ini, yang diimplementasikan dalam fungsi searchData, menggunakan algoritma pencarian linear (linear search). Fungsi ini bekerja dengan cara menelusuri (traversing) linked list mulai dari node pertama (head). Ia menggunakan sebuah pointer temporer untuk bergerak dari satu node ke node berikutnya dan sebuah variabel counter (pos) untuk menghitung posisi (dimulai dari 1). Pada setiap node, program akan membandingkan data di dalam node tersebut dengan key (nilai yang dicari). Jika data ditemukan, program akan mencetak pesan yang menunjukkan posisi data tersebut dan menghentikan pencarian. Jika program selesai menelusuri seluruh list (mencapai NULL) tanpa menemukan data, ia akan menampilkan pesan bahwa data tidak ditemukan.

### Soal 1

buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya

```c++


```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

Bagian pencarian pada program ini, yang diimplementasikan dalam fungsi cariPembeli, menggunakan algoritma pencarian linear (linear search). Fungsi ini bekerja dengan cara menelusuri (traversing) seluruh antrian dari head (paling depan) sampai ke akhir. Ia menggunakan sebuah pointer temporer untuk bergerak dari satu node ke node berikutnya dan sebuah variabel counter (posisi) untuk menghitung posisi antrian, dimulai dari 1. Pada setiap node, program akan membandingkan nama pembeli di node tersebut dengan nama yang dicari (namaCari). Keunikan dari fungsi ini adalah ia tidak berhenti setelah menemukan kecocokan pertama; ia akan terus mencari hingga akhir antrian. Hal ini memungkinkan program untuk menemukan dan menampilkan semua pembeli yang mungkin memiliki nama yang sama, lengkap dengan posisi antrian dan detail pesanan mereka. Jika setelah menelusuri seluruh antrian tidak ada satupun nama yang cocok, program akan menampilkan pesan bahwa pembeli tidak ditemukan.

### Soal 2
gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN

```c++


```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

Fungsi pencarian (cariBuku) pada program ini menerapkan algoritma pencarian linear (linear search) yang fleksibel. Pertama, program ini mengizinkan pengguna untuk memilih kriteria pencarian: berdasarkan ISBN, Judul, atau Penulis. Setelah pengguna memasukkan kata kunci pencarian (searchTerm), fungsi akan menelusuri (traversing) keseluruhan linked list satu per satu, mulai dari head. Pada setiap node, ia akan membandingkan data buku dengan kata kunci tersebut. Program ini dirancang untuk menemukan dan menampilkan semua data buku yang cocok, sehingga ia tidak berhenti setelah temuan pertama dan akan terus mencari hingga akhir list. Jika tidak ada satupun data yang cocok ditemukan setelah seluruh list diperiksa, program akan menampilkan pesan bahwa buku tidak ditemukan.

## Referensi

1. https://www.kodingakademi.id/mengenal-linear-search-algoritma-pencarian-dasar/ (diakses pada 18 Oktober 2025)
2. https://daismabali.medium.com/metode-searching-dalam-struktur-data-dan-implementasi-pemrogramannya-d97582084866 (diakses pada 18 Oktober 2025)
3. https://www.kodingakademi.id/pengenalan-searching-dalam-c/ (diakses pada 18 Oktober 2025)

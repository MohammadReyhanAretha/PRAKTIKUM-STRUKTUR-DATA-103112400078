# <h1 align="center">Laporan Praktikum Modul 6 <br>STACK</h1>
<p align="center">MOHAMMAD REYHAN ARETHA FATIN - 103112400078</p>

## Dasar Teori
Stack (Tumpukan) adalah salah satu bentuk struktur data linier yang menerapkan prinsip operasi LIFO (Last In First Out). Sesuai dengan namanya, "tumpukan", data yang terakhir kali dimasukkan adalah data yang akan pertama kali dikeluarkan. Bayangkan sebuah tumpukan piring; Anda hanya bisa menambah piring baru di atas (paling atas) dan mengambil piring dari atas (paling atas). Titik akses tunggal dalam stack ini disebut sebagai "Top"

Terdapat dua operasi utama dalam stack. Operasi pertama adalah Push, yaitu proses menyisipkan atau menambahkan elemen baru ke dalam tumpukan. Elemen baru ini akan selalu ditempatkan di posisi Top. Operasi kedua adalah Pop, yaitu proses mengambil atau mengeluarkan elemen dari tumpukan. Elemen yang diambil pastilah elemen yang berada di posisi Top.

Stack dapat diimplementasikan menggunakan dua cara: pointer (seperti singly linked list) atau tabel (menggunakan array). Dalam implementasi menggunakan tabel/array, stack memiliki jumlah tumpukan yang terbatas, yang ditentukan oleh ukuran maksimum array (Imax). Indikator Top digunakan sebagai indeks array untuk menandai posisi data teratas. Saat stack kosong, Top biasanya diinisialisasi ke 0 (atau -1, tergantung konvensi). Operasi Push dilakukan dengan menambah nilai Top (Top = Top + 1) lalu memasukkan data ke array pada indeks Top tersebut. Sebaliknya, operasi Pop dilakukan dengan mengambil data pada indeks Top, kemudian mengurangi nilai Top (TOP = TOP - 1).

## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data)
{
    Node *newNode = new Node();
    newNode->data = data;
    newNode->next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top->data;
    Node *temp = top;
    top = top->next;
    
    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
    {
        cout << "Stack kosong." << endl;
        return;
    }

    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << " -> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;
}

int main()
{
    Node*stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);
    
    cout << "menampilkan isi stack: " << endl;
    show(stack);

    cout << "pop: " <<(stack) <<endl;

    cout << "menampilkan sisa stack: " << endl;
    show(stack);

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/guided1.png)

program yang mengimplementasikan stack menggunakan linked list. Program melakukan push 10, 20, dan 30. Saat show(stack) dipanggil pertama kali, stack dicetak dengan benar sebagai TOP -> 30 -> 20 -> 10 -> NULL. Namun, pada baris cout << "pop: " <<(stack) <<endl;, terjadi kesalahan di mana program mencetak alamat memori dari pointer stack (misalnya 0xa1f6eff8), bukan memanggil fungsi pop(stack) untuk mengeluarkan elemen. Akibatnya, tidak ada elemen yang dihapus dari stack. Oleh karena itu, ketika show(stack) dipanggil untuk kedua kalinya, isi stack ditampilkan tetap utuh seperti semula: TOP -> 30 -> 20 -> 10 -> NULL.

## UNGUIDED

### Soal 1

> ![Screenshot bagian x](OUTPUT/SOAL1.png)

### Soal 2

> ![Screenshot bagian x](OUTPUT/SOAL2.png)

### Soal 3

> ![Screenshot bagian x](OUTPUT/SOAL3.png)

### JAWABAN NOMOR 1,2,3

#### stack.h
```c++
#ifndef STACK_H
#define STACK_H

#include <iostream>
#define MAX_STACK 20 

typedef int infotype;

struct Stack {
    infotype info[MAX_STACK + 1]; 
    int top;
};
void createStack(Stack &S);
bool isEmpty(Stack S);
bool isFull(Stack S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);
void getInputStream(Stack &S);

#endif
```
#### stack.cpp
```c++
#include "stack.h"
#include <iostream> 

using namespace std; 

void createStack(Stack &S) {
    S.top = 0;
}

bool isEmpty(Stack S) {
    return S.top == 0;
}
bool isFull(Stack S) {
    return S.top == MAX_STACK;
}
void push(Stack &S, infotype x) {
    if (!isFull(S)) {
        S.top++; 
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}
infotype pop(Stack &S) {
    if (!isEmpty(S)) {
        infotype x = S.info[S.top];
        S.top--; 
        return x;
    } else {
        cout << "Stack kosong!" << endl; 
        return -1; 
    }
}

void printInfo(Stack S) {
    cout << "[TOP] "; 
    for (int i = S.top; i >= 1; i--) {
        cout << S.info[i] << " "; 
    }
    cout << endl; 
}

void balikStack(Stack &S) {
    Stack temp1, temp2;
    createStack(temp1);
    createStack(temp2);

    while (!isEmpty(S)) {
        push(temp1, pop(S));
    }
    while (!isEmpty(temp1)) {
        push(temp2, pop(temp1));
    }
    while (!isEmpty(temp2)) {
        push(S, pop(temp2));
    }
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);
    while (!isEmpty(S) && x > S.info[S.top]) {
        push(temp, pop(S));
    }
    push(S, x);
    while (!isEmpty(temp)) {
        push(S, pop(temp));
    }
}

void getInputStream(Stack &S) {
    char c;
    c = cin.get(); 
    while (c != '\n') {
        if (c >= '0' && c <= '9') {
            push(S, c - '0');
        }
        c = cin.get(); 
    }
}
```
#### main.cpp
```c++
#include "stack.h"
#include <iostream>

using namespace std;

int main() {
    
    // Latihan 1
    cout << "Hello world!" << endl; 
    Stack S1;
    createStack(S1); 
    push(S1, 3);     
    push(S1, 4);     
    push(S1, 8);     
    pop(S1);         
    push(S1, 2);     
    push(S1, 3);     
    pop(S1);         
    push(S1, 9);     
    printInfo(S1);   
    cout << "balik stack" << endl; 
    balikStack(S1);  
    printInfo(S1);   

    cout << endl; 

    // Latihan 2
    cout << "Hello world!" << endl; 
    Stack S2;
    createStack(S2); 
    pushAscending(S2, 3); 
    pushAscending(S2, 4); 
    pushAscending(S2, 8); 
    pushAscending(S2, 2); 
    pushAscending(S2, 3); 
    pushAscending(S2, 9); 
    printInfo(S2); 
    cout << "balik stack" << endl; 
    balikStack(S2); 
    printInfo(S2); 

    cout << endl; 

    // Latihan 3
    cout << "Hello world!" << endl; 
    Stack S3;
    createStack(S3); 
    
    cin.sync(); 
    
    getInputStream(S3); 
    printInfo(S3); 
    cout << "balik stack" << endl; 
    balikStack(S3); 
    printInfo(S3); 

    return 0; 
}
```
#### OUTPUT & DEKSRIPSI PROGRAM
> Output soal 1
> 
> ![Screenshot bagian x](OUTPUT/unguided1.png)

Program implementasi stack berbasis array. Program membuat stack S1 dan melakukan serangkaian operasi: push(3), push(4), push(8), pop() (menghapus 8), push(2), push(3), pop() (menghapus 3), dan terakhir push(9). Fungsi printInfo(S1) kemudian mencetak isi stack dari atas ke bawah, menghasilkan [TOP] 9 2 4 3. Setelah itu, fungsi balikStack(S1) dipanggil, yang membalik urutan elemen dalam stack. Pemanggilan printInfo(S1) yang kedua kalinya menunjukkan stack yang telah dibalik: [TOP] 3 4 2 9.
> Output soal 2
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

Program yang menggunakan fungsi pushAscending. Fungsi ini memastikan setiap elemen yang dimasukkan (3, 4, 8, 2, 3, 9) ke stack S2 akan menjaga stack tetap terurut, dengan elemen terkecil berada di posisi top. Setiap kali push, elemen baru disisipkan ke posisi yang benar dengan memindahkan elemen yang lebih besar ke stack sementara lalu mengembalikannya. Hasil cetakan pertama printInfo(S2) menunjukkan stack yang terurut [TOP] 2 3 3 4 8 9 (2 adalah elemen teratas). Kemudian, balikStack(S2) membalik urutan stack ini, sehingga hasil cetakan kedua adalah [TOP] 9 8 4 3 3 2, yang kini terurut dengan elemen terbesar di atas.

> Output soal 3
> 
> ![Screenshot bagian x](OUTPUT/unguided3.png)
> 
Program yang menguji fungsi getInputStream. Setelah "Hello world!" tercetak, program menunggu input pengguna. Pengguna memasukkan 4729601, yang ditampilkan di layar. Fungsi getInputStream membaca input ini karakter per karakter dan langsung melakukan push setiap digit ke stack S3. Karena stack bersifat LIFO (Last-In, First-Out), digit '1' yang terakhir dimasukkan menjadi elemen top. Cetakan printInfo(S3) pertama menunjukkan isi stack dalam urutan terbalik dari input: [TOP] 1 0 6 9 2 7 4. Terakhir, fungsi balikStack(S3) dipanggil, membalikkan stack kembali ke urutan aslinya, yang dicetak sebagai [TOP] 4 7 2 9 6 0 1.




## Referensi

1. https://www.geeksforgeeks.org/stack-data-structure/ (diakses pada 1 November 2025)
2. https://www.programiz.com/dsa/stack (diakses pada 1 November 2025)
3. https://www.tutorialspoint.com/data_structures_algorithms/stack_algorithm.htm (diakses pada 1 November 2025)

# <h1 align="center">Laporan Praktikum Modul 1 <br> CODE BLOCKS IDE & PENGENALAN BAHASA C++</h1>
<p align="center">MOHAMMAD REYHAN ARETHA FATIN - 103112400078</p>

## Dasar Teori
Bahasa C++ adalah bahasa pemrograman yang dibuat oleh Bjarne Stroustrup, dikembangkan sebagai versi yang lebih canggih dari bahasa C. Bahasa ini mendukung paradigma pemrograman berorientasi objek, yang membedakannya dari pendahulunya. Dalam praktikum ini, C++ digunakan sebagai bahasa utama. C++ memiliki struktur dasar yang terdiri dari pustaka (#include) dan fungsi main(). Komponen utamanya adalah variabel untuk menyimpan data, konstanta untuk nilai tetap, dan operator untuk melakukan perhitungan atau logika. Interaksi dengan pengguna ditangani oleh cin (input) dan cout (output). Alur program dikendalikan oleh pernyataan kondisional seperti if dan switch untuk pengambilan keputusan , serta perulangan seperti for dan while untuk tugas berulang. Terakhir, struct digunakan untuk mengelompokkan berbagai tipe data yang saling terkait menjadi satu kesatuan.

## Guided

### Aritmatika
```c++
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}
```
> Output
> 
> ![Screenshot bagian x](OUTPUT/aritmatika.png)

Program ini bersifat non-interaktif atau statis. Tidak meminta input: Program ini langsung berjalan tanpa memintamu memasukkan angka apa pun. Perhitungan sudah ditentukan Operasi matematikanya (misalnya, z = 5 - 3;) sudah tertulis di dalam kode. Nilainya sudah pasti dan tidak bisa diubah saat program berjalan. Tujuannya biasanya untuk mendemonstrasikan sebuah perhitungan spesifik atau untuk mendapatkan hasil dari sebuah rumus yang nilainya sudah diketahui. Singkatnya, program ini menjalankan perhitungan yang sudah ditetapkan dari awal dan hanya menampilkan hasilnya.

### Fungsi
```c++
#include <iostream>
using namespace std;

// Prosedur: hanya menampilkan hasil, tidak mengembalikan nilai
void tampilkanHasil(double p, double l)
{
    cout << "\n=== Hasil Perhitungan ===" << endl;
    cout << "Panjang : " << p << endl;
    cout << "Lebar   : " << l << endl;
    cout << "Luas    : " << p * l << endl;
    cout << "Keliling: " << 2 * (p + l) << endl;
}

// Fungsi: mengembalikan nilai luas
double hitungLuas(double p, double l)
{
    return p * l;
}

// Fungsi: mengembalikan nilai keliling
double hitungKeliling(double p, double l)
{
    return 2 * (p + l);
}

int main()
{
    double panjang, lebar;

    cout << "Masukkan panjang: ";
    cin >> panjang;
    cout << "Masukkan lebar  : ";
    cin >> lebar;

    // Panggil fungsi
    double luas = hitungLuas(panjang, lebar);
    double keliling = hitungKeliling(panjang, lebar);

    cout << "\nDihitung dengan fungsi:" << endl;
    cout << "Luas      = " << luas << endl;
    cout << "Keliling  = " << keliling << endl;

    // Panggil prosedur
    tampilkanHasil(panjang, lebar);

    return 0;
}

```

> Output
> 
> ![Screenshot bagian x](OUTPUT/fungsi.png)

Program ini bertugas untuk menghitung luas dan keliling persegi panjang. Kamu hanya perlu memasukkan nilai panjang dan lebar. Program ini menggunakan "fungsi" terpisah untuk masing-masing perhitungan, sehingga kodenya lebih rapi dan terstruktur.

### Kondisi
```c++
int main()
{
    int kode_hari;
    cout << "Menentukan hari kerja/libur\n"<<endl;
    cout << "1=Senin 3=Rabu 5=Jumat 7=Minggu "<<endl;
    cout << "2=Selasa 4=Kamis 6=Sabtu "<<endl;
    cin >> kode_hari;
    switch (kode_hari)
    {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout<<"Hari Kerja";
        break;
    case 6:
    case 7:
        cout<<"Hari Libur";
        break;
    default:
        cout<<"Kode masukan salah!!!";
    }
    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/kondisi.png)

Program ini adalah penentu hari kerja atau hari libur. Kamu memasukkan angka yang mewakili hari (misalnya 1 untuk Senin, 6 untuk Sabtu). Program kemudian akan menggunakan logika if-else atau switch untuk memeriksa angka tersebut dan memberimu output "Hari Kerja" atau "Hari Libur" sesuai aturan yang ditentukan.

### Perulangan
```c++
int main()
{
    int i = 1;
    int jum;
    cin >> jum;
    do
    {
        cout << "bahlil ke-" << (i + 1) << endl;
        i++;
    } while (i < jum);
    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/perulangan.png)

Program ini menunjukkan cara kerja perulangan (looping). Kamu memasukkan sebuah angka (misalnya 5), dan program akan mencetak sebuah kalimat berulang kali, dari angka 2 sampai angka yang kamu masukkan. Ini berguna untuk melakukan tugas yang sama berkali-kali secara otomatis.

### Struct
```c++
#include <iostream>
#include <string>
using namespace std;

// Definisi struct
struct Mahasiswa {
    string nama;
    string nim;
    float ipk;
};

int main() {

    Mahasiswa mhs1;

    cout << "Masukkan Nama Mahasiswa: ";
    getline(cin, mhs1.nama);
    // cin >> mhs1.nama;
    cout << "Masukkan NIM Mahasiswa : ";
    cin >> mhs1.nim;
    cout << "Masukkan IPK Mahasiswa : ";
    cin >> mhs1.ipk;

    cout << "\n=== Data Mahasiswa ===" << endl;
    cout << "Nama : " << mhs1.nama << endl;
    cout << "NIM  : " << mhs1.nim << endl;
    cout << "IPK  : " << mhs1.ipk << endl;

    return 0;
}

```

> Output
> 
> ![Screenshot bagian x](OUTPUT/struct.png)

Program ini berfungsi seperti formulir digital untuk data mahasiswa. Kamu akan diminta mengisi: Nama, NIM, IPK, Data tersebut kemudian disimpan dalam sebuah struct, yaitu sebuah "wadah" yang bisa menampung berbagai jenis data yang saling berhubungan. Setelah diisi, program akan menampilkan kembali data yang sudah kamu masukkan.

### Test
```c++
#include <iostream>
using namespace std;
int main()
{
    string ch;
    cout << "Masukkan sebuah karakter: ";
    // cin >> ch;
    ch = getchar();  //Menggunakan getchar() untuk membaca satu karakter
    cout << "Karakter yang Anda masukkan adalah: " << ch << endl;
    return 0;
}

```
> Output
> 
> ![Screenshot bagian x](OUTPUT/testcpp.png)

Program ini dirancang untuk membaca satu karakter saja. Walaupun kamu mengetik "Kelapa Muda", program hanya akan mengambil dan menampilkan huruf pertamanya, yaitu 'K'. Ini menunjukkan cara kerja input dasar untuk tipe data karakter (char) di C++

## Unguided

### Soal 1

> ![Screenshot bagian x](SOAL/GSoal1.png)

```c++
#include <iostream>
using namespace std;

int main() {
   float a, b;
   cout << "masukkan angka : ";
   cin >> a;
   cout << "masukkan angka : ";
   cin >> b;
   cout << "penjumlahan : " << a + b << endl;
   cout << "pengurangan : " << a - b << endl;
   cout << "perkalian : " << a * b << endl;
   cout << "pembagian : " << a / b << endl;

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/Soal1.png)

Program ini seperti kalkulator dasar. Kamu memasukkan dua angka, lalu program akan otomatis melakukan empat operasi matematika dasar:
Penjumlahan (+), Pengurangan (-), Perkalian (*), Pembagian (/), Hasil dari setiap operasi kemudian ditampilkan di layar. Program aritmatika.png juga melakukan hal serupa, yaitu menghitung nilai menggunakan operasi matematika dan menampilkan hasilnya.

### Soal 2

> ![Screenshot bagian x](SOAL/GSoal3.png)

```c++
#include <iostream>
#include <string>

using namespace std;

int main() {
    int angka;
    string tulisan = "";

    cout << "Masukkan angka (0-100): ";
    cin >> angka;

    string satuan[] = {"", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan"};

    if (angka < 0 || angka > 100) {
        tulisan = "Input tidak valid. Harap masukkan angka antara 0 dan 100.";
    } else if (angka == 0) {
        tulisan = "nol";
    } else if (angka == 100) {
        tulisan = "seratus";
    } else if (angka == 11) {
        tulisan = "sebelas";
    } else if (angka < 10) {
        tulisan = satuan[angka];
    } else if (angka < 20) {
        tulisan = satuan[angka % 10] + " belas";
    } else {
        int puluhan = angka / 10;
        int sisa = angka % 10;
        tulisan = satuan[puluhan] + " puluh " + satuan[sisa];
    }

    cout << "Output: " << angka << " : " << tulisan << endl;

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/Soal2.png)

Ini adalah program penerjemah angka menjadi tulisan. Kamu memasukkan sebuah angka (contohnya 79), dan program akan mengubahnya menjadi format teks dalam bahasa Indonesia, yaitu "tujuh puluh sembilan".

### Soal 3

> ![Screenshot bagian x](SOAL/GSoal3.png)

```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    cout << "Input: ";
    cin >> n;
    cout << "Output:" << endl;

    for (int i = n; i >= 1; i--) {
        for (int k = 0; k < n - i; k++) {
            cout << "  ";
        }
        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }
        cout << "* ";
        for (int j = 1; j <= i; j++) {
            cout << j << " ";
        }
        cout << endl;
    }
    for (int k = 0; k < n; k++) {
        cout << "  ";
    }
    cout << "*" << endl;

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/Soal3.png)

Program ini adalah contoh kreativitas menggunakan perulangan bersarang (nested loop). Kamu memasukkan satu angka, dan program akan menggunakan angka tersebut sebagai titik awal untuk menggambar pola segitiga simetris yang unik menggunakan angka dan simbol bintang *.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)

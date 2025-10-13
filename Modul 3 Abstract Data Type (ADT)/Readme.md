# <h1 align="center">Laporan Praktikum Modul 3 <br> Abstract Data Type</h1>
<p align="center">Zaki Hamdani - 103112400089</p>

## Dasar Teori

Abstract Data Type (ADT) membahas konsep pembentukan tipe data abstrak yang memisahkan antara spesifikasi dan implementasi suatu tipe data. ADT merupakan tipe data buatan pengguna yang memiliki sekumpulan operasi dasar (primitif) untuk mengelola dan memanipulasi data, seperti konstruktor, selektor, mutator, validator, dan destruktor. Dalam penerapannya, ADT biasanya terdiri dari dua bagian, yaitu file header (.h) yang berisi definisi tipe dan deklarasi fungsi, serta file implementasi (.cpp) yang memuat realisasi fungsinya. Konsep ini meningkatkan modularitas, keterbacaan, dan kemudahan pemeliharaan program, seperti pada contoh ADT mahasiswa dan pelajaran dalam bahasa C++.

## Guide

## Menghitung Rata Rata

## mahasiswa.h
```go
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};

void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);

#endif
```

## Mahasiswa.cpp
```go
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m) .nim;
    cout << "input nilai = ";
    cin >> (m) .nilai1;
    cout << "input niali2 = ";
    cin >> m .nilai2;

}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}
```

## main.cpp
```go
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main(){
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata rata = " << rata2(mhs);
    return 0;
}
```

## Unguide

### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.
```go
#include <iostream>
#include <string>
#include <iomanip>
#include <limits>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3f * uts + 0.4f * uas + 0.3f * tugas;
}

int main() {
    Mahasiswa mhs[10];
    int n = 0;
    while (true) {
        cout << "\n1. Tambah data\n2. Tampilkan data\n3. Keluar\nPilih menu: ";
        int pilihan;
        if (!(cin >> pilihan)) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Input tidak valid.\n";
            continue;
        }

        if (pilihan == 1) {
            if (n >= 10) {
                cout << "Data penuh (maks 10 mahasiswa).\n";
                continue;
            }
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Nama   : ";
            getline(cin, mhs[n].nama);
            cout << "NIM    : ";
            getline(cin, mhs[n].nim);
            cout << "Nilai UTS  : ";
            while (!(cin >> mhs[n].uts)) {
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                cout << "Masukkan angka untuk UTS: ";
            }
            cout << "Nilai UAS  : ";
            while (!(cin >> mhs[n].uas)) {
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                cout << "Masukkan angka untuk UAS: ";
            }
            cout << "Nilai Tugas: ";
            while (!(cin >> mhs[n].tugas)) {
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                cout << "Masukkan angka untuk Tugas: ";
            }
            mhs[n].nilaiAkhir = hitungNilaiAkhir(mhs[n].uts, mhs[n].uas, mhs[n].tugas);
            n++;
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Data berhasil ditambah.\n";
        } else if (pilihan == 2) {
            if (n == 0) {
                cout << "Belum ada data.\n";
                continue;
            }
            cout << "\nDaftar Nilai Mahasiswa\n";
            cout << left << setw(4) << "No" << setw(25) << "Nama" << setw(12) << "NIM" << setw(10) << "NilaiAkhir" << '\n';
            cout << string(55, '-') << '\n';
            cout << fixed << setprecision(2);
            for (int i = 0; i < n; ++i) {
                cout << left << setw(4) << (i + 1)
                     << setw(25) << mhs[i].nama
                     << setw(12) << mhs[i].nim
                     << setw(10) << mhs[i].nilaiAkhir << '\n';
            }
        } else if (pilihan == 3) {
            cout << "Keluar.\n";
            break;
        } else {
            cout << "Pilihan tidak tersedia.\n";
        }
    }
    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no1.png)

Program ini merupakan aplikasi sederhana untuk mengelola data mahasiswa menggunakan struktur data dan fungsi dalam bahasa C++. Program mendefinisikan sebuah struct bernama *Mahasiswa* yang berisi field nama, NIM, nilai UTS, UAS, tugas, dan nilai akhir. Fungsi *hitungNilaiAkhir()* digunakan untuk menghitung nilai akhir mahasiswa dengan rumus 0.3 × UTS + 0.4 × UAS + 0.3 × tugas. Di dalam fungsi utama (*main*), program menampilkan menu dengan tiga pilihan yaitu menambah data, menampilkan data, dan keluar. Pengguna dapat memasukkan hingga 10 data mahasiswa, di mana setiap data yang diinput akan otomatis dihitung nilai akhirnya. Hasil data kemudian ditampilkan dalam bentuk tabel rapi menggunakan format dari pustaka *iomanip*. Program ini juga dilengkapi validasi input dan pembatasan jumlah data, sehingga mencerminkan penerapan prinsip modularitas, pengelolaan data terstruktur, serta konsep dasar *Abstract Data Type (ADT)* dalam pemrograman.


### Soal 2

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5

Nilai setelah dikuadratkan: 25

```go
#include <iostream>
using namespace std;

void kuadratkan(int &x) {
    x = x * x;
}

int main() {
    int nilai = 5;

    cout << "Nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "Nilai setelah dikuadratkan: " << nilai << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no2.png)

Program ini menggunakan call by reference agar parameter x di prosedur kuadratkan langsung mengacu pada variabel asli yang dikirim dari main(). Dengan demikian, ketika x dikuadratkan (x = x * x), nilai asli variabel nilai ikut berubah. Hasilnya, setelah prosedur dipanggil, nilai nilai berubah dari 5 menjadi 25.

## Referensi
1. https://www.w3schools.com/cpp/cpp_references.asp
2. https://www.w3schools.com/cpp/cpp_function_reference.asp
3. https://www.w3schools.com/cpp/cpp_function_structures.asp
4. https://www.w3schools.com/cpp/exercise.asp?x=xrcise_function_reference1
5. https://www.w3schools.com/cpp/cpp_function_param.asp





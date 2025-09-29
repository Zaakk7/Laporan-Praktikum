# <h1 align="center">Laporan Praktikum Modul 1 <br> Pengenalan c++</h1>
<p align="center">Zaki Hamdani - 103112400089</p>

## Dasar Teori

Dalam C++ ada beberapa dasar penting yang biasa dipelajari, yaitu struct, aritmatika, kondisi, perulangan, dan fungsi. Struct dipakai buat ngumpulin beberapa variabel dengan tipe berbeda dalam satu wadah supaya data lebih gampang diatur. Aritmatika berhubungan sama operator kayak +, -, *, /, dan % buat ngelakuin hitungan matematis. Kondisi atau percabangan (if, else if, else, switch) dipakai biar program bisa milih jalannya sesuai syarat yang ada. Perulangan (for, while, do while) berguna buat ngejalanin kode berulang-ulang tanpa harus nulis perintah banyak kali. Sementara itu, fungsi adalah blok kode yang bisa dipanggil kapan aja buat tugas tertentu, jadi program lebih rapi, gampang dibaca, dan bisa dipakai lagi.

## Guide

## (Struck)
```go
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

## (Aritmatika)
```go
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

## (Kondisi)
```go
#include <iostream>
using namespace std;

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

## (Perulangan)
```go
#include <iostream>
using namespace std;

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

## (Fungsi)
```go
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

## (Test)
```go
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

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan betipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut

```go
#include <iostream>

using namespace std;

int main(){
    float a;
    float b;

    cout << "Masukan Bilangan ke 1: ";
    cin >> a;
    cout << "Masukan bilangan ke 2: ";
    cin >> b;
    
    float penjumlahan = a + b;
    float pengurangan = a - b;
    float perkalian = a * b;
    float pembagian = a / b;

    cout << "penjumlahan: " << a << " dengan " << b << " adalah: " << penjumlahan << endl;
    cout << "pengurangan: " << a << " dengan " << b << " adalah: " << pengurangan << endl;
    cout << "perkalian: " << a << " dengan " << b << " adalah: " << perkalian << endl;
    cout << "pembagian: " << a << " dengan " << b << " adalah: " << pembagian << endl;

    return 0;

}
```

> Output
> ![Screenshot bagian x](Output/output_no1.png)

Penjelasan Kode
Program di atas meminta pengguna memasukkan dua bilangan, lalu menghitung penjumlahan, pengurangan, perkalian, dan pembagiannya. Hasil dari setiap operasi ditampilkan ke layar menggunakan cout, dan return 0; menandakan program selesai dengan normal.

### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100

```go
#include <iostream>
#include <string>
using namespace std;

int main() {
    int angka;
    string teks;
    
    string satuan[] = {"nol", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan"};
    string belasan[] = {"sepuluh", "sebelas", "dua belas", "tiga belas", "empat belas", "lima belas", 
                        "enam belas", "tujuh belas", "delapan belas", "sembilan belas"};
    
    cout << "Masukkan angka (0-100): ";
    cin >> angka;
    
    if (angka < 0 || angka > 100) {
        cout << "Angka harus antara 0 dan 100!" << endl;
        return 1;
    }
    
    if (angka < 10) {
        teks = satuan[angka];
    } else if (angka >= 10 && angka < 20) {
        teks = belasan[angka - 10];
    } else if (angka >= 20 && angka < 100) {
        int puluhan = angka / 10;
        int sisa = angka % 10;
        if (sisa == 0) {
            teks = satuan[puluhan] + " puluh";
        } else {
            teks = satuan[puluhan] + " puluh " + satuan[sisa];
        }
    } else if (angka == 100) {
        teks = "seratus";
    }
    
    cout << angka << " : " << teks << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/output_no2.png)

Program di atas digunakan untuk mengubah angka menjadi tulisan dalam bahasa Indonesia untuk rentang 0–100. Pertama, pengguna diminta memasukkan angka, lalu program mengecek apakah angka valid. Jika kurang dari 10, hasil diambil dari array satuan, jika 10–19 diambil dari array belasan, jika 20–99 dibentuk dari kata “puluh” ditambah satuan, dan khusus angka 100 ditampilkan sebagai “seratus”. Hasil akhirnya ditampilkan ke layar dalam bentuk angka dan teks.

### soal 3

Buatlah program yang dapat memberikan input dan output sbb.

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    
    cout << "input: ";
    cin >> n;
    
    cout << "output:" << endl;
    
    for (int i = n; i >= 1; i--) {
        
        for (int s = 0; s < (n - i); s++) {
            cout << "  ";
        }
        
        
        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }
        
        cout << "* ";
        
        
        for (int j = 1; j <= i; j++) {
            cout << j;
            if (j < i) {
                cout << " ";
            }
        }
        cout << endl;
    }
    
    
    for (int s = 0; s < n; s++) {
        cout << "  ";
    }
    cout << "*" << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/output_no3.png)

Program di atas meminta input sebuah angka `n`, lalu menampilkan pola berbentuk segitiga menurun dengan angka dari besar ke kecil di sebelah kiri, tanda `*` di tengah, dan angka dari kecil ke besar di sebelah kanan. Setiap baris bergeser ke kanan dengan spasi sesuai urutan, dan di bagian akhir program menambahkan satu `*` di bawah tengah pola.

## Referensi
1. https://www.w3schools.com/cpp/cpp_variables_multiple.asp
2. https://www.w3schools.com/cpp/cpp_conditions.asp
3. https://www.w3schools.com/cpp/cpp_arrays.asp
4. https://www.w3schools.com/cpp/cpp_conditions_else.asp
5. https://www.w3schools.com/cpp/cpp_for_loop.asp
6. https://www.w3schools.com/cpp/cpp_conditions_elseif.asp


# <h1 align="center">Laporan Praktikum Modul 1 <br> Pengenalan c++</h1>
<p align="center">Zaki Hamdani - 103112400089</p>

## Dasar Teori

Call by reference adalah metode pemanggilan fungsi di C++ di mana yang dikirim ke fungsi bukan nilai variabel, melainkan alamat memorinya. Dengan menambahkan tanda & pada parameter, fungsi dapat mengakses dan mengubah nilai asli variabel yang dikirim dari program utama. Berbeda dengan call by value yang hanya menyalin nilai, call by reference memungkinkan perubahan di dalam fungsi langsung memengaruhi variabel asli. Metode ini lebih efisien karena tidak membuat salinan data dan sering digunakan saat program perlu memodifikasi nilai variabel secara langsung.

## Guide


## Unguide

### Soal 1

Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:
1 2 3
4 5 6
7 8 9

Matriks Hasil Transpose:
1 4 7
2 5 8
3 6 9

```go
#include <iostream>
using namespace std;

int main() {
    int matrik[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    int transpose[3][3];

    cout << "Matriks Awal:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matrik[i][j] << " ";
        }
        cout << endl;
    }

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matrik[i][j];
        }
    }

    cout << "\nMatriks Hasil Transpose:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << transpose[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no1.png)

Program di atas Program ini berfungsi untuk melakukan **transpose** pada matriks 3x3, yaitu menukar baris menjadi kolom dan sebaliknya. Di awal, matriks `matrik` diinisialisasi dengan nilai 1–9, lalu dibuat matriks kosong `transpose` untuk menampung hasilnya. Program pertama menampilkan matriks awal, kemudian menggunakan dua perulangan untuk menukar posisi elemen dengan rumus `transpose[j][i] = matrik[i][j]`. Setelah proses selesai, hasil transpose ditampilkan, menghasilkan matriks dengan baris dan kolom yang saling bertukar posisi.


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
1. https://www.w3schools.com/cpp/cpp_variables_multiple.asp
2. https://www.w3schools.com/cpp/cpp_conditions.asp
3. https://www.w3schools.com/cpp/cpp_arrays.asp
4. https://www.w3schools.com/cpp/cpp_conditions_else.asp
5. https://www.w3schools.com/cpp/cpp_for_loop.asp
6. https://www.w3schools.com/cpp/cpp_conditions_elseif.asp




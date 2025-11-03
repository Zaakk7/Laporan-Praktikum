# <h1 align="center">Laporan Praktikum Modul 7 <br> Stack</h1>
<p align="center">Zaki Hamdani - 103112400089</p>

## Dasar Teori
Dasar teori dari program stack ini adalah bahwa **stack** merupakan salah satu bentuk struktur data linear yang bekerja berdasarkan prinsip **LIFO (Last In First Out)**, artinya elemen yang terakhir dimasukkan akan menjadi elemen pertama yang diambil. Stack dapat direpresentasikan menggunakan **array** atau **pointer**, dengan satu penunjuk utama yang disebut **TOP** untuk menunjukkan posisi elemen teratas. Operasi dasar pada stack meliputi **push** (menambah elemen ke atas stack), **pop** (menghapus elemen dari atas stack), dan **printInfo** (menampilkan isi stack). Selain itu, dapat ditambahkan operasi tambahan seperti **balikStack** untuk membalik urutan data, **pushAscending** untuk menyisipkan elemen agar tetap terurut menaik, serta **getInputStream** untuk membaca input secara berurutan dari pengguna. Dengan implementasi berbasis array, stack memiliki batas ukuran tetap, namun mudah diakses karena indeks dapat digunakan langsung tanpa manajemen memori dinamis.

## Guide

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpety(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data){
    Node *newNode = new Node;
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpety(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    top = top -> next;

    Node *temp;
    return poppedData;
}

void show (Node *top)
{
    if (isEmpety(top))
    {
        cout << "Stack kosong," << endl;
        return;
    }
    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << "-> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;

}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi stack:" << endl;
    show (stack);

    cout << "pop;" << pop(stack) << endl;

    cout << "Menampilkan sisa Stack:" << endl;
    show(stack);

    return 0;
}
```


## Unguide

### Soal 1

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
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
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}
```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 2);
    push(S, 9);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no1.png)

Pada program pertama, dibuat ADT Stack menggunakan array yang mendukung operasi dasar yaitu createStack, push, pop, printInfo, dan balikStack. Program ini menunjukkan cara kerja stack dengan prinsip LIFO (Last In First Out), di mana data yang terakhir dimasukkan akan menjadi data pertama yang diambil. Fungsi push digunakan untuk menambahkan elemen baru ke atas stack, sedangkan pop menghapus elemen teratas. printInfo digunakan untuk menampilkan isi stack dari posisi TOP ke bawah, dan balikStack digunakan untuk membalik urutan elemen dalam stack. Program ini menjadi dasar untuk memahami struktur data stack dengan representasi tabel (array).

### Soal 2

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif
```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
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
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

// ------------------------------
// Tambahan: pushAscending
// ------------------------------
void pushAscending(Stack &S, infotype x) {
    if (S.top >= MAX - 1) {
        cout << "Stack penuh!" << endl;
        return;
    }

    Stack temp;
    createStack(temp);

    // Pindahkan semua elemen yang lebih kecil dari x
    while (S.top >= 0 && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    // Masukkan elemen baru (x)
    push(S, x);

    // Kembalikan elemen dari temp ke stack utama
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}
```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no2.png)

Program kedua merupakan pengembangan dari program pertama dengan menambahkan prosedur pushAscending, yang berfungsi untuk menjaga agar elemen-elemen dalam stack tetap terurut secara menaik (ascending) dari bawah ke atas. Dalam implementasinya, elemen sementara dipindahkan ke stack bantu saat ditemukan nilai yang lebih besar dari elemen baru yang akan dimasukkan. Setelah elemen baru berhasil disisipkan, elemen-elemen sebelumnya dikembalikan ke stack utama. Program ini memperkenalkan logika kontrol dan penggunaan stack tambahan untuk mengatur posisi penyisipan data, serta memperlihatkan penerapan konsep algoritma sederhana dalam pengelolaan tumpukan.

### Soal 3


### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);
void getInputStream(Stack &S);

#endif
```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
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
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    if (S.top >= MAX - 1) {
        cout << "Stack penuh!" << endl;
        return;
    }

    Stack temp;
    createStack(temp);

    while (S.top >= 0 && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}

// --------------------------------
// Tambahan: getInputStream
// --------------------------------
void getInputStream(Stack &S) {
    char ch;
    cout << "Masukkan angka : ";
    while (true) {
        ch = cin.get();
        if (ch == '\n') break; 
        if (isdigit(ch)) {
            int x = ch - '0';
            push(S, x);
        }
    }
}
```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    getInputStream(S);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no3.png)

Program ketiga menambahkan fitur interaktif menggunakan prosedur getInputStream, yang memungkinkan pengguna memasukkan deretan angka langsung dari keyboard (tanpa spasi). Setiap karakter yang dimasukkan dibaca menggunakan cin.get() dan dikonversi menjadi angka untuk dimasukkan ke dalam stack satu per satu menggunakan operasi push. Program akan berhenti membaca input ketika pengguna menekan tombol Enter. Melalui pengembangan ini, mahasiswa belajar bagaimana menghubungkan konsep struktur data dengan interaksi pengguna (I/O stream), serta bagaimana data dinamis dari input dapat diproses langsung ke dalam struktur stack.

## Referensi
1. https://www.w3schools.com/cpp/cpp_functions.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_user_input.asp
4. https://www.w3schools.com/cpp/cpp_while_loop.asp
5. https://www.w3schools.com/cpp/cpp_stacks.asp

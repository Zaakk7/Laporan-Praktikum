# <h1 align="center">Laporan Praktikum Modul 5 <br> Singly Linked List (Bagian Kedua)</h1>
<p align="center">Zaki Hamdani - 103112400089</p>

## Dasar Teori

Singly Linked List merupakan salah satu bentuk struktur data dinamis yang terdiri dari serangkaian elemen (node) yang saling terhubung melalui pointer. Setiap node terdiri dari dua bagian utama, yaitu data (informasi yang disimpan) dan pointer next (penunjuk ke node berikutnya). Struktur ini hanya memiliki satu arah akses, yaitu dari node pertama (head) menuju node terakhir yang menunjuk ke NULL. Karena sifatnya yang dinamis, ukuran Singly Linked List dapat bertambah atau berkurang sesuai kebutuhan tanpa harus menentukan kapasitas di awal seperti pada array. Operasi dasar yang umum dilakukan meliputi pembuatan list, penambahan elemen (insert), penghapusan elemen (delete), penelusuran (traverse/view), dan pembaruan data (update). Kelebihan utama dari Singly Linked List adalah efisiensi dalam manipulasi data (terutama penyisipan dan penghapusan), meskipun akses data harus dilakukan secara berurutan dari awal list.meliharaan program, seperti pada contoh ADT mahasiswa dan pelajaran dalam bahasa C++.

## Guide

### linkedlist.cpp
```go
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}


void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next
    }
    cout << "NULL\n";
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```


## Unguide

### Soal 1
Buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani menggunakan c++
```go
#include <iostream>
#include <string>
using namespace std;

struct Pembeli {
    string nama;
    string pesanan;
    Pembeli* next;
};

Pembeli* front = nullptr;
Pembeli* rear = nullptr;

bool isEmpty() {
    return front == nullptr;
}

void tambahAntrian(string nama, string pesanan) {
    Pembeli* baru = new Pembeli;
    baru->nama = nama;
    baru->pesanan = pesanan;
    baru->next = nullptr;

    if (isEmpty()) {
        front = rear = baru;
    } else {
        rear->next = baru;
        rear = baru;
    }
    cout << "Antrian berhasil ditambahkan!\n";
}

void layaniAntrian() {
    if (isEmpty()) {
        cout << "Antrian kosong!\n";
        return;
    }

    Pembeli* hapus = front;
    cout << "Melayani antrian: " << hapus->nama << " (" << hapus->pesanan << ")\n";
    front = front->next;
    delete hapus;

    if (front == nullptr)
        rear = nullptr;
}

void tampilkanAntrian() {
    if (isEmpty()) {
        cout << "Antrian kosong!\n";
        return;
    }

    Pembeli* bantu = front;
    cout << "Daftar Antrian:\n";
    while (bantu != nullptr) {
        cout << "- " << bantu->nama << " (" << bantu->pesanan << ")\n";
        bantu = bantu->next;
    }
}

int main() {
    int pilihan;
    string nama, pesanan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "Masukkan Nama: ";
                getline(cin, nama);
                cout << "Masukkan Pesanan: ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilkanAntrian();
                break;
            case 4:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 4);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no1.png)

Program di atas merupakan implementasi **struktur data antrian (queue)** menggunakan **single linked list** dalam bahasa C++. Setiap elemen antrian berisi data pembeli berupa **nama dan pesanan** yang disimpan dalam struct `Pembeli`. Program menggunakan dua pointer, yaitu `front` untuk menunjuk pembeli yang berada di depan antrian (akan dilayani lebih dulu) dan `rear` untuk menunjuk pembeli terakhir. Fungsi `tambahAntrian()` menambahkan pembeli baru di belakang antrian, `layaniAntrian()` menghapus pembeli dari depan antrian sebagai proses pelayanan, dan `tampilkanAntrian()` menampilkan seluruh daftar pembeli yang sedang menunggu. Menu interaktif disediakan agar pengguna dapat menambah, melayani, atau melihat antrian secara dinamis sesuai urutan kedatangan (FIFO — First In First Out).

### Soal 2
buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 

```go
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = nullptr;

void tambahNode(int nilai) {
    Node* baru = new Node;
    baru->data = nilai;
    baru->next = nullptr;

    if (head == nullptr) {
        head = baru;
    } else {
        Node* bantu = head;
        while (bantu->next != nullptr)
            bantu = bantu->next;
        bantu->next = baru;
    }
}

void tampilkanList() {
    Node* bantu = head;
    if (bantu == nullptr) {
        cout << "List kosong!\n";
        return;
    }
    while (bantu != nullptr) {
        cout << bantu->data;
        if (bantu->next != nullptr) cout << " -> ";
        bantu = bantu->next;
    }
    cout << endl;
}

void reverseList() {
    Node* prev = nullptr;
    Node* current = head;
    Node* next = nullptr;

    while (current != nullptr) {
        next = current->next;  
        current->next = prev;  
        prev = current;        
        current = next;        
    }

    head = prev;  
}

int main() {
    tambahNode(1);
    tambahNode(2);
    tambahNode(3);

    cout << "Linked List sebelum dibalik: ";
    tampilkanList();

    reverseList();

    cout << "Linked List setelah dibalik: ";
    tampilkanList();

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no2.png)

Program di atas merupakan implementasi **pembalikan (reverse)** pada **singly linked list** menggunakan bahasa C++. Setiap elemen list disimpan dalam **struct Node** yang memiliki dua komponen yaitu `data` dan pointer `next` untuk menunjuk node berikutnya. Fungsi `tambahNode()` digunakan untuk menambahkan data di akhir list, sedangkan `tampilkanList()` menampilkan seluruh isi list secara berurutan. Proses utama terdapat pada fungsi `reverseList()`, yang menggunakan tiga pointer — `prev`, `current`, dan `next` — untuk membalik arah sambungan antar-node sehingga urutan list menjadi terbalik. Awalnya list berisi `1 → 2 → 3`, dan setelah fungsi pembalik dijalankan, urutannya berubah menjadi `3 → 2 → 1`.


## Referensi
1. https://www.w3schools.com/dsa/dsa_theory_linkedlists.php
2. https://www.w3schools.com/dsa/dsa_algo_linkedlists_operations.php
3. https://www.w3schools.com/dsa/dsa_data_linkedlists_types.php
4. https://www.w3schools.com/dsa/dsa_theory_linkedlists_memory.php
5. https://www.w3schools.com/dsa/dsa_data_queues.php


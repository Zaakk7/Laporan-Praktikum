# <h1 align="center">Laporan Praktikum Modul 13 <br> Multi Linked List </h1>
<p align="center">Zaki Hamdani - 103112400089</p>

## Dasar Teori

Dasar teori dari modul **Multi Linked List** adalah bahwa struktur data ini merupakan perluasan dari konsep linked list tunggal maupun ganda, di mana setiap elemen pada list induk dapat memiliki list lain yang terhubung sebagai list anak. Multi Linked List memungkinkan representasi hubungan **hierarkis** antara data, misalnya hubungan *pegawai–anak* sebagaimana ditampilkan pada modul, sehingga setiap node induk tidak hanya menyimpan informasi dan pointer ke node berikutnya, tetapi juga memiliki pointer menuju sebuah list anak yang berisi elemen-elemen terkait. Dengan struktur seperti ini, Multi Linked List menjadi sangat fleksibel untuk mengelola data yang memiliki relasi satu‐ke‐banyak, karena operasi dasar seperti **insert**, **delete**, dan **pencarian** dapat dilakukan baik pada level induk maupun level anak secara terpisah namun tetap terhubung, sehingga struktur ini efisien dalam mengorganisasi data kompleks yang membutuhkan keterkaitan antar elemen.

## Guide

```go
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }
    
    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
     cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;
    
    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");
    
    printAll(list);
    cout << "\n";
    
    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");
    
    printAll(list);
    
    return 0;
}
```


## Unguide

### Soal 2
Perhatikan program 46 multilist.h, buat multilist.cpp untuk implementasi semua fungsi pada
multilist.h. Buat main.cpp untuk pemanggilan fungsi-fungsi tersebut.

## multilist.h
```go

```

## multilist.cpp

```go

```

## main.cpp

```go

```

> Output
> ![Screenshot bagian x](Output/Output_no1.png)

Program ini merupakan implementasi struktur data **Queue berbasis array dengan mekanisme Alternatif 1**, yaitu *head diam dan tail bergerak*, sehingga elemen baru selalu ditambahkan di bagian belakang (enqueue) dan elemen pertama dihapus dari bagian depan (dequeue). Pada saat dequeue, semua elemen digeser satu posisi ke kiri untuk mempertahankan head tetap di indeks 0. Program terdiri dari tiga file: `queue.h` yang mendefinisikan struktur dan prototipe fungsi, `queue.cpp` yang berisi implementasi operasi queue seperti pengecekan kosong/penuh, enqueue, dequeue, serta fungsi untuk menampilkan isi queue, dan `main.cpp` yang mengeksekusi berbagai operasi enqueue dan dequeue sambil menampilkan perubahan kondisi queue di setiap langkah. Hasil akhirnya memperlihatkan bagaimana antrean berubah sesuai prinsip **FIFO (First In First Out)**, hingga akhirnya kembali menjadi queue kosong.

### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

## queue.cpp
```go

```

> Output
> ![Screenshot bagian x](Output/Output_no2.png)

Pada mekanisme **Queue Alternatif 2**, pergerakan antrean diatur dengan memindahkan posisi **head** dan **tail** tanpa menggeser isi array, sehingga operasi menjadi lebih efisien dibanding Alternatif 1. Saat melakukan **enqueue**, nilai baru ditambahkan ke indeks setelah tail dan tail bergerak maju satu posisi; sedangkan head tetap berada pada posisi terakhir elemen yang belum dihapus. Pada operasi **dequeue**, tidak ada penggeseran elemen, namun **head maju satu langkah** untuk menunjuk ke elemen berikutnya, dan jika head dan tail menjadi sama, queue dianggap kembali kosong dan keduanya diset ke `-1`. Implementasi ini memperlihatkan bagaimana antrean tetap mengikuti prinsip **FIFO**, tetapi dengan pengelolaan indeks yang lebih hemat waktu karena tidak perlu melakukan shifting data setiap kali penghapusan.



## Referensi
1. 


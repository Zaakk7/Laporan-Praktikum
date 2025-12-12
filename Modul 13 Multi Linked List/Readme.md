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

## multilist.cpp

```go
#include <iostream>
#include "multilist.h"
using namespace std;

/***************** Pengecekan List Kosong *****************/
bool ListEmpty(listinduk L){
    return (L.first == Nil);
}

bool ListEmptyAnak(listanak L){
    return (L.first == Nil);
}

/***************** Create List *****************/
void CreateList(listinduk &L){
    L.first = Nil;
    L.last  = Nil;
}

void CreateListAnak(listanak &L){
    L.first = Nil;
    L.last  = Nil;
}

/***************** Manajemen Memori *****************/
address alokasi(infotypeinduk X){
    address P = new elemen_list_induk;
    if(P != Nil){
        P->info = X;
        CreateListAnak(P->lanak);
        P->next = Nil;
        P->prev = Nil;
    }
    return P;
}

address_anak alokasiAnak(infotypeanak X){
    address_anak P = new elemen_list_anak;
    if(P != Nil){
        P->info = X;
        P->next = Nil;
        P->prev = Nil;
    }
    return P;
}

void dealokasi(address P){
    delete P;
}

void dealokasiAnak(address_anak P){
    delete P;
}

/***************** FIND ELEM *****************/
address findElm(listinduk L, infotypeinduk X){
    address P = L.first;
    while(P != Nil){
        if(P->info == X){
            return P;
        }
        P = P->next;
    }
    return Nil;
}

address_anak findElm(listanak L, infotypeanak X){
    address_anak P = L.first;
    while(P != Nil){
        if(P->info == X){
            return P;
        }
        P = P->next;
    }
    return Nil;
}

boolean fFindElm(listinduk L, address P){
    address Q = L.first;
    while(Q != Nil){
        if(Q == P) return true;
        Q = Q->next;
    }
    return false;
}

boolean fFindElmanak(listanak L, address_anak P){
    address_anak Q = L.first;
    while(Q != Nil){
        if(Q == P) return true;
        Q = Q->next;
    }
    return false;
}

/***************** INSERT INDUK *****************/
void insertFirst(listinduk &L, address P){
    if(ListEmpty(L)){
        L.first = P;
        L.last  = P;
    } else {
        P->next = L.first;
        L.first->prev = P;
        L.first = P;
    }
}

void insertAfter(listinduk &L, address Prec, address P){
    if(Prec != Nil){
        P->next = Prec->next;
        P->prev = Prec;

        if(Prec->next != Nil)
            Prec->next->prev = P;
        else
            L.last = P;

        Prec->next = P;
    }
}

void insertLast(listinduk &L, address P){
    if(ListEmpty(L)){
        insertFirst(L, P);
    } else {
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

/***************** INSERT ANAK *****************/
void insertFirstAnak(listanak &L, address_anak P){
    if(ListEmptyAnak(L)){
        L.first = P;
        L.last  = P;
    } else {
        P->next = L.first;
        L.first->prev = P;
        L.first = P;
    }
}

void insertAfterAnak(listanak &L, address_anak Prec, address_anak P){
    P->next = Prec->next;
    P->prev = Prec;

    if(Prec->next != Nil)
        Prec->next->prev = P;
    else
        L.last = P;

    Prec->next = P;
}

void insertLastAnak(listanak &L, address_anak P){
    if(ListEmptyAnak(L)){
        insertFirstAnak(L, P);
    } else {
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

/***************** DELETE INDUK *****************/
void delFirst(listinduk &L, address &P){
    P = L.first;
    if(L.first == L.last){
        L.first = Nil;
        L.last  = Nil;
    } else {
        L.first = P->next;
        L.first->prev = Nil;
        P->next = Nil;
    }
}

void delLast(listinduk &L, address &P){
    P = L.last;
    if(L.first == L.last){
        L.first = Nil;
        L.last  = Nil;
    } else {
        L.last = P->prev;
        L.last->next = Nil;
        P->prev = Nil;
    }
}

void delAfter(listinduk &L, address &P, address Prec){
    if (Prec != Nil && Prec->next != Nil){
        P = Prec->next;               // Elemen yang akan dihapus
        Prec->next = P->next;         // Loncatkan P

        if (P->next != Nil){          // Jika bukan elemen terakhir
            P->next->prev = Prec;
        } else {                      // Jika P adalah elemen terakhir
            L.last = Prec;
        }

        P->next = Nil;                // Putuskan link P
        P->prev = Nil;
    }
}


/***************** DELETE ANAK *****************/
void delFirstAnak(listanak &L, address_anak &P){
    P = L.first;
    if(L.first == L.last){
        L.first = Nil;
        L.last  = Nil;
    } else {
        L.first = P->next;
        L.first->prev = Nil;
    }
}

void delLastAnak(listanak &L, address_anak &P){
    P = L.last;
    if(L.first == L.last){
        L.first = Nil;
        L.last  = Nil;
    } else {
        L.last = P->prev;
        L.last->next = Nil;
    }
}

void delAfterAnak(listanak &L, address_anak &P, address_anak Prec){
    if (Prec != Nil && Prec->next != Nil){
        P = Prec->next;                  // P adalah elemen yang akan dihapus
        Prec->next = P->next;            // Loncatkan P

        if (P->next != Nil){             // Jika bukan elemen terakhir
            P->next->prev = Prec;
        } else {                         // Jika P adalah elemen terakhir
            L.last = Prec;
        }

        P->next = Nil;                   // Putus link
        P->prev = Nil;
    }
}


/***************** DELETE P SPECIFIC *****************/
void delP(listinduk &L, infotypeinduk X){
    address P = findElm(L, X);
    if(P != Nil){

        // hapus semua anak
        address_anak A;
        while(!ListEmptyAnak(P->lanak)){
            delFirstAnak(P->lanak, A);
            dealokasiAnak(A);
        }

        // hapus induk
        if(P == L.first){
            delFirst(L, P);
        } else if(P == L.last){
            delLast(L, P);
        } else {
            delAfter(L, P->prev, P);
        }
        dealokasi(P);
    }
}

void delPAnak(listanak &L, infotypeanak X){
    address_anak P = findElm(L, X);

    if(P != Nil){
        if(P == L.first){
            delFirstAnak(L, P);
        } else if(P == L.last){
            delLastAnak(L, P);
        } else {
            delAfterAnak(L, P->prev, P);
        }
        dealokasiAnak(P);
    }
}

/***************** PRINT INFO *****************/
void printInfo(listinduk L){
    address P = L.first;
    cout << "=== DATA INDUK DAN ANAK ===\n";

    while(P != Nil){
        cout << "Induk: " << P->info << endl;

        address_anak A = P->lanak.first;
        while(A != Nil){
            cout << "  - Anak: " << A->info << endl;
            A = A->next;
        }
        P = P->next;
    }
}

```

## main.cpp

```go
#include <iostream>
#include "multilist.h"
using namespace std;

int main(){

    listinduk L;
    CreateList(L);

    // insert induk
    address P1 = alokasi(1);
    insertFirst(L, P1);

    address P2 = alokasi(2);
    insertLast(L, P2);

    // insert anak ke induk 1
    address_anak A1 = alokasiAnak(10);
    address_anak A2 = alokasiAnak(20);

    insertFirstAnak(P1->lanak, A1);
    insertLastAnak(P1->lanak, A2);

    // insert anak ke induk 2
    address_anak B1 = alokasiAnak(30);
    insertFirstAnak(P2->lanak, B1);

    printInfo(L);

    return 0;
}

```

Program multilist yang telah dibuat merupakan implementasi struktur data **Multi Linked List**, yaitu gabungan antara list induk dan list anak yang saling terhubung untuk merepresentasikan hubungan satu-ke-banyak. Setiap elemen induk memiliki sebuah list anak tersendiri, sehingga operasi seperti **insert**, **delete**, dan **cari elemen** dilakukan tidak hanya pada list utama, tetapi juga pada list anak yang dimiliki setiap induk. File *multilist.h* berisi deklarasi struktur dan fungsi, *multilist.cpp* berisi implementasi seluruh operasi seperti `insertFirst`, `insertLast`, `insertAfter`, serta operasi penghapusan termasuk penghapusan anak saat induk dihapus, sedangkan *main.cpp* digunakan untuk menguji fungsi-fungsi tersebut dengan membuat data induk, menambahkan anak, dan menampilkannya. Struktur ini memungkinkan pengelolaan data bertingkat secara efisien dan terorganisir.

### Soal 3
Buatlah implementasi ADT Doubly Linked list pada file “circularlist.cpp”. Tambahkan fungsi/prosedur berikut pada file “main.cpp”.

• fungsi create ( in nama, nim : string, jenis_kelamin : char, ipk : float)
• fungsi disediakan, ketik ulang code yang diberikan
• fungsi mengalokasikan sebuah elemen list dengan info sesuai input
```
address createData(string nama, string nim, char jenis_kelamin, float ipk)
{
    /**
     * PR : mengalokasikan sebuah elemen list dengan info dengan info sesuai input
     * FS : address P menunjuk elemen dengan info sesuai input
     */
    infotype x;
    address P;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;
    P = alokasi(x);
    return P;
}
```

Cobalah hasil implementasi ADT pada file “main.cpp”

```
int main()
{
    List L, A, B, L2;
    address P1 = Nil;
    address P2 = Nil;
    infotype x;
    createList(L);

    cout<<"coba insert first, last, dan after"<<endl;

    P1 = createData("Danu", "04", 'l', 4.0);
    insertFirst(L,P1);

    P1 = createData("Fahmi", "06", 'l',3.45);
    insertLast(L,P1);

    P1 = createData("Bobi", "02", 'l',3.71);
    insertFirst(L,P1);

    P1 = createData("Ali", "01", 'l', 3.3);
    insertFirst(L,P1);

    P1 = createData("Gita", "07", 'p', 3.75);
    insertLast(L,P1);

    x.nim = "07";
    P1 = findElm(L,x);
    P2 = createData("Cindi", "03", 'p', 3.5);
    insertAfter(L, P1, P2);

    x.nim = "02";
    P1 = findElm(L,x);
    P2 = createData("Hilmi", "08", 'p', 3.3);
    insertAfter(L, P1, P2);

    x.nim = "04";
    P1 = findElm(L,x);
    P2 = createData("Eli", "05", 'p', 3.4);
    insertAfter(L, P1, P2);

    printInfo(L);
    return 0;
}
```

## circular.h
```go
#ifndef CIRCULARLIST_H_INCLUDED
#define CIRCULARLIST_H_INCLUDED
#include <iostream>
using namespace std;

#define Nil NULL

// ====== TIPE DATA ======
struct infotype {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
};

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

// ====== PROTOTYPE ADT ======
void createList(List &L);

address alokasi(infotype x);

void dealokasi(address P);

void insertFirst(List &L, address P);

void insertAfter(List &L, address Prec, address P);

void insertLast(List &L, address P);

void deleteFirst(List &L, address &P);

void deleteAfter(List &L, address Prec, address &P);

void deleteLast(List &L, address &P);

address findElm(List L, infotype x);

void printInfo(List L);

#endif
```

## circular.cpp
```go
#include "circularlist.h"

// Membuat list kosong
void createList(List &L){
    L.first = Nil;
}

// Alokasi node baru
address alokasi(infotype x){
    address P = new ElmList;
    if(P != Nil){
        P->info = x;
        P->next = Nil;
    }
    return P;
}

// Dealokasi node
void dealokasi(address P){
    delete P;
}

// Insert First (circular)
void insertFirst(List &L, address P){
    if(L.first == Nil){
        L.first = P;
        P->next = P;     // circular
    } else {
        address Q = L.first;
        while(Q->next != L.first){
            Q = Q->next;
        }
        P->next = L.first;
        Q->next = P;
        L.first = P;
    }
}

// Insert After
void insertAfter(List &L, address Prec, address P){
    if(Prec != Nil){
        P->next = Prec->next;
        Prec->next = P;
    }
}

// Insert Last
void insertLast(List &L, address P){
    if(L.first == Nil){
        insertFirst(L, P);
    } else {
        address Q = L.first;
        while(Q->next != L.first){
            Q = Q->next;
        }
        Q->next = P;
        P->next = L.first;
    }
}

// Delete First
void deleteFirst(List &L, address &P){
    P = L.first;
    if(L.first->next == L.first){
        L.first = Nil;
    } else {
        address Q = L.first;
        while(Q->next != L.first){
            Q = Q->next;
        }
        L.first = P->next;
        Q->next = L.first;
    }
    P->next = Nil;
}

// Delete After
void deleteAfter(List &L, address Prec, address &P){
    P = Prec->next;
    Prec->next = P->next;
    P->next = Nil;
}

// Delete Last
void deleteLast(List &L, address &P){
    address Q = L.first;
    while(Q->next->next != L.first){
        Q = Q->next;
    }
    P = Q->next;
    Q->next = L.first;
    P->next = Nil;
}

// Find Elm berdasarkan nim
address findElm(List L, infotype x){
    if(L.first == Nil) return Nil;

    address P = L.first;
    do{
        if(P->info.nim == x.nim){
            return P;
        }
        P = P->next;
    } while(P != L.first);

    return Nil;
}

// Print semua data
void printInfo(List L){
    if(L.first == Nil){
        cout << "List kosong" << endl;
    } else {
        address P = L.first;
        do{
            cout << "Nama : " << P->info.nama << endl;
            cout << "NIM  : " << P->info.nim << endl;
            cout << "L/P  : " << P->info.jenis_kelamin << endl;
            cout << "IPK  : " << P->info.ipk << endl;
            cout << endl;

            P = P->next;
        } while(P != L.first);
    }
}
```

## main.cpp
```go
#include <iostream>
#include "circularlist.h"
using namespace std;

address createData(string nama, string nim, char jenis_kelamin, float ipk)
{
    infotype x;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;

    return alokasi(x);
}

int main()
{
    List L;
    address P1, P2;
    infotype x;

    createList(L);

    cout << "coba insert first, last, dan after" << endl;

    P1 = createData("Danu", "04", 'l', 4.0);
    insertFirst(L,P1);

    P1 = createData("Fahmi", "06", 'l',3.45);
    insertLast(L,P1);

    P1 = createData("Bobi", "02", 'l',3.71);
    insertFirst(L,P1);

    P1 = createData("Ali", "01", 'l', 3.3);
    insertFirst(L,P1);

    P1 = createData("Gita", "07", 'p', 3.75);
    insertLast(L,P1);

    x.nim = "07";
    P1 = findElm(L,x);
    P2 = createData("Cindi", "03", 'p', 3.5);
    insertAfter(L, P1, P2);

    x.nim = "02";
    P1 = findElm(L,x);
    P2 = createData("Hilmi", "08", 'p', 3.3);
    insertAfter(L, P1, P2);

    x.nim = "04";
    P1 = findElm(L,x);
    P2 = createData("Eli", "05", 'p', 3.4);
    insertAfter(L, P1, P2);

    printInfo(L);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no2.png)

Program circular linked list ini mengelola data mahasiswa menggunakan struktur list melingkar, di mana setiap elemen memiliki informasi berupa nama, NIM, jenis kelamin, dan IPK. List bersifat circular sehingga elemen terakhir selalu menunjuk kembali ke elemen pertama, memungkinkan traversal tanpa ujung sampai kembali ke awal. Program menyediakan berbagai operasi seperti membuat list, menambah data di awal, akhir, atau setelah elemen tertentu, menghapus elemen pertama, terakhir, atau setelah elemen tertentu, serta mencari elemen berdasarkan NIM. Pada fungsi utama, beberapa data mahasiswa dibuat menggunakan fungsi `createData`, kemudian dimasukkan ke dalam list sesuai urutan perintah menggunakan `insertFirst`, `insertLast`, dan `insertAfter`. Akhirnya, fungsi `printInfo` menampilkan seluruh isi list secara vertikal, menghasilkan daftar mahasiswa lengkap dalam urutan yang telah dibentuk oleh operasi penyisipan.


## Referensi
1. https://www.w3schools.com/dsa/dsa_data_linkedlists_types.php
2. https://www.w3schools.com/dsa/trydsa.php?filename=demo_linkedlists_circsingly
3. https://www.w3schools.com/dsa/dsa_theory_linkedlists.php
4. https://www.w3schools.com/dsa/dsa_algo_linkedlists_operations.php]
5. https://www.w3schools.com/dsa/

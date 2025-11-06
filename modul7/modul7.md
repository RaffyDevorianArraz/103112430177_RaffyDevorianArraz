# <h1 align="center">Laporan Praktikum Modul 7 <br> Stack</h1>
<p align="center"> Raffy Devorian Arraz - 103112430177</p>

## Dasar Teori
Dasar teori dari program stack ini adalah bahwa **stack** merupakan salah satu struktur data linear yang bekerja dengan prinsip **LIFO (Last In First Out)**, yaitu elemen yang dimasukkan terakhir akan menjadi elemen pertama yang dikeluarkan. Stack dapat diimplementasikan menggunakan **array** maupun **pointer**, dengan satu variabel penunjuk utama bernama **TOP** yang menunjukkan posisi elemen paling atas. Operasi dasar yang umum digunakan pada stack antara lain **push** (menambahkan elemen ke bagian atas stack), **pop** (menghapus elemen teratas), dan **printInfo** (menampilkan seluruh isi stack). Selain itu, dapat pula ditambahkan operasi tambahan seperti **balikStack** untuk membalik urutan elemen, **pushAscending** untuk menambahkan elemen agar data tetap terurut naik, serta **getInputStream** untuk membaca data input secara berurutan dari pengguna. Jika stack diimplementasikan menggunakan array, maka ukuran stack bersifat tetap, namun akses elemen menjadi lebih cepat karena dapat dilakukan langsung melalui indeks tanpa pengelolaan memori dinamis.

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
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/soal%201.png)

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
    pop(S);
    push(S, 8);
    pop(S);
    push(S, 2);
    pop(S);
    push(S, 3);
    push(S, 9);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
   
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%201.png)

Pada program pertama, dibuat sebuah **ADT Stack** yang diimplementasikan menggunakan **array**. Stack memiliki dua atribut utama, yaitu **array info** untuk menyimpan data dan variabel **top** sebagai penunjuk posisi elemen teratas. Fungsi **createStack()** berfungsi untuk menginisialisasi stack agar berada dalam keadaan kosong dengan menetapkan nilai **top = -1**. Operasi **push()** digunakan untuk menambahkan elemen baru ke bagian atas stack selama kapasitas belum mencapai batas maksimum, sedangkan **pop()** berfungsi menghapus elemen paling atas dan mengembalikannya. Prosedur **printInfo()** digunakan untuk menampilkan seluruh isi stack dari elemen teratas hingga terbawah. Selain itu, terdapat juga prosedur **balikStack()** yang bertugas membalik urutan elemen dengan cara memindahkan elemen satu per satu ke stack sementara, lalu mengembalikannya sehingga urutannya menjadi kebalikan dari sebelumnya. Secara keseluruhan, struktur stack pada program ini bekerja berdasarkan prinsip **LIFO (Last In First Out)**, yaitu elemen yang dimasukkan terakhir akan keluar terlebih dahulu.

### Soal 2
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/soal%202.png)

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

void pushAscending(Stack &S, infotype x) {
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
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%202.png)

Pada program kedua, ditambahkan prosedur **pushAscending()** yang berfungsi menjaga agar elemen-elemen dalam stack tetap tersusun secara **menaik (ascending)** dari bawah ke atas setiap kali ada data baru yang dimasukkan. Prosedur ini bekerja dengan membuat **stack sementara** untuk menampung elemen-elemen yang bernilai lebih besar dari data yang akan disisipkan. Setelah posisi yang sesuai ditemukan, data baru dimasukkan ke **stack utama** menggunakan operasi **push()**. Kemudian, seluruh elemen dari stack sementara dipindahkan kembali ke stack utama sehingga urutan datanya tetap terjaga. Dengan cara ini, meskipun dilakukan penyisipan berulang kali, susunan ascending pada stack tidak berubah. Namun, saat isi stack ditampilkan menggunakan **printInfo()**, urutan yang terlihat dari atas ke bawah tampak seperti **descending**, karena sebenarnya urutan ascending-nya terbaca dari bawah ke atas.

### Soal 3
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/soal%203.png)

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

void getInputStream(Stack &S) {
    cout << "Masukkan angka (ENTER untuk selesai): ";

    char c;
    cin.get(c); 

    while (c != '\n') {     
        if (c >= '0' && c <= '9') {   
            push(S, c - '0');        
        }
        cin.get(c);
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
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%203.png)

Pada program ketiga, ditambahkan prosedur **getInputStream()** yang berfungsi untuk memungkinkan program membaca masukan dari pengguna secara langsung dalam bentuk karakter demi karakter tanpa perlu dipisahkan oleh spasi. Proses pembacaan dilakukan menggunakan **cin.get()**, sehingga setiap karakter yang diketik akan diproses hingga pengguna menekan tombol **ENTER** sebagai tanda akhir input. Jika karakter yang dibaca merupakan digit angka, maka karakter tersebut akan dikonversi menjadi **integer** dan dimasukkan ke dalam stack melalui operasi **push()**. Dengan mekanisme ini, pengguna dapat memasukkan deretan angka seperti sebuah string, misalnya *4729601*, dan setiap digitnya akan otomatis disimpan ke dalam stack sesuai urutan input. Oleh karena itu, **getInputStream()** memberikan cara yang lebih praktis dan efisien bagi pengguna dalam memasukkan data ke stack.

## Referensi
1. https://www.w3schools.com/cpp/cpp_user_input.asp
2. https://www.w3schools.com/cpp/cpp_while_loop.asp
3. https://www.w3schools.com/cpp/cpp_stacks.asp

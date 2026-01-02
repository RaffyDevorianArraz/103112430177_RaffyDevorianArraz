# <h1 align="center">Laporan Praktikum Modul 8 <br>QUEUE</h1>
<p align="center">103112430177 - RAFFY DEVORIAN ARRAZ</p>

## Dasar Teori
Queue merupakan struktur data yang bekerja seperti antrean di loket tiket Kereta Api, di mana elemen yang masuk lebih awal akan diproses lebih dahulu dan elemen yang masuk terakhir akan diproses paling akhir, sesuai dengan prinsip FIFO (*First In First Out*). Dengan mekanisme ini, setiap data dilayani berdasarkan urutan kedatangannya, sehingga Queue sangat sesuai untuk kebutuhan pemrosesan yang menuntut keadilan dan keteraturan. Dalam bahasa pemrograman C, Queue dapat dibuat menggunakan array atau linked list; array menawarkan pengelolaan indeks yang relatif mudah, sementara linked list memberikan fleksibilitas lebih dalam menambah dan menghapus elemen tanpa harus memindahkan data lainnya.

## Guided

```c++
#include <iostream>
using namespace std;

#define MAX 5 // ukuran maksimal queue

// Struktur Queue
struct Queue {
    int data[MAX];
    int head;
    int tail;
};

// Membuat antrean kosong
void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFull(Queue Q) {
    return (Q.tail == MAX - 1);
}

// Menampilkan isi antrian
void printQueue(Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

void enqueue(Queue &Q, int x) {
    if (isFull(Q)) {
        cout << "Queue penuh! Tidak bisa menambah data." << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueue: " << x << endl;
    }
}

void dequeue(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong! Tidak ada data yang dihapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head] << endl;
        // Jika hanya 1 elemen
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            // Geser semua elemen ke kiri
            for (int i = Q.head; i < Q.tail; i++) {
                Q.data[i] = Q.data[i + 1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;
}
```

## UNGUIDED

### Soal 1
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 1 (head diam, tail bergerak).

#### queue.h
```c++
#ifndef QUEUE_H
#define QUEUE_H

const int MAX = 5;
typedef int infotype;

struct Queue {
    infotype info[MAX];
    int head, tail;
};

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)) {
        Q.head = 0;
        Q.tail = 0;
    } else {
        Q.tail++;
    }

    Q.info[Q.tail] = x;
}

infotype dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype x = Q.info[Q.head];

    if (Q.head == Q.tail) {
        createQueue(Q);
    } else {
        Q.head++;
    }

    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
        return;
    }

    for (int i = Q.head; i <= Q.tail; i++) {
        cout << Q.info[i] << " ";
    }
    cout << endl;
}

```

#### main.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    Queue Q;
    createQueue(Q);

    cout << "------------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "------------------------" << endl;
    printInfo(Q);

    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}

```
> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%208/jawaban%201.png)

Program ini dibuat menggunakan array statis di mana head selalu berada pada indeks awal (0), sedangkan tail bergerak maju saat enqueue. Ketika dequeue, head hanya naik sementara, tetapi jika queue kembali kosong, head dan tail di-reset ke −1. Cara ini sederhana namun tidak efisien karena ruang kosong di depan array tidak bisa dipakai kembali; akibatnya queue bisa dianggap penuh meskipun masih ada slot kosong setelah beberapa operasi dequeue.


### Soal 2
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

#### queue.cpp
```c++
#include <iostream>
using namespace std;

#define MAX 5
typedef int infotype;

struct Queue {
    infotype data[MAX];
    int front, rear;
};

void createQueue(Queue &Q) {
    Q.front = -1;
    Q.rear  = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.front == -1 && Q.rear == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.rear == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)) {
        Q.front = 0;
        Q.rear  = 0;
    } else {
        Q.rear++;
    }

    Q.data[Q.rear] = x;
}

infotype dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype x = Q.data[Q.front];

    if (Q.front == Q.rear) {
        createQueue(Q);
    } else {
        Q.front++;
    }

    return x;
}

void printQueue(Queue Q) {
    cout << Q.front << " - " << Q.rear << "\t|\t";

    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
        return;
    }

    for (int i = Q.front; i <= Q.rear; i++) {
        cout << Q.data[i] << " ";
    }
    cout << endl;
}

int main() {
    Queue Q;
    createQueue(Q);

    cout << "------------------------" << endl;
    cout << " F - R \t | Queue info" << endl;
    cout << "------------------------" << endl;

    printQueue(Q);

    enqueue(Q, 10); printQueue(Q);
    enqueue(Q, 20); printQueue(Q);
    enqueue(Q, 30); printQueue(Q);
    dequeue(Q);     printQueue(Q);
    enqueue(Q, 40); printQueue(Q);
    dequeue(Q);     printQueue(Q);

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%208/jawaban%202.png)

Program ini baik head maupun tail bergerak maju mengikuti operasi enqueue dan dequeue. Pendekatan ini lebih realistis karena elemen yang keluar benar-benar dilewati oleh head. Namun tetap tidak efisien karena array tidak berputar; ketika tail mencapai ujung array, queue dianggap penuh walaupun masih ada ruang kosong di depan akibat dequeuing.


### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q){
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q){
    return (Q.head == -1);
}

bool isFullQueue(Queue Q){
    return ((Q.tail + 1) % MAX == Q.head);
}

void enqueue(Queue &Q, infotype x){
    if (isFullQueue(Q)){
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)){
        Q.head = 0;
        Q.tail = 0;
    } else {
        Q.tail = (Q.tail + 1) % MAX;
    }

    Q.info[Q.tail] = x;
}

infotype dequeue(Queue &Q){
    if (isEmptyQueue(Q)){
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype val = Q.info[Q.head];

    if (Q.head == Q.tail){
        createQueue(Q);
    } else {
        Q.head = (Q.head + 1) % MAX;
    }

    return val;
}

void printInfo(Queue Q){
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)){
        cout << "empty queue" << endl;
        return;
    }

    int i = Q.head;
    while (true){
        cout << Q.info[i] << " ";
        if (i == Q.tail) break;
        i = (i + 1) % MAX;
    }
    cout << endl;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%208/jawaban%203.png)

Program ini menggunakan konsep circular sehingga head dan tail berputar kembali ke indeks 0 menggunakan operasi modulo. Ruang kosong akibat dequeue dapat digunakan kembali, dan queue hanya penuh jika (tail + 1) % MAX == head. Implementasi ini paling efisien karena memaksimalkan penggunaan array dan sangat cocok untuk sistem antrian yang berjalan terus-menerus.

## Referensi
1. https://www.w3schools.com/cpp/cpp_queues.asp
2. https://www.w3schools.com/dsa/dsa_data_queues.php
3. https://www.w3schools.com/cpp/cpp_data_structures.asp
4. https://www.w3schools.com/cpp/exercise.asp?x=xrcise_queues1
5. https://www.w3schools.com/dsa/dsa_intro.php
6. https://www.w3schools.com/dsa/dsa_data_structures.php

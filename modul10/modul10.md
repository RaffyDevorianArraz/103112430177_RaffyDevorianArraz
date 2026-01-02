# <h1 align="center">Laporan Praktikum Modul 10 <br> Tree </h1>
<p align="center">103112430177 - RAFFY DEVORIAN ARRAZ</p>

## Dasar Teori
Rekursif merupakan teknik pemrograman di mana sebuah fungsi memanggil dirinya sendiri untuk menyelesaikan masalah yang dapat dibagi menjadi submasalah serupa, dengan syarat memiliki *base case* sebagai penghenti dan *recursive case* sebagai proses berulang. Teknik ini membuat kode lebih sederhana dan mudah dipahami, namun cenderung kurang efisien karena membutuhkan memori tambahan untuk setiap pemanggilan fungsi. Rekursif banyak dimanfaatkan pada struktur data seperti tree, karena memudahkan operasi traversal, pencarian, serta pengelolaan node dalam struktur hierarkis.

## Guide

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru->data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}

Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);
    
    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = insert(root->kanan, nilai);

    return root;
}

Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root;

    if (nilai < root->data)
        return search(root->kiri, nilai);

    return search(root->kanan, nilai);
}

Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;

        return current;
}

Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        else if (root->kanan == NULL){
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data);
    }
    return root;
}

Node *update(Node *root, int Lama, int baru)
{
    if (search(root, Lama) != NULL)
    {
        root = hapus(root, Lama);
        root = insert(root, baru);
        cout << "Data " << Lama << " diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "Data " << Lama << " tidak ditemukan!" << endl;
    }
    return root;
}

void preOrder(Node *root)
{
    if (root != NULL)
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << "Data berhasil dimasukan.\n" << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVELSAL) ===" << endl;
    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "Cari " << cari1 << ": " << (search(root,cari1) ? "Ketemu" : "Tidak Aada") << endl;
    cout << "Cari " << cari2 << ": " << (search(root,cari2) ? "Ketemu" : "Tidak Aada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    root = update(root, 5, 8);
    cout << "Hasil Order setelah update: ";
    cout << endl;
    cout << endl;

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "== 5. TEST DELETE ===" << endl;
    cout << "Menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    return 0;
}
```


## Unguide

### Soal 1
## bstree.h
```go
#ifndef BSTREE_H
#define BSTREE_H

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

#define Nil NULL

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address searchNode(address root, infotype x);
void inorderTraversal(address root);

#endif
```

## bstreee.cpp

```go
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = Nil;
    p->right = Nil;
    return p;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } 
    else if (x < root->info) {
        insertNode(root->left, x);
    } 
    else if (x > root->info) {
        insertNode(root->right, x);
    }
    // jika sama, data tidak dimasukkan
}

address searchNode(address root, infotype x) {
    if (root == Nil || root->info == x) {
        return root;
    }
    if (x < root->info) {
        return searchNode(root->left, x);
    } else {
        return searchNode(root->right, x);
    }
}

void inorderTraversal(address root) {
    if (root != Nil) {
        inorderTraversal(root->left);
        cout << root->info << " ";
        inorderTraversal(root->right);
    }
}
```

## main.cpp

```go
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    address root = Nil;

    insertNode(root, 8);
    insertNode(root, 3);
    insertNode(root, 10);
    insertNode(root, 1);
    insertNode(root, 6);
    insertNode(root, 14);
    insertNode(root, 4);
    insertNode(root, 7);
    insertNode(root, 13);

    cout << "Inorder Traversal: ";
    inorderTraversal(root);
    cout << endl;

    infotype cari = 6;
    address hasil = searchNode(root, cari);

    if (hasil != Nil) {
        cout << "Data " << cari << " ditemukan" << endl;
    } else {
        cout << "Data " << cari << " tidak ditemukan" << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%2010/jawaban1.png )

Kode ini mengimplementasikan **Binary Search Tree (BST)** menggunakan C++ dengan **rekursif**. BST adalah struktur data berbentuk pohon di mana setiap node memiliki nilai yang lebih kecil di subpohon kiri dan lebih besar di subpohon kanan. Fungsi `insertNode` menambahkan node baru secara rekursif sesuai aturan BST, `searchNode` mencari node tertentu, dan `inorderTraversal` menampilkan isi pohon secara terurut. Struktur kode dipisahkan menjadi **header (`bstree.h`)** untuk deklarasi, **implementasi (`bstree.cpp`)** untuk logika fungsi, dan **main (`main.cpp`)** untuk pengujian. Program ini memanfaatkan rekursi untuk menyederhanakan proses traversal dan pencarian, sehingga kode lebih ringkas dan mudah dipahami.

### Soal 2
## bstree.h
```go
#ifndef BSTREE_H
#define BSTREE_H

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

#define Nil NULL

// Deklarasi fungsi
address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void InOrder(address root);

int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root, int start);

#endif

```

### bstree.cpp
```
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = Nil;
    p->right = Nil;
    return p;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
}

address findNode(infotype x, address root) {
    if (root == Nil || root->info == x) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}

int hitungJumlahNode(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return 1 + hitungJumlahNode(root->left)
                 + hitungJumlahNode(root->right);
    }
}

int hitungTotalInfo(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return root->info
             + hitungTotalInfo(root->left)
             + hitungTotalInfo(root->right);
    }
}

int hitungKedalaman(address root, int start) {
    if (root == Nil) {
        return start;
    } else {
        int kiri  = hitungKedalaman(root->left, start + 1);
        int kanan = hitungKedalaman(root->right, start + 1);
        return (kiri > kanan) ? kiri : kanan;
    }
}
```

### main.cpp
```
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    address root = Nil;

    // insert node
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6); // duplikat tidak dimasukkan
    insertNode(root, 7);

    cout << "InOrder Traversal: ";
    InOrder(root);
    cout << endl;

    cout << "Kedalaman tree : " << hitungKedalaman(root, 0) << endl;
    cout << "Jumlah node     : " << hitungJumlahNode(root) << endl;
    cout << "Total info      : " << hitungTotalInfo(root) << endl;

    return 0;
}
```
> Output
> ![Screenshot bagian x]( https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%2010/jawaban2.png)

Kode ini mengimplementasikan pohon biner pencarian menggunakan bahasa C++. Setiap node menyimpan nilai dan memiliki anak kiri dan kanan, dengan aturan bahwa nilai di anak kiri lebih kecil dan di anak kanan lebih besar. Fungsi insert menambahkan node baru secara rekursif, find mencari node tertentu, dan InOrder menampilkan isi pohon secara terurut. Selain itu, terdapat fungsi untuk menghitung jumlah node, total nilai semua node, dan kedalaman pohon. Pendekatan rekursif membuat kode lebih ringkas dan memudahkan operasi pada struktur data pohon yang bersifat hierarkis.
### Soal 3
## no3.cpp
```go
#include <iostream>
#include <stack>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Preorder Iterative
void preorderIterative(Node* root) {
    if (!root) return;

    stack<Node*> s;
    s.push(root);

    while (!s.empty()) {
        Node* current = s.top();
        s.pop();
        cout << current->data << " ";

        if (current->right) s.push(current->right);
        if (current->left) s.push(current->left);
    }
}

// Postorder Iterative
void postorderIterative(Node* root) {
    if (!root) return;

    stack<Node*> s1, s2;
    s1.push(root);

    while (!s1.empty()) {
        Node* current = s1.top();
        s1.pop();
        s2.push(current);

        if (current->left) s1.push(current->left);
        if (current->right) s1.push(current->right);
    }

    while (!s2.empty()) {
        cout << s2.top()->data << " ";
        s2.pop();
    }
}

int main() {
    // Membuat tree baru dengan node berbeda
    Node* root = new Node(10);
    root->left = new Node(5);
    root->right = new Node(15);
    root->left->left = new Node(3);
    root->left->right = new Node(7);
    root->right->left = new Node(12);
    root->right->right = new Node(18);

    cout << "Pre-order (Iterative)  : ";
    preorderIterative(root);

    cout << "\nPost-order (Iterative) : ";
    postorderIterative(root);

    cout << endl;
    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%2010/jawaban%203.png)
Kode ini membuat pohon biner dan melakukan traversal secara iteratif menggunakan stack. Fungsi preorderIterative menampilkan node dimulai dari akar kemudian anak kiri dan kanan, sedangkan fungsi postorderIterative menampilkan node mulai dari anak hingga akar. Pendekatan iteratif ini menghindari penggunaan rekursi sehingga meminimalkan penggunaan memori call stack. Struktur pohon yang digunakan berbeda dari contoh sebelumnya untuk menunjukkan fleksibilitas traversal pada berbagai bentuk pohon biner.
## Referensi
1. https://www.w3schools.com/dsa/dsa_theory_trees.php
2. https://www.w3schools.com/dsa/dsa_data_binarytrees.php
3. https://www.w3schools.com/dsa/dsa_data_binarysearchtrees.php

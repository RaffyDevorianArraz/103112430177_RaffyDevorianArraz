# <h1 align="center">Laporan Praktikum Modul 14 <br>GRAPH</h1>
<p align="center">103112430177 - RAFFY DEVORIAN ARRAZ</p>

## Dasar Teori
Graph adalah struktur data non-linear yang terdiri dari simpul yang saling terhubung oleh sisi, baik berarah maupun tidak. Representasinya bisa menggunakan adjacency matrix atau adjacency list, dengan list lebih efisien untuk graph jarang. Operasi utama pada graph termasuk penelusuran seperti BFS yang menjelajahi per level, DFS yang menjelajahi secara mendalam, serta topological sort untuk mengurutkan simpul pada directed acyclic graph berdasarkan dependensi.

## Guided
#### graf.h
```c++
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif
```
#### graf.cpp
```c++
#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}

```
#### main.cpp
```c++
#include "graf.h"
#include "graf.cpp"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}

```

## UNGUIDED 
#### graph.h
```c++
#ifndef GRAPH_H
#define GRAPH_H

typedef int infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode Next;
};

struct ElmEdge {
    adrNode Node;
    adrEdge Next;
};

struct Graph {
    adrNode first;
};

adrNode findNode(Graph G, infoGraph X);

void CreateGraph(Graph &G);
adrNode InsertNode(Graph &G, infoGraph X);
void ConnectNode(Graph &G, infoGraph X1, infoGraph X2);
void PrintInfoGraph(Graph G);

void PrintDFS(Graph G, adrNode N);
void PrintBFS(Graph G, adrNode N);

void resetVisited(Graph &G);

#endif
```
#### graph.cpp
```c++
#include <iostream>
#include <queue>
#include "graph.h"
using namespace std;

void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode findNode(Graph G, infoGraph X) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == X) return P;
        P = P->Next;
    }
    return NULL;
}

adrNode InsertNode(Graph &G, infoGraph X) {
    adrNode newNode = new ElmNode;
    newNode->info = X;
    newNode->visited = 0;
    newNode->firstEdge = NULL;
    newNode->Next = NULL;

    if (G.first == NULL) {
        G.first = newNode;
    } else {
        adrNode P = G.first;
        while (P->Next != NULL) P = P->Next;
        P->Next = newNode;
    }
    return newNode;
}

void ConnectNode(Graph &G, infoGraph X1, infoGraph X2) {
    adrNode node1 = findNode(G, X1);
    adrNode node2 = findNode(G, X2);
    if (node1 == NULL || node2 == NULL) return;

    adrEdge e1 = new ElmEdge;
    e1->Node = node2;
    e1->Next = NULL;

    if (node1->firstEdge == NULL) node1->firstEdge = e1;
    else {
        adrEdge P = node1->firstEdge;
        while (P->Next != NULL) P = P->Next;
        P->Next = e1;
    }

    adrEdge e2 = new ElmEdge;
    e2->Node = node1;
    e2->Next = NULL;

    if (node2->firstEdge == NULL) node2->firstEdge = e2;
    else {
        adrEdge P = node2->firstEdge;
        while (P->Next != NULL) P = P->Next;
        P->Next = e2;
    }
}

void PrintInfoGraph(Graph G) {
    cout << "Graph Nodes and Connections:" << endl;
    adrNode P = G.first;
    while (P != NULL) {
        cout << "Node " << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL) {
            cout << E->Node->info << " ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
    cout << endl;
}

void resetVisited(Graph &G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->Next;
    }
}

void DFS(adrNode N) {
    if (N == NULL || N->visited) return;
    cout << N->info << " ";
    N->visited = 1;
    adrEdge E = N->firstEdge;
    while (E != NULL) {
        if (!E->Node->visited) DFS(E->Node);
        E = E->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    cout << "DFS from node " << N->info << ": ";
    resetVisited(G);
    DFS(N);
    cout << endl;
}

void PrintBFS(Graph G, adrNode N) {
    cout << "BFS from node " << N->info << ": ";
    resetVisited(G);
    queue<adrNode> q;
    q.push(N);
    N->visited = 1;
    while (!q.empty()) {
        adrNode cur = q.front();
        q.pop();
        cout << cur->info << " ";
        adrEdge E = cur->firstEdge;
        while (E != NULL) {
            if (!E->Node->visited) {
                E->Node->visited = 1;
                q.push(E->Node);
            }
            E = E->Next;
        }
    }
    cout << endl;
}

```
#### main.cpp
```c++
#include <iostream>
#include "graph.h"
using namespace std;

int main() {
    Graph G;
    CreateGraph(G);

    // Menambahkan node
    for (int i = 1; i <= 6; i++) InsertNode(G, i);

    // Membuat koneksi berbeda
    ConnectNode(G, 1, 2);
    ConnectNode(G, 1, 3);
    ConnectNode(G, 2, 4);
    ConnectNode(G, 2, 5);
    ConnectNode(G, 3, 6);

    // Menampilkan info graph
    PrintInfoGraph(G);

    // DFS dan BFS mulai dari node 1
    adrNode start = findNode(G, 1);
    if (start != NULL) {
        PrintDFS(G, start);
        PrintBFS(G, start);
    }

    // DFS dari node 3
    adrNode node3 = findNode(G, 3);
    if (node3 != NULL) PrintDFS(G, node3);

    return 0;
}

```
> Output
> ![Screenshot bagian x](../modul14/output/14.png)

Graph adalah struktur data non-linear yang terdiri dari simpul atau node yang saling terhubung oleh sisi atau edge. Graph dapat bersifat terarah atau tidak terarah dan digunakan untuk merepresentasikan hubungan antar objek seperti jaringan, rute, atau dependensi. Implementasi graph bisa menggunakan daftar ketetanggaan atau matriks ketetanggaan, dengan daftar ketetanggaan lebih efisien untuk graph yang jarang memiliki edge. Algoritma dasar pada graph termasuk penelusuran kedalaman untuk menjelajahi node secara mendalam, penelusuran lebar untuk menjelajahi node per level, serta algoritma pengurutan topologis untuk menyusun node pada graph terarah tanpa siklus sesuai urutan ketergantungan.

## Referensi
1.GeeksforGeeks: Graph and its representations https://www.geeksforgeeks.org/graph-and-its-representations/

2.GeeksforGeeks: Depth First Search or DFS for a Graph https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/

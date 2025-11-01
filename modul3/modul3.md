# <h1 align="center">Laporan Praktikum Modul 03 <br> Abstract Data Type</h1>
<p align="center">Raffy Devorian Arraz - 103112430177</p>

## Dasar Teori
Dasar teori dari program di atas berkaitan dengan Abstract Data Type (ADT) merupakan konsep dasar dalam pemrograman terstruktur yang digunakan untuk mendefinisikan tipe data baru beserta operasi-operasi dasar (primitif) yang dapat dilakukan terhadapnya. ADT bersifat abstrak karena pengguna hanya mengetahui apa yang dapat dilakukan tanpa perlu memahami bagaimana cara kerjanya secara internal. Dalam ADT biasanya terdapat konstruktor untuk membentuk objek, selector untuk mengakses nilai, mutator untuk mengubah nilai, validator untuk memeriksa keabsahan data, destruktor untuk menghapus objek, serta operator relasional, aritmatika, dan fungsi input/output sebagai antarmuka. Implementasi ADT umumnya dibagi menjadi dua bagian, yaitu file header (.h) yang berisi definisi tipe data dan deklarasi fungsi, serta file implementasi (.cpp) yang berisi realisasi fungsi tersebut. Dengan memisahkan spesifikasi dan implementasi, ADT dapat meningkatkan modularitas, reusabilitas, serta memudahkan pemeliharaan kode program.


## Guided

### Menghitung Rata Rata

### mahasiswa.h
```go
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};

void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);

#endif
```

### Mahasiswa.cpp
```go
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m) .nim;
    cout << "input nilai = ";
    cin >> (m) .nilai1;
    cout << "input niali2 = ";
    cin >> m .nilai2;

}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}
```

### main.cpp
```go
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main(){
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata rata = " << rata2(mhs);
    return 0;
}
```

## Unguided

### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.

```go
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return (0.3f * uts) + (0.4f * uas) + (0.3f * tugas);
}

void inputMahasiswa(Mahasiswa &mhs) {
    cout << "Masukkan Nama          : ";
    getline(cin, mhs.nama);
    cout << "Masukkan NIM           : ";
    getline(cin, mhs.nim);
    cout << "Masukkan Nilai UTS     : ";
    cin >> mhs.uts;
    cout << "Masukkan Nilai UAS     : ";
    cin >> mhs.uas;
    cout << "Masukkan Nilai Tugas   : ";
    cin >> mhs.tugas;
    cin.ignore(); 
    mhs.nilaiAkhir = hitungNilaiAkhir(mhs.uts, mhs.uas, mhs.tugas);
}

void tampilMahasiswa(Mahasiswa mhs[], int jumlah) {
    cout << "\n==============================================\n";
    cout << "          DATA MAHASISWA TERDAFTAR             \n";
    cout << "==============================================\n";
    for (int i = 0; i < jumlah; i++) {
        cout << "Mahasiswa ke-" << i + 1 << endl;
        cout << "Nama         : " << mhs[i].nama << endl;
        cout << "NIM          : " << mhs[i].nim << endl;
        cout << "UTS          : " << mhs[i].uts << endl;
        cout << "UAS          : " << mhs[i].uas << endl;
        cout << "Tugas        : " << mhs[i].tugas << endl;
        cout << "Nilai Akhir  : " << mhs[i].nilaiAkhir << endl;
        cout << "----------------------------------------------\n";
    }
}

int main() {
    Mahasiswa daftarMhs[10];
    int jumlah;

    cout << "Masukkan jumlah mahasiswa (maksimal 10): ";
    cin >> jumlah;
    cin.ignore();

    if (jumlah > 10 || jumlah <= 0) {
        cout << "Jumlah tidak valid! Harus antara 1 sampai 10." << endl;
        return 0;
    }

    for (int i = 0; i < jumlah; i++) {
        cout << "\nInput data mahasiswa ke-" << i + 1 << endl;
        inputMahasiswa(daftarMhs[i]);
    }

    tampilMahasiswa(daftarMhs, jumlah);

    cout << "\nData berhasil ditampilkan!" << endl;
    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%203/jawaban%201.png)

Program ini menggunakan struct untuk menyimpan dan mengelola data beberapa mahasiswa yang mencakup nama, NIM, nilai UTS, UAS, tugas, serta nilai akhirnya. Perhitungan nilai akhir dilakukan dengan fungsi hitungNilaiAkhir() yang menerapkan bobot tertentu untuk setiap komponen nilai. Data dimasukkan melalui fungsi inputMahasiswa() dengan parameter referensi agar setiap perubahan tersimpan langsung pada objek mahasiswa. Setelah semua data diinput, fungsi tampilMahasiswa() menampilkan hasilnya secara terstruktur. Program ini mencerminkan penerapan konsep struct, fungsi, array, dan referensi dalam pengolahan data sederhana di C++.

### Soal 2
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%203/Screenshot%202025-10-13%20181006.png)


### pelajaran.h
```go
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED

#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);

void tampil_pelajaran(pelajaran pel);

#endif
```
### pelajaran.cpp
```go
#include <iostream>
#include "pelajaran.h"
using namespace std;

pelajaran create_pelajaran(string namapel, string kodepel) {
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```
### main.cpp
```go
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";

    pelajaran pel = create_pelajaran(namapel, kodepel);

    tampil_pelajaran(pel);

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%203/jawaban%202.png)

Program ini menerapkan konsep modularisasi dengan header file (.h) dan implementasi terpisah (.cpp) dalam C++. Struct pelajaran digunakan untuk menyimpan data nama dan kode mata pelajaran. Fungsi create_pelajaran() membuat dan mengembalikan objek pelajaran berdasarkan input nama serta kode, sedangkan tampil_pelajaran() menampilkan informasi tersebut ke layar. Fungsi main() memanggil keduanya untuk menampilkan data pelajaran “Struktur Data” dengan kode “STD”. Pendekatan ini membuat program lebih terstruktur, mudah dirawat, dan sesuai praktik pemrograman terorganisir di C++.

### Soal 3

Buatlah program dengan ketentuan :
- 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
- fungsi/prosedur yang menampilkan isi sebuah array integer 2D
- fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu
- fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah
pointer

```go
#include <iostream>
using namespace std;

void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

void tukarNilai(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

void tukarPosisi(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int A[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int B[3][3] = {
        {10, 11, 12},
        {13, 14, 15},
        {16, 17, 18}
    };

    cout << "=== ARRAY SEBELUM DITUKAR ===\n";
    cout << "Array A:\n"; tampilArray(A);
    cout << "\nArray B:\n"; tampilArray(B);

    tukarPosisi(A, B, 1, 1); // Menukar elemen di posisi [1][1]

    cout << "\n=== SETELAH MENUKAR ELEMEN [1][1] ===\n";
    cout << "Array A:\n"; tampilArray(A);
    cout << "\nArray B:\n"; tampilArray(B);

    int x = 50, y = 100;
    int *ptr1 = &x;
    int *ptr2 = &y;

    cout << "\n=== NILAI SEBELUM DITUKAR DENGAN POINTER ===\n";
    cout << "x = " << x << ", y = " << y << endl;

    tukarPointer(ptr1, ptr2);

    cout << "=== NILAI SETELAH DITUKAR DENGAN POINTER ===\n";
    cout << "x = " << x << ", y = " << y << endl;

    return 0;
}


```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%203/jawaban%203.png))

Program ini menunjukkan penerapan fungsi, array 2 dimensi, referensi, dan pointer dalam C++. Fungsi tampilArray() menampilkan isi matriks, tukarPosisi() menukar elemen antar dua matriks berdasarkan indeks tertentu, sedangkan tukarPointer() menukar nilai dua variabel melalui pointer. Konsep ini memperlihatkan bagaimana data dapat dimanipulasi secara langsung baik dengan referensi (&) maupun pointer (*), sehingga program lebih fleksibel dalam mengubah nilai di memori tanpa harus mengembalikannya melalui return statement.

## Referensi

1. [https://www.w3schools.com/dsa/dsa_intro.php]
2. [https://www.w3schools.com/cpp/cpp_data_structures.asp]

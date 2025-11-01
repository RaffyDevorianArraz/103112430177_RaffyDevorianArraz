# <h1 align="center">Laporan Praktikum Modul 02 <br> PENGENALAN BAHASA C++ (BAGIAN KEDUA)</h1>
<p align="center">Raffy Devorian Arraz - 103112430177</p>

## Dasar Teori
Dasar teori dari program tersebut berkaitan dengan **konsep fungsi dan pemanggilan dengan referensi (*call by reference*)** dalam bahasa C++. Berdasarkan Modul 2 “Pengenalan Bahasa C++ (Bagian Kedua)” pada mata kuliah Struktur Data, *call by reference* adalah metode pengiriman parameter di mana alamat memori dari variabel asli dikirimkan ke fungsi, bukan salinan nilainya. Dengan mekanisme ini, setiap perubahan yang dilakukan pada parameter di dalam fungsi akan secara langsung memengaruhi variabel aslinya di luar fungsi. Pada kode tersebut, fungsi `kuadratkan(int &x)` menggunakan parameter referensi (ditandai dengan `&`), sehingga saat nilai `x` diubah menjadi hasil kuadratnya (`x = x * x`), variabel `nilai` di fungsi `main()` ikut mengalami perubahan. Pendekatan ini membuat manipulasi data menjadi lebih efisien karena tidak perlu mengembalikan nilai melalui *return statement* dan menghindari duplikasi data di memori.

## Guided

### array
```go
#include <iostream>
using namespace std;

int main() {

    int nilai[5] = {1, 2, 3, 4, 5};

    for ( int i = 0;  i < 5; i++)
    {
       
        cout << "elemen ke-" << i << "=" << nilai[i] << endl;
    }
    return 0;
} 
```

### array 2
```go
#include <iostream>
using namespace std;

int main()
{
    char pesan_array[] = "Nasi Padang";
    char *pesan_pointer = "Ayam Bakar 23";

    cout << "String Array : " << pesan_array << endl;
    cout << "String Pointer : " << pesan_pointer << endl;

    // Mengubah karakter dalam array diperbolehkan
    pesan_array[0] = 'h';
    cout << "String Array setelah diubah: " << pesan_array << endl;

    // Pointer dapat diubah untuk menunjuk ke string lain
    pesan_pointer = "Sariaman";
    cout << "String Pointer setelah menunjuk ke string lain: " << pesan_pointer << endl;

    return 0;
}
```


### matriks
```go
#include <iostream>
using namespace std;

int main(){
    int matriks[3][3] ={
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}};

    for (int i = 0; i < 3; i++)
        {
        for (int j = 0; j < 3; j++)
    {
            cout << matriks[i][j]<< " ";
    }
    cout << endl;

    }
    return 0;
}
```

### pointer
```go
#include <iostream>
using namespace std;

int main()
{
    int umur = 25;
    int *p_umur;

    p_umur = &umur;

    cout << "Nilai 'umur': " << umur << endl;
    cout << "Alamat memori 'umur': " << &umur << endl;
    cout << "Nilai 'p_umur' (alamat): " << p_umur << endl;
    cout << "Nilai yang diakses 'p_umur': " << p_umur << endl;
    cout << "Alamat memori dari pointer 'p_umur' itu sendiri: " << p_umur << endl;
    return 0;
}
```

### array_pointer
```go
#include <iostream>
using namespace std;

int main()
{
    int data[5] = {10, 20, 30, 40, 50};
    int *p_data = data;

    cout << "Mengakses elemen array cara normal:" << endl;

    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << data[i] << endl;
    }

    cout << "Mengakses elemen array menggunakan pointer:" << endl;

    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << *(p_data + i) << endl;
    }

    return 0;
}
```

### string_pointer
```go
#include <iostream>
using namespace std;

int main()
{
    char pesan_array[] = "Nasi Padang";
    char *pesan_pointer = "Ayam Bakar 23";

    cout << "String Array: " << pesan_array << endl;
    cout << "String Pointer: " << pesan_pointer << endl;

    // Mengubah karakter dalam array diperbolehkan
    pesan_array[0] = 'h';
    cout << "String Array setelah diubah: " << pesan_array << endl;

    // Pointer dapat diubah untuk menunjuk ke string lain
    pesan_pointer = "Sariman";
    cout << "String Pointer setelah menunjuk ke string lain: " << pesan_pointer << endl;

    return 0;
}
```

### call by pointer

```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}
```

### call by reference

```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
```

## Unguided

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
    int matriks[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int transpose[3][3];

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matriks[i][j];
        }
    }

    cout << "Matriks Awal:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
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
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/modul%202/jawaban%20no%201.png)

Program di atas berfungsi untuk melakukan transpose pada sebuah matriks berukuran 3x3 menggunakan bahasa C++. Pertama, matriks awal diinisialisasi dengan elemen bernilai 1 hingga 9. Kemudian, dibuat matriks baru bernama `transpose` untuk menyimpan hasil penukaran baris dan kolom. Proses transpose dilakukan dengan menggunakan dua perulangan bersarang, di mana setiap elemen `matriks[i][j]` ditukar posisinya menjadi `transpose[j][i]`, sehingga baris menjadi kolom dan sebaliknya. Setelah proses selesai, program menampilkan matriks awal dan matriks hasil transpose ke layar, sehingga pengguna dapat melihat perbedaan antara keduanya.


### Soal 2

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5
Nilai setelah dikuadratkan: 25

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
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/modul%202/jawaban%20no%202.png))

Program di atas digunakan untuk **mengkuadratkan sebuah bilangan menggunakan konsep *call by reference*** dalam bahasa C++. Variabel `nilai` diinisialisasi dengan angka 5, lalu ditampilkan sebagai nilai awal. Fungsi `kuadratkan(int &x)` menerima parameter berupa *reference* (`&`), sehingga setiap perubahan pada variabel `x` di dalam fungsi akan langsung mengubah nilai asli di luar fungsi. Di dalam fungsi, nilai `x` dikalikan dengan dirinya sendiri (`x = x * x`), sehingga hasilnya adalah kuadrat dari nilai awal. Setelah fungsi dipanggil, program menampilkan nilai yang sudah dikuadratkan, yaitu 25.
## Referensi

1. https://www.w3schools.com/cpp/cpp_arrays.asp
2. https://www.w3schools.com/cpp/cpp_references.asp
3. https://www.w3schools.com/cpp/cpp_pointers.asp

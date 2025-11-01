# <h1 align="center">Laporan Praktikum Modul 01 <br>  Pengenalan C++</h1>
<p align="center">Raffy Devorian Arraz - 103112430177</p>

## Dasar Teori

Dalam bahasa C++, terdapat beberapa konsep dasar yang penting untuk dipahami, yaitu **struct**, **aritmatika**, **kondisi**, **perulangan**, dan **fungsi**. `Struct` digunakan untuk mengelompokkan beberapa variabel dengan tipe data berbeda ke dalam satu wadah agar pengelolaan data menjadi lebih mudah. Konsep **aritmatika** berkaitan dengan penggunaan operator seperti `+`, `-`, `*`, `/`, dan `%` untuk melakukan operasi matematika. **Kondisi** atau percabangan (`if`, `else if`, `else`, `switch`) memungkinkan program mengambil keputusan dan menjalankan perintah tertentu berdasarkan syarat yang terpenuhi. **Perulangan** (`for`, `while`, `do while`) digunakan untuk mengeksekusi kode secara berulang tanpa perlu menulis instruksi yang sama berkali-kali. Sedangkan **fungsi** adalah sekumpulan perintah dalam satu blok kode yang bisa dipanggil kapan pun untuk melakukan tugas tertentu, sehingga program menjadi lebih terstruktur, mudah dibaca, dan efisien digunakan kembali.

## guided


### guide 1
```go
#include <iostream>
#include <string>
using namespace std;

// Definisi struct
struct Mahasiswa {
    string nama;
    string nim;
    float ipk;
};

int main() {

    Mahasiswa mhs1;

    cout << "Masukkan Nama Mahasiswa: ";
    getline(cin, mhs1.nama);
    cout << "Masukkan NIM Mahasiswa : ";
    cin >> mhs1.nim;
    cout << "Masukkan IPK Mahasiswa : ";
    cin >> mhs1.ipk;

    cout << "\n=== Data Mahasiswa ===" << endl;
    cout << "Nama : " << mhs1.nama << endl;
    cout << "NIM  : " << mhs1.nim << endl;
    cout << "IPK  : " << mhs1.ipk << endl;

    return 0;
}
```

### guide 2
```go
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}
```

### guide 3
```go
#include <iostream>
using namespace std;

int main()
{
    int kode_hari;
    cout << "Menentukan hari kerja/libur\n"<<endl;
    cout << "1=Senin 3=Rabu 5=Jumat 7=Minggu "<<endl;
    cout << "2=Selasa 4=Kamis 6=Sabtu "<<endl;
    cin >> kode_hari;
    switch (kode_hari)
    {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout<<"Hari Kerja";
        break;
    case 6:
    case 7:
        cout<<"Hari Libur";
        break;
    default:
        cout<<"Kode masukan salah!!!";
    }
    return 0;
}
```

### guide 4
```go
#include <iostream>
using namespace std;

int main()
{
    int i = 1;
    int jum;
    cin >> jum;
    do
    {
        cout << "bahlil ke-" << (i + 1) << endl;
        i++;
    } while (i < jum);
    return 0;
}
```

### guide 5
```go
#include <iostream>
using namespace std;

// Prosedur: hanya menampilkan hasil, tidak mengembalikan nilai
void tampilkanHasil(double p, double l)
{
    cout << "\n=== Hasil Perhitungan ===" << endl;
    cout << "Panjang : " << p << endl;
    cout << "Lebar   : " << l << endl;
    cout << "Luas    : " << p * l << endl;
    cout << "Keliling: " << 2 * (p + l) << endl;
}

// Fungsi: mengembalikan nilai luas
double hitungLuas(double p, double l)
{
    return p * l;
}

// Fungsi: mengembalikan nilai keliling
double hitungKeliling(double p, double l)
{
    return 2 * (p + l);
}

int main()
{
    double panjang, lebar;

    cout << "Masukkan panjang: ";
    cin >> panjang;
    cout << "Masukkan lebar  : ";
    cin >> lebar;

    // Panggil fungsi
    double luas = hitungLuas(panjang, lebar);
    double keliling = hitungKeliling(panjang, lebar);

    cout << "\nDihitung dengan fungsi:" << endl;
    cout << "Luas      = " << luas << endl;
    cout << "Keliling  = " << keliling << endl;

    // Panggil prosedur
    tampilkanHasil(panjang, lebar);

    return 0;
}

```

### guide 6
```go
#include <iostream>
using namespace std;
int main()
{
    string ch;
    cout << "Masukkan sebuah karakter: ";
    // cin >> ch;
    ch = getchar();  //Menggunakan getchar() untuk membaca satu karakter
    cout << "Karakter yang Anda masukkan adalah: " << ch << endl;
    return 0;
}
```


## Unguided

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan betipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```go
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    float x, y;

    cout << "=== Program Kalkulator Sederhana ===" << endl;
    cout << "Masukkan bilangan pertama: ";
    cin >> x;
    cout << "Masukkan bilangan kedua : ";
    cin >> y;
    cout << endl;

    cout << fixed << setprecision(2); 

    float tambah = x + y;
    cout << "Hasil penjumlahan     : " << x << " + " << y << " = " << tambah << endl;

    float pengurangan = x - y;
    cout << "Hasil pengurangan     : " << x << " - " << y << " = " << pengurangan << endl;

    float perkalian = x * y;
    cout << "Hasil perkalian       : " << x << " * " << y << " = " << perkalian << endl;

    if (y != 0) {
        float pembagian = x / y;
        cout << "Hasil pembagian       : " << x << " / " << y << " = " << pembagian << endl;
    } else {
        cout << "Hasil pembagian       : Tidak dapat dilakukan (pembagi = 0)" << endl;
    }

    cout << "===================================" << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/LAPRAK/jawaban%201.png)

Program tersebut adalah kalkulator sederhana yang dibuat dengan C++. Cara kerjanya, pengguna diminta memasukkan dua bilangan, lalu program otomatis menampilkan hasil penjumlahan, pengurangan, perkalian, dan pembagian dari kedua bilangan tersebut. Untuk operasi bagi, program juga sudah diberi pengaman: kalau bilangan kedua yang dimasukkan adalah nol, program akan memberi tahu bahwa pembagian tidak bisa dilakukan. Jadi, program ini bisa membantu menghitung operasi dasar secara cepat dan aman langsung lewat terminal.


### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100.

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Masukkan angka (0-100): ";
    cin >> n;

    cout << n << " : ";

    if (n < 0 || n > 100) {
        cout << "Input di luar jangkauan";
    }
    else if (n == 0) {
        cout << "nol";
    }
    else if (n == 100) {
        cout << "seratus";
    }
    else if (n < 12) {
        if (n == 1) cout << "satu";
        else if (n == 2) cout << "dua";
        else if (n == 3) cout << "tiga";
        else if (n == 4) cout << "empat";
        else if (n == 5) cout << "lima";
        else if (n == 6) cout << "enam";
        else if (n == 7) cout << "tujuh";
        else if (n == 8) cout << "delapan";
        else if (n == 9) cout << "sembilan";
        else if (n == 10) cout << "sepuluh";
        else if (n == 11) cout << "sebelas";
    }
    else if (n < 20) {
        int sisa = n - 10;
        if (sisa == 1) cout << "sebelas";
        else if (sisa == 2) cout << "dua belas";
        else if (sisa == 3) cout << "tiga belas";
        else if (sisa == 4) cout << "empat belas";
        else if (sisa == 5) cout << "lima belas";
        else if (sisa == 6) cout << "enam belas";
        else if (sisa == 7) cout << "tujuh belas";
        else if (sisa == 8) cout << "delapan belas";
        else if (sisa == 9) cout << "sembilan belas";
    }
    else {
        int puluh = n / 10;
        int satuan = n % 10;

        if (puluh == 2) cout << "dua puluh";
        else if (puluh == 3) cout << "tiga puluh";
        else if (puluh == 4) cout << "empat puluh";
        else if (puluh == 5) cout << "lima puluh";
        else if (puluh == 6) cout << "enam puluh";
        else if (puluh == 7) cout << "tujuh puluh";
        else if (puluh == 8) cout << "delapan puluh";
        else if (puluh == 9) cout << "sembilan puluh";

        if (satuan > 0) {
            cout << " ";
            if (satuan == 1) cout << "satu";
            else if (satuan == 2) cout << "dua";
            else if (satuan == 3) cout << "tiga";
            else if (satuan == 4) cout << "empat";
            else if (satuan == 5) cout << "lima";
            else if (satuan == 6) cout << "enam";
            else if (satuan == 7) cout << "tujuh";
            else if (satuan == 8) cout << "delapan";
            else if (satuan == 9) cout << "sembilan";
        }
    }

    cout << endl;
    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/LAPRAK/jawaban%202.png)

Program C++ tersebut dibuat untuk mengonversi angka antara 0 hingga 100 menjadi tulisan dalam bahasa Indonesia. Ketika pengguna memasukkan angka, program lebih dulu memeriksa apakah angkanya valid; jika tidak, akan muncul pesan bahwa input berada di luar jangkauan. Angka 0 ditampilkan sebagai “nol” dan angka 100 sebagai “seratus”. Untuk bilangan di bawah 12, program langsung menuliskan sesuai sebutan dasarnya, sedangkan bilangan 12 sampai 19 ditampilkan dengan format “... belas”. Sementara itu, angka 20 sampai 99 dipecah menjadi puluhan dan satuan, lalu digabungkan sehingga membentuk tulisan yang sesuai, contohnya angka 42 menjadi “empat puluh dua”. Dengan cara ini, program dapat menampilkan angka dalam bentuk kata yang lebih jelas dan mudah dipahami.


### Soal 3

Buatlah program yang dapat memberikan input dan output sbb.

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Masukkan angka: ";
    cin >> n;

    cout << "\n=== Pola Angka dan Bintang ===\n";

    for (int i = n; i >= 1; i--) {
        // Spasi di awal setiap baris
        for (int spasi = 0; spasi < n - i; spasi++) {
            cout << "  ";
        }

        // Bagian kiri menampilkan angka menurun
        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }

        // Simbol bintang di tengah
        cout << "* ";

        // Bagian kanan menampilkan angka menaik
        for (int k = 1; k <= i; k++) {
            cout << k << " ";
        }

        cout << endl;
    }

    // Bintang terakhir di tengah
    for (int spasi = 0; spasi < n; spasi++) {
        cout << "  ";
    }
    cout << "*" << endl;

    cout << "===============================" << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/LAPRAK/jawaban%203.png)

Program ini menghasilkan pola simetris angka dan bintang berdasarkan input pengguna. Dimulai dari baris dengan angka menurun di kiri, bintang di tengah, dan angka menaik di kanan, kemudian pola mengecil secara bertahap hingga tersisa satu bintang di bagian bawah. Setiap baris diberi spasi di awal untuk menjaga kesimetrisan tampilan, menciptakan bentuk seperti segitiga terbalik yang berpusat pada simbol `*`.


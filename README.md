# <h1 align="center">Laporan Praktikum Modul 8 <br>QUEUE</h1>
<p align="center">M. AFRIZA MARANTIKA - 103112430271</p>

## Dasar Teori
Queue adalah struktur data yang bekerja seperti antrean di loket tiket. Siapa yang datang lebih dulu akan dilayani lebih dulu, sedangkan yang datang belakangan harus menunggu giliran. Pola ini disebut FIFO (First In First Out). Artinya, elemen pertama yang masuk ke dalam Queue juga akan menjadi elemen pertama yang keluar. Dalam bahasa C, Queue bisa dibuat menggunakan array maupun linked list. Implementasi dengan array lebih mudah karena menggunakan indeks, sedangkan linked list lebih fleksibel karena penambahan dan penghapusan data tidak memerlukan pergeseran elemen.

## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

// ukuran maksimal queue
#define MAX 5

// struktur queue
struct Queue {
   // datanya pake array yaa, bukan linked list
   int data[MAX];
   int head;
   int tail;
};

// membuat antrian kosong
void buat_queue (Queue &Q) {
   Q.head = -1;
   Q.tail = -1;
   // kenapa head dan tail-nya -1?
   // karena index array mulai dari 0
}

// cek queueu-nya kosong ngga?
bool cek_kosong (Queue Q) {
   return (Q.head == -1 && Q.tail == -1);
}

// cek queue-nya penuh ngga?
bool cek_penuh (Queue Q) {
   return (Q.tail == MAX - 1);
}

// menampilkan isi queue
void print_queue (Queue Q) {
   if (cek_kosong(Q)) {
      cout << "queue kosong" << endl;
   } else {
      cout << "queue : ";
      for (int i = Q.head; i <= Q.tail; i++) {
         cout << Q.data[i] << " -> ";
      }
      cout << endl;
   }
}

// menambahkan elemen (enqueue)
void enqueue (Queue &Q, int x) {
   if (cek_penuh(Q)) {
      cout << "queue sudah penuh, tidak bisa menambah data" << endl;
   } else {
      if (cek_kosong(Q)) {
         Q.head = Q.tail = 0;
      } else {
         Q.tail++;
      }

      Q.data[Q.tail] = x;
      cout << "menambahkan " << x << " ke dalam queue" << endl;
   }
}

// menghapus elemen (dequeue)
void dequeue (Queue &Q) {
   if (cek_kosong(Q)) {
      cout << "queue kosong, tidak ada yang bisa dihapus" << endl;
   } else {
      cout << "dequeue " << Q.data[Q.head] << " dari dalam queue" << endl;

      // jika hanya ada 1 elemen
      if (Q.head == Q.tail) {
         Q.head = Q.tail = -1;
      } else {
         // geser semua elemen ke depan/kiri
         // biar tempat kosong di depan dipenuhin
         // dan tempat di belakang bisa dikosongin
         for (int i = Q.head; i < Q.tail; i++) {
            Q.data[i] = Q.data[i + 1];
         }

         Q.tail--;
      }
   }
}

// eksekutor
int main() {
   Queue Q;
   buat_queue(Q);

   enqueue(Q, 5);
   enqueue(Q, 2);
   enqueue(Q, 7);
   print_queue(Q);

   dequeue(Q);
   print_queue(Q);

   enqueue(Q, 4);
   enqueue(Q, 9);
   print_queue(Q);

   dequeue(Q);
   dequeue(Q);
   print_queue(Q);

   return 0;
}
```
> Output
> 
> ![Screenshot bagian x]()
Program diatas adalah program implementasi struktur data queue berbasis array dengan kapasitas maksimal lima elemen. Program ini menggunakan variabel head dan tail untuk melacak posisi awal dan akhir antrian, yang awalnya bernilai -1 sebagai tanda bahwa antrian kosong. Operasi enqueue menambahkan elemen di bagian belakang antrian jika belum penuh, sementara operasi dequeue menghapus elemen paling depan; jika hanya tersisa satu elemen, antrian dikosongkan, sedangkan jika lebih, elemen-elemen di geser ke kiri agar tetap berurutan. Program juga menyediakan fungsi untuk memeriksa apakah antrian kosong atau penuh, serta untuk menampilkan isi antrian. Di bagian main, program mendemonstrasikan proses penambahan, penghapusan, dan penampilan isi queue secara berurutan.

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
    infotype data[MAX];
    int front;
    int rear;
};

void initQueue(Queue &Q);
bool isEmpty(const Queue &Q);
bool isFull(const Queue &Q);
void push(Queue &Q, infotype x);
infotype pop(Queue &Q);
void showQueue(const Queue &Q);

#endif

```
#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void initQueue(Queue &Q) {
    Q.front = Q.rear = -1;
}

bool isEmpty(const Queue &Q) {
    return (Q.front == -1);
}

bool isFull(const Queue &Q) {
    return (Q.rear == MAX - 1);
}

void push(Queue &Q, infotype x) {
    if (isFull(Q)) {
        cout << "Queue penuh!\n";
        return;
    }

    if (isEmpty(Q)) {
        Q.front = 0;
        Q.rear = 0;
        Q.data[Q.rear] = x;
    } else {
        Q.rear++;
        Q.data[Q.rear] = x;
    }
}

infotype pop(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!\n";
        return -1;
    }

    infotype temp = Q.data[Q.front];

    if (Q.front == Q.rear) {
        initQueue(Q);
    } else {
        Q.front++;
    }

    return temp;
}

void showQueue(const Queue &Q) {
    cout << Q.front << " - " << Q.rear << "\t|\t";

    if (isEmpty(Q)) {
        cout << "empty queue\n";
        return;
    }

    for (int i = Q.front; i <= Q.rear; i++) {
        cout << Q.data[i] << " ";
    }
    cout << endl;
}

```

#### main.cpp
```c++
#ifndef QUEUE_H
#define QUEUE_H

const int MAX = 5;
typedef int infotype;

struct Queue {
    infotype data[MAX];
    int front;
    int rear;
};

void initQueue(Queue &Q);
bool isEmpty(const Queue &Q);
bool isFull(const Queue &Q);
void push(Queue &Q, infotype x);
infotype pop(Queue &Q);
void showQueue(const Queue &Q);

#endif

```
> Output soal 1
> 
> ![Screenshot bagian x]()

Program tersebut membuat struktur antrian (queue) menggunakan array, di mana data masuk lewat belakang menggunakan fungsi enqueue dan keluar lewat depan menggunakan dequeue, dengan head menunjukkan posisi awal antrian dan tail menunjukkan posisi akhir, sehingga data diproses berdasarkan prinsip First In, First Out (FIFO) layaknya orang sedang mengantri.

### Soal 2
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void initQueue(Queue &Q){
    Q.front = -1;
    Q.rear = -1;
}

bool isEmpty(const Queue &Q){
    return (Q.front == -1);
}

bool isFull(const Queue &Q){
    return (Q.rear == MAX - 1);
}

void push(Queue &Q, infotype x){
    if (isFull(Q)){
        cout << "Queue penuh!\n";
        return;
    }

    if (isEmpty(Q)){
        Q.front = 0;
    }

    Q.rear++;
    Q.data[Q.rear] = x;
}

infotype pop(Queue &Q){
    if (isEmpty(Q)){
        cout << "Queue kosong!\n";
        return -1;
    }

    infotype value = Q.data[Q.front];

    if (Q.front == Q.rear){
        initQueue(Q);
    } else {
        Q.front++;
    }

    return value;
}

void showQueue(const Queue &Q){
    cout << Q.front << " - " << Q.rear << "\t|\t";

    if (isEmpty(Q)){
        cout << "empty queue\n";
        return;
    }

    for (int i = Q.front; i <= Q.rear; i++){
        cout << Q.data[i] << " ";
    }
    cout << endl;
}

```

> Output soal 2
> 
> ![Screenshot bagian x]()

Program ini membuat struktur queue sederhana menggunakan array. Queue dimulai kosong karena initQueue memberi nilai -1 pada front dan rear. Lalu program menyediakan cara mengecek apakah queue kosong (isEmpty) atau penuh (isFull). Ketika data dimasukkan lewat push, posisi rear digeser ke kanan dan nilai baru ditambahkan; jika sebelumnya kosong, front ikut di-set ke 0. Saat menghapus data dengan pop, program mengambil nilai dari front dan menggeser front satu langkah, atau mengosongkan queue jika datanya tinggal satu. Fungsi showQueue menampilkan posisi front–rear serta isi antrian. Program ini bekerja seperti antrian biasa: masuk dari belakang, keluar dari depan.


### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q){
    Q.front = -1;
    Q.rear  = -1;
}

bool isEmptyQueue(const Queue &Q){
    return Q.front == -1;
}

bool isFullQueue(const Queue &Q){
    return ((Q.rear + 1) % MAX) == Q.front;
}

void enqueue(Queue &Q, infotype x){
    if (isFullQueue(Q)){
        cout << "Queue penuh!\n";
        return;
    }

    if (isEmptyQueue(Q)){
        Q.front = Q.rear = 0;
    } else {
        Q.rear = (Q.rear + 1) % MAX;
    }

    Q.data[Q.rear] = x;
}

infotype dequeue(Queue &Q){
    if (isEmptyQueue(Q)){
        cout << "Queue kosong!\n";
        return -1;
    }

    int val = Q.data[Q.front];

    if (Q.front == Q.rear){
        Q.front = Q.rear = -1;
    } else {
        Q.front = (Q.front + 1) % MAX;
    }

    return val;
}

void printInfo(const Queue &Q){
    cout << Q.front << " - " << Q.rear << " | ";

    if (isEmptyQueue(Q)){
        cout << "empty queue\n";
        return;
    }

    int pos = Q.front;
    while (true){
        cout << Q.data[pos] << " ";
        if (pos == Q.rear) break;
        pos = (pos + 1) % MAX;
    }

    cout << endl;
}

```

> Output soal 3
> 
> ![Screenshot bagian x]()
Program ini membuat circular queue, yaitu antrian yang indeksnya berputar. Front dan rear bernilai -1 saat queue kosong, bertambah melingkar saat enqueue, dan maju saat dequeue. Jika front dan rear kembali sama setelah penghapusan, queue jadi kosong lagi. PrintInfo menampilkan posisi front–rear dan seluruh isi antrian dengan cara berputar. Program ini bekerja seperti antrian biasa tetapi memanfaatkan array supaya bisa berputar.
## Referensi

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

## Referensi

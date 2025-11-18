
1. PENJELASAN QUEUE
   
Kode berikut menunjukkan cara membuat antrian sederhana di Python. Antrian bekerja seperti barisan orang yang menunggu giliran: siapa yang datang dulu, dia yang diproses terlebih dahulu.

---

1. Membuat Antrian Kosong

```python
queue = []
```

Baris ini menyiapkan sebuah list kosong yang akan digunakan sebagai tempat menampung elemen-elemen antrian.

---

### **2. Menambahkan Elemen ke Dalam Antrian**

```python
queue.append('A')
queue.append('B')
queue.append('C')
```

Dengan menggunakan `append()`, setiap data baru ditempatkan di bagian belakang antrian. Setelah tiga perintah ini, urutan datanya menjadi A, lalu B, kemudian C.

---

### **3. Mengambil Elemen Pertama (Dequeue)**

```python
element = queue.pop(0)
```

Perintah `pop(0)` menghapus dan mengembalikan elemen yang berada di posisi paling depan. Karena A berada di urutan pertama, maka A yang keluar dari antrian.

---

### **4. Melihat Elemen Paling Depan**

```python
frontElement = queue[0]
```

Kode ini hanya menampilkan isi antrian terdepan setelah proses dequeue, tanpa menghapus elemen tersebut.

---

### **5. Mengecek Apakah Antrian Masih Berisi**

```python
isEmpty = not bool(queue)
```

Dengan mengevaluasi `bool(queue)`, kita bisa mengetahui apakah antrian masih memiliki elemen atau tidak. Penggunaan `not` membalik nilai tersebut agar lebih mudah dibaca.

---

### **6. Mengetahui Jumlah Data Dalam Antrian**

```python
print("Size: ", len(queue))
```

Perintah `len(queue)` mengembalikan jumlah elemen yang tersisa. Karena elemen pertama sudah diambil, sekarang ada dua item yang masih ada dalam antrian.

---



Siap, aku parafrase penjelasan untuk kode **Stack** ini dengan gaya berbeda dan tidak mirip dengan penjelasan Queue tadi.

---

2. PENJELASAN STACK

Kode berikut memperlihatkan bagaimana cara membuat dan menggunakan **Stack** di Python. Stack bekerja dengan prinsip **LIFO (Last In, First Out)** — data yang terakhir dimasukkan akan menjadi yang pertama diambil.

---

### **1. Membuat Stack Kosong**

```python
stack = []
```

Bagian ini membuat sebuah list kosong yang berfungsi sebagai wadah data untuk stack.

---

### **2. Push (Menambahkan Elemen ke Puncak Stack)**

```python
stack.append('A')
stack.append('B')
stack.append('C')
```

Setiap kali `append()` dipanggil, elemen baru ditempatkan di posisi paling atas dari stack. Urutannya menjadi A → B → C, dengan C sebagai elemen teratas.

---

### **3. Pop (Mengambil Elemen Teratas)**

```python
element = stack.pop()
```

Karena stack menggunakan konsep LIFO, `pop()` secara otomatis mengambil elemen terakhir yang dimasukkan. Dalam kasus ini, C yang keluar.

---

### **4. Peek (Melihat Elemen Teratas Tanpa Menghapus)**

```python
topElement = stack[-1]
```

Kode ini hanya menampilkan elemen paling atas saat ini. Karena C sudah di-pop, elemen teratas menjadi B.

---

### **5. Mengecek Apakah Stack Kosong**

```python
isEmpty = not bool(stack)
```

Nilai stack akan dianggap kosong jika list tidak berisi apa pun. Dengan `not bool(stack)`, kita dapat mengetahui apakah masih ada elemen yang tersisa.

---

### **6. Mengetahui Jumlah Elemen di Dalam Stack**

```python
print("Size: ", len(stack))
```

`len(stack)` menghitung banyaknya elemen yang masih ada di dalam stack. Setelah satu elemen di-pop, jumlahnya tersisa dua.

---




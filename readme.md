
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



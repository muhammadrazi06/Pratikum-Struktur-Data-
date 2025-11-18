**Stack** adalah struktur data yang bekerja dengan prinsip **LIFO (Last In, First Out)** — artinya **elemen terakhir yang dimasukkan akan menjadi yang pertama dikeluarkan**.

Bayangkan tumpukan piring:

* Piring yang terakhir diletakkan di atas adalah yang pertama kali diambil.
* Piring yang di bawah hanya bisa diambil setelah piring di atasnya diangkat.

---

### 🧩 **Ciri-ciri Stack**

1. Akses data hanya melalui satu ujung (disebut **top**).
2. Dua operasi utama:

   * **Push** → menambahkan data ke atas tumpukan.
   * **Pop** → menghapus data dari atas tumpukan.
3. Operasi tambahan (kadang ada):

   * **Peek / Top** → melihat elemen paling atas tanpa menghapusnya.
   * **isEmpty** → memeriksa apakah stack kosong.
   * **isFull** → memeriksa apakah stack penuh (jika ukurannya tetap).

---

### ⚙️ **Contoh Konseptual**

Misalnya ada stack kosong, lalu dilakukan:

```
Push(A) → Stack: [A]
Push(B) → Stack: [A, B]
Push(C) → Stack: [A, B, C]
Pop()   → Keluarkan C → Stack: [A, B]
```

Urutan keluar: **C, lalu B, lalu A** → sesuai prinsip **LIFO**.

---

### 💻 **Contoh Program (Python)**

```python
stack = []

# Menambah elemen (Push)
stack.append('A')
stack.append('B')
stack.append('C')

# Menghapus elemen (Pop)
print(stack.pop())  # Output: C

# Melihat elemen teratas
print(stack[-1])    # Output: B

# Mengecek apakah stack kosong
print(len(stack) == 0)
```

---

### 📘 **Contoh Penggunaan Stack di Dunia Nyata**

1. **Undo/Redo** pada aplikasi (Word, Photoshop, dll).
2. **Back/Forward** pada browser.
3. **Evaluasi ekspresi matematika** (misalnya infix ke postfix).
4. **Penyimpanan pemanggilan fungsi (Call Stack)** pada program.

---

Kamu mau saya lanjutkan dengan **perbedaan Stack dan Queue**, atau **cara membuat Stack sendiri (tanpa list bawaan Python)?**

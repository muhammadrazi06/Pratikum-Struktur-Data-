# PENJELASAN Linked List 

1. Definisi Node — struktur data dasar

```python
class Node:
    def __init__(self, data=None, pointer=None):
        self.data = data
        self.next = pointer
```

* `class Node:` membuat tipe data baru untuk menyimpan elemen Linked List.
* `def __init__(self, data=None, pointer=None):` konstruktor Node, dieksekusi tiap kali `Node(...)` dipanggil.
* `self.data = data` menyimpan nilai/data yang ingin disimpan dalam node (contoh: "apel", 5, objek lain).
* `self.next = pointer` menyimpan *reference* (penunjuk) ke node berikutnya. Awalnya `None` berarti tidak menunjuk ke node mana pun (node terakhir atau list kosong).
* **Konsekuensi:** Node hanya tahu tentang node setelahnya; tidak ada penunjuk ke node sebelumnya (sifat singly linked).

---

2. Definisi LinkedList dan inisialisasi

```python
class LinkedList:
    def __init__(self):
        self.head = None
```

* `class LinkedList:` kelas untuk mengelola kumpulan `Node`.
* `self.head = None` menandakan posisi awal — belum ada node; `head` adalah entry point/list pointer ke node pertama.
* **State awal:** `head -> None` (kosong).

---

3. `insert_at_first(self, data)` — memasukkan node di depan

```python
def insert_at_first(self, data):
    node = Node(data, self.head)
    self.head = node
```

* `Node(data, self.head)` membuat node baru, `data` disimpan, dan `next` di-set ke `self.head` (node lama).
* `self.head = node` mengalihkan head ke node baru.
* **Efek:** node baru menjadi node pertama; urutan bergeser satu ke belakang.
* **Contoh state:**

  * Sebelum: `head -> A -> B -> None`
  * Setelah `insert_at_first("X")`: `head -> X -> A -> B -> None`
* **Kompleksitas waktu:** O(1) — operasi konstan.

---

4. `insert_at_last(self, data)` — memasukkan node di akhir

```python
def insert_at_last(self, data):
    if self.head is None:
        self.head = Node(data)
    else:
        node_sekarang = self.head
        while node_sekarang.next:
            node_sekarang = node_sekarang.next

        node = Node(data)
        node_sekarang.next = node
```

* `if self.head is None:` — jika list kosong, node baru langsung menjadi `head`.
* Jika tidak kosong:

  * `node_sekarang = self.head` mulai dari head.
  * `while node_sekarang.next:` melangkah dari node ke node sampai menemukan node yang `next`-nya `None` (node terakhir).
  * `node = Node(data)` membuat node baru.
  * `node_sekarang.next = node` menghubungkan node terakhir lama ke node baru.
* **Efek:** data ditambahkan di posisi akhir.
* **Contoh state:**

  * Sebelum: `head -> A -> B -> None`
  * Setelah `insert_at_last("Z")`: `head -> A -> B -> Z -> None`
* **Kompleksitas waktu:** O(n) karena perlu traversal sampai akhir (n = panjang list).
* **Catatan:** Jika sering menambahkan di akhir, mempertimbangkan menyimpan `tail` (pointer ke akhir) agar O(1).

---

5. `insert_at(self, index, data)` — sisip di posisi tertentu

```python
def insert_at(self, index, data):
    if index < 0 or index > self.length() - 1:
        print("index tidak valid")
    elif index == 0:
        self.insert_at_first(data)
    else:
        urutan = 0
        node_sekarang = self.head

        while urutan < index - 1:
            urutan += 1
            node_sekarang = node_sekarang.next

        node = Node(data, node_sekarang.next)
        node_sekarang.next = node
```

Validasi index:

  * `if index < 0 or index > self.length() - 1:` memblok index yang negatif atau lebih besar dari `length()-1`.
  * **Catatan penting / potensi masalah:** kondisi ini **mencegah** menyisip tepat setelah elemen terakhir (yaitu index == length()). Jadi kamu **tidak bisa** menggunakan `insert_at(length(), data)` untuk menambahkan di akhir — harus pakai `insert_at_last`. Ini mungkin bukan behavior yang diharapkan secara umum.
* `elif index == 0:` menyederhanakan kasus sisip di depan dengan memanggil `insert_at_first`.
* Untuk index > 0:

  * `urutan = 0` sebagai penghitung posisi.
  * `node_sekarang = self.head` mulai dari head.
  * `while urutan < index - 1:` melangkah sampai node sebelum posisi sisip.
  * `node = Node(data, node_sekarang.next)` buat node baru yang `next`-nya menunjuk ke node yang sebelumnya berada di posisi `index`.
  * `node_sekarang.next = node` ubah pointer agar node baru terpasang di antara `node_sekarang` dan `node_sekarang.next`.
* **Konsep visual:**

  * Sebelum: `... -> P (index-1) -> Q (index) -> ...`
  * Setelah sisip: `... -> P -> NEW -> Q -> ...`
* **Kompleksitas waktu:** O(n) karena traversing sampai posisi index.
* **Corner case:** Jika `index` lebih besar dari `length()-1`, dicetak "index tidak valid". Jika ingin mengizinkan sisip di akhir, ubah validasi menjadi `index > self.length()`.

---

6. `remove_first(self)` — hapus node pertama

```python
def remove_first(self):
    if self.head is None:
        print("tidak ada data yang bisa dihapus")
    else:
        self.head = self.head.next
```

* `if self.head is None:` — jika kosong, tampilkan pesan karena tidak ada yang dihapus.
* `self.head = self.head.next` — head digeser ke node berikutnya; node pertama yang lama kehilangan referensi sehingga Python akan menggarbagenya jika tidak ada referensi lain.
* **Efek:** node pertama dihapus.
* **Contoh:** `head -> A -> B -> C` -> setelah remove_first -> `head -> B -> C`.
* **Kompleksitas waktu:** O(1).

---

7. `remove_last(self)` — hapus node terakhir

```python
def remove_last(self):
    if self.head is None:
        print("tidak ada data yang bisa dihapus")
    elif self.head.next is None:
        self.head = None
    else:
        node_sebelumnya = None
        node_sekarang = self.head

        while node_sekarang.next:
            node_sebelumnya = node_sekarang
            node_sekarang = node_sekarang.next

        node_sebelumnya.next = None
```

* `if self.head is None:` — list kosong → tidak ada yang dihapus.
* `elif self.head.next is None:` — hanya ada satu node → hapus dengan `self.head = None`.
* Untuk lebih dari satu node:

  * `node_sebelumnya = None`, `node_sekarang = self.head`.
  * Loop `while node_sekarang.next:` bergerak sampai node terakhir (`node_sekarang.next` menjadi `None`).
  * Selama loop, `node_sebelumnya` selalu diisi node sebelum `node_sekarang`.
  * Setelah loop, `node_sebelumnya.next = None` memutus link ke node terakhir → node terakhir terhapus.
* **Contoh:**

  * `A -> B -> C -> None` → setelah remove_last → `A -> B -> None`
* **Kompleksitas waktu:** O(n) karena traversing dari head ke node terakhir.
* **Catatan:** Jika sering menghapus di akhir, menyimpan `tail` bisa mempercepat jika diseimbangkan dengan pemeliharaan `tail`.

---

8. `remove_at(self, index)` — hapus node pada posisi tertentu

```python
def remove_at(self, index):
    if index < 0 or index > self.length():
        print("index invalid")
    elif index == 0:
        self.remove_first()
    else:
        urutan = 0
        node_sekarang = self.head

        while urutan < index - 1:
            node_sekarang = node_sekarang.next
            urutan += 1

        node_sekarang.next = node_sekarang.next.next
```

* **Validasi index:**

  * `if index < 0 or index > self.length():` — ini menolak index lebih besar dari `length()`. Biasanya valid index penghapusan adalah `0 <= index < length()`. Kondisi `index > self.length()` akan mengizinkan `index == length()`? Tidak — karena `>` bukan `>=`. Namun sebaiknya gunakan `index >= self.length()` untuk menolak index di luar range. Sekarang:

    * Jika `index == length()`, misalnya length=3 dan index=3, `index > self.length()` false (3>3 false), jadi tidak terpanggil → kode akan lanjut dan kemungkinan error saat mengakses `node_sekarang.next` karena `node_sekarang` akan menjadi `None` pada iterasi — sehingga kemungkinan `AttributeError`. Jadi ini adalah **potensi bug**.
* `elif index == 0:` — panggil `remove_first`.
* Untuk index > 0:

  * Traversal sampai node sebelum posisi penghapusan.
  * `node_sekarang.next = node_sekarang.next.next` memutus node pada posisi `index` dan menghubungkan node sebelumnya ke node setelahnya.
* **Contoh:**

  * `A -> B -> C -> D` ; `remove_at(2)` → hapus `C` → `A -> B -> D`
* **Kompleksitas waktu:** O(n).
* **Penting:** perlu perbaikan validasi (gunakan `if index < 0 or index >= self.length():`).

---

9. `print(self)` — menampilkan semua data

```python
def print(self):
    if self.head is None:
        print("data kosong")
    else:
        text_print = ""
        node_sekarang = self.head

        while node_sekarang:
            text_print += str(node_sekarang.data) + " -> "
            node_sekarang = node_sekarang.next

        print(text_print)
```

* Jika `head` kosong → cetak "data kosong".
* Jika tidak:

  * Inisialisasi `text_print` kosong.
  * Iterasi dari `head` ke setiap node menggunakan `while node_sekarang:`.
  * Tambahkan string `"<data> -> "` untuk setiap node.
  * Setelah loop, cetak `text_print` yang berisi urutan node.
* **Catatan:** akhiran string akan berakhir dengan `" -> "`; untuk output rapih bisa modifikasi agar menghapus trailing arrow.

---

10. `length(self)` — hitung jumlah node

```python
def length(self):
    urutan = 0
    data_sekarang = self.head

    while data_sekarang:
        data_sekarang = data_sekarang.next
        urutan += 1

    return urutan
```

* `urutan` adalah counter.
* Loop berjalan dari head ke akhir, menambah `urutan` tiap kali melewati node.
* Kembalikan jumlah node yang ditemukan.
* **Kompleksitas waktu:** O(n) setiap kali dipanggil. Banyak pemanggilan `length()` di method lain (mis. insert_at/penghapusan) berarti overhead tambahan — bisa dioptimalkan dengan menyimpan atribut `size` yang diupdate saat insert/remove sehingga `length()` O(1).

---

11. Contoh Penggunaan — langkah demi langkah (state tracking)

Kode:

```python
LL = LinkedList()

# insert
LL.insert_at_first("jeruk")
LL.insert_at_first("mangga")
LL.insert_at_first("manggis")
LL.insert_at_last("apel")
LL.insert_at(2, "anggur")

# remove
LL.remove_first()
LL.remove_last()
LL.remove_at(1)
LL.remove_at(1)

# print
LL.print()
print(LL.length())
```

Mari ikuti perubahan state satu-per-satu:

1. `LL = LinkedList()` → state: `head -> None`
2. `insert_at_first("jeruk")` → `head -> jeruk`
3. `insert_at_first("mangga")` → `head -> mangga -> jeruk`
4. `insert_at_first("manggis")` → `head -> manggis -> mangga -> jeruk`
5. `insert_at_last("apel")` → traverse ke akhir; result: `head -> manggis -> mangga -> jeruk -> apel`
6. `insert_at(2, "anggur")` → sisip pada index 2 (0-based):

   * index 0: manggis
   * index 1: mangga
   * index 2: (sisip) → setelah sisip: `head -> manggis -> mangga -> anggur -> jeruk -> apel`
7. `remove_first()` → hapus `manggis` → `head -> mangga -> anggur -> jeruk -> apel`
8. `remove_last()` → hapus `apel` → `head -> mangga -> anggur -> jeruk`
9. `remove_at(1)` → hapus node di index 1 (`anggur`) → `head -> mangga -> jeruk`
10. `remove_at(1)` → hapus node di index 1 (`jeruk`) → `head -> mangga`
11. `LL.print()` → cetak: `mangga -> ` (format saat ini menambahkan `->` setelah tiap node)
12. `print(LL.length())` → `1`

Jadi output akhir: `mangga -> ` dan `1`.



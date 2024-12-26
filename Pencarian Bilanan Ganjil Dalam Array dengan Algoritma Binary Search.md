<h2 align="center"><strong>PENCARIAN BILANGAN GANJIL DALAM ARRAY DENGAN ALGORITMA BINARY SEARCH</strong></h2>
</p>

<br>

<p align="center">
  <strong>Disusun Oleh:</strong><br>
  Liya Khoirunnisa / 2311102124<br>
  Fatik Nurimamah / 2311102190<br>
  S1 IF 11 05


### Source Code :
```python
# @title
import time
import matplotlib.pyplot as plt
from prettytable import PrettyTable

# Fungsi untuk melakukan Binary Search secara iteratif
def pencarianBinerIteratif(arr, target):
    rendah, tinggi = 0, len(arr) - 1
    while rendah <= tinggi:
        tengah = (rendah + tinggi) // 2  # Menentukan indeks tengah
        if arr[tengah] == target:  # Jika target ditemukan di indeks tengah
            return tengah
        elif arr[tengah] < target:  # Jika target lebih besar dari nilai tengah
            rendah = tengah + 1
        else:  # Jika target lebih kecil dari nilai tengah
            tinggi = tengah - 1
    return -1  # Jika target tidak ditemukan

# Fungsi untuk melakukan Binary Search secara rekursif
def pencarianBinerRekursif(arr, target, rendah, tinggi):
    if rendah > tinggi:  # Jika tidak ada lagi elemen yang perlu dicari
        return -1
    tengah = (rendah + tinggi) // 2  # Menentukan indeks tengah
    if arr[tengah] == target:  # Jika target ditemukan di indeks tengah
        return tengah
    elif arr[tengah] < target:  # Jika target lebih besar dari nilai tengah
        return pencarianBinerRekursif(arr, target, tengah + 1, tinggi)
    else:  # Jika target lebih kecil dari nilai tengah
        return pencarianBinerRekursif(arr, target, rendah, tengah - 1)

# Fungsi untuk mencari bilangan ganjil dalam array
def cariBilanganGanjil(arr):
    return [x for x in arr if x % 2 != 0]

# List untuk menyimpan data ukuran array dan waktu eksekusi
ukuranArray = []  # Menyimpan ukuran array yang diuji
waktuIteratif = []  # Menyimpan waktu eksekusi untuk metode iteratif
waktuRekursif = []  # Menyimpan waktu eksekusi untuk metode rekursif

# Fungsi untuk mencetak tabel perbandingan waktu eksekusi
def cetakTabelEksekusi():
    tabel = PrettyTable()
    tabel.field_names = ["Ukuran Array", "Waktu Iteratif (s)", "Waktu Rekursif (s)"]
    for i in range(len(ukuranArray)):
        tabel.add_row([ukuranArray[i], waktuIteratif[i], waktuRekursif[i]])
    print(tabel)

# Fungsi untuk memperbarui grafik perbandingan waktu eksekusi
def perbaruiGrafik():
    plt.figure(figsize=(8, 6))
    plt.plot(ukuranArray, waktuIteratif, label='Iteratif', marker='o', linestyle='-')
    plt.plot(ukuranArray, waktuRekursif, label='Rekursif', marker='x', linestyle='-')
    plt.title('Perbandingan Waktu Eksekusi Binary Search (Iteratif vs Rekursif)')
    plt.xlabel('Ukuran Array')
    plt.ylabel('Waktu Eksekusi (detik)')
    plt.legend()
    plt.grid(True)
    plt.show(block=False)
    plt.pause(0.1)

# Input data secara manual
while True:
    try:
        ukuranInput = input("Masukkan ukuran array (ketik 'selesai' untuk keluar): ")

        if ukuranInput.lower() == "selesai":
            break  # Keluar dari loop jika pengguna mengetik 'selesai'

        ukuran = int(ukuranInput)  # Mengkonversi input menjadi ukuran array
        arr = list(range(1, ukuran + 1))  # Membuat array dengan elemen dari 1 hingga 'ukuran'
        bilanganGanjil = cariBilanganGanjil(arr)  # Mencari bilangan ganjil dalam array

        waktuIteratifTotal = 0  # Inisialisasi variabel untuk menghitung total waktu eksekusi iteratif
        waktuRekursifTotal = 0  # Inisialisasi variabel untuk menghitung total waktu eksekusi rekursif

        # Mengukur waktu untuk mencari setiap bilangan ganjil
        for target in bilanganGanjil:
            # Menghitung waktu eksekusi untuk metode iteratif
            mulaiIteratif = time.time()
            pencarianBinerIteratif(bilanganGanjil, target)
            selesaiIteratif = time.time()
            waktuIteratifTotal += selesaiIteratif - mulaiIteratif

            # Menghitung waktu eksekusi untuk metode rekursif
            mulaiRekursif = time.time()
            pencarianBinerRekursif(bilanganGanjil, target, 0, len(bilanganGanjil) - 1)
            selesaiRekursif = time.time()
            waktuRekursifTotal += selesaiRekursif - mulaiRekursif

        # Hitung rata-rata waktu per pencarian
        waktuIteratif.append(waktuIteratifTotal / len(bilanganGanjil))
        waktuRekursif.append(waktuRekursifTotal / len(bilanganGanjil))

        # Tambahkan ukuran array ke daftar ukuranArray
        ukuranArray.append(ukuran)

        # Cetak tabel dan perbarui grafik
        cetakTabelEksekusi()
        perbaruiGrafik()

    except ValueError:
        print("Masukkan angka yang valid!")  # Menangani input yang tidak valid

```


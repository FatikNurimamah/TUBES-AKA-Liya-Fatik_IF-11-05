<h2 align="center"><strong>PENCARIAN BILANGAN GANJIL DALAM ARRAY DENGAN ALGORITMA BINARY SEARCH</strong></h2>
</p>

<br>

<p align="center">
  <strong>LIFAT TEAM:</strong><br>
  Liya Khoirunnisa (2311102124)<br>
  Fatik Nurimamah (2311102190)<br>
  S1 IF 11 05


### Source Code :
```python
import time
import matplotlib.pyplot as plt
from prettytable import PrettyTable  # Mengimpor PrettyTable

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

# Fungsi untuk memperbarui grafik
def perbaruiGrafik(targets, waktuIteratif, waktuRekursif):
    plt.figure(figsize=(8, 6))
    plt.plot(targets, waktuIteratif, label='Iteratif', marker='o', linestyle='-')
    plt.plot(targets, waktuRekursif, label='Rekursif', marker='x', linestyle='-')
    plt.title('Perbandingan Waktu Eksekusi Binary Search (Iteratif vs Rekursif)')
    plt.xlabel('Inputan (Angka)')
    plt.ylabel('Waktu Eksekusi (detik)')
    plt.legend()
    plt.grid(True)
    plt.show(block=False)
    plt.pause(0.1)

# Fungsi untuk mencetak tabel eksekusi
def cetakTabelEksekusi(targets, waktuIteratif, waktuRekursif):
    tabel = PrettyTable()
    tabel.field_names = ["Inputan (Angka)", "Waktu Iteratif (s)", "Waktu Rekursif (s)"]
    for i in range(len(targets)):
        tabel.add_row([targets[i], waktuIteratif[i], waktuRekursif[i]])
    print(tabel)


    
targets = []  # Menyimpan target yang dicari
waktuIteratif = []  # Menyimpan waktu eksekusi iteratif
waktuRekursif = []  # Menyimpan waktu eksekusi rekursif
    
try:
    # Input ukuran array
    ukuran = int(input("Masukkan ukuran array: "))  
    arr = list(map(int, input(f"Masukkan {ukuran} angka dipisahkan dengan spasi: ").split()))
    
    if len(arr) != ukuran:
        print("Jumlah angka yang dimasukkan tidak sesuai dengan ukuran array!")
    else:
        bilanganGanjil = cariBilanganGanjil(arr)  # Mencari bilangan ganjil dalam array

        if not bilanganGanjil:
            print("Tidak ada bilangan ganjil dalam array.")
        else:
            print("Bilangan ganjil dalam array:", bilanganGanjil)

            # Melakukan pencarian angka berkali-kali
            while True:
                # Input angka yang akan dicari
                target = int(input("Masukkan angka ganjil yang ingin dicari (atau -1 untuk berhenti): "))
                if target == -1:  # Jika -1 dimasukkan, berhenti
                    break

                if target not in bilanganGanjil:
                    print(f"Angka {target} tidak ditemukan dalam daftar bilangan ganjil.")
                    continue

                # Menambahkan target yang dicari untuk grafik
                targets.append(target)

                # Ukur waktu untuk pencarian biner iteratif
                start = time.time()
                indeks_iteratif = pencarianBinerIteratif(bilanganGanjil, target)
                end = time.time()
                waktu_iteratif = end - start

                # Ukur waktu untuk pencarian biner rekursif
                start = time.time()
                indeks_rekursif = pencarianBinerRekursif(bilanganGanjil, target, 0, len(bilanganGanjil) - 1)
                end = time.time()
                waktu_rekursif = end - start

                if indeks_iteratif != -1:
                    print(f"Angka {target} ditemukan pada indeks {indeks_iteratif} di array bilangan ganjil (iteratif).")
                else:
                    print(f"Angka {target} tidak ditemukan di array bilangan ganjil (iteratif).")

                if indeks_rekursif != -1:
                    print(f"Angka {target} ditemukan pada indeks {indeks_rekursif} di array bilangan ganjil (rekursif).")
                else:
                    print(f"Angka {target} tidak ditemukan di array bilangan ganjil (rekursif).")

                # Menambahkan waktu eksekusi untuk grafik
                waktuIteratif.append(waktu_iteratif)  # Menyimpan waktu eksekusi iteratif
                waktuRekursif.append(waktu_rekursif)  # Menyimpan waktu eksekusi rekursif

                # Memperbarui grafik setelah eksekusi
                perbaruiGrafik(targets, waktuIteratif, waktuRekursif)

                # Menampilkan tabel eksekusi
                cetakTabelEksekusi(targets, waktuIteratif, waktuRekursif)

except ValueError:
    print("Masukkan angka yang valid!")

```


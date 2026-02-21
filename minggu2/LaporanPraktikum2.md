# Laporan Praktikum Sistem Operasi 2

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 2.1 - Identifikasi CPU dan Memori

Kode 1.1 : Melihat informasi CPU

![minggu1/image/kode1.1.png](image/kode1.1.png)

Kode 1.2 : Melihat penggunaan memori

![minggu1/image/kode1.2.png](image/kode1.2.png)

Kode 1.3 : Informasi DMI

![minggu1/image/kode1.3.png](image/kode1.3.png)

#### Latihan 2.1

Catat: (1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

>Jawaban :
>1. Jumlah CPU(s) : 3  
>2. Jumlah Core(s) per socket : 3  
>3. Jumlah Thread(s) per core : 1  
>4. Total RAM : 3.3Gi  
>5. Total Swap : 0B  

>Perbedaan RAM vs swap adalah RAM adalah memori fisik cepat yang digunakan untuk menyimpan data dan program yang sedang aktif. Swap adalah ruang di harddisk yang digunakan sebagai "RAM cadangan" ketika RAM fisik penuh. Swap lebih lambat dari RAM, sehingga penggunaan swap berlebihan dapat memperlambat sistem.


## Praktikum 2.2 - Identifikasi Perangkat PCI/USB dan Driver

Kode 1.4 : Daftar perangkat PCI (ringkas)

![minggu1/image/kode1.4.png](image/kode1.4.png)

Kode 1.5: Melihat driver perangkat PCI

![minggu1/image/kode1.5.png](image/kode1.5.png)

Kode 1.6: Mencari info NIC dan drivernya

![minggu1/image/kode1.6.png](image/kode1.6.png)

Kode 1.7: Daftar perangkat USB

![alt text](image/kode1.7.png)

Kode 1.8: Topologi perangkat USB

![minggu1/image/kode1.8.png](image/kode1.8.png)

#### Latihan 2.2

Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka
heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya. 

>Jawaban :  
>1. Perangkat --> Ethernet Controller [0200] (NIC)  
>2. Vendor:Device ID -->  8086:001e  
>3. Nama driver/modul -->	e1000  
>4. Deskripsi fungsi --> Mengatur komunikasi jaringan (network interface card) agar komputer dapat terhubung ke jaringan lokal/internet



## Praktikum 2.3 — Identifikasi Storage dan Filesystem

Kode 1.9: Melihat block device dan filesystem

![minggu1/image/kode1.9.png](image/kode1.9.png)

Kode 1.10: Melihat UUID filesystem

![minggu1/image/kode1.10.png](image/kode1.10.png)

Kode 1.11: Melihat device untuk root filesystem

![minggu1/image/kode1.11.png](image/kode1.11.png)


## Praktikum 2.4 — Melihat Modul Aktif dan Informasinya

Kode 1.13: Cek versi kernel

![alt text](image/kode1.13.png)

Kode 1.14: Daftar modul aktif

![alt text](image/kode1.14.png)

Kode 1.15: Detail modul dengan modinfo

![alt text](image/kode1.15.png)

Kode 1.16: Load modul dan verifikasi

![alt text](image/kode1.16.png)

Kode 1.17: Cek log kernel terbaru

![alt text](image/kode1.17.png)


## Praktikum 2.5 — Konfigurasi Auto-load dan Blacklist

Kode 1.18: Menambahkan modul untuk auto-load (demo)

![alt text](image/kode1.18.png)

Kode 1.19: Verifikasi modul aktif

![alt text](image/kode1.19.png)

Kode 1.20: Contoh blacklist modul (jangan diterapkan sembarangan)

![alt text](image/kode1.20.png)


## Praktikum 2.6 — Mengenali Block vs Character Device

Kode 1.21: Melihat detail device node disk

![alt text](image/kode1.21.png)

Kode 1.22: Melihat detail device node terminal

![alt text](image/kode1.22.png)

Kode 1.23: Mapping disk/partisi

![alt text](image/kode1.23.png)

#### Latihan 2.3

Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan
character device. (Hint: karakter pertama pada permission string)

>Jawaban :  
Dari output ls -l, perbedaannya terletak pada karakter pertama dari string permission  
>1. Block device → karakter pertama b  
Contoh: /dev/sda  
Fungsi: akses data per blok (hardisk, SSD)  
>2. Character device → karakter pertama c  
Contoh: /dev/tty  
Fungsi: akses data per karakter (terminal, keyboard)


## Praktikum 2.7 — Melihat Informasi udev

Kode 1.24: Melihat atribut udev untuk disk

![alt text](image/kode1.24.png)

Kode 1.25: Monitor event udev (opsional)

![alt text](image/kode1.25.png)


## Praktikum 2.8 — Membuat Workspace Praktikum

Kode 1.26: Membuat workspace praktikum

![alt text](image/kode1.26.png)

Kode 1.27: Membuat file contoh

![alt text](image/kode1.27.png)

Kode 1.28: Mengisi file log contoh

![alt text](image/kode1.28.png)

Kode 1.29: Membaca file dengan less

![alt text](image/kode1.29.png)


## Praktikum 2.9 — Pencarian Pola dengan grep

Kode 1.30: grep sederhana

![alt text](image/kode1.30.png)

Kode 1.31: grep case-insensitive

![alt text](image/kode1.31.png)

Kode 1.32: grep dengan nomor baris

![alt text](image/kode1.32.png)

Kode 1.33: grep invert match

![alt text](image/kode1.33.png)

### Latihan 2.4

Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)

>Jawaban : 
![alt text](image/kode1.33(latihan2.4).png)


## Praktikum 2.10 — Substitusi dengan sed (Aman di File Latihan)

Kode 1.34: Membuat file config latihan

![alt text](image/kode1.34.png)

Kode 1.35: sed substitusi tanpa in-place

![alt text](image/kode1.35.png)

Kode 1.36: sed in-place

![alt text](image/kode1.36.png)

Kode 1.37: sed global replacement

![alt text](image/kode1.37.png)


## Praktikum 2.11 — Ekstraksi Kolom dengan awk

Kode 1.38: Output df -h

![alt text](image/kode1.38.png)

Kode 1.39: awk print kolom tertentu

![alt text](image/kode1.39.png)

Kode 1.40: awk filter berdasarkan kondisi

![alt text](image/kode1.40.png)


## Praktikum 2.12 — Melihat Proses dengan ps

Kode 1.41: ps aux

![alt text](image/kode1.41.png)

Kode 1.42: Filter proses dengan grep

![alt text](image/kode1.42.png)


## Praktikum 2.13 — Monitoring Real-time dengan top

Kode 1.43: Menjalankan top

![alt text](image/kode1.43.png)


## Praktikum 2.14 — Menghentikan Proses dengan kill

Kode 1.44: Membuat proses dummy

![alt text](image/kode1.44.png)

Kode 1.45: Mencari PID sleep

![alt text](image/kode1.45.png)

Kode 1.46: Mengirim SIGTERM

![alt text](image/kode1.46.png)

Kode 1.47: Verifikasi proses sudah berhenti

![alt text](image/kode1.47.png)

Kode 1.48: Mengirim SIGKILL (opsional)

![alt text](image/kode1.48.png)


## Praktikum 2.15 — Cek Disk, Load, dan Service

Kode 1.49: Cek kapasitas disk

![alt text](image/kode1.49.png)

Kode 1.50: Cek ukuran direktori (contoh /var)

![alt text](image/kode1.50.png)

Kode 1.51: Cek load average

![alt text](image/kode1.51.png)

Kode 1.52: Service yang gagal

![alt text](image/kode1.52.png)

Kode 1.53: Log error terbaru

![alt text](image/kode1.53.png)


## Praktikum 2.16 — Monitoring Port dan Koneksi (Network Basics)

Kode 1.54: Cek IP address

![alt text](image/kode1.54.png)

Kode 1.55: Cek routing

![alt text](image/kode1.55.png)

Kode 1.56: Cek port listening

![alt text](image/kode1.56.png)

### Latihan 2.5

Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut secara singkat.

>Jawaban :  
Port 53  
service/proses yang membukanya : DNS (Domain Name System)  
Kegunaaan port : Menerjemahkan nama domain (seperti google.com) menjadi IP address (seperti 142.250.185.46) agar komputer bisa saling terhubung.

# Latihan

## Latihan 2.A
Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat, ID vendor:device, dan kernel driver in use.
>Jawaban :  
Nama Perangkat : Intel Corporation 82540EM Gigabit Ethernet Controller  
ID vendor:device : 8086:001e  
Kernel driver in use : e1000

## Latihan 2.B
Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan lsblk -f dan tuliskan tipe filesystem serta UUID-nya.
>Jawaban :  
Root device : /dev/sda2  
Tipe filesystem	: ext4  
UUID : 115fe37b-f6f4-4307-8131-1b03b5b65ed4

## Latihan 2.C
Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO, WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.
>Jawaban :  
![alt text](image/kodelatihan2c.png)

## Latihan 2.D
Gunakan sed untuk mengganti semua kata server menjadi node pada file latihan. Tunjukkan sebelum dan sesudah.
>Jawaban :  
![alt text](image/kodelatihan2d.png)

## Latihan 2.E
Gunakan df -h lalu awk untuk menampilkan filesystem yang penggunaan disk di atas 70%.
>Jawaban :   
![alt text](image/kodelatihan2e.png) 


## Latihan 2.F
Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan SIGTERM. Jelaskan beda SIGTERM vs SIGKILL.
>Jawaban :  
![alt text](image/kodelatihan2f.png)  
SIGTERM : Menghentikan secara halus. Proses bisa melakukan cleanup (menutup file, menyimpan data) sebelum berhenti
>
>SIGKILL : Menghentikan secara paksa. Proses langsung dihentikan oleh kernel, tanpa kesempatan cleanup.

## Latihan 2.G
Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.
>Jawaban :  
ssh  
![alt text](image/kodelatihan2g(ssh).png)
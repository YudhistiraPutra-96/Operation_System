# Laporan Praktikum 10

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## PRAKTIKUM

## Praktikum 10.1

### Langkah 1
Input
```bash
free -h
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# free -h
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       378Mi       2.8Gi       1.1Mi       355Mi       3.0Gi
Swap:          511Mi          0B       511Mi
```

### Langkah 2
Input
```bash
cat /proc/meminfo | head -n 20
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# cat /proc/meminfo | head -n 20
MemTotal:        3504528 kB
MemFree:         2909672 kB
MemAvailable:    3116948 kB
Buffers:           21472 kB
Cached:           323112 kB
SwapCached:            0 kB
Active:           310416 kB
Inactive:          82940 kB
Active(anon):      58608 kB
Inactive(anon):        0 kB
Active(file):     251808 kB
Inactive(file):    82940 kB
Unevictable:       27316 kB
Mlocked:           27316 kB
SwapTotal:        524284 kB
SwapFree:         524284 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 0 kB
Writeback:             0 kB
```

### Analisis
1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya di bawah 10%, sistem mulai kekurangan memori.
2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah pernah memindahkan data ke disk karena RAM tidak cukup.
3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai
dengan kolom buff/cache pada free -h.

Jawaban :  
1. (3116948/3504528) * 100% = 88,9405934265612944 % 
2. Ya, berarti kernel belum pernah memindahkan data ke swap karena RAM masih cukup.  
3. Buffers: 21472 kB, Cached: 323112 kB, Ini sudah sesuai dengan dengan kolom buff/cache pada free -h.


## Praktikum 10.2

### Langkah 1
Input
```bash
vmstat 1 5
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 2  0      0 2910952  21512 342800    0    0   105    16 1114    0  0  7 93  0  0  0
 0  0      0 2910952  21512 342800    0    0     0     0 1244  212  0 11 89  0  0  0
 0  0      0 2910952  21512 342800    0    0     0     0 1278  208  0 11 89  0  0  0
 0  0      0 2910952  21512 342800    0    0     0     0 1211  159  0  9 91  0  0  0
 0  0      0 2910952  21512 342800    0    0     0     0 1193  102  0  7 93  0  0  0
```

### Analisis
1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM cukup, kedua nilai ini selalu 0.
2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas swap. Ini masih wajar jika tidak terus-menerus.
3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory pressure serius — performa turun drastis karena akses disk jauh lebih lambat dari RAM.
4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami kondisi keseluruhan RAM saat itu.

Jawaban :   
1. Nilai keduanya sama-sama 0 
2. Nilai keduanya sama-sama tidak lebih dari 0 
3. Nilai keduanya sama-sama tidak lebih dari 0 
4. free -> sekitar 2.91 GB memori kosong, cache -> sekitar 3.42 GB digunakan sebagai cache file, Ini menunjukkan RAM masih sangat longgar. 

## Praktikum 10.3

### Langkah 1
Input
```bash
sudo fallocate -l 512M /swapfile-week10
ls -lh /swapfile-week10
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# sudo fallocate -l 512M /swapfile-week10
root@ubuntuser:~/praktikum-os/week10-memory# ls -lh /swapfile-week10
-rw-r--r-- 1 root root 512M May  3 05:33 /swapfile-week10
```

### Langkah 2
Input
```bash
sudo chmod 600 /swapfile-week10
ls -lh /swapfile-week10
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# sudo chmod 600 /swapfile-week10
root@ubuntuser:~/praktikum-os/week10-memory# ls -lh /swapfile-week10
-rw------- 1 root root 512M May  3 05:33 /swapfile-week10
```

### Langkah 3
Input
```bash
sudo mkswap /swapfile-week10
sudo swapon /swapfile-week10
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# sudo mkswap /swapfile-week10
Setting up swapspace version 1, size = 512 MiB (536866816 bytes)
no label, UUID=561a9ccd-7b32-45c2-9ba3-ba83a1c3b128
root@ubuntuser:~/praktikum-os/week10-memory# sudo swapon /swapfile-week10
```

### Langkah 4
Input
```bash
swapon --show
free -h
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# swapon --show
NAME             TYPE SIZE USED PRIO
/swapfile-week10 file 512M   0B   -2
root@ubuntuser:~/praktikum-os/week10-memory# free -h
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       365Mi       2.8Gi       1.1Mi       361Mi       3.0Gi
Swap:          511Mi          0B       511Mi
```

### Langkah 5
Input
```bash
cat /proc/sys/vm/swappiness
sudo sysctl vm.swappiness=10
cat /proc/sys/vm/swappiness
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# cat /proc/sys/vm/swappiness
60
root@ubuntuser:~/praktikum-os/week10-memory# sudo sysctl vm.swappiness=10
vm.swappiness = 10
root@ubuntuser:~/praktikum-os/week10-memory# cat /proc/sys/vm/swappiness
10
```

### Analisis
1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam menggunakan swap?
2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
3. Apakah entri /swapfile-week10 muncul di swapon –show? Jika tidak, pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3.

Jawaban :  
1. 60, yang artinya	Kernel cukup agresif menggunakan swap. Mulai memindahkan page tidak aktif ke swap meskipun RAM masih tersedia. Cocok untuk desktop, kurang ideal untuk server yang butuh performa tinggi. 
2. Performa lebih stabil (tanpa paging ke disk), tetapi risiko kehabisan RAM lebih tinggi jika beban meningkat drastis. 
3. Ya muncul  

## Praktikum 10.4

### Langkah 1
Input
```bash
ps aux --sort=-%mem | head
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# ps aux --sort=-%mem | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1094  0.2  1.2 617808 44080 ?        Ssl  04:40   0:09 /usr/libexec/fwupd/fwupd
root         378  0.1  0.7 288988 27324 ?        SLsl 04:39   0:07 /sbin/multipathd -d -s
root         701  0.0  0.6 109688 23132 ?        Ssl  04:39   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         325  0.0  0.5  66840 17888 ?        S<s  04:39   0:00 /usr/lib/systemd/systemd-journald
root         638  0.0  0.3 468972 13544 ?        Ssl  04:39   0:00 /usr/libexec/udisks2/udisksd
root           1  0.0  0.3  22044 13280 ?        Ss   04:39   0:02 /sbin/init splash noprompt noshell automatic-ubiquity
root         703  0.0  0.3 392100 13072 ?        Ssl  04:39   0:00 /usr/sbin/ModemManager
systemd+     458  0.0  0.3  21588 12996 ?        Ss   04:39   0:00 /usr/lib/systemd/systemd-resolved
root        1380  0.0  0.3  20292 11492 ?        Ss   05:20   0:00 /usr/lib/systemd/systemd --user
```

### Langkah 2
Input
```bash
top
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# top
top - 06:04:58 up  1:25,  2 users,  load average: 0.00, 0.00, 0.00
Tasks: 139 total,   1 running, 138 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.2 us,  1.7 sy,  0.0 ni, 91.3 id,  0.0 wa,  0.0 hi,  6.9 si,  0.0
MiB Mem : 10.8/3422.4   [|||||                                             ]
MiB Swap:  0.0/512.0    [                                                  ]

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+
   1365 yudhis    20   0   13764   7512   6008 S   5.6   0.2   0:07.30
     30 root      20   0       0      0      0 S   2.0   0.0   0:15.56
   1507 root      20   0       0      0      0 I   1.5   0.0   0:03.80
    766 root      20   0  293152   3764   3284 S   0.5   0.1   0:05.57
   1304 root      20   0       0      0      0 I   0.5   0.0   0:00.42
   1582 root      20   0   11940   6008   3780 R   0.5   0.2   0:00.03
      1 root      20   0   22044  13292   9532 S   0.0   0.4   0:02.30
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.09
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     11 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.10
     17 root      20   0       0      0      0 I   0.0   0.0   0:01.73
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.46
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     21 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     23 root      rt   0       0      0      0 S   0.0   0.0   0:00.70
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.05
     26 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     27 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     28 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     29 root      rt   0       0      0      0 S   0.0   0.0   0:00.49
     36 root      20   0       0      0      0 S   0.0   0.0   0:00.03
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     38 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     39 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     40 root      20   0       0      0      0 S   0.0   0.0   0:00.00
```

### Analisis
1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses menggunakan 512 MB RAM. Apakah wajar untuk jenis program tersebut?
3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan berdasarkan %MEM?

Jawaban :  
1. 1365 yudhis    20   0   13764   7512   6008 S   5.6   0.2   0:07.30, %MEM = 0.2 dan RSS = 7512  
2. RSS = 7512 berarti proses menggunkan 7 MB RAM 
3. VSZ mencakup library yang di-share, memory-mapped files, dan heap yang dialokasikan tapi belum digunakan, sedangkan RSS hanya menghitung page yang benar-benar ada di RAM 
4. Ya, seharusnya konsisten karena keduanya membaca dari sumber yang sama (/proc). Perbedaan bisa terjadi jika ada jeda waktu antara menjalankan ps dan melihat top atau proses baru lahir atau mati di antara kedua perintah
 

## Praktikum 10.5

### Langkah 1
Input
```bash
nano monitor-memori.sh
#!/bin/bash
set -euo pipefail

THRESHOLD=20

echo "=== Monitor Memori ==="
date
echo

free -h

echo

AVAIL=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')
if [ "$AVAIL" -lt "$THRESHOLD" ]; then
    echo "PERINGATAN: Memori tersedia hanya ${AVAIL}%"
else
    echo "Status: Memori tersedia ${AVAIL}% (normal)"
fi

echo
echo "--- 5 Proses Memori Tertinggi ---"
ps aux --sort=-%mem | head -n 6 | tail -n 5
```

### Langkah 2
Input
```bash
chmod +x monitor-memori.sh
bash monitor-memori.sh
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# chmod +x monitor-memori.sh
root@ubuntuser:~/praktikum-os/week10-memory# bash monitor-memori.sh
=== Monitor Memori ===
Sun May  3 06:22:07 AM UTC 2026

               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       369Mi       2.8Gi       1.1Mi       362Mi       3.0Gi
Swap:          511Mi          0B       511Mi

Status: Memori tersedia 89% (normal)

--- 5 Proses Memori Tertinggi ---
root        1094  0.1  1.2 617808 44080 ?        Ssl  04:40   0:10 /usr/libexec/fwupd/fwupd
root         378  0.1  0.7 288988 27324 ?        SLsl 04:39   0:09 /sbin/multipathd -d -s
root         701  0.0  0.6 109688 23132 ?        Ssl  04:39   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         325  0.0  0.5  66840 17900 ?        S<s  04:39   0:00 /usr/lib/systemd/systemd-journald
root         638  0.0  0.3 468972 13544 ?        Ssl  04:39   0:00 /usr/libexec/udisks2/udisksd
```

### Analisis
1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk ’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagi kolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan persentase bilangan bulat.
2. Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] bernilai benar jika persentase memori tersedia di bawah 20.
3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada output? Mengapa demikian?

Jawaban :  
3. Sebelumnya (THRESHOLD=20): AVAIL=66 ≥ 20 → status "normal", Setelah diubah (THRESHOLD=90): AVAIL=66 < 90 → "PERINGATAN", Karena threshold dinaikkan menjadi 90%, sementara memori tersedia hanya 66% → kondisi dianggap "warning" meskipun secara teknis sistem masih sehat. 


## Praktikum 10.6

### Langkah 1
Input
```bash
strace ls 2>&1 | head -n 30
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# strace ls 2>&1 | head -n 30
execve("/usr/bin/ls", ["ls"], 0x7ffe1220f220 /* 24 vars */) = 0
brk(NULL)                               = 0x5e66b035d000
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7caa10f92000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=32431, ...}) = 0
mmap(NULL, 32431, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7caa10f8a000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=174472, ...}) = 0
mmap(NULL, 181960, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7caa10f5d000
mmap(0x7caa10f63000, 118784, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x7caa10f63000
mmap(0x7caa10f80000, 24576, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x23000) = 0x7caa10f80000
mmap(0x7caa10f86000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x29000) = 0x7caa10f86000
mmap(0x7caa10f88000, 5832, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7caa10f88000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220\243\2\0\0\0\0\0"..., 832) = 832
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
fstat(3, {st_mode=S_IFREG|0755, st_size=2125328, ...}) = 0
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
mmap(NULL, 2170256, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7caa10c00000
mmap(0x7caa10c28000, 1605632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x28000) = 0x7caa10c28000
mmap(0x7caa10db0000, 323584, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b0000) = 0x7caa10db0000
mmap(0x7caa10dff000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1fe000) = 0x7caa10dff000
mmap(0x7caa10e05000, 52624, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7caa10e05000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
```

### Langkah 2
Input
```bash
strace -c ls
strace -c ls /etc 2>&1 | tail -5
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# strace -c ls
monitor-memori.sh
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 25.93    0.005700         633         9           close
 15.49    0.003405         486         7           openat
 13.06    0.002870         159        18           mmap
 10.14    0.002229         278         8           fstat
  9.78    0.002149        2149         1           execve
  7.66    0.001683        1683         1           prlimit64
  6.27    0.001379        1379         1           arch_prctl
  3.20    0.000703         140         5           mprotect
  2.53    0.000557         557         1           munmap
  1.77    0.000389         389         1           getrandom
  1.39    0.000306          61         5           read
  0.84    0.000184          92         2           pread64
  0.71    0.000156          78         2         2 statfs
  0.41    0.000090          90         1           rseq
  0.27    0.000059          19         3           brk
  0.22    0.000049          24         2           getdents64
  0.14    0.000031          31         1           write
  0.09    0.000020          20         1           set_tid_address
  0.05    0.000012           6         2           ioctl
  0.05    0.000010           5         2         2 access
  0.00    0.000000           0         1           set_robust_list
------ ----------- ----------- --------- --------- ----------------
100.00    0.021981         297        74         4 total
root@ubuntuser:~/praktikum-os/week10-memory# strace -c ls /etc 2>&1 | tail -5
  0.05    0.000007           7         1         1 ioctl
  0.02    0.000003           3         1           prlimit64
  0.02    0.000003           3         1           getrandom
------ ----------- ----------- --------- --------- ----------------
100.00    0.013907         187        74         5 total
```

### Analisis
1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan fungsi singkat masing-masing berdasarkan argumen yang terlihat.
2. Dari ringkasan strace -c, system call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti program bermasalah, ataukah bagian normal dari logika program?
4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang menyebabkan perbedaan tersebut?

Jawaban :  
1. openat() =	Membuka file atau direktori, read()	= Membaca data dari file descriptor, write() = Menulis data ke file descriptor (misalnya ke terminal), close() =	Menutup file descriptor
2. 9 = close, 7 = openat, 18 = mmap 
3. Ya, ada access dengan 2 errors dan openat dengan 5 errors. 
>Apakah berarti program bermasalah? TIDAK. Ini adalah bagian normal dari logika program:
>access("/etc/ld.so.nohwcap", F_OK) = -1 ENOENT → hanya mengecek apakah file ada, gagal normal karena file memang tidak ada  
>Program tetap berjalan normal karena error tersebut diantisipasi 
4. Disini jumlah system call nya sama di 74


## STUDI KASUS

## Studi Kasus 10.1

### Langkah 1
Input
```bash
free -h
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# free -h
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       378Mi       2.8Gi       1.1Mi       355Mi       3.0Gi
Swap:          511Mi          0B       511Mi
```

### Langkah 2
Input
```bash
top
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# top
top - 05:24:59 up 45 min,  2 users,  load average: 0.02, 0.04, 0.00
Tasks: 142 total,   1 running, 141 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.2 us,  2.0 sy,  0.0 ni, 89.6 id,  0.2 wa,  0.0 hi,  8.2 si,  0.0
MiB Mem : 11.1/3422.4   [|||||                                             ]
MiB Swap:  0.0/512.0    [                                                  ]

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+
   1365 yudhis    20   0   13764   7512   6008 S   5.4   0.2   0:01.09
     30 root      20   0       0      0      0 S   2.3   0.0   0:08.42
   1348 root      20   0       0      0      0 I   1.8   0.0   0:03.16
   1407 root      20   0   11940   5960   3732 R   0.9   0.2   0:00.04
     29 root      rt   0       0      0      0 S   0.5   0.0   0:00.40
    378 root      rt   0  288988  27324   8760 S   0.5   0.8   0:04.42
      1 root      20   0   22044  13280   9532 S   0.0   0.4   0:01.94
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.07
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     11 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.05
     17 root      20   0       0      0      0 I   0.0   0.0   0:01.03
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.25
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     21 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     23 root      rt   0       0      0      0 S   0.0   0.0   0:00.50
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.03
     25 root      20   0       0      0      0 I   0.0   0.0   0:00.02
     26 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     27 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     28 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     32 root       0 -20       0      0      0 I   0.0   0.0   0:00.19
     36 root      20   0       0      0      0 S   0.0   0.0   0:00.03
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     38 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     39 root      20   0       0      0      0 S   0.0   0.0   0:00.00
```

### Analisis
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang menggunakan swap, yang berarti performa menurun.
3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut menjadi kandidat utama penyebab lambatnya server.

Jawaban :  
1. Tidak. available = 3.0 Gi pada sistem dengan RAM 3.3 Gi berarti memori masih sangat cukup. Jika available di bawah 200 MB pada server dengan RAM 2 GB, itu baru dikategorikan kekurangan memori. 
2. Tidak. used = 0B pada swap berarti kernel tidak menggunakan swap sama sekali. Performa tidak terpengaruh oleh swap.  
3.    378 root      rt   0  288988  27324   8760 S   0.5   0.8   0:04.42

## Studi Kasus 10.2

### Langkah 1
Input
```bash
mkdir -p ~/praktikum-os/week10-memory/syscall-case
cd ~/praktikum-os/week10-memory/syscall-case
echo "PORT=8080" > app.conf
ls -l app.conf
cat app.conf
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory# mkdir -p ~/praktikum-os/week10-memory/syscall-case
root@ubuntuser:~/praktikum-os/week10-memory# cd ~/praktikum-os/week10-memory/syscall-case
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# echo "PORT=8080" > app.conf
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# ls -l app.conf
-rw-r--r-- 1 root root 10 May  4 11:19 app.conf
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# cat app.conf
PORT=8080
```

### Langkah 2
Input
```bash
chmod 000 app.conf
ls -l app.conf
sudo -u nobody cat app.conf
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# chmod 000 app.conf
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# ls -l app.conf
---------- 1 root root 10 May  4 11:19 app.conf
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# sudo -u nobody cat
 app.conf
cat: app.conf: Permission denied
```

### Langkah 3
Input
```bash
chmod 644 app.conf
ls -l app.conf
cat app.conf
```

Output
```bash
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# chmod 644 app.conf
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# ls -l app.conf
-rw-r--r-- 1 root root 10 May  4 11:19 app.conf
root@ubuntuser:~/praktikum-os/week10-memory/syscall-case# cat app.conf
PORT=8080
```

### Analisis
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System call apa yang gagal?
2. Apa perbedaan pesan error Permission denied vs No such file or directory? Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
3. Permission 644 berarti apa untuk owner, group, dan others?

Jawaban :  
1. Setelah chmod 000, file tidak memiliki bit izin baca (r) untuk siapapun. Ketika cat mencoba membuka file, kernel memeriksa izin dan menolak akses.  
2. Permission denied (EACCES): File ada tapi izin baca tidak cukup, sedangkan No such file or directory (ENOENT): File tidak ditemukan  
3. chmod 644 = rw-r--r--
- Owner (root): rw- (baca + tulis) = 6
- Group: r-- (baca saja) = 4
- Others: r-- (baca saja) = 4  

## TUGAS

## Tugas 10.1

### Langkah 1
Input :
```bash
nano memory-audit.sh
```

### Langkah 2
Input :
```bash
#!/bin/bash
set -euo pipefail

LAPORAN="memory-report.txt"

{
    echo "=== LAPORAN MEMORI SISTEM ==="
    date
    echo
    echo "--- Ringkasan free -h ---"
    free -h
    echo
    echo "--- /proc/meminfo ---"
    cat /proc/meminfo | head -n 20
} > "$LAPORAN"

echo "Laporan disimpan ke: $LAPORAN"
cat "$LAPORAN"
```

### Langkah 3
Input :
```bash
chmod +x ~/praktikum-os/week10-memory/memory-audit.sh
cd ~/praktikum-os/week10-memory
bash memory-audit.sh
```

Output : 
```bash
root@ubuntuser:~/praktikum-os/week10-memory# chmod +x ~/praktikum-os/week10-memory/memory-audit.sh
root@ubuntuser:~/praktikum-os/week10-memory# cd ~/praktikum-os/week10-memory
root@ubuntuser:~/praktikum-os/week10-memory# bash memory-audit.sh
Laporan disimpan ke: memory-report.txt
=== LAPORAN MEMORI SISTEM ===
Mon May  4 12:39:37 PM UTC 2026

--- Ringkasan free -h ---
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       412Mi       1.3Gi       1.1Mi       1.9Gi       2.9Gi
Swap:             0B          0B          0B

--- /proc/meminfo ---
MemTotal:        3504528 kB
MemFree:         1340484 kB
MemAvailable:    3082388 kB
Buffers:           12140 kB
Cached:          1757236 kB
SwapCached:            0 kB
Active:           321556 kB
Inactive:        1492368 kB
Active(anon):      54392 kB
Inactive(anon):      132 kB
Active(file):     267164 kB
Inactive(file):  1492236 kB
Unevictable:       27300 kB
Mlocked:           27300 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 8 kB
Writeback:             0 kB
```

### Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?

Jawaban :  
1. (3082388/3504528) * 100% = 87.9544406551 %, kondisinya normal 
2. buff/cache tidak dihitung sebagai memori terpakai karena Linux secara otomatis akan membebaskan cache tersebut ketika ada aplikasi baru yang membutuhkan memori. Ketika aplikasi baru meminta memori, kernel akan melepaskan sebagian cache secara transparan tanpa mengganggu proses yang sedang berjalan.  
3. Tidak lebih dari 0 dan nilai Swapfree juga 0 


## Tugas 10.2

### Langkah 1
Input :
```bash
ps aux --sort=-%mem | head -n 10 > top-memory-process.txt
cat top-memory-process.txt
```

Output : 
```bash
root@ubuntuser:~/praktikum-os/week10-memory# ps aux --sort=-%mem | head -n 10 > top-memory-process.txt
root@ubuntuser:~/praktikum-os/week10-memory# cat top-memory-process.txt
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        2713  0.0  0.7 223568 27308 ?        SLsl 12:25   0:01 /sbin/multipathd -d -s
root         723  0.0  0.6 109688 23148 ?        Ssl  11:45   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root       19267  0.0  0.3 468848 13632 ?        Ssl  12:34   0:00 /usr/libexec/udisks2/udisksd
root           1  0.2  0.3  22060 13392 ?        Ss   11:44   0:10 /usr/lib/systemd/systemd --system --deserialize=60 splash noprompt noshell automatic-ubiquity
systemd+   19272  0.0  0.3  21584 13188 ?        Ss   12:34   0:00 /usr/lib/systemd/systemd-resolved
root        9507  0.0  0.3 392100 12892 ?        Ssl  12:31   0:00 /usr/sbin/ModemManager
root       19266  0.0  0.3  34172 12620 ?        S<s  12:34   0:00 /usr/lib/systemd/systemd-journald
root        1073  0.0  0.3  20280 11504 ?        Ss   11:49   0:00 /usr/lib/systemd/systemd --user
yudhis       985  0.0  0.3  20084 11296 ?        Ss   11:47   0:00 /usr/lib/systemd/systemd --user
```

### Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?

Jawaban :  
1. proses yang berada di urutan pertama adalah multipathd dengan nilai %MEM sebesar 0.7 persen dan RSS sebesar 27308 KB. 
2. 27308/1024 = 26.66796875, untuk kewajaran, multipathd dengan ukuran sekitar 27 MB tergolong wajar karena daemon ini memang perlu memantau dan mengelola jalur-jalur storage.
3. 2.2 persen, ini berarti kelima proses terbesar tersebut secara bersama-sama hanya menggunakan sekitar 2.2 persen dari total RAM. 


## Tugas 10.3

### Langkah 1
Input :
```bash
sudo fallocate -l 256M /swapfile-tugas-week10
ls -lh /swapfile-tugas-week10
sudo chmod 600 /swapfile-tugas-week10
sudo mkswap /swapfile-tugas-week10
sudo swapon /swapfile-tugas-week10
swapon --show
```

### Langkah 2
Input :
```bash
{
    echo "=== VERIFIKASI SWAP ==="
    swapon --show
    echo
    free -h
} > swap-check.txt

cat swap-check.txt
```

Output : 
```bash
root@ubuntuser:~/praktikum-os/week10-memory# sudo fallocate -l 256M /swapfile-tugas-week10
root@ubuntuser:~/praktikum-os/week10-memory# ls -lh /swapfile-tugas-week10
-rw-r--r-- 1 root root 256M May  4 13:05 /swapfile-tugas-week10
root@ubuntuser:~/praktikum-os/week10-memory# sudo chmod 600 /swapfile-tugas-week10
root@ubuntuser:~/praktikum-os/week10-memory# ls -lh /swapfile-tugas-week10
-rw------- 1 root root 256M May  4 13:05 /swapfile-tugas-week10
root@ubuntuser:~/praktikum-os/week10-memory# sudo mkswap /swapfile-tugas-week10
Setting up swapspace version 1, size = 256 MiB (268431360 bytes)
no label, UUID=0ed4a629-1bc9-48e9-ba9b-2c63a6cc423b
root@ubuntuser:~/praktikum-os/week10-memory# sudo swapon /swapfile-tugas-week10
root@ubuntuser:~/praktikum-os/week10-memory# swapon --show
NAME                   TYPE SIZE USED PRIO
/swapfile-tugas-week10 file 256M   0B   -2
root@ubuntuser:~/praktikum-os/week10-memory# {
    echo "=== VERIFIKASI SWAP ==="
    swapon --show
    echo
    free -h
} > swap-check.txt

cat swap-check.txt
=== VERIFIKASI SWAP ===
NAME                   TYPE SIZE USED PRIO
/swapfile-tugas-week10 file 256M   0B   -2

               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       408Mi       1.3Gi       1.1Mi       1.9Gi       2.9Gi
Swap:          255Mi          0B       255Mi
```

### Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?

Jawaban :  
1. 
- NAME: /swapfile-tugas-week10 
- TYPE: file 
- SIZE: 256M 
- USED: 0B 
2. Iya, yang awalnya 0 menjadi 255/256 MB 
3. file swap menyimpan potongan-potongan memori dari proses yang sedang berjalan. Ketika kernel membutuhkan ruang RAM tambahan, ia memindahkan halaman memori yang jarang diakses ke swap file. Jika permission diatur ke 644 (rw-r--r--), maka semua pengguna di sistem dapat membaca file swap tersebut. 


## Tugas 10.4

### Langkah 1
Input :
```bash
strace -c ls 2> strace-summary.txt
strace ls /etc 2> strace-ls-etc.txt
cat strace-summary.txt
```

Output : 
```bash
root@ubuntuser:~/praktikum-os/week10-memory# strace -c ls 2> strace-summary.txt
memory-audit.sh    strace-summary.txt  top-memory-process.txt
memory-report.txt  swap-check.txt
monitor-memori.sh  syscall-case
root@ubuntuser:~/praktikum-os/week10-memory# strace ls /etc 2> strace-ls-etc.txt
adduser.conf            kernel               rc1.d
alternatives            landscape            rc2.d
apparmor                ldap                 rc3.d
apparmor.d              ld.so.cache          rc4.d
apport                  ld.so.conf           rc5.d
apt                     ld.so.conf.d         rc6.d
bash.bashrc             legal                rcS.d
bash_completion         libaudit.conf        resolv.conf
bash_completion.d       libblockdev          rmt
bindresvport.blacklist  libibverbs.d         rpc
binfmt.d                libnl-3              rsyslog.conf
byobu                   libpaper.d           rsyslog.d
ca-certificates         locale.alias         screenrc
ca-certificates.conf    locale.conf          security
cloud                   locale.gen           selinux
console-setup           localtime            sensors3.conf
credstore               logcheck             sensors.d
credstore.encrypted     login.defs           services
cron.d                  logrotate.conf       sgml
cron.daily              logrotate.d          shadow
cron.hourly             lsb-release          shadow-
cron.monthly            lvm                  shells
crontab                 machine-id           skel
cron.weekly             magic                sos
cron.yearly             magic.mime           ssh
cryptsetup-initramfs    manpath.config       ssl
crypttab                mdadm                subgid
dbus-1                  mime.types           subgid-
debconf.conf            mke2fs.conf          subuid
debian_version          ModemManager         subuid-
default                 modprobe.d           sudo.conf
deluser.conf            modules              sudoers
depmod.d                modules-load.d       sudoers.d
dhcp                    mtab                 sudo_logsrvd.conf
dhcpcd.conf             multipath            supercat
dpkg                    multipath.conf       sysctl.conf
e2scrub.conf            nanorc               sysctl.d
environment             needrestart          sysstat
ethertypes              netconfig            systemd
fonts                   netplan              terminfo
fstab                   network              thermald
fuse.conf               networkd-dispatcher  timezone
fwupd                   networks             tmpfiles.d
gai.conf                newt                 ubuntu-advantage
ghostscript             nftables.conf        ucf.conf
gnutls                  nsswitch.conf        udev
groff                   opt                  udisks2
group                   os-release           ufw
group-                  overlayroot.conf     update-manager
grub.d                  PackageKit           update-motd.d
gshadow                 pam.conf             update-notifier
gshadow-                pam.d                UPower
gss                     papersize            usb_modeswitch.conf
hdparm.conf             passwd               usb_modeswitch.d
host.conf               passwd-              vconsole.conf
hostname                perl                 vim
hosts                   pki                  vmware-tools
hosts.allow             plymouth             vtrgb
hosts.deny              pm                   w3m
ImageMagick-6           polkit-1             wgetrc
init.d                  pollinate            X11
initramfs-tools         profile              xattr.conf
inputrc                 profile.d            xdg
iproute2                protocols            xml
iscsi                   python3              zsh_command_not_found
issue                   python3.12
issue.net               rc0.d
root@ubuntuser:~/praktikum-os/week10-memory# cat strace-summary.txt
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 27.04    0.004953         275        18           mmap
 26.66    0.004882         542         9           close
 13.60    0.002491        2491         1           execve
  8.65    0.001584         792         2         2 access
  8.27    0.001514         757         2           pread64
  6.37    0.001166         166         7           openat
  4.28    0.000784         156         5           read
  3.73    0.000683          85         8           fstat
  0.40    0.000074          14         5           mprotect
  0.25    0.000046          23         2           getdents64
  0.17    0.000032          16         2         2 statfs
  0.16    0.000030          10         3           write
  0.14    0.000026          26         1           munmap
  0.08    0.000015           5         3           brk
  0.07    0.000012           6         2           ioctl
  0.03    0.000006           6         1           getrandom
  0.02    0.000004           4         1           arch_prctl
  0.02    0.000004           4         1           prlimit64
  0.02    0.000003           3         1           set_tid_address
  0.02    0.000003           3         1           set_robust_list
  0.02    0.000003           3         1           rseq
------ ----------- ----------- --------- --------- ----------------
100.00    0.018315         240        76         4 total
```

### Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
2. System call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?

Jawaban :   
1. 
- mmap = memetakan file atau perangkat ke dalam memori

- close = menutup file descriptor

- execve = menjalankan program baru (dalam hal ini /usr/bin/ls)

- access = mengecek izin akses file

- openat = membuka file atau direktori  
2. mmap (18 kali) = paling sering dipanggil karena ls perlu memetakan library shared ke memori proses agar fungsi-fungsi standar C dapat digunakan. 
3. Ya, ada 4 errors (2 pada access, 2 pada statfs). Program tetap berjalan normal karena error tersebut diantisipasi, misalnya access gagal karena file /etc/ld.so.nohwcap memang tidak ada. 


## Tugas 10.5

### Langkah 1
Input :
```bash
nano diagnosa-server.sh
```

### Langkah 2
Input :
```bash
#!/bin/bash
set -euo pipefail

LAPORAN="diagnosa-server-lambat.txt"
WARN_MEM=false
WARN_SWAP=0

cek_memori() {
    echo "--- Kondisi Memori ---"
    free -h
    echo
    AVAIL_PCT=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')
    if [ "$AVAIL_PCT" -lt 20 ]; then
        echo "PERINGATAN: Memori tersedia hanya ${AVAIL_PCT}%"
        WARN_MEM=true
    fi
}

cek_swap() {
    echo "--- Penggunaan Swap ---"
    swapon --show 2>/dev/null || echo "Tidak ada swap aktif"
    echo
    WARN_SWAP=$(free | awk '/Swap/ {print $3}')
    if [ "$WARN_SWAP" -gt 0 ]; then
        echo "INFO: Swap digunakan (${WARN_SWAP} kB)"
    fi
}

cek_proses() {
    echo "--- 10 Proses Memori Tertinggi ---"
    ps aux --sort=-%mem | head -n 11
    echo
}

cek_paging() {
    echo "--- Aktivitas Paging (5 sampel) ---"
    vmstat 1 5
    echo
}

ringkasan() {
    echo "=== RINGKASAN ==="
    if [ "$WARN_MEM" = true ]; then
        echo "- Memori: KRITIS - perlu tindakan segera"
    else
        echo "- Memori: normal"
    fi
    if [ "$WARN_SWAP" -gt 0 ]; then
        echo "- Swap: aktif - pantau aktivitas paging"
    else
        echo "- Swap: tidak digunakan"
    fi
}

{
    echo "=== LAPORAN DIAGNOSA SERVER ==="
    date
    echo
    cek_memori
    cek_swap
    cek_proses
    cek_paging
    ringkasan
} | tee "$LAPORAN"

echo
echo "Laporan disimpan ke: $LAPORAN"
```

### Langkah 3
Input :
```bash
chmod +x diagnosa-server.sh
cd ~/praktikum-os/week10-memory
bash diagnosa-server.sh
```

Output : 
```bash
root@ubuntuser:~/praktikum-os/week10-memory# nano diagnosa-server.sh
root@ubuntuser:~/praktikum-os/week10-memory# chmod +x diagnosa-server.sh
root@ubuntuser:~/praktikum-os/week10-memory# cd ~/praktikum-os/week10-memory
root@ubuntuser:~/praktikum-os/week10-memory# bash diagnosa-server.sh
=== LAPORAN DIAGNOSA SERVER ===
Mon May  4 01:22:45 PM UTC 2026

--- Kondisi Memori ---
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       407Mi       1.3Gi       1.1Mi       1.9Gi       2.9Gi
Swap:             0B          0B          0B

--- Penggunaan Swap ---

--- 10 Proses Memori Tertinggi ---
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root       25042  0.1  1.2 478516 42464 ?        Ssl  13:12   0:01 /usr/libexec/fwupd/fwupd
root        2713  0.0  0.7 223568 27308 ?        SLsl 12:25   0:02 /sbin/multipathd -d -s
root         723  0.0  0.6 109688 23148 ?        Ssl  11:45   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root       19267  0.0  0.3 468848 13632 ?        Ssl  12:34   0:00 /usr/libexec/udisks2/udisksd
root           1  0.1  0.3  22060 13392 ?        Ss   11:44   0:10 /usr/lib/systemd/systemd --system --deserialize=60 splash noprompt noshell automatic-ubiquity
systemd+   19272  0.0  0.3  21584 13192 ?        Ss   12:34   0:00 /usr/lib/systemd/systemd-resolved
root        9507  0.0  0.3 392100 12892 ?        Ssl  12:31   0:00 /usr/sbin/ModemManager
root       19266  0.0  0.3  34172 12724 ?        S<s  12:34   0:00 /usr/lib/systemd/systemd-journald
root        1073  0.0  0.3  20280 11504 ?        Ss   11:49   0:00 /usr/lib/systemd/systemd --user
yudhis       985  0.0  0.3  20084 11300 ?        Ss   11:47   0:00 /usr/lib/systemd/systemd --user

--- Aktivitas Paging (5 sampel) ---
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 1  0      0 1340432  13384 1937120    0    0   134   655  406    0  1  2 96  0  0  0
 2  0      0 1340432  13384 1937228    0    0     0     4  614  202  0  1 99  0  0  0
 0  0      0 1340432  13384 1937228    0    0     0    20  286  105  0  1 99  0  0  0
 0  0      0 1340432  13384 1937228    0    0     0     0  232   65  0  0 100  0  0  0
 1  0      0 1340432  13384 1937228    0    0     0     0  243   81  0  0 100  0  0  0

=== RINGKASAN ===
- Memori: normal
- Swap: tidak digunakan

Laporan disimpan ke: diagnosa-server-lambat.txt
```

### Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?

Jawaban :  
1. Dipecah agar kode terstruktur, mudah dibaca, dan mudah diuji per bagian.
- cek_memori = cek kondisi RAM dan hitung persentase available
- cek_swap = cek swap aktif dan penggunaannya
- cek_proses = tampilkan 10 proses pemakan memori terbanyak
- cek_paging = pantau aktivitas swap in/out dengan vmstat
- ringkasan = simpulkan status sistem 
2. Normal, available 2.9 GB dari 3.3 GB total (88%), swap tidak digunakan 
3. Agar output bisa lihat di layar dan simpan ke file secara bersamaan. 
4. Tidak ada (si dan so = 0 semua), performa server baik karena tidak ada paging ke disk.  
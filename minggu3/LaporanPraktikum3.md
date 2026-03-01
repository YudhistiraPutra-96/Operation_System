# Laporan Praktikum 3

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

# Latihan

## Latihan 3.1 

Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log

### Jawaban  

Kode :  
```bash
echo "===== Mencari 10 file terbesar di /var/log/ ====="
echo "Waktu: $(date)"
echo "----------------------------------------"

find /var/log/ -type f -exec ls -lh {} \; 2> error.log | sort -k5 -rh | head -10 | tee large-logs.txt

echo "----------------------------------------"
echo "Hasil disimpan di: large-logs.txt"
echo "Error disimpan di: error.log"
```

Output :  
```bash
===== Mencari 10 file terbesar di /var/log/ =====
Waktu: Sun Mar  1 02:53:00 AM UTC 2026
----------------------------------------
-rw-r-----+ 1 root systemd-journal 8.0M Mar  1 02:51 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/system.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  1 02:50 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/user-1000.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  1 02:49 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/user-1000@0f79df4e279e44348b9cbc14e0758413-0000000000004506-00064be43e247cb2.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  1 02:49 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/system@96e54f1d9caa451fbc46a287b4558688-0000000000004630-00064bed76a4fc32.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  1 02:45 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/system@0f79df4e279e44348b9cbc14e0758413-0000000000004507-00064be43e259dee.journal
-rw-r-----+ 1 root systemd-journal 8.0M Feb 28 15:45 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/user-1000@19af25cf95f044a6b45608dca5ba6cef-0000000000003ed9-00064be357886d4d.journal
-rw-r-----+ 1 root systemd-journal 8.0M Feb 28 15:45 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/system@0f79df4e279e44348b9cbc14e0758413-0000000000004184-00064be439f6f23d.journal
-rw-r-----+ 1 root systemd-journal 8.0M Feb 28 15:44 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/system@19af25cf95f044a6b45608dca5ba6cef-0000000000003b6b-00064be356b75c01.journal
-rw-r-----+ 1 root systemd-journal 8.0M Feb 28 14:41 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/system@00064be356b91d3f-58fcbedc8d458978.journal~
-rw-r-----+ 1 root systemd-journal 8.0M Feb 28 14:39 /var/log/journal/e8a3965095c9428fa119c510ba2d12c9/user-1000@e6da2d1511eb40e8ac82ae54e3dbd71f-000000000000369a-00064be336b98a36.journal
----------------------------------------
Hasil disimpan di: large-logs.txt
Error disimpan di: error.log
```


## Latihan 3.2

Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.

### Jawaban :    

Kode :  
```bash
cat /etc/passwd | cut -d: -f1 | sort | tee sorted-users.txt
```

Output :  
```bash
_apt
backup
bin
daemon
dhcpcd
fwupd-refresh
games
irc
landscape
list
lp
mail
man
messagebus
news
nobody
polkitd
pollinate
proxy
root
sshd
sync
sys
syslog
systemd-network
systemd-resolve
systemd-timesync
tcpdump
tss
usbmux
uucp
uuidd
www-data
yudhis
```


## Latihan 3.3

Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file

### Jawaban    

Kode :  
```bash
LOGFILE="system-monitor-$(date +%Y%m%d-%H%M%S).log"
ITERATIONS=12
COUNTER=1

echo "===== SYSTEM MONITORING LOG =====" | tee -a "$LOGFILE"
echo "Start time: $(date)" | tee -a "$LOGFILE"
echo "Monitoring setiap 5 detik selama 1 menit" | tee -a "$LOGFILE"
echo "===================================" | tee -a "$LOGFILE"
echo "" | tee -a "$LOGFILE"

while [ $COUNTER -le $ITERATIONS ]; do
    TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S")

    echo "[$TIMESTAMP] Iterasi ke-$COUNTER" | tee -a "$LOGFILE"
    echo "-----------------------------------" | tee -a "$LOGFILE"

    echo "CPU Usage:" | tee -a "$LOGFILE"
    top -bn1 | grep "Cpu(s)" | tee -a "$LOGFILE"

    echo "Memory Usage:" | tee -a "$LOGFILE"
    free -h | tee -a "$LOGFILE"

    echo "Load Average:" | tee -a "$LOGFILE"
    uptime | tee -a "$LOGFILE"

    echo "" | tee -a "$LOGFILE"

    COUNTER=$((COUNTER + 1))

    if [ $COUNTER -le $ITERATIONS ]; then
        sleep 5
    fi
done

echo "===================================" | tee -a "$LOGFILE"
echo "Monitoring selesai: $(date)" | tee -a "$LOGFILE"
echo "Log disimpan di: $LOGFILE"
```

Output :  
```bash
===== SYSTEM MONITORING LOG =====
Start time: Sun Mar  1 03:05:10 AM UTC 2026
Monitoring setiap 5 detik selama 1 menit
===================================

[2026-03-01 03:05:10] Iterasi ke-1
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 97.3 id,  2.7 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       351Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:10 up 19 min,  2 users,  load average: 0.00, 0.01, 0.05

[2026-03-01 03:05:15] Iterasi ke-2
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       352Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:16 up 19 min,  2 users,  load average: 0.00, 0.01, 0.05

[2026-03-01 03:05:21] Iterasi ke-3
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       353Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:21 up 19 min,  2 users,  load average: 0.00, 0.01, 0.05

[2026-03-01 03:05:26] Iterasi ke-4
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       353Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:26 up 20 min,  2 users,  load average: 0.08, 0.03, 0.05

[2026-03-01 03:05:31] Iterasi ke-5
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.2 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       353Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:33 up 20 min,  2 users,  load average: 0.15, 0.04, 0.06

[2026-03-01 03:05:38] Iterasi ke-6
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  1.7 sy,  0.0 ni, 98.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       353Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:39 up 20 min,  2 users,  load average: 0.14, 0.04, 0.06

[2026-03-01 03:05:44] Iterasi ke-7
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 98.7 id,  0.0 wa,  0.0 hi,  1.3 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       353Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:44 up 20 min,  2 users,  load average: 0.13, 0.04, 0.06

[2026-03-01 03:05:50] Iterasi ke-8
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       353Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:50 up 20 min,  2 users,  load average: 0.12, 0.04, 0.05

[2026-03-01 03:05:55] Iterasi ke-9
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  1.1 sy,  0.0 ni, 98.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       356Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:05:56 up 20 min,  2 users,  load average: 0.10, 0.04, 0.05

[2026-03-01 03:06:01] Iterasi ke-10
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       356Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:06:02 up 20 min,  2 users,  load average: 0.09, 0.04, 0.05

[2026-03-01 03:06:07] Iterasi ke-11
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       356Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:06:07 up 20 min,  2 users,  load average: 0.08, 0.04, 0.05

[2026-03-01 03:06:12] Iterasi ke-12
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       356Mi       2.9Gi       1.1Mi       265Mi       3.0Gi
Swap:             0B          0B          0B
Load Average:
 03:06:12 up 20 min,  2 users,  load average: 0.08, 0.03, 0.05

===================================
Monitoring selesai: Sun Mar  1 03:06:12 AM UTC 2026
Log disimpan di: system-monitor-20260301-030510.log
```



## Latihan 3.4
Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file

### Jawaban :

Kode :  
```bash
find / -name "*.conf" 2> /dev/null | tee all-config-files.txt | wc -l
```
Output :  
```bash
401
```


## Latihan 3.5

Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry

### Jawaban :  

Kode :  
```bash
tar -cvf backup.tar praktikum-os 2> backup-error.log | while read line; do echo "$(date '+%F %T') $line"; done | tee backup-success.log
```
Output :  
```bash
2026-03-01 03:54:41 praktikum-os/
2026-03-01 03:54:41 praktikum-os/week03/
2026-03-01 03:54:41 praktikum-os/week03/backup-error.log
2026-03-01 03:54:41 praktikum-os/week03/backup-success.l
2026-03-01 03:54:41 praktikum-os/week03/backup-success.log
2026-03-01 03:54:41 praktikum-os/week03/backup.tar
2026-03-01 03:54:41 praktikum-os/week02/
2026-03-01 03:54:41 praktikum-os/week02/server.log
2026-03-01 03:54:41 praktikum-os/week02/data.log
2026-03-01 03:54:41 praktikum-os/week02/server1.log
2026-03-01 03:54:41 praktikum-os/week02/config.txt
2026-03-01 03:54:41 praktikum-os/week02/server1.log.bak
2026-03-01 03:54:41 praktikum-os/week02/server.log.bak
2026-03-01 03:54:41 praktikum-os/week02/notes.txt
```
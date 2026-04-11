# Laporan Praktikum 7

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## Tugas Praktikum 1 — Toolkit Bash Administrator Pribadi  
### Langkah 1 : Buat Workspace
Input :
```bash
mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}

cd ~/praktikum-os/week07-bash

touch sample-app.conf
touch logs/app-{01,02,03}.log
touch sampel/catatan-{a,b}.txt
touch sampel/backup-{01,02}.tar
touch "ruang-nama/laporan server april.txt"
touch "ruang-nama/backup [mingguan] server.conf"

echo "✅ Workspace siap"
```
Output :
```bash
root@ubuntuser:/home/yudhis# mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
root@ubuntuser:/home/yudhis# cd ~/praktikum-os/week07-bash
root@ubuntuser:~/praktikum-os/week07-bash# touch sample-app.conf
root@ubuntuser:~/praktikum-os/week07-bash# touch logs/app-{01,02,03}.log
root@ubuntuser:~/praktikum-os/week07-bash# touch sampel/catatan-{a,b}.txt
root@ubuntuser:~/praktikum-os/week07-bash# touch sampel/backup-{01,02}.tar
root@ubuntuser:~/praktikum-os/week07-bash# touch "ruang-nama/laporan server april.txt"
root@ubuntuser:~/praktikum-os/week07-bash# touch "ruang-nama/backup [mingguan] server.conf"
root@ubuntuser:~/praktikum-os/week07-bash# echo "✅ Workspace siap"
✅ Workspace siap
```

### Langkah 2 : Backup dan Tambahkan Konfigurasi ke .bashrc
Input :
```bash
cp ~/.bashrc ~/.bashrc.bak-praktikum-$(date +%Y%m%d)

cat <<'EOF' >> ~/.bashrc

# ===== PRAKTIKUM BASH SHELL - TUGAS 1 =====
# 1. PATH ke direktori bin pribadi
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"

# 2. Alias untuk kerja harian
alias ll='ls -lah --color=auto'
alias hist10='history | tail -10'
alias dfh='df -h'
alias freeh='free -h'

# 3. Fungsi untuk backup dengan timestamp
backup_file() {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_file <nama_file>"
        return 1
    fi
    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"
    if [ ! -f "$src" ]; then
        echo "Error: File '$src' tidak ditemukan!"
        return 2
    fi
    mkdir -p "$dst"
    local timestamp=$(date +%Y%m%d_%H%M%S)
    cp "$src" "$dst/$(basename "$src").$timestamp.bak"
    echo "✅ Backup berhasil: $dst/$(basename "$src").$timestamp.bak"
}
# ===== END PRAKTIKUM =====

EOF

source ~/.bashrc

echo "✅ Konfigurasi ditambahkan ke .bashrc"
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cp ~/.bashrc ~/.bashrc.bak-praktikum-$(date +%Y%m%d)
root@ubuntuser:~/praktikum-os/week07-bash# cat <<'EOF' >> ~/.bashrc
> # ===== PRAKTIKUM BASH SHELL - TUGAS 1 =====
# 1. PATH ke direktori bin pribadi
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"

# 2. Alias untuk kerja harian
alias ll='ls -lah --color=auto'
alias hist10='history | tail -10'
alias dfh='df -h'
alias freeh='free -h'

# 3. Fungsi untuk backup dengan timestamp
backup_file() {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_file <nama_file>"
        return 1
    fi
    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"
    if [ ! -f "$src" ]; then
        echo "Error: File '$src' tidak ditemukan!"
        return 2
    fi
    mkdir -p "$dst"
    local timestamp=$(date +%Y%m%d_%H%M%S)
    cp "$src" "$dst/$(basename "$src").$timestamp.bak"
    echo "✅ Backup berhasil: $dst/$(basename "$src").$timestamp.bak"
}
# ===== END PRAKTIKUM =====
> EOF
root@ubuntuser:~/praktikum-os/week07-bash# source ~/.bashrc
root@ubuntuser:~/praktikum-os/week07-bash# echo "✅ Konfigurasi ditambahkan ke .bashrc"
✅ Konfigurasi ditambahkan ke .bashrc
```

### Langkah 3 : Buat Script di direktori bin
Input :
```bash
cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
#!/usr/bin/env bash

echo "=========================================="
echo "        RINGKASAN SISTEM"
echo "=========================================="
echo "Hostname    : $(hostname)"
echo "User        : $(whoami)"
echo "Tanggal     : $(date '+%Y-%m-%d %H:%M:%S')"
echo "Uptime      : $(uptime -p)"
echo "Memory      : $(free -h | grep Mem | awk '{print $3 "/" $2}')"
echo "Disk /      : $(df -h / | tail -1 | awk '{print $3 "/" $2 " (" $5 ")"}')"
echo "Shell aktif : $SHELL"
echo "=========================================="
EOF

chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem

echo "✅ Script ringkas-sistem siap"
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
> #!/usr/bin/env bash

echo "=========================================="
echo "        RINGKASAN SISTEM"
echo "=========================================="
echo "Hostname    : $(hostname)"
echo "User        : $(whoami)"
echo "Tanggal     : $(date '+%Y-%m-%d %H:%M:%S')"
echo "Uptime      : $(uptime -p)"
echo "Memory      : $(free -h | grep Mem | awk '{print $3 "/" $2}')"
echo "Disk /      : $(df -h / | tail -1 | awk '{print $3 "/" $2 " (" $5 ")"}')"
echo "Shell aktif : $SHELL"
echo "=========================================="
> EOF
root@ubuntuser:~/praktikum-os/week07-bash# chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
root@ubuntuser:~/praktikum-os/week07-bash# echo "✅ Script ringkas-sistem siap"
✅ Script ringkas-sistem siap
```

### Langkah 4 : Uji Semua Konfigurasi  
Input :
```bash
echo "=== TEST 1: Isi PATH ==="
echo "$PATH" | tr ':' '\n' | grep "week07-bash/bin"

echo -e "\n=== TEST 2: Uji alias ll ==="
ll ~/praktikum-os/week07-bash/ | head -5

echo -e "\n=== TEST 3: Uji fungsi backup_file ==="
backup_file ~/praktikum-os/week07-bash/sample-app.conf

echo -e "\n=== TEST 4: Uji script ringkas-sistem ==="
cd /tmp
ringkas-sistem

cd ~/praktikum-os/week07-bash
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# echo "=== TEST 1: Isi PATH ==="
=== TEST 1: Isi PATH ===
root@ubuntuser:~/praktikum-os/week07-bash# echo "$PATH" | tr ':' '\n' | grep "week07-bash/bin"
/root/praktikum-os/week07-bash/bin
root@ubuntuser:~/praktikum-os/week07-bash# echo -e "\n=== TEST 2: Uji alias ll ==="

=== TEST 2: Uji alias ll ===
root@ubuntuser:~/praktikum-os/week07-bash# ll ~/praktikum-os/week07-bash/ | head -5
total 28K
drwxr-xr-x 7 root root 4.0K Apr 10 13:05 .
drwxr-xr-x 7 root root 4.0K Apr 10 13:04 ..
drwxr-xr-x 2 root root 4.0K Apr 10 13:04 backup
drwxr-xr-x 2 root root 4.0K Apr 10 13:20 bin
root@ubuntuser:~/praktikum-os/week07-bash# echo -e "\n=== TEST 3: Uji fungsi backup_file ==="

=== TEST 3: Uji fungsi backup_file ===
root@ubuntuser:~/praktikum-os/week07-bash# backup_file ~/praktikum-os/week07-bash/sample-app.conf
✅ Backup berhasil: /root/praktikum-os/week07-bash/backup/sample-app.conf.20260410_132242.bak
root@ubuntuser:~/praktikum-os/week07-bash# echo -e "\n=== TEST 4: Uji script ringkas-sistem ==="

=== TEST 4: Uji script ringkas-sistem ===
root@ubuntuser:~/praktikum-os/week07-bash# cd /tmp
root@ubuntuser:/tmp# ringkas-sistem
==========================================
        RINGKASAN SISTEM
==========================================
Hostname    : ubuntuser
User        : root
Tanggal     : 2026-04-10 13:23:02
Uptime      : up 26 minutes
Memory      : 363Mi/3.3Gi
Disk /      : 3.7G/50G (8%)
Shell aktif : /bin/bash
==========================================
root@ubuntuser:/tmp# cd ~/praktikum-os/week07-bash
root@ubuntuser:~/praktikum-os/week07-bash#
```

### Langkah 5 : Buat Laporan Tugas 1
Input :
```bash
cat <<'EOF' > ~/praktikum-os/week07-bash/toolkit-bash-report.txt
==========================================
LAPORAN TUGAS PRAKTIKUM 1
Toolkit Bash Administrator Pribadi
==========================================
Tanggal: $(date '+%Y-%m-%d %H:%M:%S')
User: $(whoami)
Host: $(hostname)

------------------------------------------
1. KONFIGURASI YANG DITAMBAHKAN KE .bashrc
------------------------------------------
EOF

echo -e "\n--- Isi konfigurasi ---" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
grep -A 30 "PRAKTIKUM BASH SHELL" ~/.bashrc >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt

echo -e "\n\n------------------------------------------
2. HASIL \$PATH
------------------------------------------" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
echo "$PATH" | tr ':' '\n' >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt

echo -e "\n\n------------------------------------------
3. TYPE ALIAS, FUNGSI, DAN SCRIPT
------------------------------------------" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
echo "--- Alias ll ---" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
type ll >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt 2>&1

echo -e "\n--- Fungsi backup_file ---" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
type backup_file >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt 2>&1

echo -e "\n--- Script ringkas-sistem ---" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
type ringkas-sistem >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt 2>&1

echo -e "\n\n------------------------------------------
4. HASIL UJI COBA
------------------------------------------" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
echo "Hasil uji alias ll:" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
ll ~/praktikum-os/week07-bash/ >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt 2>&1

echo -e "\nHasil uji fungsi backup_file:" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
backup_file ~/praktikum-os/week07-bash/sample-app.conf >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt 2>&1

echo -e "\nHasil uji script ringkas-sistem:" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt
ringkas-sistem >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt 2>&1

echo -e "\n\n==========================================
LAPORAN SELESAI
==========================================" >> ~/praktikum-os/week07-bash/toolkit-bash-report.txt

echo "✅ Laporan Tugas 1 selesai: ~/praktikum-os/week07-bash/toolkit-bash-report.txt"

cat ~/praktikum-os/week07-bash/toolkit-bash-report.txt
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat ~/praktikum-os/week07-bash/toolkit-bash-report.txt
==========================================
LAPORAN TUGAS PRAKTIKUM 1
Toolkit Bash Administrator Pribadi
==========================================
Tanggal: $(date '+%Y-%m-%d %H:%M:%S')
User: $(whoami)
Host: $(hostname)

------------------------------------------
1. KONFIGURASI YANG DITAMBAHKAN KE .bashrc
------------------------------------------

--- Isi konfigurasi ---
# ===== PRAKTIKUM BASH SHELL - TUGAS 1 =====
# 1. PATH ke direktori bin pribadi
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"

# 2. Alias untuk kerja harian
alias ll='ls -lah --color=auto'
alias hist10='history | tail -10'
alias dfh='df -h'
alias freeh='free -h'

# 3. Fungsi untuk backup dengan timestamp
backup_file() {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_file <nama_file>"
        return 1
    fi
    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"
    if [ ! -f "$src" ]; then
        echo "Error: File '$src' tidak ditemukan!"
        return 2
    fi
    mkdir -p "$dst"
    local timestamp=$(date +%Y%m%d_%H%M%S)
    cp "$src" "$dst/$(basename "$src").$timestamp.bak"
    echo "✅ Backup berhasil: $dst/$(basename "$src").$timestamp.bak"
}
# ===== END PRAKTIKUM =====



------------------------------------------
2. HASIL $PATH
------------------------------------------
/root/praktikum-os/week07-bash/bin
/usr/local/sbin
/usr/local/bin
/usr/sbin
/usr/bin
/sbin
/bin
/usr/games
/usr/local/games
/snap/bin


------------------------------------------
3. TYPE ALIAS, FUNGSI, DAN SCRIPT
------------------------------------------
--- Alias ll ---
ll is aliased to `ls -lah --color=auto'

--- Fungsi backup_file ---
backup_file is a function
backup_file ()
{
    if [ $# -ne 1 ]; then
        echo "Usage: backup_file <nama_file>";
        return 1;
    fi;
    local src="$1";
    local dst="$HOME/praktikum-os/week07-bash/backup";
    if [ ! -f "$src" ]; then
        echo "Error: File '$src' tidak ditemukan!";
        return 2;
    fi;
    mkdir -p "$dst";
    local timestamp=$(date +%Y%m%d_%H%M%S);
    cp "$src" "$dst/$(basename "$src").$timestamp.bak";
    echo "✅ Backup berhasil: $dst/$(basename "$src").$timestamp.bak"
}

--- Script ringkas-sistem ---
ringkas-sistem is hashed (/root/praktikum-os/week07-bash/bin/ringkas-sistem)


------------------------------------------
4. HASIL UJI COBA
------------------------------------------
Hasil uji alias ll:
total 32K
drwxr-xr-x 7 root root 4.0K Apr 10 13:26 .
drwxr-xr-x 7 root root 4.0K Apr 10 13:04 ..
drwxr-xr-x 2 root root 4.0K Apr 10 13:22 backup
drwxr-xr-x 2 root root 4.0K Apr 10 13:20 bin
drwxr-xr-x 2 root root 4.0K Apr 10 13:06 logs
drwxr-xr-x 2 root root 4.0K Apr 10 13:08 ruang-nama
drwxr-xr-x 2 root root 4.0K Apr 10 13:07 sampel
-rw-r--r-- 1 root root    0 Apr 10 13:05 sample-app.conf
-rw-r--r-- 1 root root 2.4K Apr 10 13:31 toolkit-bash-report.txt

Hasil uji fungsi backup_file:
✅ Backup berhasil: /root/praktikum-os/week07-bash/backup/sample-app.conf.20260410_133235.bak

Hasil uji script ringkas-sistem:
==========================================
        RINGKASAN SISTEM
==========================================
Hostname    : ubuntuser
User        : root
Tanggal     : 2026-04-10 13:32:46
Uptime      : up 36 minutes
Memory      : 361Mi/3.3Gi
Disk /      : 3.7G/50G (8%)
Shell aktif : /bin/bash
==========================================


==========================================
LAPORAN SELESAI
==========================================
```  



## Tugas Praktikum 2 — Audit File Konfigurasi dan Logging Aman
### Langkah 1 : Persiapan dan Membuat Laporan Audit
Input :
```bash
cd ~/praktikum-os/week07-bash

TGL=$(date +%F)

echo "=== MEMULAI AUDIT KONFIGURASI ==="
echo "Tanggal audit: $TGL"
echo "Laporan: audit-konfigurasi-$TGL.txt"
echo "Error log: audit-error.log"
``
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cd ~/praktikum-os/week07-bash
root@ubuntuser:~/praktikum-os/week07-bash# TGL=$(date +%F)
root@ubuntuser:~/praktikum-os/week07-bash# echo "=== MEMULAI AUDIT KONFIGURASI ==="
=== MEMULAI AUDIT KONFIGURASI ===
root@ubuntuser:~/praktikum-os/week07-bash# echo "Tanggal audit: $TGL"
Tanggal audit: 2026-04-10
root@ubuntuser:~/praktikum-os/week07-bash# echo "Laporan: audit-konfigurasi-$TGL.txt"
Laporan: audit-konfigurasi-2026-04-10.txt
root@ubuntuser:~/praktikum-os/week07-bash# echo "Error log: audit-error.log"
Error log: audit-error.log
```  

### Langkah 2 : Mencari File *.conf di /etc (dengan pemisahan output)
Input :
```bash
find /etc -name "*.conf" 2> audit-error.log > audit-konfigurasi-2026-04-10.txt

echo "=== HASIL PENCARIAN FILE .conf ==="
echo "Jumlah file ditemukan: $(wc -l < audit-konfigurasi-2026-04-10.txt)"
echo "Jumlah error: $(wc -l < audit-error.log)"
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# find /etc -name "*.conf" 2> audit-error.log > audit-konfigurasi-2026-04-10.txt
root@ubuntuser:~/praktikum-os/week07-bash# echo "=== HASIL PENCARIAN FILE .conf ==="
=== HASIL PENCARIAN FILE .conf ===
root@ubuntuser:~/praktikum-os/week07-bash# echo "Jumlah file ditemukan: $(wc -l < audit-konfigurasi-2026-04-10.txt)"
Jumlah file ditemukan: 179
root@ubuntuser:~/praktikum-os/week07-bash# echo "Jumlah error: $(wc -l < audit-error.log)"
Jumlah error: 0
root@ubuntuser:~/praktikum-os/week07-bash#
```  

### Langkah 3 : Menampilkan Isi Laporan dengan tee (ke terminal + file)
Input :
```bash
echo "=== 10 FILE .conf PERTAMA ===" | tee -a audit-ringkasan-2026-04-10.txt
head -10 audit-konfigurasi-2026-04-10.txt | tee -a audit-ringkasan-2026-04-10.txt

echo -e "\n=== JUMLAH TOTAL ===" | tee -a audit-ringkasan-2026-04-10.txt
echo "Total file konfigurasi: $(wc -l < audit-konfigurasi-2026-04-10.txt)" | tee -a audit-ringkasan-2026-04-10.txt
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# echo "=== 10 FILE .conf PERTAMA ===" | tee -a audit-ringkasan-2026-04-10.txt
=== 10 FILE .conf PERTAMA ===
root@ubuntuser:~/praktikum-os/week07-bash# head -10 audit-konfigurasi-2026-04-10.txt | tee -a audit-ringkasan-2026-04-10.txt
/etc/UPower/UPower.conf
/etc/nftables.conf
/etc/ld.so.conf
/etc/sudo_logsrvd.conf
/etc/systemd/resolved.conf
/etc/systemd/logind.conf
/etc/systemd/sleep.conf
/etc/systemd/pstore.conf
/etc/systemd/timesyncd.conf.d/cloud-init.conf
/etc/systemd/user.conf
root@ubuntuser:~/praktikum-os/week07-bash# echo -e "\n=== JUMLAH TOTAL ===" | tee -a audit-ringkasan-2026-04-10.txt
echo "Total file konfigurasi: $(wc -l < audit-konfigurasi-2026-04-10.txt)" | tee -a audit-ringkasan-2026-04-10.txt

=== JUMLAH TOTAL ===
Total file konfigurasi: 179
```  

### Langkah 4 : Mencari File Konfigurasi dengan Kata Kunci Tertentu (pipeline)
Input :
```bash
echo -e "\n=== FILE YANG BERHUBUNGAN DENGAN NETWORK/SSH ===" | tee -a audit-ringkasan-2026-04-10.txt

find /etc -name "*.conf" 2>/dev/null | grep -E "network|ssh" | sort | tee -a audit-ringkasan-2026-04-10.txt

echo -e "\nJumlah file network/ssh: $(find /etc -name "*.conf" 2>/dev/null | grep -E "network|ssh" | wc -l)" | tee -a audit-ringkasan-2026-04-10.txt
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# echo -e "\n=== FILE YANG BERHUBUNGAN DENGAN NETWORK/SSH ===" | tee -a audit-ringkasan-2026-04-10.txt

=== FILE YANG BERHUBUNGAN DENGAN NETWORK/SSH ===
root@ubuntuser:~/praktikum-os/week07-bash# find /etc -name "*.conf" 2>/dev/null | grep -E "network|ssh" | sort | tee -a audit-ringkasan-2026-04-10.txt
/etc/modprobe.d/blacklist-rare-network.conf
/etc/sysctl.d/10-network-security.conf
/etc/systemd/networkd.conf
root@ubuntuser:~/praktikum-os/week07-bash# echo -e "\nJumlah file network/ssh: $(find /etc -name "*.conf" 2>/dev/null | grep -E "network|ssh" | wc -l)" | tee -a audit-ringkasan-2026-04-10.txt

Jumlah file network/ssh: 3
```  

### Langkah 5 : Menggunakan Command Substitution untuk Ringkasan
Input :
```bash
cat <<EOF > audit-final-2026-04-10.txt
==========================================
LAPORAN AUDIT KONFIGURASI SISTEM
==========================================
Waktu Audit : $(date '+%Y-%m-%d %H:%M:%S')
User        : $(whoami)
Hostname    : $(hostname)
==========================================

1. STATISTIK FILE KONFIGURASI
   Total file *.conf      : $(wc -l < audit-konfigurasi-2026-04-10.txt) file
   Total error saat scan  : $(wc -l < audit-error.log) error

2. DIREKTORI DENGAN FILE .conf TERBANYAK
$(find /etc -name "*.conf" 2>/dev/null | xargs dirname | sort | uniq -c | sort -rn | head -5)

3. CONTOH ISI SALAH SATU FILE KONFIGURASI
   (File: /etc/resolv.conf)
------------------------------------------
$(head -5 /etc/resolv.conf 2>/dev/null || echo "Tidak bisa membaca file")
------------------------------------------

==========================================
EOF

echo "✅ Laporan final selesai dibuat"
cat audit-final-2026-04-10.txt
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat <<EOF > audit-final-2026-04-10.txt
> ==========================================
LAPORAN AUDIT KONFIGURASI SISTEM
==========================================
Waktu Audit : $(date '+%Y-%m-%d %H:%M:%S')
User        : $(whoami)
Hostname    : $(hostname)
==========================================

1. STATISTIK FILE KONFIGURASI
   Total file *.conf      : $(wc -l < audit-konfigurasi-2026-04-10.txt) file
   Total error saat scan  : $(wc -l < audit-error.log) error

2. DIREKTORI DENGAN FILE .conf TERBANYAK
$(find /etc -name "*.conf" 2>/dev/null | xargs dirname | sort | uniq -c | sort -rn | head -5)

3. CONTOH ISI SALAH SATU FILE KONFIGURASI
   (File: /etc/resolv.conf)
------------------------------------------
$(head -5 /etc/resolv.conf 2>/dev/null || echo "Tidak bisa membaca file")
------------------------------------------

==========================================
> EOF
root@ubuntuser:~/praktikum-os/week07-bash# echo "✅ Laporan final selesai dibuat"
cat audit-final-2026-04-10.txt
✅ Laporan final selesai dibuat
==========================================
LAPORAN AUDIT KONFIGURASI SISTEM
==========================================
Waktu Audit : 2026-04-10 13:57:01
User        : root
Hostname    : ubuntuser
==========================================

1. STATISTIK FILE KONFIGURASI
   Total file *.conf      : 179 file
   Total error saat scan  : 0 error

2. DIREKTORI DENGAN FILE .conf TERBANYAK
     47 /etc/fonts/conf.d
     30 /etc
     14 /etc/fonts/conf.avail
     10 /etc/sysctl.d
     10 /etc/security

3. CONTOH ISI SALAH SATU FILE KONFIGURASI
   (File: /etc/resolv.conf)
------------------------------------------
# This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
# Do not edit.
#
# This file might be symlinked as /etc/resolv.conf. If you're looking at
# /etc/resolv.conf and seeing this text, you have followed the symlink.
------------------------------------------

==========================================
```  

### Langkah 6 : Membuat Analisis Singkat tentang Pentingnya Pemisahan stdout/stderr
Input :
```bash
cat <<'EOF' >> audit-final-2026-04-10.txt

4. ANALISIS PENTINGNYA PEMISAHAN STDOUT DAN STDERR
==================================================
Dalam audit sistem, pemisahan stdout (output normal) dan stderr (pesan error)
sangat penting karena:

1. DIAGNOSIS YANG AKURAT
   - Error seperti "Permission denied" menunjukkan file yang tidak bisa diakses
   - Tanpa pemisahan, error akan tercampur dengan hasil audit yang valid

2. PEMANTAUAN KEAMANAN
   - File yang tidak bisa dibaca mungkin butuh investigasi lebih lanjut
   - Bisa mengindikasikan masalah izin atau kebijakan keamanan

3. OTOMASI DAN REPORTING
   - Dengan 2> error.log, kita bisa mengabaikan error yang tidak relevan
   - Atau sebaliknya, fokus hanya pada error untuk troubleshooting

4. INTEGRITAS DATA
   - Output normal tetap bersih untuk dianalisis lebih lanjut
   - Error tidak mencemari data audit yang sebenarnya

Contoh dalam praktik ini:
- stdout (>) ke audit-konfigurasi-*.txt : daftar file valid
- stderr (2>) ke audit-error.log : pesan error (jika ada)

==================================================
EOF

echo "✅ Analisis ditambahkan ke laporan"
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat <<'EOF' >> audit-final-2026-04-10.txt
> 4. ANALISIS PENTINGNYA PEMISAHAN STDOUT DAN STDERR
==================================================
Dalam audit sistem, pemisahan stdout (output normal) dan stderr (pesan error)
sangat penting karena:

1. DIAGNOSIS YANG AKURAT
   - Error seperti "Permission denied" menunjukkan file yang tidak bisa diakses
   - Tanpa pemisahan, error akan tercampur dengan hasil audit yang valid

2. PEMANTAUAN KEAMANAN
   - File yang tidak bisa dibaca mungkin butuh investigasi lebih lanjut
   - Bisa mengindikasikan masalah izin atau kebijakan keamanan

3. OTOMASI DAN REPORTING
   - Dengan 2> error.log, kita bisa mengabaikan error yang tidak relevan
   - Atau sebaliknya, fokus hanya pada error untuk troubleshooting

4. INTEGRITAS DATA
   - Output normal tetap bersih untuk dianalisis lebih lanjut
   - Error tidak mencemari data audit yang sebenarnya

Contoh dalam praktik ini:
- stdout (>) ke audit-konfigurasi-*.txt : daftar file valid
- stderr (2>) ke audit-error.log : pesan error (jika ada)

==================================================
> EOF
root@ubuntuser:~/praktikum-os/week07-bash# echo "✅ Analisis ditambahkan ke laporan"
✅ Analisis ditambahkan ke laporan
```  

### Langkah 7 : Verifikasi Semua File Laporan
Input :
```bash
echo "=== ISI LENGKAP LAPORAN FINAL ==="
cat audit-final-2026-04-10.txt
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# echo "=== ISI LENGKAP LAPORAN FINAL ==="
cat audit-final-2026-04-10.txt
=== ISI FILE SEKARANG ===
==========================================
LAPORAN AUDIT KONFIGURASI SISTEM
==========================================
Waktu Audit : 2026-04-10 13:57:01
User        : root
Hostname    : ubuntuser
==========================================

1. STATISTIK FILE KONFIGURASI
   Total file *.conf      : 179 file
   Total error saat scan  : 0 error

2. DIREKTORI DENGAN FILE .conf TERBANYAK
     47 /etc/fonts/conf.d
     30 /etc
     14 /etc/fonts/conf.avail
     10 /etc/sysctl.d
     10 /etc/security

3. CONTOH ISI SALAH SATU FILE KONFIGURASI
   (File: /etc/resolv.conf)
------------------------------------------
# This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
# Do not edit.
#
# This file might be symlinked as /etc/resolv.conf. If you're looking at
# /etc/resolv.conf and seeing this text, you have followed the symlink.
------------------------------------------

4. ANALISIS PENTINGNYA PEMISAHAN STDOUT DAN STDERR
==================================================
Dalam audit sistem, pemisahan stdout (output normal) dan stderr (pesan error)
sangat penting karena:

1. DIAGNOSIS YANG AKURAT
   - Error seperti "Permission denied" menunjukkan file yang tidak bisa diakses
   - Tanpa pemisahan, error akan tercampur dengan hasil audit yang valid

2. PEMANTAUAN KEAMANAN
   - File yang tidak bisa dibaca mungkin butuh investigasi lebih lanjut
   - Bisa mengindikasikan masalah izin atau kebijakan keamanan

3. OTOMASI DAN REPORTING
   - Dengan 2> error.log, kita bisa mengabaikan error yang tidak relevan
   - Atau sebaliknya, fokus hanya pada error untuk troubleshooting

4. INTEGRITAS DATA
   - Output normal tetap bersih untuk dianalisis lebih lanjut
   - Error tidak mencemari data audit yang sebenarnya

Contoh dalam praktik ini:
- stdout (>) ke audit-konfigurasi-*.txt : daftar file valid
- stderr (2>) ke audit-error.log : pesan error (jika ada)

==================================================
```  

## Tugas Praktikum 3 — Mini Health Check Harian Server
### Langkah 1 : Buat Script Daily Health Check
Input :
```bash
cd ~/praktikum-os/week07-bash

cat <<'EOF' > bin/daily-healthcheck
#!/usr/bin/env bash

# ============================================
# SCRIPT: daily-healthcheck
# FUNGSI: Health check harian server
# ============================================

# Konfigurasi
LOG_DIR="$HOME/praktikum-os/week07-bash/logs"
TGL=$(date +%F)
LOG_FILE="$LOG_DIR/healthcheck-$TGL.log"

# Buat direktori logs jika belum ada
mkdir -p "$LOG_DIR"

# Fungsi untuk menampilkan header
show_header() {
    echo "=========================================="
    echo "     DAILY HEALTH CHECK SERVER"
    echo "=========================================="
}

# Mulai health check
{
    show_header
    echo ""
    
    # 1. Tanggal dan Waktu
    echo " [1] TANGGAL & WAKTU"
    echo "    $(date '+%Y-%m-%d %H:%M:%S')"
    echo ""
    
    # 2. Hostname
    echo "  [2] HOSTNAME"
    echo "    $(hostname)"
    echo ""
    
    # 3. User Aktif
    echo " [3] USER AKTIF"
    echo "    User: $(whoami)"
    echo "    Shell: $SHELL"
    echo ""
    
    # 4. Uptime
    echo "  [4] UPTIME"
    echo "    $(uptime -p)"
    echo ""
    
    # 5. Penggunaan Memory
    echo " [5] PENGGUNAAN MEMORY"
    free -h | grep -E "Mem|Swap" | while read line; do
        echo "    $line"
    done
    echo ""
    
    # 6. Penggunaan Filesystem Root
    echo " [6] PENGGUNAAN FILESYSTEM ROOT (/)" 
    df -h / | tail -1 | awk '{print "    Size: " $2 " | Used: " $3 " | Avail: " $4 " | Use%: " $5}'
    echo ""
    
    # 7. 10 Baris Terakhir History (yang relevan dengan pengecekan)
    echo " [7] 10 PERINTAH TERAKHIR (history)"
    echo "    (Perintah yang berhubungan dengan monitoring)"
    history | tail -20 | grep -E "df|free|uptime|ps|top|htop|systemctl" | tail -10 | while read line; do
        echo "    $line"
    done
    echo ""
    
    # 8. Proses yang menggunakan CPU tinggi (top 3)
    echo " [8] 3 PROSES DENGAN CPU TERTINGGI"
    ps aux --sort=-%cpu | head -4 | tail -3 | while read line; do
        echo "    $line"
    done
    echo ""
    
    # 9. Cek service penting (opsional)
    echo " [9] STATUS SERVICE PENTING"
    for service in ssh cron; do
        if systemctl is-active --quiet "$service" 2>/dev/null; then
            echo "     $service: running"
        else
            echo "     $service: not running atau tidak tersedia"
        fi
    done
    echo ""
    
    show_header
    echo " Health check selesai: $(date '+%Y-%m-%d %H:%M:%S')"
    
} | tee -a "$LOG_FILE"

# Cek status exit
if [ $? -eq 0 ]; then
    echo ""
    echo " Laporan tersimpan di: $LOG_FILE"
else
    echo " Terjadi error saat menjalankan health check"
    exit 1
fi
EOF

chmod +x bin/daily-healthcheck
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat <<'EOF' > bin/daily-healthche
ck
> #!/usr/bin/env bash
>
# ============================================
# SCRIPT: daily-healthcheck
# FUNGSI: Health check harian server
# ============================================

# Konfigurasi
LOG_DIR="$HOME/praktikum-os/week07-bash/logs"
TGL=$(date +%F)
LOG_FILE="$LOG_DIR/healthcheck-$TGL.log"

# Buat direktori logs jika belum ada
mkdir -p "$LOG_DIR"

# Fungsi untuk menampilkan header
show_header() {
    echo "=========================================="
    echo "     DAILY HEALTH CHECK SERVER"
    echo "=========================================="
}

# Mulai health check
{
    show_header
    echo ""

>     # 1. Tanggal dan Waktu
    echo " [1] TANGGAL & WAKTU"
    echo "    $(date '+%Y-%m-%d %H:%M:%S')"
    echo ""

>   # 2. Hostname
    echo " [2] HOSTNAME"
    echo "    $(hostname)"
    echo ""

>  # 3. User Aktif
    echo " [3] USER AKTIF"
    echo "    User: $(whoami)"
    echo "    Shell: $SHELL"
    echo ""

> # 4. Uptime
    echo " [4] UPTIME"
    echo "    $(uptime -p)"
    echo ""

    # 5. Penggunaan Memory
    echo " [5] PENGGUNAAN MEMORY"
    free -h | grep -E "Mem|Swap" | while read line; do
        echo "    $line"
    done
    echo ""

    # 6. Penggunaan Filesystem Root
    echo " [6] PENGGUNAAN FILESYSTEM ROOT (/)"
    df -h / | tail -1 | awk '{print "    Size: " $2 " | Used: " $3 " | Avail
: " $4 " | Use%: " $5}'
    echo ""

    # 7. 10 Baris Terakhir History (yang relevan dengan pengecekan)
    echo " [7] 10 PERINTAH TERAKHIR (history)"
    echo "    (Perintah yang berhubungan dengan monitoring)"
    history | tail -20 | grep -E "df|free|uptime|ps|top|htop|systemctl" | ta
il -10 | while read line; do
        echo "    $line"
    done
    echo ""

>  # 8. Proses yang menggunakan CPU tinggi (top 3)
    echo " [8] 3 PROSES DENGAN CPU TERTINGGI"
    ps aux --sort=-%cpu | head -4 | tail -3 | while read line; do
        echo "    $line"
    done
    echo ""

    # 9. Cek service penting (opsional)
    echo "🔧 [9] STATUS SERVICE PENTING"
    for service in ssh cron; do
        if systemctl is-active --quiet "$service" 2>/dev/null; then
            echo "     $service: running"
        else
            echo "     $service: not running atau tidak tersedia"
        fi
    done
    echo ""

    show_header
    echo " Health check selesai: $(date '+%Y-%m-%d %H:%M:%S')"

} | tee -a "$LOG_FILE"

# Cek status exit
if [ $? -eq 0 ]; then
    echo ""
    echo " Laporan tersimpan di: $LOG_FILE"
else
    echo " Terjadi error saat menjalankan health check"
    exit 1
fi
> EOF
root@ubuntuser:~/praktikum-os/week07-bash# chmod +x bin/daily-healthcheck
``` 

### Langkah 2 : Jalankan Script Health Check
Input :
```bash
daily-healthcheck
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# daily-healthcheck
==========================================
     DAILY HEALTH CHECK SERVER
==========================================

 [1] TANGGAL & WAKTU
    2026-04-11 02:16:02

 [2] HOSTNAME
    ubuntuser

 [3] USER AKTIF
    User: root
    Shell: /bin/bash

 [4] UPTIME
    up 17 minutes

 [5] PENGGUNAAN MEMORY
    Mem:           3.3Gi       352Mi       2.9Gi       1.0Mi       245Mi       3.0Gi
    Swap:             0B          0B          0B

 [6] PENGGUNAAN FILESYSTEM ROOT (/)
    Size: 50G | Used: 3.5G | Avail: 44G | Use%: 8%

 [7] 10 PERINTAH TERAKHIR (history)
    (Perintah yang berhubungan dengan monitoring)

 [8] 3 PROSES DENGAN CPU TERTINGGI
    root        1193  166  0.1  11016  4632 pts/2    R+   02:16   0:00 ps aux --sort=-%cpu
    root        1176  5.8  0.0   7340  2160 pts/2    S+   02:16   0:00 bash /root/praktikum-os/week07-bash/bin/daily-healthcheck
    root        1173  4.5  0.1   7340  3708 pts/2    S+   02:16   0:00 bash /root/praktikum-os/week07-bash/bin/daily-healthcheck

 [9] STATUS SERVICE PENTING
     ssh: running
     cron: running

==========================================
     DAILY HEALTH CHECK SERVER
==========================================
 Health check selesai: 2026-04-11 02:16:02

 Laporan tersimpan di: /root/praktikum-os/week07-bash/logs/healthcheck-2026-04-11.log
``` 

### Langkah 3 : Uji Script dari Direktori Berbeda
Input :
```bash
cd /tmp

daily-healthcheck

cd ~/praktikum-os/week07-bash
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cd /tmp

daily-healthcheck

cd ~/praktikum-os/week07-bash
==========================================
     DAILY HEALTH CHECK SERVER
==========================================

 [1] TANGGAL & WAKTU
    2026-04-11 02:19:53

[2] HOSTNAME
    ubuntuser

 [3] USER AKTIF
    User: root
    Shell: /bin/bash

[4] UPTIME
    up 21 minutes

 [5] PENGGUNAAN MEMORY
    Mem:           3.3Gi       352Mi       2.9Gi       1.0Mi       246Mi       3.0Gi
    Swap:             0B          0B          0B

 [6] PENGGUNAAN FILESYSTEM ROOT (/)
    Size: 50G | Used: 3.5G | Avail: 44G | Use%: 8%

 [7] 10 PERINTAH TERAKHIR (history)
    (Perintah yang berhubungan dengan monitoring)

 [8] 3 PROSES DENGAN CPU TERTINGGI
    root        1233  200  0.1  11016  4624 pts/2    R+   02:19   0:00 ps aux --sort=-%cpu
    root        1216  9.0  0.0   7340  2120 pts/2    S+   02:19   0:00 bash /root/praktikum-os/week07-bash/bin/daily-healthcheck
    root        1217  9.0  0.0   5692  1988 pts/2    S+   02:19   0:00 tee -a /root/praktikum-os/week07-bash/logs/healthcheck-2026-04-11.log

🔧 [9] STATUS SERVICE PENTING
     ssh: running
     cron: running

==========================================
     DAILY HEALTH CHECK SERVER
==========================================
 Health check selesai: 2026-04-11 02:19:53

 Laporan tersimpan di: /root/praktikum-os/week07-bash/logs/healthcheck-2026-04-11.log
``` 

### Langkah 4 : Buat Alias untuk Mempermudah
Input :
```bash
cat <<'EOF' >> ~/.bashrc

# Alias untuk health check
alias hc='daily-healthcheck'
alias hclog='tail -20 ~/praktikum-os/week07-bash/logs/healthcheck-*.log | tail -20'
EOF

source ~/.bashrc

echo "=== UJI ALIAS hc ==="
hc 2>&1 | head -10
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat <<'EOF' >> ~/.bashrc
> # Alias untuk health check
alias hc='daily-healthcheck'
alias hclog='tail -20 ~/praktikum-os/week07-bash/logs/healthcheck-*.log | tail -20'
> EOF
root@ubuntuser:~/praktikum-os/week07-bash# source ~/.bashrc
root@ubuntuser:~/praktikum-os/week07-bash# echo "=== UJI ALIAS hc ==="
hc 2>&1 | head -10
=== UJI ALIAS hc ===
==========================================
     DAILY HEALTH CHECK SERVER
==========================================

 [1] TANGGAL & WAKTU
    2026-04-11 02:22:36

[2] HOSTNAME
    ubuntuser

``` 

### Langkah 5 : Buat Dokumentasi Script
Input :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat <<'EOF' > healthcheck-documentation.txt
> ==========================================
 DOKUMENTASI DAILY-HEALTHCHECK
==========================================

LOKASI SCRIPT
   ~/praktikum-os/week07-bash/bin/daily-healthcheck

FUNGSI TIAP BAGIAN
------------------------------------------
1. TANGGAL & WAKTU
   - Menampilkan waktu eksekusi health check
   - Berguna untuk tracking kapan pengecekan dilakukan

2. HOSTNAME
   - Memastikan sedang di server yang benar
   - Mencegah kesalahan maintenance di server salah

3. USER AKTIF
   - Mengetahui siapa yang menjalankan health check
   - Menggunakan environment variable $USER dan $SHELL

> 4. UPTIME
   - Mengetahui sudah berapa lama server berjalan
   - Indikator apakah server baru restart

5. PENGGUNAAN MEMORY
   - Memonitor RAM dan Swap usage
   - Deteksi dini kebocoran memory

6. PENGGUNAAN FILESYSTEM ROOT
   - Memonitor kapasitas disk partisi root
   - Mencegah disk full yang bisa ganggu service

7. 10 PERINTAH TERAKHIR (history)
   - Melihat perintah monitoring sebelumnya
   - Membantu rekap aktivitas administrator

8. 3 PROSES DENGAN CPU TERTINGGI
   - Identifikasi proses yang boros CPU
   - Untuk investigasi performa

9. STATUS SERVICE PENTING
   - Memastikan service critical berjalan
   - ssh: akses remote, cron: job terjadwal

> KONSEP BASH YANG DIGUNAKAN
------------------------------------------
Environment Variable: $HOME, $SHELL, $USER
PATH: Script di bin/ bisa dipanggil dari mana saja
Alias: hc untuk daily-healthcheck
History: Mengambil perintah dari history
tee: Output ke terminal dan file sekaligus
Penanganan error: Cek exit status dengan $?
> OUTPUT
------------------------------------------
Terminal    : Menampilkan hasil health check
Log file    : ~/praktikum-os/week07-bash/logs/healthcheck-YYYY-MM-DD.log

==========================================
> EOF
```
Output :
```bash
root@ubuntuser:~/praktikum-os/week07-bash# cat healthcheck-documentation.txt
==========================================
 DOKUMENTASI DAILY-HEALTHCHECK
==========================================

LOKASI SCRIPT
   ~/praktikum-os/week07-bash/bin/daily-healthcheck

FUNGSI TIAP BAGIAN
------------------------------------------
1. TANGGAL & WAKTU
   - Menampilkan waktu eksekusi health check
   - Berguna untuk tracking kapan pengecekan dilakukan

2. HOSTNAME
   - Memastikan sedang di server yang benar
   - Mencegah kesalahan maintenance di server salah

3. USER AKTIF
   - Mengetahui siapa yang menjalankan health check
   - Menggunakan environment variable $USER dan $SHELL


4. UPTIME
   - Mengetahui sudah berapa lama server berjalan
   - Indikator apakah server baru restart

5. PENGGUNAAN MEMORY
   - Memonitor RAM dan Swap usage
   - Deteksi dini kebocoran memory

6. PENGGUNAAN FILESYSTEM ROOT
   - Memonitor kapasitas disk partisi root
   - Mencegah disk full yang bisa ganggu service

7. 10 PERINTAH TERAKHIR (history)
   - Melihat perintah monitoring sebelumnya
   - Membantu rekap aktivitas administrator

8. 3 PROSES DENGAN CPU TERTINGGI
   - Identifikasi proses yang boros CPU
   - Untuk investigasi performa

9. STATUS SERVICE PENTING
   - Memastikan service critical berjalan
   - ssh: akses remote, cron: job terjadwal


ONSEP BASH YANG DIGUNAKAN
------------------------------------------
Environment Variable: $HOME, $SHELL, $USER
PATH: Script di bin/ bisa dipanggil dari mana saja
Alias: hc untuk daily-healthcheck
History: Mengambil perintah dari history
tee: Output ke terminal dan file sekaligus
Penanganan error: Cek exit status dengan $?
OUTPUT
------------------------------------------
Terminal    : Menampilkan hasil health check
Log file    : ~/praktikum-os/week07-bash/logs/healthcheck-YYYY-MM-DD.log

==========================================
``` 


## Tugas Praktikum 4 — Penanganan File dengan Nama Kompleks dan Arsip Aman
### Langkah 1 : Buat File Contoh dengan Nama Bervariasi
Input :
```bash
cd ~/praktikum-os/week07-bash

mkdir -p tugas4-sample tugas4-backup

cd tugas4-sample

echo "=== MEMBUAT FILE CONTOH DENGAN NAMA BERBEDA ==="

touch "laporan keuangan april.csv"
touch "backup server 2026.tar"

touch "config[production].ini"
touch "data[2026-04-10].json"
touch "log_backup_(server).txt"

touch access-log-01.txt
touch access-log-02.txt
touch access-log-03.txt
touch error-log-01.txt
touch error-log-02.txt
touch error-log-03.txt

touch "this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log"

touch user_data_2024.csv
touch user_data_2025.csv
touch user_data_2026.csv

echo ""
echo "✅ File contoh telah dibuat"
echo ""

echo "=== DAFTAR FILE DI tugas4-sample ==="
ls -la
```
Output :
```bash
=== MEMBUAT FILE CONTOH DENGAN NAMA BERBEDA ===

✅ File contoh telah dibuat

=== DAFTAR FILE DI tugas4-sample ===
total 8
drwxr-xr-x 2 root root 4096 Apr 11 02:39  .
drwxr-xr-x 9 root root 4096 Apr 11 02:39  ..
-rw-r--r-- 1 root root    0 Apr 11 02:39  access-log-01.txt
-rw-r--r-- 1 root root    0 Apr 11 02:39  access-log-02.txt
-rw-r--r-- 1 root root    0 Apr 11 02:39  access-log-03.txt
-rw-r--r-- 1 root root    0 Apr 11 02:39 'backup server 2026.tar'
-rw-r--r-- 1 root root    0 Apr 11 02:39 'config[production].ini'
-rw-r--r-- 1 root root    0 Apr 11 02:39 'data[2026-04-10].json'
-rw-r--r-- 1 root root    0 Apr 11 02:39  error-log-01.txt
-rw-r--r-- 1 root root    0 Apr 11 02:39  error-log-02.txt
-rw-r--r-- 1 root root    0 Apr 11 02:39  error-log-03.txt
-rw-r--r-- 1 root root    0 Apr 11 02:39 'laporan keuangan april.csv'
-rw-r--r-- 1 root root    0 Apr 11 02:39 'log_backup_(server).txt'
-rw-r--r-- 1 root root    0 Apr 11 02:39  this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log
-rw-r--r-- 1 root root    0 Apr 11 02:39  user_data_2024.csv
-rw-r--r-- 1 root root    0 Apr 11 02:39  user_data_2025.csv
-rw-r--r-- 1 root root    0 Apr 11 02:39  user_data_2026.csv
```   

### Langkah 2 : Demonstrasi Perbedaan Quoting (Tanpa vs Dengan Quoting)
Input :
```bash
echo "=========================================="
echo "DEMONSTRASI PERBEDAAN QUOTING"
echo "=========================================="
echo ""

FILE_SPASI="laporan keuangan april.csv"

echo "1️. TANPA QUOTING (SALAH)"
echo "   Perintah: ls -la $FILE_SPASI"
echo "   Hasil:"
ls -la $FILE_SPASI 2>&1
echo "Error: Bash memecah jadi 4 argumen terpisah!"
echo ""

echo "2️. DENGAN QUOTING GANDA (BENAR)"
echo "   Perintah: ls -la \"$FILE_SPASI\""
echo "   Hasil:"
ls -la "$FILE_SPASI"
echo "Berhasil: Seluruh nama file dianggap 1 argumen!"
echo ""

FILE_KURUNG="config[production].ini"

echo "3️. TANPA QUOTING untuk file dengan tanda kurung"
echo "   Perintah: ls $FILE_KURUNG"
ls $FILE_KURUNG 2>&1
echo "Error: Tanda [ ] diinterpretasikan sebagai wildcard!"
echo ""

echo "4️. DENGAN QUOTING atau ESCAPE"
echo "   Perintah: ls \"$FILE_KURUNG\""
ls "$FILE_KURUNG"
echo "Berhasil dengan double quote"
echo ""

echo "5️. MENGGUNAKAN ESCAPE (backslash)"
echo "   Perintah: ls config\[production\].ini"
ls config\[production\].ini
echo "Berhasil dengan escape character"
echo ""
```
Output :
```bash
==========================================
DEMONSTRASI PERBEDAAN QUOTING
==========================================

1️. TANPA QUOTING (SALAH)
   Perintah: ls -la laporan keuangan april.csv
   Hasil:
ls: cannot access 'laporan': No such file or directory
ls: cannot access 'keuangan': No such file or directory
ls: cannot access 'april.csv': No such file or directory
Error: Bash memecah jadi 4 argumen terpisah!

2️. DENGAN QUOTING GANDA (BENAR)
   Perintah: ls -la "laporan keuangan april.csv"
   Hasil:
-rw-r--r-- 1 root root 0 Apr 11 02:39 'laporan keuangan april.csv'
Berhasil: Seluruh nama file dianggap 1 argumen!

3️. TANPA QUOTING untuk file dengan tanda kurung
   Perintah: ls config[production].ini
'config[production].ini'
Error: Tanda [ ] diinterpretasikan sebagai wildcard!

4️. DENGAN QUOTING atau ESCAPE
   Perintah: ls "config[production].ini"
'config[production].ini'
Berhasil dengan double quote

5️. MENGGUNAKAN ESCAPE (backslash)
   Perintah: ls config\[production\].ini
'config[production].ini'
Berhasil dengan escape character

```    

### Langkah 3 : Preview Wildcard dengan echo (Praktik Aman)
Input :
```bash
echo ""
echo "=========================================="
echo "PREVIEW WILDCARD DENGAN echo (PRAKTIK AMAN)"
echo "=========================================="
echo ""

echo "Pola 1: *.txt"
echo "   Preview:"
echo *.txt
echo "   Jumlah file: $(echo *.txt | wc -w) file"
echo ""

echo "Pola 2: access-log-*.txt"
echo "   Preview:"
echo access-log-*.txt
echo "   Jumlah file: $(echo access-log-*.txt | wc -w) file"
echo ""

echo "Pola 3: *-log-*.txt"
echo "   Preview:"
echo *-log-*.txt
echo "   Jumlah file: $(echo *-log-*.txt | wc -w) file"
echo ""

echo "Pola 4: user_data_202?.csv"
echo "   Preview:"
echo user_data_202?.csv
echo "   Jumlah file: $(echo user_data_202?.csv | wc -w) file"
echo ""

echo "Pola 5: *[2026]*"
echo "   Preview:"
echo *[2026]* 2>&1
echo "Perhatikan: wildcard dengan [ ] bisa error jika tidak ada yang cocok!"
echo ""
```
Output :
```bash
==========================================
PREVIEW WILDCARD DENGAN echo (PRAKTIK AMAN)
==========================================

Pola 1: *.txt
   Preview:
access-log-01.txt access-log-02.txt access-log-03.txt error-log-01.txt error-log-02.txt error-log-03.txt log_backup_(server).txt
   Jumlah file: 7 file

Pola 2: access-log-*.txt
   Preview:
access-log-01.txt access-log-02.txt access-log-03.txt
   Jumlah file: 3 file

Pola 3: *-log-*.txt
   Preview:
access-log-01.txt access-log-02.txt access-log-03.txt error-log-01.txt error-log-02.txt error-log-03.txt
   Jumlah file: 6 file

Pola 4: user_data_202?.csv
   Preview:
user_data_2024.csv user_data_2025.csv user_data_2026.csv
   Jumlah file: 3 file

Pola 5: *[2026]*
   Preview:
access-log-01.txt access-log-02.txt access-log-03.txt backup server 2026.tar data[2026-04-10].json error-log-01.txt error-log-02.txt error-log-03.txt user_data_2024.csv user_data_2025.csv user_data_2026.csv
Perhatikan: wildcard dengan [ ] bisa error jika tidak ada yang cocok!

```   
 
### Langkah 4 : Salin File ke Backup dengan Nama yang Aman
Input :
```bash
echo ""
echo "=========================================="
echo "SALIN FILE KE DIREKTORI BACKUP"
echo "=========================================="
echo ""

BACKUP_DIR="$HOME/praktikum-os/week07-bash/tugas4-backup"
SOURCE_DIR="$HOME/praktikum-os/week07-bash/tugas4-sample"

TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BACKUP_SUBDIR="$BACKUP_DIR/backup_$TIMESTAMP"
mkdir -p "$BACKUP_SUBDIR"

echo "Backup akan disimpan di: $BACKUP_SUBDIR"
echo ""

echo "1️. Menyalin file dengan spasi (menggunakan quote):"
cp -v "laporan keuangan april.csv" "$BACKUP_SUBDIR/"
echo ""

echo "2️. Menyalin file dengan tanda kurung (menggunakan escape):"
cp -v config\[production\].ini "$BACKUP_SUBDIR/"
echo ""

echo "3️. Menyalin file dengan wildcard (sudah dipreview):"
cp -v access-log-*.txt "$BACKUP_SUBDIR/"
echo ""

echo "4️. Menyalin file dengan nama panjang:"
cp -v "this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log" "$BACKUP_SUBDIR/"
echo ""

echo "5️. Menyalin semua file .csv:"
cp -v *.csv "$BACKUP_SUBDIR/"
echo ""

echo "6️. Menyalin file dengan nama berkarakter khusus menggunakan variabel:"
FILE_SPECIAL="log_backup_(server).txt"
cp -v "$FILE_SPECIAL" "$BACKUP_SUBDIR/"
echo ""

echo "Semua file berhasil disalin!"
echo ""

echo "=== ISI DIREKTORI BACKUP ==="
ls -la "$BACKUP_SUBDIR/"
```
Output :
```bash
==========================================
SALIN FILE KE DIREKTORI BACKUP
==========================================

Backup akan disimpan di: /root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511

1️. Menyalin file dengan spasi (menggunakan quote):
'laporan keuangan april.csv' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/laporan keuangan april.csv'

2️. Menyalin file dengan tanda kurung (menggunakan escape):
'config[production].ini' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/config[production].ini'

3️. Menyalin file dengan wildcard (sudah dipreview):
'access-log-01.txt' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/access-log-01.txt'
'access-log-02.txt' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/access-log-02.txt'
'access-log-03.txt' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/access-log-03.txt'

4️. Menyalin file dengan nama panjang:
'this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log'

5️. Menyalin semua file .csv:
'laporan keuangan april.csv' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/laporan keuangan april.csv'
'user_data_2024.csv' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/user_data_2024.csv'
'user_data_2025.csv' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/user_data_2025.csv'
'user_data_2026.csv' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/user_data_2026.csv'

6️. Menyalin file dengan nama berkarakter khusus menggunakan variabel:
'log_backup_(server).txt' -> '/root/praktikum-os/week07-bash/tugas4-backup/backup_20260411_024511/log_backup_(server).txt'

Semua file berhasil disalin!

=== ISI DIREKTORI BACKUP ===
total 8
drwxr-xr-x 2 root root 4096 Apr 11 02:45  .
drwxr-xr-x 3 root root 4096 Apr 11 02:45  ..
-rw-r--r-- 1 root root    0 Apr 11 02:45  access-log-01.txt
-rw-r--r-- 1 root root    0 Apr 11 02:45  access-log-02.txt
-rw-r--r-- 1 root root    0 Apr 11 02:45  access-log-03.txt
-rw-r--r-- 1 root root    0 Apr 11 02:45 'config[production].ini'
-rw-r--r-- 1 root root    0 Apr 11 02:45 'laporan keuangan april.csv'
-rw-r--r-- 1 root root    0 Apr 11 02:45 'log_backup_(server).txt'
-rw-r--r-- 1 root root    0 Apr 11 02:45  this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log
-rw-r--r-- 1 root root    0 Apr 11 02:45  user_data_2024.csv
-rw-r--r-- 1 root root    0 Apr 11 02:45  user_data_2025.csv
-rw-r--r-- 1 root root    0 Apr 11 02:45  user_data_2026.csv
```   

### Langkah 5 : Buat Arsip tar.gz dari Hasil Backup
Input :
```bash
echo ""
echo "=========================================="
echo "MEMBUAT ARSIP TAR.GZ"
echo "=========================================="
echo ""

cd "$BACKUP_DIR"

ARCHIVE_NAME="backup_archive_$TIMESTAMP.tar.gz"
ARCHIVE_PATH="$BACKUP_DIR/$ARCHIVE_NAME"

echo "Membuat arsip: $ARCHIVE_NAME"
tar -czf "$ARCHIVE_PATH" "backup_$TIMESTAMP/"

if [ $? -eq 0 ]; then
    echo "Arsip berhasil dibuat!"
    echo ""
    echo "=== INFORMASI ARSIP ==="
    ls -lh "$ARCHIVE_PATH"
    echo ""
    echo "=== ISI ARSIP (daftar file) ==="
    tar -tzf "$ARCHIVE_PATH" | head -15
else
    echo "Gagal membuat arsip"
fi

cd ~/praktikum-os/week07-bash
```
Output :
```bash
==========================================
MEMBUAT ARSIP TAR.GZ
==========================================

Membuat arsip: backup_archive_20260411_024511.tar.gz
Arsip berhasil dibuat!

=== INFORMASI ARSIP ===
-rw-r--r-- 1 root root 376 Apr 11 02:47 /root/praktikum-os/week07-bash/tugas4-backup/backup_archive_20260411_024511.tar.gz

=== ISI ARSIP (daftar file) ===
backup_20260411_024511/
backup_20260411_024511/user_data_2025.csv
backup_20260411_024511/this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log
backup_20260411_024511/user_data_2024.csv
backup_20260411_024511/access-log-01.txt
backup_20260411_024511/access-log-03.txt
backup_20260411_024511/laporan keuangan april.csv
backup_20260411_024511/user_data_2026.csv
backup_20260411_024511/config[production].ini
backup_20260411_024511/access-log-02.txt
backup_20260411_024511/log_backup_(server).txt
```   

### Langkah 6 : Simpan Riwayat Perintah ke File
Input :
```bash
echo ""
echo "=========================================="
echo "MENYIMPAN RIWAYAT PERINTAH"
echo "=========================================="
echo ""

cat <<EOF > riwayat-arsip.txt
==========================================
RIWAYAT PERINTAH TUGAS PRAKTIKUM 4
==========================================
Tanggal: $(date '+%Y-%m-%d %H:%M:%S')
User: $(whoami)
Hostname: $(hostname)
Workspace: $(pwd)

------------------------------------------
PERINTAH-PERINTAH YANG DIGUNAKAN
------------------------------------------

1. MEMBUAT FILE CONTOH:
   touch "laporan keuangan april.csv"
   touch "backup server 2026.tar"
   touch "config[production].ini"
   touch "data[2026-04-10].json"

2. DEMONSTRASI QUOTING:
   # Tanpa quote (SALAH)
   ls -la laporan keuangan april.csv
   
   # Dengan quote (BENAR)
   ls -la "laporan keuangan april.csv"
   
   # Dengan escape
   ls config\[production\].ini

3. PREVIEW WILDCARD (PRAKTIK AMAN):
   echo *.txt
   echo access-log-*.txt
   echo user_data_202?.csv

4. COPY FILE DENGAN QUOTING:
   cp -v "laporan keuangan april.csv" "\$BACKUP_DIR/"
   cp -v config\[production\].ini "\$BACKUP_DIR/"

5. COPY DENGAN WILDCARD:
   cp -v access-log-*.txt "\$BACKUP_DIR/"

6. MEMBUAT ARSIP TAR.GZ:
   tar -czf "backup_archive_\$TIMESTAMP.tar.gz" "backup_\$TIMESTAMP/"

7. MEMERIKSA ISI ARSIP:
   tar -tzf backup_archive_*.tar.gz

------------------------------------------
PENTING: SELALU GUNAKAN QUOTING UNTUK VARIABEL
YANG BERISI PATH ATAU NAMA FILE!
------------------------------------------
Contoh yang benar: cp "\$file_asli" "\$file_tujuan"
Contoh yang salah: cp \$file_asli \$file_tujuan

==========================================
EOF

cat riwayat-arsip.txt
```
Output :
```bash
==========================================
MENYIMPAN RIWAYAT PERINTAH
==========================================

==========================================
RIWAYAT PERINTAH TUGAS PRAKTIKUM 4
==========================================
Tanggal: 2026-04-11 02:49:58
User: root
Hostname: ubuntuser
Workspace: /root/praktikum-os/week07-bash

------------------------------------------
PERINTAH-PERINTAH YANG DIGUNAKAN
------------------------------------------

1. MEMBUAT FILE CONTOH:
   touch "laporan keuangan april.csv"
   touch "backup server 2026.tar"
   touch "config[production].ini"
   touch "data[2026-04-10].json"

2. DEMONSTRASI QUOTING:
   # Tanpa quote (SALAH)
   ls -la laporan keuangan april.csv

   # Dengan quote (BENAR)
   ls -la "laporan keuangan april.csv"

   # Dengan escape
   ls config\[production\].ini

3. PREVIEW WILDCARD (PRAKTIK AMAN):
   echo *.txt
   echo access-log-*.txt
   echo user_data_202?.csv

4. COPY FILE DENGAN QUOTING:
   cp -v "laporan keuangan april.csv" "$BACKUP_DIR/"
   cp -v config\[production\].ini "$BACKUP_DIR/"

5. COPY DENGAN WILDCARD:
   cp -v access-log-*.txt "$BACKUP_DIR/"

6. MEMBUAT ARSIP TAR.GZ:
   tar -czf "backup_archive_$TIMESTAMP.tar.gz" "backup_$TIMESTAMP/"

7. MEMERIKSA ISI ARSIP:
   tar -tzf backup_archive_*.tar.gz

------------------------------------------
PENTING: SELALU GUNAKAN QUOTING UNTUK VARIABEL
YANG BERISI PATH ATAU NAMA FILE!
------------------------------------------
Contoh yang benar: cp "$file_asli" "$file_tujuan"
Contoh yang salah: cp $file_asli $file_tujuan

==========================================
```    

### Langkah 7 : Refleksi Pentingnya Quoting
Input :
```bash
echo ""
echo "=========================================="
echo "REFLEKSI PENTINGNYA QUOTING DI BASH"
echo "=========================================="
echo ""

cat <<'EOF' > refleksi-quoting.txt
==========================================
REFLEKSI: MENGAPA QUOTING SANGAT PENTING?
==========================================

1. SPASI DALAM NAMA FILE
   Tanpa quote: Bash memecah nama file menjadi beberapa argumen
   Contoh: "laporan keuangan.txt" → laporan, keuangan.txt (2 argumen!)
   Dengan quote: Seluruh nama dianggap 1 argumen

2. KARAKTER SPECIAL ( *, ?, [, ], (, ), &, ;, $, !, `, | )
   Tanpa quote: Karakter ini diinterpretasikan oleh shell
   Contoh: config[prod].ini → [ ] dianggap wildcard pattern
   Dengan quote: Karakter dianggap literal (teks biasa)

3. VARIABEL YANG MENGANDUNG PATH
   Tanpa quote: Jika path mengandung spasi, akan error
   Contoh: $FILE="My Documents/file.txt"
   cp $FILE backup/ → error karena "My" dan "Documents/" terpisah
   Dengan quote: cp "$FILE" backup/ → bekerja

4. KEAMANAN (SECURITY)
   Tanpa quote: Rentan terhadap command injection
   Contoh: nama_file="file.txt; rm -rf /"
   cat $nama_file → bisa menjalankan perintah berbahaya
   Dengan quote: cat "$nama_file" → aman

5. COMMAND SUBSTITUTION
   Tanpa quote: Hasil substitution bisa pecah karena spasi
   Dengan quote: $(command) tetap utuh sebagai 1 argumen

==========================================
PRAKTIK TERBAIK (BEST PRACTICE)
==========================================

SELALU gunakan double quote untuk variabel:
   cp "$source" "$destination"
   echo "User: $USER"

Gunakan single quote untuk teks literal:
   echo 'Karakter $special @tidak &diekspansi'

Gunakan backslash untuk escape karakter tunggal:
   cp file\ dengan\ spasi.txt backup/

PREVIEW wildcard dengan echo sebelum perintah berbahaya:
   echo rm *.log  (lihat dulu filenya)
   rm *.log      (langsung hapus tanpa lihat)

==========================================
EOF

cat refleksi-quoting.txt
```
Output :
```bash
==========================================
REFLEKSI PENTINGNYA QUOTING DI BASH
==========================================

==========================================
REFLEKSI: MENGAPA QUOTING SANGAT PENTING?
==========================================

1. SPASI DALAM NAMA FILE
   Tanpa quote: Bash memecah nama file menjadi beberapa argumen
   Contoh: "laporan keuangan.txt" → laporan, keuangan.txt (2 argumen!)
   Dengan quote: Seluruh nama dianggap 1 argumen

2. KARAKTER SPECIAL ( *, ?, [, ], (, ), &, ;, $, !, `, | )
   Tanpa quote: Karakter ini diinterpretasikan oleh shell
   Contoh: config[prod].ini → [ ] dianggap wildcard pattern
   Dengan quote: Karakter dianggap literal (teks biasa)

3. VARIABEL YANG MENGANDUNG PATH
   Tanpa quote: Jika path mengandung spasi, akan error
   Contoh: $FILE="My Documents/file.txt"
   cp $FILE backup/ → error karena "My" dan "Documents/" terpisah
   Dengan quote: cp "$FILE" backup/ → bekerja

4. KEAMANAN (SECURITY)
   Tanpa quote: Rentan terhadap command injection
   Contoh: nama_file="file.txt; rm -rf /"
   cat $nama_file → bisa menjalankan perintah berbahaya
   Dengan quote: cat "$nama_file" → aman

5. COMMAND SUBSTITUTION
   Tanpa quote: Hasil substitution bisa pecah karena spasi
   Dengan quote: $(command) tetap utuh sebagai 1 argumen

==========================================
PRAKTIK TERBAIK (BEST PRACTICE)
==========================================

SELALU gunakan double quote untuk variabel:
   cp "$source" "$destination"
   echo "User: $USER"

Gunakan single quote untuk teks literal:
   echo 'Karakter $special @tidak &diekspansi'

Gunakan backslash untuk escape karakter tunggal:
   cp file\ dengan\ spasi.txt backup/

PREVIEW wildcard dengan echo sebelum perintah berbahaya:
   echo rm *.log  (lihat dulu filenya)
   rm *.log      (langsung hapus tanpa lihat)

==========================================
```   

### Langkah 8 : Tampilkan Ringkasan Tugas 4
Input :
```bash
echo ""
echo "=========================================="
echo "RINGKASAN TUGAS PRAKTIKUM 4"
echo "=========================================="
echo ""

echo "DAFTAR FILE AWAL (di tugas4-sample):"
ls -1 tugas4-sample/ | head -10
echo "   ... dan seterusnya"
echo ""

echo "DAFTAR FILE HASIL BACKUP:"
ls -1 "$BACKUP_SUBDIR/"
echo ""

echo "FILE ARSIP TAR.GZ:"
ls -lh "$BACKUP_DIR"/*.tar.gz
echo ""

echo "FILE RIWAYAT PERINTAH:"
ls -lh riwayat-arsip.txt
echo ""

echo "REFLEKSI QUOTING:"
ls -lh refleksi-quoting.txt
echo ""

echo "=========================================="
echo "TUGAS 4 SELESAI!"
echo "=========================================="
```
Output :
```bash
==========================================
RINGKASAN TUGAS PRAKTIKUM 4
==========================================

DAFTAR FILE AWAL (di tugas4-sample):
access-log-01.txt
access-log-02.txt
access-log-03.txt
backup server 2026.tar
config[production].ini
data[2026-04-10].json
error-log-01.txt
error-log-02.txt
error-log-03.txt
laporan keuangan april.csv
   ... dan seterusnya

DAFTAR FILE HASIL BACKUP:
access-log-01.txt
access-log-02.txt
access-log-03.txt
'config[production].ini'
'laporan keuangan april.csv'
'log_backup_(server).txt'
this_is_a_very_long_filename_for_testing_wildcard_pattern_matching.log
user_data_2024.csv
user_data_2025.csv
user_data_2026.csv

FILE ARSIP TAR.GZ:
-rw-r--r-- 1 root root 376 Apr 11 02:47 /root/praktikum-os/week07-bash/tugas4-backup/backup_archive_20260411_024511.tar.gz

FILE RIWAYAT PERINTAH:
-rw-r--r-- 1 root root 1.5K Apr 11 02:49 riwayat-arsip.txt

REFLEKSI QUOTING:
-rw-r--r-- 1 root root 1.8K Apr 11 02:53 refleksi-quoting.txt

==========================================
TUGAS 4 SELESAI!
==========================================
```
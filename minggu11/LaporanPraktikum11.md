# Laporan Praktikum 11

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## PRAKTIKUM

## Praktikum 9.1

### Langkah 1
Input
```bash
sudo mkdir -p ~/praktikum-os/week11/lab-permissions
cd ~/praktikum-os/week11/lab-permissions
echo "data rahasia" > secret.txt
echo '#!/bin/bash' > myscript.sh
echo 'echo Hello' >> myscript.sh
ls -la
```

Output
```bash
root@ubuntuser:~# mkdir -p ~/praktikum-os/week11/lab-permissions
root@ubuntuser:~# cd ~/praktikum-os/week11/lab-permissions
root@ubuntuser:~/praktikum-os/week11/lab-permissions# echo "data rahasia" > secret.txt
root@ubuntuser:~/praktikum-os/week11/lab-permissions# echo '#!/bin/bash' > myscript.sh
root@ubuntuser:~/praktikum-os/week11/lab-permissions# echo 'echo Hello' >> myscript.sh
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ls -la
total 16
drwxr-xr-x 2 root root 4096 May 10 08:02 .
drwxr-xr-x 3 root root 4096 May 10 08:00 ..
-rw-r--r-- 1 root root   23 May 10 08:02 myscript.sh
-rw-r--r-- 1 root root   13 May 10 08:01 secret.txt
```

### Langkah 2
Input
```bash
chmod 600 secret.txt
ls -l secret.txt
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-permissions# chmod 600 secret.txt
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ls -l secret.txt
-rw------- 1 root root 13 May 10 08:01 secret.txt
```

### Langkah 3
Input
```bash
chmod 755 myscript.sh
ls -l myscript.sh
./myscript.sh
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-permissions# chmod 755 myscript.sh
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ls -l myscript.sh
-rwxr-xr-x 1 root root 23 May 10 08:02 myscript.sh
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ./myscript.sh
Hello
```

### Langkah 4
Input
```bash
mkdir shared-dir
chmod g+s shared-dir
ls -ld shared-dir
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-permissions# mkdir shared-dir
root@ubuntuser:~/praktikum-os/week11/lab-permissions# chmod g+s shared-dir
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ls -ld shared-dir
drwxr-sr-x 2 root root 4096 May 10 08:07 shared-dir
```

### Langkah 5
Input
```bash
umask
umask 027
touch testfile-027
ls -l testfile-027
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-permissions# umask
0022
root@ubuntuser:~/praktikum-os/week11/lab-permissions# umask 027
root@ubuntuser:~/praktikum-os/week11/lab-permissions# touch testfile-027
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ls -l testfile-027
-rw-r----- 1 root root 0 May 10 08:10 testfile-027
```

### Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?

Jawaban :   
1. Karena permission 600 berarti:
- Owner: rw- (baca+tulis)
- Group: --- (tanpa akses)
- Others: --- (tanpa akses)  
Jadi hanya owner yang bisa membaca/menulis. 
2. 600 membuat file privat hanya untuk owner. 755 membuat file bisa dijalankan semua orang, tetapi hanya owner yang bisa mengedit. 
3. File baru mendapat 640 (rw-r-----). Bukan 777 karena file reguler tidak pernah mendapat izin execute dari umask, dan defaultnya 666 dikurangi umask 027. 

### Tantangan
Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan perubahan output ls -l sebelum dan sesudahnya.

Penjelasan : owner dari user menjadi root, group dari user menjadi root.

Input
```bash
sudo chown root:root secret.txt
ls -l secret.txt
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-permissions# sudo chown root:root secret.txt
root@ubuntuser:~/praktikum-os/week11/lab-permissions# ls -l secret.txt
-rw------- 1 root root 13 May 10 08:01 secret.txt
```


## Praktikum 9.2

### Langkah 1
Input
```bash
mkdir -p ~/praktikum-os/week11/lab-acl
cd ~/praktikum-os/week11/lab-acl
echo "Data petting" > confidential.txt
chmod 640 confidential.txt
ls -l confidential.txt
getfacl confidential.txt
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-permissions# mkdir -p ~/praktikum-o
s/week11/lab-acl
root@ubuntuser:~/praktikum-os/week11/lab-permissions# cd ~/praktikum-os/week11/lab-acl
root@ubuntuser:~/praktikum-os/week11/lab-acl# echo "Data petting" > confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# chmod 640 confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# ls -l confidential.txt
-rw-r----- 1 root root 13 May 10 08:19 confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# getfacl confidential.txt
# file: confidential.txt
# owner: root
# group: root
user::rw-
group::r--
other::---

```

### Langkah 2
Input
```bash
sudo setfacl -m u:root:r confidential.txt
ls -l confidential.txt
getfacl confidential.txt
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-acl# sudo setfacl -m u:root:r confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# ls -l confidential.txt
-rw-r-----+ 1 root root 13 May 10 08:19 confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# getfacl confidential.txt
# file: confidential.txt
# owner: root
# group: root
user::rw-
user:root:r--
group::r--
mask::r--
other::---

```

### Langkah 3
Input
```bash
mkdir shared
sudo setfacl -d -m u:root:rwx shared
sudo setfacl -d -m u:www-data:r-x shared
getfacl shared

touch shared/inherited.txt
getfacl shared/inherited.txt
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-acl# mkdir shared
root@ubuntuser:~/praktikum-os/week11/lab-acl# sudo setfacl -d -m u:root:rwx shared
root@ubuntuser:~/praktikum-os/week11/lab-acl# sudo setfacl -d -m u:www-data:r-x shared
root@ubuntuser:~/praktikum-os/week11/lab-acl# getfacl shared
# file: shared
# owner: root
# group: root
user::rwx
group::r-x
other::---
default:user::rwx
default:user:root:rwx
default:user:www-data:r-x
default:group::r-x
default:mask::rwx
default:other::---

root@ubuntuser:~/praktikum-os/week11/lab-acl# touch shared/inherited.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# getfacl shared/inherited.txt
# file: shared/inherited.txt
# owner: root
# group: root
user::rw-
user:root:rwx                   #effective:rw-
user:www-data:r-x               #effective:r--
group::r-x                      #effective:r--
mask::rw-
other::---

```

### Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?

Jawaban :  
1. Karena belum ada ACL tambahan, hanya permission Unix standar (owner, group, others). 
2. ls -l menampilkan tanda + di akhir permission. getfacl menunjukkan daftar lengkap ACL termasuk user tambahan. 
3. Karena direktori shared memiliki default ACL, sehingga setiap file/direktori baru di dalamnya otomatis mendapat ACL yang sama. 

### Tantangan
Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt. Setelah itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.

Input
```bash
sudo groupadd readonly-group
sudo setfacl -m g:readonly-group:r confidential.txt
getfacl confidential.txt

sudo setfacl -x u:root confidential.txt
getfacl confidential.txt
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11/lab-acl# sudo groupadd readonly-group
root@ubuntuser:~/praktikum-os/week11/lab-acl# sudo setfacl -m g:readonly-group:r confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# getfacl confidential.txt
# file: confidential.txt
# owner: root
# group: root
user::rw-
user:root:r--
group::r--
group:readonly-group:r--
mask::r--
other::---

root@ubuntuser:~/praktikum-os/week11/lab-acl# sudo setfacl -x u:root confidential.txt
root@ubuntuser:~/praktikum-os/week11/lab-acl# getfacl confidential.txt
# file: confidential.txt
# owner: root
# group: root
user::rw-
group::r--
group:readonly-group:r--
mask::r--
other::---

```


## Praktikum 9.3A

### Langkah 1
Input
```bash
sudo useradd -m -s /bin/bash userA
sudo useradd -m -s /bin/bash userB
sudo passwd userA
sudo passwd userB
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo useradd -m -s /bin/bash userA
root@ubuntuser:~/praktikum-os/week11# sudo useradd -m -s /bin/bash userB
root@ubuntuser:~/praktikum-os/week11# sudo passwd userA
New password:
Retype new password:
passwd: password updated successfully
root@ubuntuser:~/praktikum-os/week11# sudo passwd userB
New password:
Retype new password:
passwd: password updated successfully
```

### Langkah 2
Input
```bash
id userA
getent passwd userA
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# id userA
uid=1001(userA) gid=1002(userA) groups=1002(userA)
root@ubuntuser:~/praktikum-os/week11# getent passwd userA
userA:x:1001:1002::/home/userA:/bin/bash
```

### Langkah 3
Input
```bash
sudo usermod -s /bin/zsh userA
getent passwd userA
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo usermod -s /bin/zsh userA
usermod: Warning: missing or non-executable shell '/bin/zsh'
root@ubuntuser:~/praktikum-os/week11# getent passwd userA
userA:x:1001:1002::/home/userA:/bin/zsh
```

### Langkah 4
Input
```bash
sudo usermod -L userB
sudo passwd -S userB
sudo usermod -U userB
sudo passwd -S userB
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo usermod -L userB
root@ubuntuser:~/praktikum-os/week11# sudo passwd -S userB
userB L 2026-05-10 0 99999 7 -1
root@ubuntuser:~/praktikum-os/week11# sudo usermod -U userB
root@ubuntuser:~/praktikum-os/week11# sudo passwd -S userB
userB P 2026-05-10 0 99999 7 -1
```

### Analisis
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
2. Bagaimana status passwd -S userB berubah saat akun di-lock?

Jawaban :  
1. Belum ada perbedaan karena kita belum menambah group. Nanti setelah usermod -aG, akan muncul group tambahan di output id. 
2. Dari P (unlocked) menjadi L (locked), lalu kembali ke P setelah di-unlock 


## Praktikum 9.3B

### Langkah 1
Input
```bash

sudo groupadd labgroup
sudo groupadd readonly - group

sudo usermod - aG labgroup , readonly - group userA

sudo usermod - aG readonly - group userB

id userA
id userB
getent group labgroup
getent group readonly - group
Kode 1.22: La
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo groupadd labgroup
root@ubuntuser:~/praktikum-os/week11# sudo groupadd readonly-group
groupadd: group 'readonly-group' already exists
root@ubuntuser:~/praktikum-os/week11# sudo usermod -aG labgroup,readonly-group userA
root@ubuntuser:~/praktikum-os/week11# sudo usermod -aG readonly-group userB
root@ubuntuser:~/praktikum-os/week11# id userA
uid=1001(userA) gid=1002(userA) groups=1002(userA),1001(readonly-group),1004(labgroup)
root@ubuntuser:~/praktikum-os/week11# id userB
uid=1002(userB) gid=1003(userB) groups=1003(userB),1001(readonly-group)
root@ubuntuser:~/praktikum-os/week11# getent group labgroup
labgroup:x:1004:userA
root@ubuntuser:~/praktikum-os/week11# getent group readonly-group
readonly-group:x:1001:userA,userB
```

### Analisis
1. Apa yang ditampilkan id userA vs groups userA?
2. Mengapa -a pada usermod -aG penting?

Jawaban :  
1. id userA menampilkan UID, GID, dan semua group (primary + supplementary). groups userA hanya menampilkan nama-nama group saja. Keduanya isinya sama. 
2. Tanpa -a, opsi -G akan mengganti semua supplementary group lama dengan yang baru. Dengan -aG, group lama tetap dipertahankan dan hanya menambah yang baru. 


## Praktikum 9.3C

### Langkah 1
Input
```bash
sudo chage -M 60 -W 7 -m 1 userA
sudo chage -l userA
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo chage -M 60 -W 7 -m 1 userA
root@ubuntuser:~/praktikum-os/week11# sudo chage -l userA
Last password change                                    : May 10, 2026
Password expires                                        : Jul 09, 2026
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 1
Maximum number of days between password change          : 60
Number of days of warning before password expires       : 7
```

### Langkah 2
Input
```bash
sudo chage -d 0 userA
sudo chage -l userA | head -1
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo chage -d 0 userA
root@ubuntuser:~/praktikum-os/week11# sudo chage -l userA | head -1
Last password change                                    : password must be changed
```

### Langkah 3
Input
```bash
sudo passwd -l userB
sudo passwd -S userB
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo passwd -l userB
passwd: password changed.
root@ubuntuser:~/praktikum-os/week11# sudo passwd -S userB
userB L 2026-05-10 0 99999 7 -1
```

### Langkah 4
Input
```bash
sudo passwd -u userB
sudo passwd -S userB
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo passwd -u userB
passwd: password changed.
root@ubuntuser:~/praktikum-os/week11# sudo passwd -S userB

userB P 2026-05-10 0 99999 7 -1
```

### Analisis
1. Apa arti nilai yang ditampilkan chage -l userA?
2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?

Jawaban :  
1. Menampilkan kebijakan password: kapan terakhir ganti, kapan expired, batas minimal/maksimal hari, hari peringatan, dan masa tenggang setelah expired. 
2. Output menunjukkan huruf L (locked) bukan P (active password). 
3. Keduanya sama-sama memaksa ganti password saat login berikutnya. chage -d 0 lebih eksplisit karena langsung mengatur last password change ke 0 (epoch). passwd -e adalah cara singkatnya. 

### Tantangan
Buat user bernama intern yang:
- memiliki shell /bin/bash;
- menjadi anggota labgroup;
- dipaksa ganti password pada login pertama;
- password expired setelah 45 hari dengan warning 7 hari sebelumnya.

Input
```bash
sudo useradd -m -s /bin/bash intern
sudo usermod -aG labgroup intern
sudo passwd intern
sudo chage -d 0 intern
sudo chage -M 45 -W 7 intern
sudo chage -l intern
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo useradd -m -s /bin/bash intern
root@ubuntuser:~/praktikum-os/week11# sudo usermod -aG labgroup intern
root@ubuntuser:~/praktikum-os/week11# sudo passwd intern
New password:
Retype new password:
passwd: password updated successfully
root@ubuntuser:~/praktikum-os/week11# sudo chage -d 0 intern
root@ubuntuser:~/praktikum-os/week11# sudo chage -M 45 -W 7 intern
root@ubuntuser:~/praktikum-os/week11# sudo chage -l intern
Last password change                                    : password must be changed
Password expires                                        : password must be changed
Password inactive                                       : password must be changed
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 7
```


## Praktikum 9.4

### Langkah 1
Input
```bash
sudo visudo -f /etc/sudoers.d/lab-userA
userA ALL=(root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
userA ALL=(root) /bin/systemctl status *
```

### Langkah 2
Input
```bash
sudo -l -U userA
sudo grep " userA " / var / log / auth . log | tail -10
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo -l -U userA
Matching Defaults entries for userA on ubuntuser:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User userA may run the following commands on ubuntuser:
    (root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
    (root) /bin/systemctl status *
root@ubuntuser:~/praktikum-os/week11# sudo grep "userA" /var/log/auth.log | tail -5
2026-05-10T08:50:18.495578+00:00 ubuntuser sudo:     root : TTY=pts/2 ; PWD=/root/praktikum-os/week11 ; USER=root ; COMMAND=/usr/bin/chage -d 0 userA
2026-05-10T08:50:18.610462+00:00 ubuntuser chage[1785]: changed password expiry for userA
2026-05-10T08:50:28.791151+00:00 ubuntuser sudo:     root : TTY=pts/2 ; PWD=/root/praktikum-os/week11 ; USER=root ; COMMAND=/usr/bin/chage -l userA
2026-05-10T08:57:37.888718+00:00 ubuntuser sudo:     root : TTY=pts/2 ; PWD=/root/praktikum-os/week11 ; USER=root ; COMMAND=/usr/sbin/visudo -f /etc/sudoers.d/lab-userA
2026-05-10T08:59:25.224010+00:00 ubuntuser sudo:     root : TTY=pts/2 ; PWD=/root/praktikum-os/week11 ; USER=root ; COMMAND=/usr/bin/grep userA /var/log/auth.log
```

### Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
3. Informasi apa saja yang dicatat di log sudo?

Jawaban :  
1. Agar lebih rapi dan aman. File terpisah tidak akan hilang saat update sistem, dan lebih mudah dikelola per aplikasi/user. 
2. Tanpa password: apt update dan apt upgrade. Masih perlu password: systemctl status *. 
3. User, TTY, working directory, user target (USER=root), dan perintah yang dijalankan. 

### Tantangan
Tambahkan satu aturan baru agar userA boleh menjalankan /bin/systemctl restart ssh tetapi tidak boleh menjalankan reboot.

Input
```bash
sudo visudo -f /etc/sudoers.d/lab-userA
userA ALL=(root) /bin/systemctl restart ssh
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo visudo -f /etc/sudoers.d/lab-userA
  GNU nano 7.2            /etc/sudoers.d/lab-userA.tmp *
userA ALL=(root) /bin/systemctl restart ssh
userA ALL=(root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
userA ALL=(root) /bin/systemctl status *



^G Help        ^O Write Out   ^W Where Is    ^K Cut         ^T Execute
^X Exit        ^R Read File   ^\ Replace     ^U Paste       ^J Justify
```


## Praktikum 9.5

### Langkah 1
Input
```bash
sudo dd if=/dev/zero of=/tmp/quota-test.img bs=1M count=100
sudo mkfs.ext4 /tmp/quota-test.img
sudo mkdir -p /mnt/quota-test
sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo dd if=/dev/zero of=/tmp/quota-tes
t.img bs=1M count=100
100+0 records in
100+0 records out
104857600 bytes (105 MB, 100 MiB) copied, 0.524212 s, 200 MB/s
root@ubuntuser:~/praktikum-os/week11# sudo mkfs.ext4 /tmp/quota-test.img
mke2fs 1.47.0 (5-Feb-2023)
Discarding device blocks: done
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done

root@ubuntuser:~/praktikum-os/week11# sudo mkdir -p /mnt/quota-test
root@ubuntuser:~/praktikum-os/week11# sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
```

### Langkah 2
Input
```bash
sudo quotacheck -cug /mnt/quota-test
sudo quotaon -v /mnt/quota-test
sudo repquota /mnt/quota-test
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo quotacheck -cug /mnt/quota-test
root@ubuntuser:~/praktikum-os/week11# sudo quotaon -v /mnt/quota-test
quotaon: Your kernel probably supports ext4 quota feature but you are using external quota files. Please switch your filesystem to use ext4 quota feature as external quota files on ext4 are deprecated.
/dev/loop0 [/mnt/quota-test]: group quotas turned on
/dev/loop0 [/mnt/quota-test]: user quotas turned on
root@ubuntuser:~/praktikum-os/week11# sudo repquota /mnt/quota-test
*** Report for user quotas on device /dev/loop0
Block grace time: 7days; Inode grace time: 7days
                        Block limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
----------------------------------------------------------------------
root      --      20       0       0              2     0     0


```

### Langkah 3
Input
```bash
sudo edquota -u userA
sudo repquota /mnt/quota-test
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo edquota -u userA
  GNU nano 7.2                  /tmp//EdP.aGA5bHP *
Disk quotas for user userA (uid 1001):
  Filesystem                   blocks       soft       hard     inodes     >
  /dev/loop0                        0       5120      10240          0     >






^G Help        ^O Write Out   ^W Where Is    ^K Cut         ^T Execute
^X Exit        ^R Read File   ^\ Replace     ^U Paste       ^J Justify
root@ubuntuser:~/praktikum-os/week11# sudo repquota /mnt/quota-test
*** Report for user quotas on device /dev/loop0
Block grace time: 7days; Inode grace time: 7days
                        Block limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
----------------------------------------------------------------------
root      --      20       0       0              2     0     0
userA     --       4    5120   10240              1     0     0

```

### Langkah 4
Input
```bash
sudo quotaoff /mnt/quota-test
sudo umount /mnt/quota-test
sudo rm /tmp/quota-test.img
```

### Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?

Jawaban :  
1. Soft limit masih bisa dilewati sementara (grace period). Hard limit tidak bisa dilewati sama sekali, akan langsung error. 
2. Agar aman dan tidak mengganggu sistem utama. Jika salah konfigurasi, hanya image file yang rusak, bukan partisi/home sebenarnya. 
3. Muncul kolom soft, hard, grace untuk block dan file limits, serta ada nilai used/quota yang terisi. 

### Tantangan
Coba atur quota baru untuk userA dengan batas inode yang sangat kecil, kemudian jelaskan kapan pembatasan inode lebih penting daripada pembatasan block.

Penjelasan : Inode quota lebih penting ketika banyak file kecil yang jumlahnya sangat banyak, misalnya:

- Direktori cache aplikasi (ribuan file kecil)

- Server email (ribuan file pesan)

- Temporary file dari script/program

Block quota mungkin masih aman karena total ukuran kecil, tapi inode bisa habis duluan karena setiap file minimal membutuhkan 1 inode.

Input
```bash
sudo setquota -u userA 10240 20480 3 5 /mnt/quota-test
sudo repquota -v /mnt/quota-test
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# sudo setquota -u userA 10240 20480 3 5 /mnt/quota-test
root@ubuntuser:~/praktikum-os/week11# sudo repquota -v /mnt/quota-test
*** Report for user quotas on device /dev/loop0
Block grace time: 7days; Inode grace time: 7days
                        Block limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
----------------------------------------------------------------------
root      --      20       0       0              2     0     0
userA     --       0   10240   20480              0     3     5

Statistics:
Total blocks: 7
Data blocks: 1
Entries: 2
Used average: 2.000000

```


## LATIHAN

## Latihan Latihan 9.A — Audit dan Kolaborasi

### 1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan tiga file yang Anda kenali beserta alasannya.

### Jawaban :   
Input:
```bash
find / -perm -4000 -type f 2>/dev/null
```
Output:
```bash
root@ubuntuser:~/praktikum-os/week11# find / -perm -4000 -type f 2>/dev/null
/usr/bin/mount
/usr/bin/su
/usr/bin/chsh
/usr/bin/chfn
/usr/bin/sudo
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/umount
/usr/bin/passwd
/usr/bin/fusermount3
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/openssh/ssh-keysign
/usr/lib/polkit-1/polkit-agent-helper-1
```

Tiga file yang saya kenali adalah /usr/bin/passwd, /usr/bin/su, dan /usr/bin/sudo. Alasannya :

- /usr/bin/passwd
Alasan: Program ini perlu menulis ke /etc/shadow (hanya bisa diakses root). SUID membuat program berjalan sebagai root sehingga user biasa bisa mengganti password sendiri.

- /usr/bin/su
Alasan: Perintah su (switch user) perlu berjalan sebagai root agar bisa berpindah ke user lain tanpa password user target.

- /usr/bin/sudo
Alasan: sudo perlu berjalan dengan privilege root agar bisa menjalankan perintah lain sebagai user lain (biasanya root).


### 2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.

### Jawaban : 
Input:
```bash
find / -type d -perm -002 2>/dev/null | head -10
```

Output
```bash
root@ubuntuser:~/praktikum-os/week11# find / -type d -perm -002 2>/dev/null | head -10
/dev/mqueue
/dev/shm
/tmp
/tmp/.ICE-unix
/tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-upower.service-72LVbL/tmp
/tmp/.XIM-unix
/tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-ModemManager.service-qByC21/tmp
/tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-systemd-resolved.service-ef2RFC/tmp
/tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-polkit.service-bTyyNq/tmp
/tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-fwupd.service-iqC9QI/tmp
```

Aman:
- /dev/mqueue
- /dev/shm
- /tmp
- /tmp/.ICE-unix
- /tmp/.XIM-unix
- /tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-upower.service-72LVbL/tmp
- /tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-ModemManager.service-qByC21/tmp
- /tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-systemd-resolved.service-ef2RFC/tmp
- /tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-polkit.service-bTyyNq/tmp
- /tmp/systemd-private-b573fec922204662bfb50c7b0b81c4b4-fwupd.service-iqC9QI/tmp

Berisiko:
Tidak ada ditemukan dari 10 output pertama.

### 3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi group proyek.

### Jawaban :
Input : 
```bash
sudo groupadd webapp-team

sudo useradd -m -s /bin/bash deploy
sudo passwd deploy

sudo mkdir -p /srv/webapp

sudo chown root:webapp-team /srv/webapp

sudo chmod 2770 /srv/webapp

sudo setfacl -m u:deploy:r-x /srv/webapp

sudo setfacl -d -m g:webapp-team:rwx /srv/webapp
sudo setfacl -d -m u:deploy:r-x /srv/webapp

ls -ld /srv/webapp
getfacl /srv/webapp
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week11# sudo groupadd webapp-team
root@ubuntuser:~/praktikum-os/week11# sudo useradd -m -s /bin/bash deploy
sudo passwd deploy
New password:
Retype new password:
passwd: password updated successfully
root@ubuntuser:~/praktikum-os/week11# sudo mkdir -p /srv/webapp
root@ubuntuser:~/praktikum-os/week11# sudo chown root:webapp-team /srv/webapp
root@ubuntuser:~/praktikum-os/week11# sudo chmod 2770 /srv/webapp
root@ubuntuser:~/praktikum-os/week11# sudo setfacl -m u:deploy:r-x /srv/webapp
root@ubuntuser:~/praktikum-os/week11# sudo setfacl -d -m g:webapp-team:rwx /srv/webapp
root@ubuntuser:~/praktikum-os/week11# sudo setfacl -d -m u:deploy:r-x /srv/webapp
root@ubuntuser:~/praktikum-os/week11# ls -ld /srv/webapp
drwxrws---+ 2 root webapp-team 4096 May 10 12:48 /srv/webapp
root@ubuntuser:~/praktikum-os/week11# getfacl /srv/webapp
getfacl: Removing leading '/' from absolute path names
# file: srv/webapp
# owner: root
# group: webapp-team
# flags: -s-
user::rwx
user:deploy:r-x
group::rwx
mask::rwx
other::---
default:user::rwx
default:user:deploy:r-x
default:group::rwx
default:group:webapp-team:rwx
default:mask::rwx
default:other::---

```

## Latihan Latihan 9.B — Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan menetapkan quota ruang serta inode sederhana pada /home/.

### Jawaban  

### Langkah 1 : Buat user intern
Input : 
```bash
sudo useradd -m -s /bin/bash intern
sudo passwd intern
```

Output :
```bash
yudhis@ubuntuser:~$ sudo useradd -m -s /bin/bash intern
[sudo] password for yudhis:
useradd: user 'intern' already exists
yudhis@ubuntuser:~$ sudo passwd intern
New password:
Retype new password:
passwd: password updated successfully
```

### Langkah 2 : Tambahkan intern ke group labgroup
Input : 
```bash
sudo usermod -aG labgroup intern
id intern
```

Output :
```bash
yudhis@ubuntuser:~$ sudo usermod -aG labgroup intern
yudhis@ubuntuser:~$ id intern
uid=1003(intern) gid=1005(intern) groups=1005(intern),1004(labgroup)
```

### Langkah 3 : Paksa ganti password tiap 45 hari, warning 7 hari
Input : 
```bash
sudo chage -M 45 -W 7 intern
sudo chage -l intern
```

Output :
```bash
yudhis@ubuntuser:~$ sudo chage -M 45 -W 7 intern
yudhis@ubuntuser:~$ sudo chage -l intern
Last password change                                    : May 10, 2026
Password expires                                        : Jun 24, 2026
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 7
```

### Langkah 4 : Beri izin sudo hanya untuk systemctl status
Input : 
```bash
sudo visudo -f /etc/sudoers.d/intern
# intern ALL=(root) NOPASSWD: /bin/systemctl status *
sudo -l -U intern
```

Output :
```bash
yudhis@ubuntuser:~$ sudo visudo -f /etc/sudoers.d/intern
visudo: /etc/sudoers.d/intern.tmp unchanged
yudhis@ubuntuser:~$ sudo -l -U intern
Matching Defaults entries for intern on ubuntuser:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User intern may run the following commands on ubuntuser:
    (root) NOPASSWD: /bin/systemctl status *
```

### Langkah 5 : Set quota ruang dan inode di /home/
Input : 
```bash
sudo setquota -u intern 102400 204800 500 1000 /home
sudo repquota -v /home | grep intern
```

Output :
```bash
yudhis@ubuntuser:~$ sudo setquota -u intern 102400 204800 500 1000 /home
setquota: Mountpoint (or device) /home not found or has no quota enabled.
setquota: Not all specified mountpoints are using quota.
yudhis@ubuntuser:~$ sudo repquota -v /home | grep intern
repquota: Mountpoint (or device) /home not found or has no quota enabled.
repquota: Not all specified mountpoints are using quota.
```

### Langkah 6 : Buat user intern
Input : 
```bash
# Cek user
getent passwd intern

# Cek group
groups intern

# Cek password aging
sudo chage -l intern

# Cek sudo
sudo -l -U intern

# Cek quota
sudo quota -u intern
```

Output :
```bash
yudhis@ubuntuser:~$ getent passwd intern
intern:x:1003:1005::/home/intern:/bin/bash
yudhis@ubuntuser:~$ groups intern
intern : intern labgroup
yudhis@ubuntuser:~$ sudo chage -l intern
Last password change                                    : password must be changed
Password expires                                        : password must be changed
Password inactive                                       : password must be changed
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 7
yudhis@ubuntuser:~$ sudo -l -U intern
Matching Defaults entries for intern on ubuntuser:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User intern may run the following commands on ubuntuser:
    (root) NOPASSWD: /bin/systemctl status *
yudhis@ubuntuser:~$ sudo quota -u intern
yudhis@ubuntuser:~$
```




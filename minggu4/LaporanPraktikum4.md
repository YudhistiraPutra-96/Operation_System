# Laporan Praktikum 4

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## TUGAS PENDAHULUAN

Jawablah pertanyaan-pertanyaan di bawah ini :

1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.

2. Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)

3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).

4. Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.

Jawaban : 

1. Perintah-perintah direktori: pwd, cd, mkdir, rmdir

    * pwd (print working directory) : Menampilkan direktori aktif saat ini.

    * cd (change directory) : Berpindah ke direktori lain. Contoh: cd /home atau cd .. (ke parent).

    * mkdir (make directory) : Membuat direktori baru. Contoh: mkdir latihan atau mkdir -p dir1/dir2 (dengan subdirektori).

    * rmdir (remove directory) : Menghapus direktori yang kosong. Jika direktori tidak kosong, akan muncul pesan error.

2. Perintah manipulasi file : cp, mv, rm (beserta format)
    * cp (copy) : Menyalin file atau direktori.  
    Format : cp [opsi] sumber tujuan  
    Contoh :

        * cp file1 file2 – menyalin file1 menjadi file2

        * cp -r dir1 dir2 – menyalin direktori secara rekursif

    * mv (move) : Memindahkan atau mengganti nama file/direktori.
    Format : mv sumber tujuan  
    Contoh :

        * mv file1 file2 – mengganti nama file1 menjadi file2

        * mv file1 dir/ – memindahkan file1 ke dalam direktori dir

    * rm (remove) : Menghapus file atau direktori.  
    Format : rm [opsi] file  
    Contoh :

        * rm file1 – menghapus file

        * rm -r dir – menghapus direktori beserta isinya

        * rm -f file – menghapus paksa tanpa konfirmasi

3. Perbedaan hard link dan soft link (symbolic link)  

* Hard link :

    * Merupakan tautan langsung ke inode file.

    * File asli dan hard link berbagi inode yang sama, sehingga perubahan pada salah satu akan terlihat di semua tautan.

    * Jika file asli dihapus, data tetap ada melalui hard link.

    * Tidak dapat dibuat lintas partisi/filesystem dan tidak dapat digunakan untuk direktori.

* Soft link (symbolic link) :

    * Berupa file khusus yang berisi path ke file target.

    * Jika file asli dihapus, tautan menjadi putus (dangling).

    * Dapat dibuat lintas filesystem dan dapat menunjuk ke direktori.

    * Ditandai dengan huruf l pada izin file dan panah -> saat dilihat dengan ls -l.

4. Maksud perintah: file, find, which, locate, grep
* file : Menentukan tipe suatu file (misalnya teks, binary, direktori, dll) berdasarkan isinya.  
Contoh: file dokumen.txt akan menampilkan dokumen.txt: ASCII text.

* find : Mencari file dan direktori dalam hierarki berdasarkan kriteria seperti nama, ukuran, waktu modifikasi, dll.  
Contoh: find /home -name "*.txt" mencari semua file berekstensi .txt di /home.

* which : Menampilkan lokasi absolut dari suatu perintah yang dieksekusi (berdasarkan PATH).  
Contoh: which ls akan menampilkan /bin/ls.

* locate : Mencari file dengan cepat menggunakan database indeks (diperbarui dengan updatedb).  
Contoh: locate passwd akan menampilkan semua file bernama passwd di sistem.

* grep (Global Regular Expression Print) : Mencari teks dalam file berdasarkan pola (regular expression).  
Contoh: grep "error" log.txt akan menampilkan baris-baris yang mengandung kata "error".



## LATIHAN

### 1. Cobalah urutan perintah berikut :
```bash
$ cd
$ pwd
$ ls –al
$ cd .
$ pwd
$ cd ..
$ pwd
$ ls -al
$ cd ..
$ pwd
$ ls -al
$ cd /etc
$ ls –al | more
$ cat passwd
$ cd –
$ pwd
```


output  
```bash
root@ubuntuser:/home/yudhis# mkdir -p ~/praktikum-os/week04
root@ubuntuser:/home/yudhis# cd ~/praktikum-os/week04
root@ubuntuser:~/praktikum-os/week04# pwd
/root/praktikum-os/week04
root@ubuntuser:~/praktikum-os/week04# cd
root@ubuntuser:~# pwd
/root
root@ubuntuser:~# ls -al
total 108
drwx------  8 root root  4096 Mar  7 05:58 .
drwxr-xr-x 27 root root  4096 Mar  7 06:06 ..
drwxr-xr-x  4 root root  4096 Mar  7 05:54 A
-rw-r--r--  1 root root     0 Mar  1 03:54 backup-error.log
-rw-r--r--  1 root root   704 Mar  1 03:53 backup-success.l
-rw-r--r--  1 root root   704 Mar  1 03:54 backup-success.log
-rw-r--r--  1 root root 30720 Mar  1 03:54 backup.tar
-rw-------  1 root root 13578 Mar  7 06:17 .bash_history
-rw-r--r--  1 root root  3106 Apr 22  2024 .bashrc
drwxr-xr-x  2 root root  4096 Mar  7 05:54 C
drwx------  5 root root  4096 Feb 21 15:32 .config
-rw-------  1 root root    20 Feb 28 15:45 .lesshst
drwxr-xr-x  3 root root  4096 Feb 28 15:08 .local
drwxr-xr-x  5 root root  4096 Mar  7 06:17 praktikum-os
-rw-r--r--  1 root root   161 Apr 22  2024 .profile
drwx------  2 root root  4096 Feb 28 14:55 .ssh
-r-xr-xr-x  1 root root  7049 Feb 18 12:32 vboxpostinstall.sh
root@ubuntuser:~# cd .
root@ubuntuser:~# pwd
/root
root@ubuntuser:~# cd ..
root@ubuntuser:/# pwd
/
root@ubuntuser:/# ls -al
total 104
drwxr-xr-x  27 root root  4096 Mar  7 06:06 .
drwxr-xr-x  27 root root  4096 Mar  7 06:06 ..
drwxr-xr-x   4 root root  4096 Mar  7 06:06 A
drwxr-xr-x   3 root root  4096 Mar  7 06:06 B
drwxr-xr-x   2 root root  4096 Mar  1 03:14 backup
lrwxrwxrwx   1 root root     7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x   2 root root  4096 Feb 26  2024 bin.usr-is-merged
drwxr-xr-x   3 root root  4096 Feb 21 15:16 boot
drwxr-xr-x   2 root root  4096 Mar  7 06:06 C
dr-xr-xr-x   2 root root  4096 Feb 18 12:25 cdrom
drwxr-xr-x  19 root root  4040 Mar  7 05:49 dev
drwxr-xr-x 112 root root  4096 Feb 28 15:47 etc
drwxr-xr-x   3 root root  4096 Feb 18 12:31 home
lrwxrwxrwx   1 root root     7 Apr 22  2024 lib -> usr/lib
lrwxrwxrwx   1 root root     9 Apr 22  2024 lib64 -> usr/lib64
drwxr-xr-x   2 root root  4096 Feb 26  2024 lib.usr-is-merged
drwx------   2 root root 16384 Feb 18 12:26 lost+found
drwxr-xr-x   2 root root  4096 Aug  5  2025 media
drwxr-xr-x   2 root root  4096 Aug  5  2025 mnt
drwxr-xr-x   2 root root  4096 Aug  5  2025 opt
dr-xr-xr-x 199 root root     0 Mar  7 05:49 proc
drwx------   8 root root  4096 Mar  7 05:58 root
drwxr-xr-x  28 root root   840 Mar  7 05:56 run
lrwxrwxrwx   1 root root     8 Apr 22  2024 sbin -> usr/sbin
drwxr-xr-x   2 root root  4096 Dec 11  2024 sbin.usr-is-merged
drwxr-xr-x   2 root root  4096 Feb 18 12:31 snap
drwxr-xr-x   2 root root  4096 Aug  5  2025 srv
dr-xr-xr-x  13 root root     0 Mar  7 05:49 sys
drwxrwxrwt  13 root root  4096 Mar  7 05:56 tmp
drwxr-xr-x  12 root root  4096 Aug  5  2025 usr
drwxr-xr-x  13 root root  4096 Feb 18 12:31 var
root@ubuntuser:/# cd ..
root@ubuntuser:/# pwd
/
root@ubuntuser:/# ls -al
total 104
drwxr-xr-x  27 root root  4096 Mar  7 06:06 .
drwxr-xr-x  27 root root  4096 Mar  7 06:06 ..
drwxr-xr-x   4 root root  4096 Mar  7 06:06 A
drwxr-xr-x   3 root root  4096 Mar  7 06:06 B
drwxr-xr-x   2 root root  4096 Mar  1 03:14 backup
lrwxrwxrwx   1 root root     7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x   2 root root  4096 Feb 26  2024 bin.usr-is-merged
drwxr-xr-x   3 root root  4096 Feb 21 15:16 boot
drwxr-xr-x   2 root root  4096 Mar  7 06:06 C
dr-xr-xr-x   2 root root  4096 Feb 18 12:25 cdrom
drwxr-xr-x  19 root root  4040 Mar  7 05:49 dev
drwxr-xr-x 112 root root  4096 Feb 28 15:47 etc
drwxr-xr-x   3 root root  4096 Feb 18 12:31 home
lrwxrwxrwx   1 root root     7 Apr 22  2024 lib -> usr/lib
lrwxrwxrwx   1 root root     9 Apr 22  2024 lib64 -> usr/lib64
drwxr-xr-x   2 root root  4096 Feb 26  2024 lib.usr-is-merged
drwx------   2 root root 16384 Feb 18 12:26 lost+found
drwxr-xr-x   2 root root  4096 Aug  5  2025 media
drwxr-xr-x   2 root root  4096 Aug  5  2025 mnt
drwxr-xr-x   2 root root  4096 Aug  5  2025 opt
dr-xr-xr-x 197 root root     0 Mar  7 05:49 proc
drwx------   8 root root  4096 Mar  7 05:58 root
drwxr-xr-x  28 root root   840 Mar  7 05:56 run
lrwxrwxrwx   1 root root     8 Apr 22  2024 sbin -> usr/sbin
drwxr-xr-x   2 root root  4096 Dec 11  2024 sbin.usr-is-merged
drwxr-xr-x   2 root root  4096 Feb 18 12:31 snap
drwxr-xr-x   2 root root  4096 Aug  5  2025 srv
dr-xr-xr-x  13 root root     0 Mar  7 06:24 sys
drwxrwxrwt  13 root root  4096 Mar  7 05:56 tmp
drwxr-xr-x  12 root root  4096 Aug  5  2025 usr
drwxr-xr-x  13 root root  4096 Feb 18 12:31 var
root@ubuntuser:/# cd /etc
root@ubuntuser:/etc# ls -al | more
total 960
drwxr-xr-x 112 root root       4096 Feb 28 15:47 .
drwxr-xr-x  27 root root       4096 Mar  7 06:06 ..
-rw-r--r--   1 root root       3444 Jul  5  2023 adduser.conf
drwxr-xr-x   2 root root       4096 Feb 21 15:21 alternatives
drwxr-xr-x   2 root root       4096 Feb 21 15:16 apparmor
drwxr-xr-x   9 root root      12288 Feb 21 15:16 apparmor.d
drwxr-xr-x   3 root root       4096 Aug  5  2025 apport
drwxr-xr-x   9 root root       4096 Feb 18 12:26 apt
-rw-r--r--   1 root root       2319 Mar 31  2024 bash.bashrc
-rw-r--r--   1 root root         45 Aug  5  2025 bash_completion
drwxr-xr-x   2 root root       4096 Aug  5  2025 bash_completion.d
-rw-r--r--   1 root root        367 Aug  2  2022 bindresvport.blacklist
drwxr-xr-x   2 root root       4096 Jul  2  2025 binfmt.d
drwxr-xr-x   2 root root       4096 Aug  5  2025 byobu
drwxr-xr-x   3 root root       4096 Aug  5  2025 ca-certificates
-rw-r--r--   1 root root       6288 Aug  5  2025 ca-certificates.conf
drwxr-xr-x   5 root root       4096 Feb 21 15:16 cloud
drwxr-xr-x   2 root root       4096 Feb 18 12:27 console-setup
drwx------   2 root root       4096 Jul  2  2025 credstore
drwx------   2 root root       4096 Jul  2  2025 credstore.encrypted
drwxr-xr-x   2 root root       4096 Aug  5  2025 cron.d
drwxr-xr-x   2 root root       4096 Feb 18 12:31 cron.daily
drwxr-xr-x   2 root root       4096 Aug  5  2025 cron.hourly
drwxr-xr-x   2 root root       4096 Aug  5  2025 cron.monthly
-rw-r--r--   1 root root       1136 Aug  5  2025 crontab
drwxr-xr-x   2 root root       4096 Aug  5  2025 cron.weekly
drwxr-xr-x   2 root root       4096 Aug  5  2025 cron.yearly
drwxr-xr-x   2 root root       4096 Aug  5  2025 cryptsetup-initramfs
-rw-r--r--   1 root root         54 Aug  5  2025 crypttab
drwxr-xr-x   4 root root       4096 Aug  5  2025 dbus-1
-rw-r--r--   1 root root       2967 Apr 12  2024 debconf.conf
-rw-r--r--   1 root root         11 Apr 22  2024 debian_version
drwxr-xr-x   3 root root       4096 Feb 28 15:23 default
-rw-r--r--   1 root root       1706 Jul  5  2023 deluser.conf
drwxr-xr-x   2 root root       4096 Aug  5  2025 depmod.d
drwxr-xr-x   3 root root       4096 Aug  5  2025 dhcp
-rw-r--r--   1 root root       1429 May  7  2024 dhcpcd.conf
drwxr-xr-x   4 root root       4096 Feb 18 12:31 dpkg
-rw-r--r--   1 root root        685 Apr  8  2024 e2scrub.conf
-rw-r--r--   1 root root        106 Aug  5  2025 environment
-rw-r--r--   1 root root       1853 Oct 17  2022 ethertypes
drwxr-xr-x   4 root root       4096 Feb 18 12:30 fonts
-rw-r--r--   1 root root        446 Feb 18 12:30 fstab
-rw-r--r--   1 root root        694 Apr  8  2024 fuse.conf
drwxr-xr-x   4 root root       4096 Feb 21 15:16 fwupd
-rw-r--r--   1 root root       2584 Jan 31  2024 gai.conf
drwxr-xr-x   4 root root       4096 Feb 21 15:21 ghostscript
drwxr-xr-x   2 root root       4096 Feb 18 12:31 gnutls
drwxr-xr-x   2 root root       4096 Aug  5  2025 groff
-rw-r--r--   1 root root        791 Feb 28 14:41 group
-rw-r--r--   1 root root        777 Feb 18 12:31 group-
drwxr-xr-x   2 root root       4096 Feb 21 15:16 grub.d
-rw-r-----   1 root shadow      665 Feb 28 14:41 gshadow
-rw-r-----   1 root shadow      654 Feb 18 12:31 gshadow-
drwxr-xr-x   3 root root       4096 Aug  5  2025 gss
-rw-r--r--   1 root root       4436 Aug  5  2025 hdparm.conf
-rw-r--r--   1 root root         92 Apr 22  2024 host.conf
-rw-r--r--   1 root root         10 Feb 18 12:31 hostname
-rw-r--r--   1 root root          0 Aug  5  2025 hosts
-rw-r--r--   1 root root        411 Feb 21 08:49 hosts.allow
-rw-r--r--   1 root root        711 Feb 21 08:49 hosts.deny
drwxr-xr-x   2 root root       4096 Feb 21 15:21 ImageMagick-6
drwxr-xr-x   2 root root       4096 Feb 28 15:23 init.d
drwxr-xr-x   5 root root       4096 Feb 21 15:16 initramfs-tools
-rw-r--r--   1 root root       1875 Mar 31  2024 inputrc
drwxr-xr-x   4 root root       4096 Aug  5  2025 iproute2
drwxr-xr-x   2 root root       4096 Aug  5  2025 iscsi
-rw-r--r--   1 root root         26 Feb  6 07:23 issue
-rw-r--r--   1 root root         19 Feb  6 07:23 issue.net
drwxr-xr-x   6 root root       4096 Feb 18 12:30 kernel
drwxrwxr-x   2 root landscape  4096 Aug  5  2025 landscape
drwxr-xr-x   2 root root       4096 Feb 21 15:16 ldap
-rw-r--r--   1 root root      32431 Feb 28 15:23 ld.so.cache
-rw-r--r--   1 root root         34 Aug  2  2022 ld.so.conf
drwxr-xr-x   2 root root       4096 Feb 18 12:30 ld.so.conf.d
-rw-r--r--   1 root root        267 Apr 22  2024 legal
-rw-r--r--   1 root root        191 Mar 31  2024 libaudit.conf
drwxr-xr-x   3 root root       4096 Aug  5  2025 libblockdev
drwxr-xr-x   2 root root       4096 Aug  5  2025 libibverbs.d
drwxr-xr-x   2 root root       4096 Aug  5  2025 libnl-3
drwxr-xr-x   2 root root       4096 Apr  8  2024 libpaper.d
-rw-r--r--   1 root root       2996 Aug  5  2025 locale.alias
-rw-r--r--   1 root root         17 Feb 18 12:31 locale.conf
--More--
root@ubuntuser:/etc# cat passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:997:997:systemd Time Synchronization:/:/usr/sbin/nologin
dhcpcd:x:100:65534:DHCP Client Daemon,,,:/usr/lib/dhcpcd:/bin/false
messagebus:x:101:102::/nonexistent:/usr/sbin/nologin
systemd-resolve:x:992:992:systemd Resolver:/:/usr/sbin/nologin
pollinate:x:102:1::/var/cache/pollinate:/bin/false
polkitd:x:991:991:User for polkitd:/:/usr/sbin/nologin
syslog:x:103:104::/nonexistent:/usr/sbin/nologin
uuidd:x:104:105::/run/uuidd:/usr/sbin/nologin
tcpdump:x:105:107::/nonexistent:/usr/sbin/nologin
tss:x:106:108:TPM software stack,,,:/var/lib/tpm:/bin/false
landscape:x:107:109::/var/lib/landscape:/usr/sbin/nologin
fwupd-refresh:x:989:989:Firmware update daemon:/var/lib/fwupd:/usr/sbin/nologin
usbmux:x:108:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
yudhis:x:1000:1000:yudhis:/home/yudhis:/bin/bash
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
root@ubuntuser:/etc# cd -
/
root@ubuntuser:/# pwd
/
root@ubuntuser:/#
```

### 2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls, pwd dan cat. Telusuri direktory /bin, /usr/bin, /sbin, /tmp dan /boot.

/bin : 
```bash
root@ubuntuser:/# cd /bin
root@ubuntuser:/bin# pwd
/bin
root@ubuntuser:/bin# ls -l | head -15
total 132692
-rwxr-xr-x 1 root root       55744 Jun 22  2025 [
-rwxr-xr-x 1 root root       14640 Mar 31  2024 411toppm
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-enabled
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-exec
-rwxr-xr-x 1 root root       18736 Aug 15  2025 aa-features-abi
-rwxr-xr-x 1 root root        1622 Feb  6 17:52 acpidbg
-rwxr-xr-x 1 root root       16422 Jul  2  2025 add-apt-repository
-rwxr-xr-x 1 root root       14720 Sep 16 00:08 addpart
lrwxrwxrwx 1 root root          25 Mar 31  2024 animate -> /etc/alternatives/animate
lrwxrwxrwx 1 root root          29 Mar 31  2024 animate-im6 -> /etc/alternatives/animate-im6
-rwxr-xr-x 1 root root       14656 Mar 31  2024 animate-im6.q16
-rwxr-xr-x 1 root root       12556 Mar 31  2024 anytopnm
-rwxr-xr-x 1 root root        2322 Apr 18  2024 apport-bug
-rwxr-xr-x 1 root root       13625 Jul  8  2025 apport-cli
```

/usr/bin : 
```bash
root@ubuntuser:/bin# cd /usr/bin
root@ubuntuser:/usr/bin# pwd
/usr/bin
root@ubuntuser:/usr/bin# ls -l | head -15
total 132692
-rwxr-xr-x 1 root root       55744 Jun 22  2025 [
-rwxr-xr-x 1 root root       14640 Mar 31  2024 411toppm
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-enabled
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-exec
-rwxr-xr-x 1 root root       18736 Aug 15  2025 aa-features-abi
-rwxr-xr-x 1 root root        1622 Feb  6 17:52 acpidbg
-rwxr-xr-x 1 root root       16422 Jul  2  2025 add-apt-repository
-rwxr-xr-x 1 root root       14720 Sep 16 00:08 addpart
lrwxrwxrwx 1 root root          25 Mar 31  2024 animate -> /etc/alternatives/animate
lrwxrwxrwx 1 root root          29 Mar 31  2024 animate-im6 -> /etc/alternatives/animate-im6
-rwxr-xr-x 1 root root       14656 Mar 31  2024 animate-im6.q16
-rwxr-xr-x 1 root root       12556 Mar 31  2024 anytopnm
-rwxr-xr-x 1 root root        2322 Apr 18  2024 apport-bug
-rwxr-xr-x 1 root root       13625 Jul  8  2025 apport-cli
```

/sbin : 
```bash
root@ubuntuser:/usr/bin# cd /sbin
root@ubuntuser:/sbin# pwd
/sbin
root@ubuntuser:/sbin# ls -l | head -15
total 34544
-rwxr-xr-x 1 root root     39680 Aug 15  2025 aa-load
-rwxr-xr-x 1 root root      3225 Aug 15  2025 aa-remove-unknown
-rwxr-xr-x 1 root root     40000 Aug 15  2025 aa-status
-rwxr-xr-x 1 root root       137 Apr 12  2024 aa-teardown
-rwxr-xr-x 1 root root     14904 Aug  5  2025 accessdb
-rwxr-xr-x 1 root root      3075 Jan  5 22:01 addgnupghome
lrwxrwxrwx 1 root root         7 Jul  5  2023 addgroup -> adduser
-rwxr-xr-x 1 root root      1053 Mar 31  2024 add-shell
-rwxr-xr-x 1 root root     55191 Jul  5  2023 adduser
-rwxr-xr-x 1 root root     60992 Sep 16 00:08 agetty
-rwxr-xr-x 1 root root   1629848 Aug 15  2025 apparmor_parser
lrwxrwxrwx 1 root root         9 Aug 15  2025 apparmor_status -> aa-status
-rwxr-xr-x 1 root root      2217 Jan  5 22:01 applygnupgdefaults
-rwxr-xr-x 1 root root     36862 Apr 16  2024 argdist-bpfcc
```

/tmp : 
```bash
root@ubuntuser:/sbin# cd /tmp
root@ubuntuser:/tmp# pwd
/tmp
root@ubuntuser:/tmp# ls -l | head -15
total 28
drwx------ 2 root root 4096 Mar  7 05:49 snap-private-tmp
drwx------ 3 root root 4096 Mar  7 06:39 systemd-private-c09f65b6edf14c99b94ea1939424ba8a-fwupd.service-txTLcP
drwx------ 3 root root 4096 Mar  7 05:49 systemd-private-c09f65b6edf14c99b94ea1939424ba8a-ModemManager.service-nK7Kw5
drwx------ 3 root root 4096 Mar  7 05:49 systemd-private-c09f65b6edf14c99b94ea1939424ba8a-polkit.service-EovV02
drwx------ 3 root root 4096 Mar  7 05:49 systemd-private-c09f65b6edf14c99b94ea1939424ba8a-systemd-logind.service-vmX4N8
drwx------ 3 root root 4096 Mar  7 05:49 systemd-private-c09f65b6edf14c99b94ea1939424ba8a-systemd-resolved.service-gcwTbN
drwx------ 3 root root 4096 Mar  7 05:56 systemd-private-c09f65b6edf14c99b94ea1939424ba8a-upower.service-imlDQi
root@ubuntuser:/tmp# cat tempfile.txt
cat: tempfile.txt: No such file or directory
```

/boot : 
```bash
root@ubuntuser:/tmp# cd /boot
root@ubuntuser:/boot# pwd
/boot
root@ubuntuser:/boot# ls -l | head -15
total 193576
-rw-r--r-- 1 root root   287599 Jan 13 13:56 config-6.8.0-100-generic
-rw-r--r-- 1 root root   287599 Feb  6 17:52 config-6.8.0-101-generic
drwxr-xr-x 5 root root     4096 Mar  7 06:42 grub
lrwxrwxrwx 1 root root       28 Mar  7 06:41 initrd.img -> initrd.img-6.8.0-101-generic
-rw-r--r-- 1 root root 74664848 Feb 21 15:16 initrd.img-6.8.0-100-generic
-rw-r--r-- 1 root root 74657887 Mar  7 06:42 initrd.img-6.8.0-101-generic
lrwxrwxrwx 1 root root       28 Feb 18 12:30 initrd.img.old -> initrd.img-6.8.0-100-generic
-rw------- 1 root root  9120274 Jan 13 13:56 System.map-6.8.0-100-generic
-rw------- 1 root root  9120274 Feb  6 17:52 System.map-6.8.0-101-generic
lrwxrwxrwx 1 root root       25 Mar  7 06:41 vmlinuz -> vmlinuz-6.8.0-101-generic
-rw------- 1 root root 15030664 Jan 13 14:42 vmlinuz-6.8.0-100-generic
-rw------- 1 root root 15030664 Feb  6 18:21 vmlinuz-6.8.0-101-generic
lrwxrwxrwx 1 root root       25 Feb 18 12:30 vmlinuz.old -> vmlinuz-6.8.0-100-generic
root@ubuntuser:/boot# cat config-5.15.0-69-generic | head -5
cat: config-5.15.0-69-generic: No such file or directory
```

### 3. Telusuri direktory /dev. Identifikasi perangkat yang tersedia. Identifikasi tty  (termninal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls –l).

Output
```bash
root@ubuntuser:/boot# cd /dev
root@ubuntuser:/dev# ls -l | head -15
total 0
crw-r--r--  1 root   root     10, 235 Mar  7 05:49 autofs
drwxr-xr-x  2 root   root         280 Mar  7 05:49 block
drwxr-xr-x  2 root   root          80 Mar  7 05:49 bsg
crw-rw----  1 root   disk     10, 234 Mar  7 05:49 btrfs-control
drwxr-xr-x  3 root   root          60 Mar  7 05:49 bus
lrwxrwxrwx  1 root   root           3 Mar  7 05:49 cdrom -> sr0
drwxr-xr-x  2 root   root        3800 Mar  7 06:39 char
crw-------  1 root   root      5,   1 Mar  7 05:49 console
lrwxrwxrwx  1 root   root          11 Mar  7 05:49 core -> /proc/kcore
drwxr-xr-x  5 root   root         100 Mar  7 05:49 cpu
crw-------  1 root   root     10, 123 Mar  7 05:49 cpu_dma_latency
crw-------  1 root   root     10, 203 Mar  7 05:49 cuse
drwxr-xr-x  7 root   root         140 Mar  7 05:49 disk
drwxr-xr-x  2 root   root          60 Mar  7 05:49 dma_heap
root@ubuntuser:/dev# who am i
yudhis   pts/2        2026-03-07 06:17 (10.0.2.2)
root@ubuntuser:/dev# ls -l /dev/pts/2
crw--w---- 1 root tty 136, 2 Mar  7 07:25 /dev/pts/2
root@ubuntuser:/dev# ls -l /dev/pts/0
crw--w---- 1 root tty 136, 0 Mar  7 05:50 /dev/pts/0
root@ubuntuser:/dev#
```

### 4. Telusuri derectory /proc. Tampilkan isi file interrupts, devices, cpuinfo, meminfo dan uptime menggunakan perintah cat. Dapatkah Anda melihat mengapa directory /proc disebut pseudo -filesystem yang memungkinkan akses ke struktur data kernel ?
 
>Direktori /proc disebut pseudo-filesystem (atau filesistem virtual) karena file-file di dalamnya tidak benar-benar tersimpan di disk. Sebaliknya, file-file tersebut dibuat secara dinamis oleh kernel saat diakses. Setiap kali kita membaca file di /proc, kernel mengambil data dari struktur data internalnya (seperti daftar proses, informasi hardware, statistik sistem) dan menyajikannya dalam format teks. Hal ini memungkinkan pengguna dan program untuk dengan mudah mengakses informasi kernel tanpa harus menggunakan system call khusus atau antarmuka pemrograman yang rumit.  
Output

```bash
root@ubuntuser:/dev# cd /proc
root@ubuntuser:/proc# cat interrupts
           CPU0       CPU1       CPU2
  0:        125          0          0   IO-APIC   2-edge      timer
  1:          0        111          0   IO-APIC   1-edge      i8042
  8:          0          0          0   IO-APIC   8-edge      rtc0
  9:          0          0          0   IO-APIC   9-fasteoi   acpi
 12:        158          0          0   IO-APIC  12-edge      i8042
 14:          0          0       5570   IO-APIC  14-edge      ata_piix
 15:          0          0          0   IO-APIC  15-edge      ata_piix
 18:          0          0          0   IO-APIC  18-fasteoi   vmwgfx
 19:          0          0      71375   IO-APIC  19-fasteoi   ehci_hcd:usb2, enp0s3
 20:          0       2125          0   IO-APIC  20-fasteoi   vboxguest
 21:      78621          0          0   IO-APIC  21-fasteoi   ahci[0000:00:0d.0], snd_intel8x0
 22:          0         26          0   IO-APIC  22-fasteoi   ohci_hcd:usb1
NMI:          0          0          0   Non-maskable interrupts
LOC:     158056     926706     183861   Local timer interrupts
SPU:          0          0          0   Spurious interrupts
PMI:          0          0          0   Performance monitoring interrupts
IWI:        240          7         15   IRQ work interrupts
RTR:          0          0          0   APIC ICR read retries
RES:       3664       3039       4172   Rescheduling interrupts
CAL:      72792      81222      68097   Function call interrupts
TLB:        205        234        235   TLB shootdowns
TRM:          0          0          0   Thermal event interrupts
THR:          0          0          0   Threshold APIC interrupts
DFR:          0          0          0   Deferred Error APIC interrupts
MCE:          0          0          0   Machine check exceptions
MCP:         19         19         19   Machine check polls
ERR:          0
MIS:          0
PIN:          0          0          0   Posted-interrupt notification event
NPI:          0          0          0   Nested posted-interrupt event
PIW:          0          0          0   Posted-interrupt wakeup event
root@ubuntuser:/proc# cat devices
Character devices:
  1 mem
  4 /dev/vc/0
  4 tty
  4 ttyS
  5 /dev/tty
  5 /dev/console
  5 /dev/ptmx
  5 ttyprintk
  7 vcs
 10 misc
 13 input
 21 sg
 29 fb
 89 i2c
108 ppp
116 alsa
128 ptm
136 pts
180 usb
189 usb_device
202 cpu/msr
203 cpu/cpuid
204 ttyMAX
226 drm
241 hidraw
242 ttyDBC
243 bsg
244 watchdog
245 remoteproc
246 ptp
247 pps
248 rtc
249 dma_heap
250 dax
251 dimmctl
252 ndctl
253 tpm
254 gpiochip
261 accel

Block devices:
  7 loop
  8 sd
  9 md
 11 sr
 65 sd
 66 sd
 67 sd
 68 sd
 69 sd
 70 sd
 71 sd
128 sd
129 sd
130 sd
131 sd
132 sd
133 sd
134 sd
135 sd
252 device-mapper
253 virtblk
254 mdp
259 blkext
root@ubuntuser:/proc# cat meminfo
MemTotal:        3504524 kB
MemFree:         2235180 kB
MemAvailable:    3064968 kB
Buffers:            7636 kB
Cached:           905672 kB
SwapCached:            0 kB
Active:           311768 kB
Inactive:         649788 kB
Active(anon):      58100 kB
Inactive(anon):        0 kB
Active(file):     253668 kB
Inactive(file):   649788 kB
Unevictable:       27300 kB
Mlocked:           27300 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:         75564 kB
Mapped:            84892 kB
Shmem:              1100 kB
KReclaimable:     120092 kB
Slab:             177888 kB
SReclaimable:     120092 kB
SUnreclaim:        57796 kB
KernelStack:        2784 kB
PageTables:         3196 kB
SecPageTables:         0 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     1752260 kB
Committed_AS:     371088 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       19572 kB
VmallocChunk:          0 kB
Percpu:             2096 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
Unaccepted:            0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
DirectMap4k:      114624 kB
DirectMap2M:     3500032 kB
root@ubuntuser:/proc# cat uptime
6146.11 17468.94
```


### 5. Ubahlah direktory home ke user lain secara langsung menggunakan cd ~username.

Output 
```bash
root@ubuntuser:/proc# cd ~yudhis
root@ubuntuser:/home/yudhis#
```  

### 6. Ubah kembali ke direktory home Anda

Output 
```bash
root@ubuntuser:/home/yudhis# cd
root@ubuntuser:~# pwd
/root
root@ubuntuser:~#
```

### 7. Buat subdirektory work dan play.

Output 
```bash
root@ubuntuser:~# mkdir work play
root@ubuntuser:~# ls -l
total 68
drwxr-xr-x 4 root root  4096 Mar  7 05:54 A
-rw-r--r-- 1 root root     0 Mar  1 03:54 backup-error.log
-rw-r--r-- 1 root root   704 Mar  1 03:53 backup-success.l
-rw-r--r-- 1 root root   704 Mar  1 03:54 backup-success.log
-rw-r--r-- 1 root root 30720 Mar  1 03:54 backup.tar
drwxr-xr-x 2 root root  4096 Mar  7 05:54 C
drwxr-xr-x 2 root root  4096 Mar  7 07:48 play
drwxr-xr-x 5 root root  4096 Mar  7 06:17 praktikum-os
-r-xr-xr-x 1 root root  7049 Feb 18 12:32 vboxpostinstall.sh
drwxr-xr-x 2 root root  4096 Mar  7 07:48 work
```

### 8. Hapus subdirektory work.

Output 
```bash
root@ubuntuser:~# rmdir work
root@ubuntuser:~# ls -l
total 64
drwxr-xr-x 4 root root  4096 Mar  7 05:54 A
-rw-r--r-- 1 root root     0 Mar  1 03:54 backup-error.log
-rw-r--r-- 1 root root   704 Mar  1 03:53 backup-success.l
-rw-r--r-- 1 root root   704 Mar  1 03:54 backup-success.log
-rw-r--r-- 1 root root 30720 Mar  1 03:54 backup.tar
drwxr-xr-x 2 root root  4096 Mar  7 05:54 C
drwxr-xr-x 2 root root  4096 Mar  7 07:48 play
drwxr-xr-x 5 root root  4096 Mar  7 06:17 praktikum-os
-r-xr-xr-x 1 root root  7049 Feb 18 12:32 vboxpostinstall.sh
```

### 9. Copy file /etc/passwd ke direktory home Anda.

Output 
```bash
root@ubuntuser:~# cp /etc/passwd .
root@ubuntuser:~# ls -l
total 68
drwxr-xr-x 4 root root  4096 Mar  7 05:54 A
-rw-r--r-- 1 root root     0 Mar  1 03:54 backup-error.log
-rw-r--r-- 1 root root   704 Mar  1 03:53 backup-success.l
-rw-r--r-- 1 root root   704 Mar  1 03:54 backup-success.log
-rw-r--r-- 1 root root 30720 Mar  1 03:54 backup.tar
drwxr-xr-x 2 root root  4096 Mar  7 05:54 C
-rw-r--r-- 1 root root  1783 Mar  7 07:51 passwd
drwxr-xr-x 2 root root  4096 Mar  7 07:48 play
drwxr-xr-x 5 root root  4096 Mar  7 06:17 praktikum-os
-r-xr-xr-x 1 root root  7049 Feb 18 12:32 vboxpostinstall.sh
```

### 10. Pindahkan ke subdirektory play

Output 
```bash
root@ubuntuser:~# mv passwd play/
root@ubuntuser:~# ls -l play
total 4
-rw-r--r-- 1 root root 1783 Mar  7 07:51 passwd
```

### 11. Ubahlah ke subdirektory play dan buat symbolic link dengan nama terminal yang menunjuk ke perangkat tty. Apa yang terjadi jika melakukan hard link ke perangkat tty ?

>Hard link tidak diizinkan untuk file device, meskipun sebagai root. 

Output 
```bash
root@ubuntuser:~# cd play
root@ubuntuser:~/play# pwd
/root/play
root@ubuntuser:~/play# who am i
yudhis   pts/2        2026-03-07 06:17 (10.0.2.2)
root@ubuntuser:~/play# ln -s /dev/pts/2 terminal
root@ubuntuser:~/play# ls -l
total 4
-rw-r--r-- 1 root root 1783 Mar  7 07:51 passwd
lrwxrwxrwx 1 root root   10 Mar  7 07:54 terminal -> /dev/pts/2
root@ubuntuser:~/play# ln /dev/pts/0 hardtty
ln: failed to create hard link 'hardtty' => '/dev/pts/0': Invalid cross-device link
```
 

### 12. Buatlah file bernama hello.txt yang berisi kata ”hello word”. Dapatkah Anda gunakan ”cp” menggunakan ”terminal” sebagai file asal untuk menghasilkan efek yang sama ?

>Tidak. Mencoba cp terminal hello2.txt akan membaca dari terminal (input keyboard) dan menulis ke file. Hasilnya tergantung apa yang diketik, bukan "hello word". 

Output 
```bash
root@ubuntuser:~/play# echo "hello word" > hello.txt
root@ubuntuser:~/play# cat hello.txt
hello word
```

### 13. Copy hello.txt ke terminal. Apa yang terjadi ?

>Tidak ada file baru, hanya output ke terminal.

Output 
```bash
root@ubuntuser:~/play# cp hello.txt /dev/pts/2
hello word
```

### 14. Masih direktory home, copy keseluruhan direktory play ke direktory bernama work menggunakan symbolic link

Output 
```bash
root@ubuntuser:~/play# cd ..
root@ubuntuser:~# pwd
/root
root@ubuntuser:~# ln -s play work
root@ubuntuser:~# ls -l
total 64
drwxr-xr-x 4 root root  4096 Mar  7 05:54 A
-rw-r--r-- 1 root root     0 Mar  1 03:54 backup-error.log
-rw-r--r-- 1 root root   704 Mar  1 03:53 backup-success.l
-rw-r--r-- 1 root root   704 Mar  1 03:54 backup-success.log
-rw-r--r-- 1 root root 30720 Mar  1 03:54 backup.tar
drwxr-xr-x 2 root root  4096 Mar  7 05:54 C
drwxr-xr-x 2 root root  4096 Mar  7 07:57 play
drwxr-xr-x 5 root root  4096 Mar  7 06:17 praktikum-os
-r-xr-xr-x 1 root root  7049 Feb 18 12:32 vboxpostinstall.sh
lrwxrwxrwx 1 root root     4 Mar  7 08:00 work -> play
```

### 15. Hapus direktory work dan isinya dengan satu perintah

Output 
```bash
root@ubuntuser:~# rm -rf work
root@ubuntuser:~# ls -l
total 64
drwxr-xr-x 4 root root  4096 Mar  7 05:54 A
-rw-r--r-- 1 root root     0 Mar  1 03:54 backup-error.log
-rw-r--r-- 1 root root   704 Mar  1 03:53 backup-success.l
-rw-r--r-- 1 root root   704 Mar  1 03:54 backup-success.log
-rw-r--r-- 1 root root 30720 Mar  1 03:54 backup.tar
drwxr-xr-x 2 root root  4096 Mar  7 05:54 C
drwxr-xr-x 2 root root  4096 Mar  7 07:57 play
drwxr-xr-x 5 root root  4096 Mar  7 06:17 praktikum-os
-r-xr-xr-x 1 root root  7049 Feb 18 12:32 vboxpostinstall.sh
```


## LAPORAN RESMI

### 1. Analisis Hasil Percobaan

### Percobaan 1: Direktory

### a. Analisis Setiap Hasil Tampilan   

* $ pwd  
Menampilkan direktori aktif saat ini, yaitu /home/user (home user).

* $ echo $HOME  
Menampilkan variabel lingkungan HOME yang berisi path home user, sama dengan hasil pwd.

* $ cd .  
Perintah cd . berpindah ke direktori saat ini (titik berarti direktori sendiri). Tidak ada perubahan direktori.

* $ pwd  
Masih /home/user.

* $ cd ..  
Berpindah ke parent direktori, yaitu /home.

* $ pwd  
Menampilkan /home.

* $ cd  
Tanpa argumen, cd kembali ke home user, yaitu /home/user.

* $ mkdir A B C A/D A/E B/F A/D/A  
Perintah ini membuat struktur direktori:

    * A, B, C di level pertama.

    * Di dalam A dibuat D dan E.

    * Di dalam B dibuat F.

    * Di dalam A/D dibuat A.
    Tidak ada output jika berhasil.

* $ ls -l  
Menampilkan daftar direktori A, B, C beserta atributnya.

* $ ls -l A  
Menampilkan isi direktori A, yaitu D dan E.

* $ ls -l A/D  
Menampilkan isi A/D, yaitu subdirektori A.

* $ rmdir B   
Mencoba menghapus direktori B. Error: rmdir: failed to remove 'B': Directory not empty karena B masih berisi subdirektori F.

* $ ls -l B  
Menampilkan isi B, yaitu F.

* $ rmdir B/F B  
Perintah ini menghapus B/F terlebih dahulu, kemudian B. Setelah B/F dihapus, B menjadi kosong sehingga rmdir B berhasil. Tidak ada output.

* $ ls -l B  
Error: ls: cannot access 'B': No such file or directory karena B sudah dihapus.

* Navigasi dengan cd:

    * $ cd A → pindah ke A, pwd menjadi /home/user/A.

    * $ cd . → tetap di A.

    * $ cd /home/user/C → pindah ke C dengan path absolut, berhasil jika C ada.

    * $ cd /user/C → Error: bash: cd: /user/C: No such file or directory karena path yang benar adalah /home/user/C, bukan /user/C.

### b. Pohon Struktur File dan Direktori (Percobaan 1 point 3)  

Berdasarkan perintah mkdir A B C A/D A/E B/F A/D/A, struktur direktori yang terbentuk adalah:
```bash
/home/user/
├── A
│   ├── D
│   │   └── A
│   └── E
├── B
│   └── F
└── C
```

### c. Penjelasan Pesan Error

* rmdir B error karena direktori tidak kosong. rmdir hanya dapat menghapus direktori kosong. Untuk menghapus direktori berisi, harus menggunakan rm -r.

* ls -l B setelah dihapus error karena direktori sudah tidak ada.

* cd /user/C error karena path absolut salah. Root (/) tidak memiliki direktori user; yang benar adalah /home/user/C.


### Percobaan 2: Manipulasi File

### a. Analisis Hasil Tampilan

* $ cat > contoh  
Membuat file contoh dengan input keyboard. Akhiri dengan Ctrl+D.

* $ cp contoh contoh1  
Menyalin contoh menjadi contoh1.

* $ ls -l  
Menampilkan kedua file.

* $ cp contoh A  
Menyalin contoh ke dalam direktori A (menjadi A/contoh).

* $ ls -l A  
Isi A sekarang ada file contoh dan subdirektori D, E.

* $ cp contoh contoh1 A/D  
Menyalin dua file ke dalam A/D.

* $ ls -l A/D  
Di A/D sekarang terdapat file contoh, contoh1, dan subdirektori A.

* $ mv contoh contoh2  
Memindahkan (rename) contoh menjadi contoh2.

* $ ls -l  
File contoh hilang, muncul contoh2.

* $ mv contoh1 contoh2 A/D  
Memindahkan contoh1 dan contoh2 ke dalam direktori A/D.

* $ ls -l A/D  
Di A/D sekarang terdapat file contoh, contoh1, contoh2, dan subdirektori A.

* $ mv contoh contoh1 C  
Error: mv: cannot stat 'contoh': No such file or directory (mungkin salah satu atau kedua file sudah tidak ada karena sudah dipindah ke A/D).

* $ ls -l C  
Direktori C kosong.

* $ rm contoh2  
Error: rm: cannot remove 'contoh2': No such file or directory karena file sudah dipindah.

* $ ls -l  
Hanya tersisa direktori A dan C.

* $ rm -i contoh  
Error: file tidak ada.

* $ rm -rf A C   
Menghapus seluruh direktori A dan C beserta isinya. Perintah -rf memaksa penghapusan rekursif tanpa konfirmasi.


### Percobaan 3 : Symbolic Link

### a. Analisis Hasil Tampilan

* $ echo "Hallo apa khabar" > halo.txt  
Membuat file teks.

* $ ls -l  
File halo.txt muncul.

* $ ln halo.txt z  
Membuat hard link z ke halo.txt.

* $ ls -l  
Dua file dengan ukuran sama dan link count menjadi 2 (kolom ketiga).

* $ cat z  
Menampilkan isi yang sama.

* $ mkdir mydir  
Membuat direktori.

* $ ln z mydir/halo.juga  
Membuat hard link lain di dalam mydir.

* $ cat mydir/halo.juga  
Isi sama.

* $ ln -s z bye.txt  
Membuat soft link bye.txt yang menunjuk ke z.

* $ ls -l bye.txt  
Menampilkan bye.txt -> z.

* $ cat bye.txt  
Membaca isi bye.txt (mengikuti link) dan menampilkan teks.

### Percobaan 4: Melihat Isi File

### a. Analisis Hasil Tampilan

* $ file halo.txt → output: halo.txt: ASCII text

* $ file bye.txt → output: bye.txt: symbolic link to z

### Percobaan 5: Mencari File

### a. Analisis Hasil Tampilan

*  $ find /home -name "*.txt" -print > myerror.txt  
Mencari semua file .txt di bawah /home, hasil disimpan ke myerror.txt.

* $ cat myerror.txt  
Menampilkan daftar file yang ditemukan.

* $ find . -name "*.txt" -exec wc -l '{}' ';'  
Menghitung jumlah baris setiap file .txt di direktori saat ini.

* $ which ls  
Menampilkan lokasi program ls, misal /bin/ls.

* $ locate "*.txt"  
Mencari semua file .txt menggunakan database locate.

### Percobaan 6: Mencari Teks pada File

### a. Analisis Hasil Tampilan

* $ grep Hallo *.txt  
Mencari kata "Hallo" di semua file .txt. Output menampilkan baris yang mengandung kata tersebut beserta nama file.



### Analisis Hasil Latihan

### Latihan 1: Urutan Perintah Navigasi

* $cd → pindah ke home.

* pwd → /home/user.

* ls -al → menampilkan semua file termasuk yang tersembunyi.

* cd . → tetap.

* pwd → /home/user.

* cd .. → pindah ke /home.

* pwd → /home.

* ls -al → menampilkan isi /home (direktori user).

* cd .. → pindah ke root (/).

* pwd → /.

* ls -al → menampilkan isi root.

* cd /etc → pindah ke /etc.

* ls -al | more → menampilkan isi /etc per halaman.

* cat passwd → menampilkan isi file /etc/passwd.

* cd - → kembali ke direktori sebelumnya, yaitu /.

* pwd → /.

### Latihan 2: Penelusuran Direktori Sistem

* /bin → berisi perintah dasar (binary) untuk semua user.

* /usr/bin → berisi lebih banyak perintah dan aplikasi.

* /sbin → berisi perintah untuk administrasi sistem (biasanya hanya root).

* /tmp → direktori sementara, dapat diakses semua user.

* /boot → berisi file boot seperti kernel dan initrd.

Semua direktori ditelusuri dengan cd, ls, dan cat untuk file teks (misal config di /boot).

### Latihan 3: Direktori /dev dan Terminal

* ls -l /dev menampilkan banyak file device.

* who am i menunjukkan terminal yang digunakan, misal pts/0.

* ls -l /dev/pts/0 menunjukkan pemilik terminal adalah user yang login (misal ubuntuser) dan group tty.

### Latihan 4: Direktori /proc

* cat /proc/interrupts, devices, cpuinfo, meminfo, uptime menampilkan informasi kernel.

* /proc disebut pseudo-filesystem karena file-file di dalamnya tidak tersimpan di disk, melainkan dibuat dinamis oleh kernel saat diakses.

### Latihan 5: cd ~username

* Jika user lain ada dan diizinkan, pindah ke home-nya. Biasanya user biasa tidak bisa karena izin, hanya root yang bisa.

### Latihan 6: cd kembali ke home sendiri.

### Latihan 7–8: Membuat dan menghapus direktori work dan play.

### Latihan 9–10: Menyalin /etc/passwd ke home lalu memindah ke play.

### Latihan 11: Symbolic link ke terminal

* ln -s /dev/pts/0 terminal berhasil.

* Hard link ke device gagal karena device file tidak mendukung hard link (berbeda filesystem dan tipe khusus).

### Latihan 12–13: File hello.txt

* cp terminal hello2.txt tidak menghasilkan efek sama karena membaca input.

* cp hello.txt /dev/pts/0 mencetak isi file ke layar.

### Latihan 14: Membuat symbolic link work ke play

* ln -s play work membuat link, bukan copy.

### Latihan 15: Menghapus link work

* rm -rf work hanya menghapus link, bukan direktori play.


### 3. Kesimpulan

Praktikum ini memberikan pemahaman komprehensif tentang sistem file Linux, meliputi struktur hierarkis dari root (/), fungsi direktori standar, serta penggunaan perintah dasar seperti cd, mkdir, cp, mv, dan rm untuk navigasi dan manipulasi file. Konsep link dipelajari melalui perbedaan hard link yang berbagi inode dan soft link sebagai pointer, dengan pemahaman bahwa hard link tidak dapat digunakan untuk direktori atau lintas filesystem. Selain itu, praktikum memperkenalkan pseudo-filesystem /proc yang menyediakan akses real-time ke data kernel, serta representasi perangkat keras sebagai file di /dev. Kemampuan mencari file dan teks dengan perintah find, locate, which, dan grep juga menjadi keterampilan penting. Secara keseluruhan, praktikum ini membangun fondasi yang kokoh untuk administrasi sistem dan pengembangan di lingkungan Linux.


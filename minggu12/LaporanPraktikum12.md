# Laporan Praktikum 11

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## PRAKTIKUM

## Praktikum 9.1

### Langkah 1
Input :
```bash
systemctl list-units --type=service --state=running
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl list-units --type=service --state=running
  UNIT                           LOAD   ACTIVE SUB     DESCRIPTION         >
  cron.service                   loaded active running Regular background p>
  dbus.service                   loaded active running D-Bus System Message>
  getty@tty1.service             loaded active running Getty on tty1
  ModemManager.service           loaded active running Modem Manager
  multipathd.service             loaded active running Device-Mapper Multip>
  polkit.service                 loaded active running Authorization Manager
  rsyslog.service                loaded active running System Logging Servi>
  ssh.service                    loaded active running OpenBSD Secure Shell>
  systemd-journald.service       loaded active running Journal Service
  systemd-logind.service         loaded active running User Login Management
  systemd-networkd.service       loaded active running Network Configuration
  systemd-resolved.service       loaded active running Network Name Resolut>
  systemd-udevd.service          loaded active running Rule-based Manager f>
  udisks2.service                loaded active running Disk Manager
  unattended-upgrades.service    loaded active running Unattended Upgrades >
  user@0.service                 loaded active running User Manager for UID>
  user@1000.service              loaded active running User Manager for UID>
  virtualbox-guest-utils.service loaded active running Virtualbox guest uti>

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization >
        SUB    → The low-level unit activation state, values depend on unit>

18 loaded units listed.
```

### Langkah 2
Input :
```bash
systemctl list-unit-files --type=service | head -30
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl list-unit-files --type=service | head -30
UNIT FILE                                    STATE           PRESET
apparmor.service                             enabled         enabled
apport-autoreport.service                    static          -
apport-coredump-hook@.service                static          -
apport-forward@.service                      static          -
apport.service                               enabled         enabled
apt-daily-upgrade.service                    static          -
apt-daily.service                            static          -
apt-news.service                             static          -
autovt@.service                              alias           -
blk-availability.service                     enabled         enabled
bolt.service                                 static          -
cloud-config.service                         enabled         enabled
cloud-final.service                          enabled         enabled
cloud-init-hotplugd.service                  static          -
cloud-init-local.service                     enabled         enabled
cloud-init.service                           enabled         enabled
console-getty.service                        disabled        disabled
console-setup.service                        enabled         enabled
container-getty@.service                     static          -
cron.service                                 enabled         enabled
cryptdisks-early.service                     masked          enabled
cryptdisks.service                           masked          enabled
dbus-org.freedesktop.hostname1.service       alias           -
dbus-org.freedesktop.locale1.service         alias           -
dbus-org.freedesktop.login1.service          alias           -
dbus-org.freedesktop.ModemManager1.service   alias           -
dbus-org.freedesktop.resolve1.service        alias           -
dbus-org.freedesktop.thermald.service        alias           -
dbus-org.freedesktop.timedate1.service       alias           -
```

### Langkah 3
Input :
```bash
systemd-analyze
systemd-analyze blame | head -15
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemd-analyze
Startup finished in 13.124s (kernel) + 12.424s (userspace) = 25.549s
graphical.target reached after 12.299s in userspace.
root@ubuntuser:~/praktikum-os/week12# systemd-analyze blame | head -15
6.582s dev-sda2.device
6.381s snapd.seeded.service
6.117s snapd.service
5.268s dpkg-db-backup.service
3.931s systemd-networkd.service
2.582s ModemManager.service
2.426s polkit.service
2.308s udisks2.service
2.244s grub-common.service
2.113s rsyslog.service
2.039s virtualbox-guest-utils.service
1.978s apparmor.service
1.869s systemd-networkd-wait-online.service
1.617s apport.service
1.344s dbus.service
```

### Tantangan

Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan. Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat fungsinya.

Input :
```bash
systemd-analyze blame | head -3
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemd-analyze blame | head -3
6.582s dev-sda2.device
6.381s snapd.seeded.service
6.117s snapd.service
```

Input :
```bash
systemctl cat dev-sda2.device 2>/dev/null || echo "Device unit tidak memiliki file unit terpisah"

systemctl cat snapd.seeded.service

systemctl cat snapd.service | head -15
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl cat dev-sda2.device 2>/dev/null || echo "Device unit tidak memiliki file unit terpisah"
Device unit tidak memiliki file unit terpisah
root@ubuntuser:~/praktikum-os/week12# systemctl cat snapd.seeded.service
# /usr/lib/systemd/system/snapd.seeded.service
[Unit]
Description=Wait until snapd is fully seeded
After=snapd.socket
Requires=snapd.socket

[Service]
Type=oneshot
ExecStart=/usr/bin/snap wait system seed.loaded
RemainAfterExit=true

[Install]
WantedBy=multi-user.target cloud-final.service
# This is handled special in snapd
# X-Snapd-Snap: do-not-start
root@ubuntuser:~/praktikum-os/week12# systemctl cat snapd.service | head -15
# /usr/lib/systemd/system/snapd.service
[Unit]
Description=Snap Daemon
After=snapd.socket
After=time-set.target
After=snapd.mounts.target
Wants=time-set.target
Wants=snapd.mounts.target
Requires=snapd.socket
OnFailure=snapd.failure.service
# This is handled by snapd
# X-Snapd-Snap: do-not-start

[Service]
# Disabled because it breaks lxd
```

PENJELASAN :

1. dev-sda2.device (6.582s)  
Ini bukanlah layanan, melainkan unit device yang merepresentasikan partisi disk sda2. Waktu inisialisasi yang lama biasanya disebabkan oleh Proses mounting filesystem, Check disk (fsck) yang berjalan, Filesystem yang besar atau lambat, dan Kemungkinan partisi swap atau LVM

2. snapd.seeded.service (6.381s)  
Layanan ini menunggu sampai snapd selesai melakukan seeding (inisialisasi awal snap packages). Seeding adalah proses dimana snapd Mengunduh snap core yang diperlukan, Menyiapkan lingkungan snap, Memverifikasi dan memasang snap dasar

3. snapd.service (6.117s)  
Snap Daemon adalah layanan utama untuk mengelola paket snap. Waktu inisialisasi yang lama disebabkan oleh Memuat dan memverifikasi snap packages yang terpasang, Menyiapkan lingkungan container untuk snap, Memeriksa dan memperbarui mount points snap, Inisialisasi koneksi ke Snap Store


## Praktikum 9.2

### Langkah 1
Input :
```bash
systemctl status ssh
systemctl is-active ssh
systemctl is-enabled ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: >
     Active: active (running) since Fri 2026-05-15 05:42:25 UTC; 23min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 857 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCC>
   Main PID: 869 (sshd)
      Tasks: 6 (limit: 4008)
     Memory: 8.4M (peak: 23.5M)
        CPU: 8.267s
     CGroup: /system.slice/ssh.service
             ├─ 869 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startup>
             ├─1133 "sshd: yudhis [priv]"
             ├─1135 "sshd: yudhis@pts/1"
             ├─1136 -bash
             ├─1145 sudo su
             └─1146 sudo su

May 15 05:42:24 ubuntuser systemd[1]: Starting ssh.service - OpenBSD Secure>
May 15 05:42:25 ubuntuser sshd[869]: Server listening on 0.0.0.0 port 22.
May 15 05:42:25 ubuntuser sshd[869]: Server listening on :: port 22.
May 15 05:42:25 ubuntuser systemd[1]: Started ssh.service - OpenBSD Secure >
May 15 05:48:00 ubuntuser sshd[1133]: Accepted password for yudhis from 10.>
May 15 05:48:20 ubuntuser sudo[1145]:   yudhis : TTY=pts/1 ; PWD=/home/yudh>
May 15 05:48:20 ubuntuser sudo[1145]: pam_unix(sudo:session): session opene>
May 15 05:48:20 ubuntuser su[1147]: (to root) root on pts/2
May 15 05:48:20 ubuntuser su[1147]: pam_unix(su:session): session opened fo>
root@ubuntuser:~/praktikum-os/week12# systemctl is-active ssh
active
root@ubuntuser:~/praktikum-os/week12# systemctl is-enabled ssh
enabled
```

### Langkah 2
Input :
```bash
sudo systemctl restart ssh
systemctl status ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo systemctl restart ssh
root@ubuntuser:~/praktikum-os/week12# systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: >
     Active: active (running) since Fri 2026-05-15 06:08:21 UTC; 12s ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 1350 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUC>
   Main PID: 1352 (sshd)
      Tasks: 6 (limit: 4008)
     Memory: 8.6M (peak: 23.5M)
        CPU: 279ms
     CGroup: /system.slice/ssh.service
             ├─1133 "sshd: yudhis [priv]"
             ├─1135 "sshd: yudhis@pts/1"
             ├─1136 -bash
             ├─1145 sudo su
             ├─1146 sudo su
             └─1352 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startup>

May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates u>
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: Found left-over process >
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates u>
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: Found left-over process >
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates u>
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: Found left-over process >
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates u>
May 15 06:08:21 ubuntuser sshd[1352]: Server listening on 0.0.0.0 port 22.
May 15 06:08:21 ubuntuser sshd[1352]: Server listening on :: port 22.
May 15 06:08:21 ubuntuser systemd[1]: Started ssh.service - OpenBSD Secure >
```

### Langkah 3
Input :
```bash
systemctl list-dependencies ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl list-dependencies ssh
ssh.service
● ├─-.mount
● ├─ssh.socket
● ├─system.slice
● └─sysinit.target
●   ├─apparmor.service
●   ├─blk-availability.service
●   ├─dev-hugepages.mount
●   ├─dev-mqueue.mount
●   ├─finalrd.service
●   ├─keyboard-setup.service
●   ├─kmod-static-nodes.service
○   ├─ldconfig.service
●   ├─lvm2-lvmpolld.socket
●   ├─lvm2-monitor.service
●   ├─multipathd.service
○   ├─open-iscsi.service
●   ├─plymouth-read-write.service
●   ├─plymouth-start.service
●   ├─proc-sys-fs-binfmt_misc.automount
●   ├─setvtrgb.service
●   ├─sys-fs-fuse-connections.mount
●   ├─sys-kernel-config.mount
●   ├─sys-kernel-debug.mount
●   ├─sys-kernel-tracing.mount
○   ├─systemd-ask-password-console.path
●   ├─systemd-binfmt.service
○   ├─systemd-firstboot.service
○   ├─systemd-hwdb-update.service
○   ├─systemd-journal-catalog-update.service
●   ├─systemd-journal-flush.service
●   ├─systemd-journald.service
○   ├─systemd-machine-id-commit.service
●   ├─systemd-modules-load.service
○   ├─systemd-pcrmachine.service
○   ├─systemd-pcrphase-sysinit.service
○   ├─systemd-pcrphase.service
○   ├─systemd-pstore.service
●   ├─systemd-random-seed.service
○   ├─systemd-repart.service
●   ├─systemd-resolved.service
●   ├─systemd-sysctl.service
```

### Langkah 4
Input :
```bash
systemctl --failed
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl --failed
  UNIT            LOAD   ACTIVE SUB    DESCRIPTION
● quotaon.service loaded failed failed Enable File System Quotas

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization >
        SUB    → The low-level unit activation state, values depend on unit>

1 loaded units listed.
```

### Tantangan
Input :
```bash
cd ~/lab-os/chapter10-services
nano cek-layanan.sh
#!/bin/bash

# Skrip untuk memeriksa status layanan dari file daftar
# Penggunaan: ./cek-layanan.sh daftar-layanan.txt

# File input: daftar layanan (satu nama per baris)
INPUT_FILE="${1:-daftar-layanan.txt}"

# File output laporan
OUTPUT_FILE="laporan-layanan.log"

# Validasi file input
if [ ! -f "$INPUT_FILE" ]; then
    echo "Error: File '$INPUT_FILE' tidak ditemukan!"
    echo "Buat file dengan daftar nama layanan (contoh: ssh, cron, rsyslog)"
    exit 1
fi

# Tulis header ke file output
echo "=====================================" > "$OUTPUT_FILE"
echo "LAPORAN STATUS LAYANAN" >> "$OUTPUT_FILE"
echo "Waktu: $(date '+%Y-%m-%d %H:%M:%S')" >> "$OUTPUT_FILE"
echo "=====================================" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Baca setiap baris dari file input
while read -r service; do
    # Skip baris kosong
    if [ -z "$service" ]; then
        continue
    fi
    
    # Periksa status layanan
    if systemctl is-active --quiet "$service"; then
        status="ACTIVE"
    else
        status="INACTIVE"
    fi
    
    # Tulis ke laporan dengan format [TANGGAL] nama-layanan: STATUS
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $service: $status" | tee -a "$OUTPUT_FILE"
    
done < "$INPUT_FILE"

echo ""
echo "Laporan tersimpan di: $OUTPUT_FILE"

chmod +x cek-layanan.sh
nano daftar-layanan.txt
text
ssh
cron
rsyslog
cups
apache2
bash
./cek-layanan.sh daftar-layanan.txt

cat laporan-layanan.log
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# cd ~/lab-os/chapter10-services
bash: cd: /root/lab-os/chapter10-services: No such file or directory
root@ubuntuser:~/praktikum-os/week12# nano cek-layanan.sh


root@ubuntuser:~/praktikum-os/week12# ./cek-layanan.sh daftar-layanan.txt
[2026-05-15 06:13:46] ssh: ACTIVE
[2026-05-15 06:13:46] cron: ACTIVE
[2026-05-15 06:13:46] rsyslog: ACTIVE
[2026-05-15 06:13:46] cups: INACTIVE
[2026-05-15 06:13:46] apache2: INACTIVE

Laporan tersimpan di: laporan-layanan.log
root@ubuntuser:~/praktikum-os/week12# cat laporan-layanan.log
=====================================
LAPORAN STATUS LAYANAN
Waktu: 2026-05-15 06:13:46
=====================================

[2026-05-15 06:13:46] ssh: ACTIVE
[2026-05-15 06:13:46] cron: ACTIVE
[2026-05-15 06:13:46] rsyslog: ACTIVE
[2026-05-15 06:13:46] cups: INACTIVE
[2026-05-15 06:13:46] apache2: INACTIVE
```


## Praktikum 9.3

### Langkah 1
Input :
```bash
cd ~/lab-os/chapter10-services
mkdir -p situs-demo
nano situs-demo/index.html

<!DOCTYPE html>
<html>
<head>
    <title>Demo Web Server</title>
    <meta charset="utf-8">
</head>
<body>
    <h1>Halo dari layanan systemd kustom!</h1>
    <p>Layanan ini dibuat pada praktek Bab 10.</p>
    <hr>
    <p><small>Server berjalan sebagai service systemd</small></p>
</body>
</html>
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# cd /root/lab-os/chapter10-services
root@ubuntuser:~/lab-os/chapter10-services# mkdir -p situs-demo
root@ubuntuser:~/lab-os/chapter10-services# nano situs-demo/index.html
```

### Langkah 2
Input :
```bash
nano ~/lab-os/chapter10-services/jalankan-server.sh

#!/bin/bash
# Skrip wrapper untuk server HTTP Python

DIREKTORI="$HOME/lab-os/chapter10-services/situs-demo"
PORT=9090

echo "Memulai server di port $PORT..."
echo "Melayani direktori: $DIREKTORI"

# Jalankan server HTTP Python
exec python3 -m http.server $PORT --directory "$DIREKTORI"

chmod +x ~/lab-os/chapter10-services/jalankan-server.sh
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# nano ~/lab-os/chapter10-services/jalankan-server.sh
root@ubuntuser:~/lab-os/chapter10-services# chmod +x ~/lab-os/chapter10-services/jalankan-server.sh
```

### Langkah 3
Input :
```bash
nano ~/lab-os/chapter10-services/demo-web.service

[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=yudhis
ExecStart=/root/lab-os/chapter10-services/jalankan-server.sh
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target

sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# nano ~/lab-os/chapter10-services/demo-web.service
root@ubuntuser:~/lab-os/chapter10-services# sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service
root@ubuntuser:~/lab-os/chapter10-services# sudo systemctl daemon-reload
```

### Langkah 4
Input :
```bash
sudo systemctl start demo-web
systemctl status demo-web
curl http://localhost:9090
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# curl http://localhost:9090
<!DOCTYPE html>
<html>
<head>
    <title>Demo Web Server</title>
    <meta charset="utf-8">
</head>
<body>
    <h1>Halo dari layanan systemd kustom!</h1>
    <p>Layanan ini dibuat pada praktek Bab 10.</p>
    <hr>
    <p><small>Server berjalan sebagai service systemd</small></p>
</body>
</html>
```

### Langkah 5
Input :
```bash
systemctl status demo-web | grep "Main PID"
sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
sleep 5
systemctl status demo-web
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# systemctl status demo-web | grep "Main PID"
   Main PID: 2394 (python3)
   root@ubuntuser:~/lab-os/chapter10-services# sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
root@ubuntuser:~/lab-os/chapter10-services# sleep 5
root@ubuntuser:~/lab-os/chapter10-services# systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; disabled; preset>
     Active: active (running) since Fri 2026-05-15 06:59:41 UTC; 11s ago
   Main PID: 2426 (python3)
      Tasks: 1 (limit: 4008)
     Memory: 9.3M (peak: 9.6M)
        CPU: 327ms
     CGroup: /system.slice/demo-web.service
             └─2426 python3 -m http.server 9090

May 15 06:59:41 ubuntuser systemd[1]: demo-web.service: Scheduled restart j>
May 15 06:59:41 ubuntuser systemd[1]: Started demo-web.service - Demo Web S>
May 15 06:59:41 ubuntuser jalankan-server.sh[2426]: Memulai server di port >
May 15 06:59:41 ubuntuser jalankan-server.sh[2426]: Melayani direktori: /ro>
```

### Langkah 6
Input :
```bash
sudo systemctl disable --now demo
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# sudo systemctl disable --now demo
-web
root@ubuntuser:~/lab-os/chapter10-services# sudo rm /etc/systemd/system/demo-web.service
root@ubuntuser:~/lab-os/chapter10-services# sudo systemctl daemon-reload
```

### Tantangan
Input :
```bash
sudo nano /etc/systemd/system/demo-web.service

[Unit]
Description=Demo Web Server Praktek Bab 10 (Modified)
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/lab-os/chapter10-services/situs-demo
Environment="PORT=9091"
ExecStart=/usr/bin/python3 -m http.server ${PORT}
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl enable --now demo-web
systemctl status demo-web
curl http://localhost:9091
systemctl is-enabled demo-web
sudo systemctl disable --now demo-web
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# sudo nano /etc/systemd/system/demo-web.service
root@ubuntuser:~/lab-os/chapter10-services# sudo systemctl daemon-reload
root@ubuntuser:~/lab-os/chapter10-services# sudo systemctl enable --now demo-web
Created symlink /etc/systemd/system/multi-user.target.wants/demo-web.service → /etc/systemd/system/demo-web.service.
root@ubuntuser:~/lab-os/chapter10-services# systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10 (Modified)
     Loaded: loaded (/etc/systemd/system/demo-web.service; enabled; preset: >
     Active: active (running) since Fri 2026-05-15 07:04:34 UTC; 8s ago
   Main PID: 3103 (python3)
      Tasks: 1 (limit: 4008)
     Memory: 9.3M (peak: 9.5M)
        CPU: 200ms
     CGroup: /system.slice/demo-web.service
             └─3103 /usr/bin/python3 -m http.server 9091

May 15 07:04:34 ubuntuser systemd[1]: Started demo-web.service - Demo Web Se>
root@ubuntuser:~/lab-os/chapter10-services# curl http://localhost:9091
<!DOCTYPE html>
<html>
<head>
    <title>Demo Web Server</title>
    <meta charset="utf-8">
</head>
<body>
    <h1>Halo dari layanan systemd kustom!</h1>
    <p>Layanan ini dibuat pada praktek Bab 10.</p>
    <hr>
    <p><small>Server berjalan sebagai service systemd</small></p>
</body>
</html>
root@ubuntuser:~/lab-os/chapter10-services# systemctl is-enabled demo-web
enabled
root@ubuntuser:~/lab-os/chapter10-services# sudo systemctl disable --now demo-web
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
Removed "/etc/systemd/system/multi-user.target.wants/demo-web.service".
```


## Praktikum 9.4

### Langkah 1
Input :
```bash
journalctl -u ssh --since "1 hour ago" --no-pager
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# journalctl -u ssh --since "1 hour ago" --no-pager
-- No entries --
```

### Langkah 2
Input :
```bash
journalctl -b -p err --no-pager
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# journalctl -b -p err --no-pager
May 15 05:42:16 ubuntuser systemd[1]: Failed to start quotaon.service - Enable File System Quotas.
May 15 05:42:24 ubuntuser kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* vmwgfx seems to be running on an unsupported hypervisor.
May 15 05:42:24 ubuntuser kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* This configuration is likely broken.
May 15 05:42:24 ubuntuser kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* Please switch to a supported graphics device to avoid problems.
May 15 05:47:09 ubuntuser login[907]: PAM unable to dlopen(pam_lastlog.so): /usr/lib/security/pam_lastlog.so: cannot open shared object file: No such file or directory
May 15 05:47:09 ubuntuser login[907]: PAM adding faulty module: pam_lastlog.so
May 15 06:32:35 ubuntuser (python3)[1603]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:39 ubuntuser (python3)[1605]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:42 ubuntuser (python3)[1607]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:45 ubuntuser (python3)[1609]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:48 ubuntuser (python3)[1612]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:52 ubuntuser (python3)[1614]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:55 ubuntuser (python3)[1616]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:32:58 ubuntuser (python3)[1620]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:01 ubuntuser (python3)[1622]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:05 ubuntuser (python3)[1624]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:08 ubuntuser (python3)[1626]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:11 ubuntuser (python3)[1628]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:14 ubuntuser (python3)[1630]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:18 ubuntuser (python3)[1632]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:21 ubuntuser (python3)[1634]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:24 ubuntuser (python3)[1636]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:27 ubuntuser (python3)[1639]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:31 ubuntuser (python3)[1641]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:34 ubuntuser (python3)[1643]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:37 ubuntuser (python3)[1646]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:40 ubuntuser (python3)[1648]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:44 ubuntuser (python3)[1651]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:47 ubuntuser (python3)[1653]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:50 ubuntuser (python3)[1655]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:53 ubuntuser (python3)[1658]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:33:57 ubuntuser (python3)[1660]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:00 ubuntuser (python3)[1663]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:03 ubuntuser (python3)[1666]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:06 ubuntuser (python3)[1668]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:10 ubuntuser (python3)[1670]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:13 ubuntuser (python3)[1672]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:16 ubuntuser (python3)[1674]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:19 ubuntuser (python3)[1676]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:23 ubuntuser (python3)[1678]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:26 ubuntuser (python3)[1680]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:29 ubuntuser (python3)[1682]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:32 ubuntuser (python3)[1684]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:36 ubuntuser (python3)[1687]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:39 ubuntuser (python3)[1689]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:42 ubuntuser (python3)[1691]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:45 ubuntuser (python3)[1693]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:49 ubuntuser (python3)[1695]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:52 ubuntuser (python3)[1698]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:55 ubuntuser (python3)[1700]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:34:58 ubuntuser (python3)[1702]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:02 ubuntuser (python3)[1707]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:05 ubuntuser (python3)[1709]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:08 ubuntuser (python3)[1711]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:11 ubuntuser (python3)[1713]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:15 ubuntuser (python3)[1715]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:18 ubuntuser (python3)[1717]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:21 ubuntuser (python3)[1719]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:24 ubuntuser (python3)[1721]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:28 ubuntuser (python3)[1723]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:31 ubuntuser (python3)[1725]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:34 ubuntuser (python3)[1727]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:37 ubuntuser (python3)[1729]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:41 ubuntuser (python3)[1731]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:44 ubuntuser (python3)[1735]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:47 ubuntuser (python3)[1737]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:50 ubuntuser (python3)[1739]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:54 ubuntuser (python3)[1741]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:35:57 ubuntuser (python3)[1743]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:00 ubuntuser (python3)[1745]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:03 ubuntuser (python3)[1747]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:07 ubuntuser (python3)[1749]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:10 ubuntuser (python3)[1753]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:13 ubuntuser (python3)[1755]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:16 ubuntuser (python3)[1757]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:20 ubuntuser (python3)[1759]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:23 ubuntuser (python3)[1761]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:26 ubuntuser (python3)[1763]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:29 ubuntuser (python3)[1765]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:33 ubuntuser (python3)[1767]: demo-web.service: Changing to the requested working directory failed: No such file or directory
May 15 06:36:36 ubuntuser (python3)[1769]: demo-web.service: Changing to the requested working directory failed: No such file or directory
```

### Langkah 3
Input :
```bash
journalctl -u ssh -f
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# journalctl -u ssh -f
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: Found left-over process 1136 (bash) in control group while starting unit. Ignoring.
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: Found left-over process 1145 (sudo) in control group while starting unit. Ignoring.
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: Found left-over process 1146 (sudo) in control group while starting unit. Ignoring.
May 15 06:08:21 ubuntuser systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
May 15 06:08:21 ubuntuser sshd[1352]: Server listening on 0.0.0.0 port 22.
May 15 06:08:21 ubuntuser sshd[1352]: Server listening on :: port 22.
May 15 06:08:21 ubuntuser systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
```

### Langkah 4
Input :
```bash
cd ~/lab-os/chapter10-services
journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
c -l log-ssh-hari-ini.txt
grep -i "error\|failed" log-ssh-hari-ini.txt | head -20
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# cd ~/lab-os/chapter10-services
root@ubuntuser:~/lab-os/chapter10-services# journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
roroot@ubuntuser:~/lab-os/chapter10-services# wc -l log-ssh-hari-ini.txt
53 log-ssh-hari-ini.txt
root@ubuntuser:~/lab-os/chapter10-services# grep -i "error\|failed" log-ssh-hari-ini.txt | head -20
May 15 07:26:34 ubuntuser sshd[3267]: Failed password for yudhis from 10.0.2.2 port 62943 ssh2
```

### Tantangan
Input :
```bash
journalctl -u ssh -p err --since "24 hours ago" --no-pager | \
> sort | uniq -c | sort -rn | head -10
```

Output :
```bash
root@ubuntuser:~/lab-os/chapter10-services# journalctl -u ssh -p err --since "24 hours ago" --no-pager | \
> sort | uniq -c | sort -rn | head -10
      1 -- No entries --
```


## Praktikum 9.5

### Langkah 1
Input :
```bash
sudo grep -n "^Port\|^#Port" /etc/ssh/sshd_config
ss -tlnp | grep ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo grep -n "^Port\|^#Port" /etc/ssh/sshd_config
1:Port 22
root@ubuntuser:~/praktikum-os/week12# ss -tlnp | grep ssh
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=1352,fd=3),("systemd",pid=1,fd=148))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=1352,fd=4),("systemd",pid=1,fd=149))
```

### Langkah 2
Input :
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.week12
sudo sed -i 's/^#Port 22/Port 2222/' /etc/ssh/sshd_config
grep "^Port" /etc/ssh/sshd_config
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.week12
root@ubuntuser:~/praktikum-os/week12# sudo sed -i 's/^#Port 22/Port 2222/' /etc/ssh/sshd_config
root@ubuntuser:~/praktikum-os/week12# grep "^Port" /etc/ssh/sshd_config
Port 22
```

### Langkah 3
Input :
```bash
sudo sshd -t
echo "Kode keluar sshd -t: $?"
sudo systemctl restart ssh
systemctl status ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo sshd -t
root@ubuntuser:~/praktikum-os/week12# echo "Kode keluar sshd -t: $?"
Kode keluar sshd -t: 0
root@ubuntuser:~/praktikum-os/week12# sudo systemctl restart ssh
root@ubuntuser:~/praktikum-os/week12# systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: e>
     Active: active (running) since Fri 2026-05-15 07:49:18 UTC; 6s ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 3591 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCC>
   Main PID: 3593 (sshd)
      Tasks: 6 (limit: 4008)
     Memory: 8.6M (peak: 23.7M)
        CPU: 541ms
     CGroup: /system.slice/ssh.service
             ├─3267 "sshd: yudhis [priv]"
             ├─3278 "sshd: yudhis@pts/1"
             ├─3279 -bash
             ├─3288 sudo su
             ├─3290 sudo su
             └─3593 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

May 15 07:49:18 ubuntuser systemd[1]: ssh.service: This usually indicates un>
May 15 07:49:18 ubuntuser systemd[1]: ssh.service: Found left-over process 3>
May 15 07:49:18 ubuntuser systemd[1]: ssh.service: This usually indicates un>
May 15 07:49:18 ubuntuser systemd[1]: ssh.service: Found left-over process 3>
May 15 07:49:18 ubuntuser systemd[1]: ssh.service: This usually indicates un>
May 15 07:49:18 ubuntuser systemd[1]: ssh.service: Found left-over process 3>
May 15 07:49:18 ubuntuser systemd[1]: ssh.service: This usually indicates un>
May 15 07:49:18 ubuntuser sshd[3593]: Server listening on 0.0.0.0 port 22.
May 15 07:49:18 ubuntuser systemd[1]: Started ssh.service - OpenBSD Secure S>
May 15 07:49:18 ubuntuser sshd[3593]: Server listening on :: port 22.
```

### Langkah 4
Input :
```bash
ss -tlnp | grep ssh
ss -tlnp | grep ssh > ~/lab-os/chapter10-services/bukti-port-ssh.txt
cat ~/lab-os/chapter10-services/bukti-port-ssh.txt
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# ss -tlnp | grep ssh
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=3593,fd=3),("systemd",pid=1,fd=148))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=3593,fd=4),("systemd",pid=1,fd=149))
root@ubuntuser:~/praktikum-os/week12# ss -tlnp | grep ssh > ~/lab-os/chapter10-services/bukti-port-ssh.txt
root@ubuntuser:~/praktikum-os/week12# cat ~/lab-os/chapter10-services/bukti-port-ssh.txt
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=3593,fd=3),("systemd",pid=1,fd=148))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=3593,fd=4),("systemd",pid=1,fd=149))
```

### Langkah 5
Input :
```bash
sudo cp /etc/ssh/sshd_config.backup.week12 /etc/ssh/sshd_config
sudo sshd -t
echo "Validasi: $?"
sudo systemctl restart ssh
ss -tlnp | grep ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo cp /etc/ssh/sshd_config.backup.week12 /etc/ssh/sshd_config
root@ubuntuser:~/praktikum-os/week12# sudo sshd -t
root@ubuntuser:~/praktikum-os/week12# sudo systemctl restart ssh
root@ubuntuser:~/praktikum-os/week12# ss -tlnp | grep ssh
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=3617,fd=3),("systemd",pid=1,fd=148))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=3617,fd=4),("systemd",pid=1,fd=149))
```

### Tantangan
Input :
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.tantangan
echo "" | sudo tee -a /etc/ssh/sshd_config
echo "# Custom security settings - Week12 Lab" | sudo tee -a /etc/ssh/sshd_config
echo "PermitRootLogin no" | sudo tee -a /etc/ssh/sshd_config
echo "MaxAuthTries 3" | sudo tee -a /etc/ssh/sshd_config
echo "LoginGraceTime 30" | sudo tee -a /etc/ssh/sshd_config
sudo grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config

sudo sshd -t
echo "Validasi: $?"
sudo systemctl reload ssh
systemctl status ssh --no-pager | head -5
sudo grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config > bukti-keamanan-ssh.txt
cat bukti-keamanan-ssh.txt

sudo cp /etc/ssh/sshd_config.backup.week12 /etc/ssh/sshd_config
sudo sshd -t
sudo systemctl reload ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config
PermitRootLogin yes
PermitRootLogin no
MaxAuthTries 3
LoginGraceTime 30

root@ubuntuser:~/praktikum-os/week12# sudo sshd -t
root@ubuntuser:~/praktikum-os/week12# echo "Validasi: $?"
Validasi: 0
root@ubuntuser:~/praktikum-os/week12# sudo systemctl reload ssh
root@ubuntuser:~/praktikum-os/week12# systemctl status ssh --no-pager | head -5
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 07:53:18 UTC; 1h 15min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
root@ubuntuser:~/praktikum-os/week12# sudo grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config > bukti-keamanan-ssh.txt
cat bukti-keamanan-ssh.txt
PermitRootLogin yes
PermitRootLogin no
MaxAuthTries 3
LoginGraceTime 30


```


## LATIHAN

## Latihan 10.1 Audit Layanan dan Analisis Boot

Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.

### 1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.

input:
```bash
systemctl list-units --type=service --state=running > layanan-aktif.txt
cat layanan-aktif.txt

systemctl status ssh --no-pager | head -20

systemctl status cron --no-pager | head -20

systemctl status rsyslog --no-pager | head -20
```

Output:
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl list-units --type=service --state=running > layanan-aktif.txt
root@ubuntuser:~/praktikum-os/week12# cat layanan-aktif.txt
  UNIT                           LOAD   ACTIVE SUB     DESCRIPTION
  cron.service                   loaded active running Regular background program processing daemon
  dbus.service                   loaded active running D-Bus System Message Bus
  fwupd.service                  loaded active running Firmware update daemon
  getty@tty1.service             loaded active running Getty on tty1
  ModemManager.service           loaded active running Modem Manager
  multipathd.service             loaded active running Device-Mapper Multipath Device Controller
  polkit.service                 loaded active running Authorization Manager
  rsyslog.service                loaded active running System Logging Service
  ssh.service                    loaded active running OpenBSD Secure Shell server
  systemd-journald.service       loaded active running Journal Service
  systemd-logind.service         loaded active running User Login Management
  systemd-networkd.service       loaded active running Network Configuration
  systemd-resolved.service       loaded active running Network Name Resolution
  systemd-udevd.service          loaded active running Rule-based Manager for Device Events and Files
  udisks2.service                loaded active running Disk Manager
  unattended-upgrades.service    loaded active running Unattended Upgrades Shutdown
  upower.service                 loaded active running Daemon for power management
  user@0.service                 loaded active running User Manager for UID 0
  user@1000.service              loaded active running User Manager for UID 1000
  virtualbox-guest-utils.service loaded active running Virtualbox guest utils

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization of SUB.
        SUB    → The low-level unit activation state, values depend on unit type.

20 loaded units listed.

root@ubuntuser:~/praktikum-os/week12# systemctl status ssh --no-pager | head -20
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 07:53:18 UTC; 1h 22min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 3616 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 3726 ExecReload=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 3727 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
   Main PID: 3617 (sshd)
      Tasks: 6 (limit: 4008)
     Memory: 8.4M (peak: 23.7M)
        CPU: 6.072s
     CGroup: /system.slice/ssh.service
             ├─3267 "sshd: yudhis [priv]"
             ├─3278 "sshd: yudhis@pts/1"
             ├─3279 -bash
             ├─3288 sudo su
             ├─3290 sudo su
             └─3617 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

root@ubuntuser:~/praktikum-os/week12# systemctl status cron --no-pager | head -20
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 05:42:24 UTC; 3h 34min ago
       Docs: man:cron(8)
   Main PID: 851 (cron)
      Tasks: 1 (limit: 4008)
     Memory: 1.2M (peak: 3.9M)
        CPU: 1.968s
     CGroup: /system.slice/cron.service
             └─851 /usr/sbin/cron -f -P

May 15 07:55:01 ubuntuser CRON[3622]: pam_unix(cron:session): session closed for user root
May 15 08:05:01 ubuntuser CRON[3638]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 15 08:05:01 ubuntuser CRON[3639]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 15 08:05:01 ubuntuser CRON[3638]: pam_unix(cron:session): session closed for user root
May 15 09:05:01 ubuntuser CRON[3657]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 15 09:05:01 ubuntuser CRON[3658]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 15 09:05:01 ubuntuser CRON[3657]: pam_unix(cron:session): session closed for user root
May 15 09:15:02 ubuntuser CRON[3737]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 15 09:15:02 ubuntuser CRON[3738]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)

root@ubuntuser:~/praktikum-os/week12# systemctl status rsyslog --no-pager | head -20
● rsyslog.service - System Logging Service
     Loaded: loaded (/usr/lib/systemd/system/rsyslog.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 05:42:22 UTC; 3h 35min ago
TriggeredBy: ● syslog.socket
       Docs: man:rsyslogd(8)
             man:rsyslog.conf(5)
             https://www.rsyslog.com/doc/
   Main PID: 678 (rsyslogd)
      Tasks: 4 (limit: 4008)
     Memory: 3.0M (peak: 5.1M)
        CPU: 1.867s
     CGroup: /system.slice/rsyslog.service
             └─678 /usr/sbin/rsyslogd -n -iNONE

May 15 05:42:19 ubuntuser systemd[1]: Starting rsyslog.service - System Logging Service...
May 15 05:42:22 ubuntuser rsyslogd[678]: imuxsock: Acquired UNIX socket '/run/systemd/journal/syslog' (fd 3) from systemd.  [v8.2312.0]
May 15 05:42:22 ubuntuser rsyslogd[678]: rsyslogd's groupid changed to 104
May 15 05:42:22 ubuntuser rsyslogd[678]: rsyslogd's userid changed to 103
May 15 05:42:22 ubuntuser rsyslogd[678]: [origin software="rsyslogd" swVersion="8.2312.0" x-pid="678" x-info="https://www.rsyslog.com"] start
May 15 05:42:22 ubuntuser systemd[1]: Started rsyslog.service - System Logging Service.
```

Penjelasan :  
1. Layanan 1: ssh.service  
Fungsi: Server SSH (Secure Shell) yang memungkinkan administrator mengakses server dari jarak jauh melalui koneksi terenkripsi

2. Layanan 2: cron.service  
Fungsi: Penjadwal tugas otomatis yang menjalankan perintah/script pada waktu yang telah ditentukan (setiap menit, jam, hari, minggu, bulan, atau saat reboot)

3. Layanan 3: rsyslog.service  
Fungsi: Sistem logging yang mengumpulkan, memfilter, dan menyimpan pesan log dari berbagai aplikasi dan kernel

### 2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.

input:
```bash
systemd-analyze blame | head -5
```

Output:
```bash
root@ubuntuser:~/praktikum-os/week12# systemd-analyze blame | head -5
6min 44.904s apt-daily.service
      6.582s dev-sda2.device
      6.381s snapd.seeded.service
      6.117s snapd.service
      5.268s dpkg-db-backup.service
```

### 3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.

input:
```bash
systemctl --failed
journalctl -u nama-layanan -n 30
```

Output:
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl --failed
  UNIT            LOAD   ACTIVE SUB    DESCRIPTION
● quotaon.service loaded failed failed Enable File System Quotas

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization o>
        SUB    → The low-level unit activation state, values depend on unit >

1 loaded units listed.
root@ubuntuser:~/praktikum-os/week12# journalctl -u nama-layanan -n 30
-- No entries --
```


## Latihan 10.2 Layanan Kustom dengan Restart Otomatis

Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.

### 1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
Input : 
```bash
nano monitor-disk.sh

#!/bin/bash
# Skrip monitor disk - Latihan 10.2
# Menuliskan penggunaan disk ke log setiap 30 detik

LOG_FILE="/var/log/monitor-disk.log"

# Buat file log jika belum ada
touch $LOG_FILE

# Loop tak terbatas dengan interval 30 detik
while true; do
    # Catat waktu dan penggunaan disk
    echo "=====================================" >> $LOG_FILE
    echo "Waktu: $(date '+%Y-%m-%d %H:%M:%S')" >> $LOG_FILE
    echo "Penggunaan Disk:" >> $LOG_FILE
    df -h >> $LOG_FILE
    echo "=====================================" >> $LOG_FILE
    echo "" >> $LOG_FILE
    
    # Kirim pesan ke journal (opsional)
    logger -t monitor-disk "Disk usage logged at $(date '+%H:%M:%S')"
    
    # Tunggu 30 detik
    sleep 30
done

chmod +x monitor-disk.sh
sudo cp monitor-disk.sh /usr/local/bin/
ls -la /usr/local/bin/monitor-disk.sh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# nano monitor-disk.sh
root@ubuntuser:~/praktikum-os/week12# chmod +x monitor-disk.sh
root@ubuntuser:~/praktikum-os/week12# sudo cp monitor-disk.sh /usr/local/bin/
root@ubuntuser:~/praktikum-os/week12# ls -la /usr/local/bin/monitor-disk.sh
-rwxr-xr-x 1 root root 718 May 15 10:05 /usr/local/bin/monitor-disk.sh
```

### 2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
Input : 
```bash
sudo nano /etc/systemd/system/monitor-disk.service

[Unit]
Description=Monitor Disk Usage Service - Latihan 10.2
Documentation=man:df(1)
After=local-fs.target

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/monitor-disk.sh
Restart=always
RestartSec=5s
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
systemctl list-unit-files --type=service | grep monitor-disk
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo nano /etc/systemd/system/monitor-disk.service
root@ubuntuser:~/praktikum-os/week12# sudo systemctl daemon-reload
root@ubuntuser:~/praktikum-os/week12# systemctl list-unit-files --type=service | grep monitor-disk
monitor-disk.service                         disabled        enabled
```

### 3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.
Input : 
```bash
sudo systemctl enable --now monitor-disk
systemctl status monitor-disk --no-pager

tail -20 /var/log/monitor-disk.log
journalctl -u monitor-disk -n 10 --no-pager


```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo systemctl enable --now monitor-disk
Created symlink /etc/systemd/system/multi-user.target.wants/monitor-disk.service → /etc/systemd/system/monitor-disk.service.
root@ubuntuser:~/praktikum-os/week12# systemctl status monitor-disk --no-pager
● monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2
     Loaded: loaded (/etc/systemd/system/monitor-disk.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 10:45:10 UTC; 4s ago
       Docs: man:df(1)
   Main PID: 4086 (monitor-disk.sh)
      Tasks: 2 (limit: 4008)
     Memory: 700.0K (peak: 1.1M)
        CPU: 145ms
     CGroup: /system.slice/monitor-disk.service
             ├─4086 /bin/bash /usr/local/bin/monitor-disk.sh
             └─4092 sleep 30

May 15 10:45:10 ubuntuser systemd[1]: Started monitor-disk.service - Mon…0.2.
Hint: Some lines were ellipsized, use -l to show in full.

root@ubuntuser:~/praktikum-os/week12# tail -20 /var/log/monitor-disk.log
tmpfs           343M  1.1M  342M   1% /run
/dev/sda2        50G  4.6G   43G  10% /
tmpfs           1.7G     0  1.7G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           343M   12K  343M   1% /run/user/1000
tmpfs           343M   12K  343M   1% /run/user/0
=====================================

=====================================
Waktu: 2026-05-15 10:48:11
Penggunaan Disk:
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           343M  1.1M  342M   1% /run
/dev/sda2        50G  4.6G   43G  10% /
tmpfs           1.7G     0  1.7G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           343M   12K  343M   1% /run/user/1000
tmpfs           343M   12K  343M   1% /run/user/0
=====================================

root@ubuntuser:~/praktikum-os/week12# journalctl -u monitor-disk -n 10 --no-pager
May 15 10:45:10 ubuntuser systemd[1]: Started monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 10:46:10 ubuntuser monitor-disk[4105]: Disk usage logged at 10:46:10
May 15 10:46:40 ubuntuser monitor-disk[4110]: Disk usage logged at 10:46:40
May 15 10:47:41 ubuntuser monitor-disk[4121]: Disk usage logged at 10:47:41
May 15 10:48:11 ubuntuser monitor-disk[4126]: Disk usage logged at 10:48:11
May 15 10:48:41 ubuntuser monitor-disk[4132]: Disk usage logged at 10:48:41
May 15 10:49:11 ubuntuser monitor-disk[4137]: Disk usage logged at 10:49:11
May 15 10:49:41 ubuntuser monitor-disk[4142]: Disk usage logged at 10:49:41
May 15 10:51:11 ubuntuser monitor-disk[4163]: Disk usage logged at 10:51:11


```

### 4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.
Input : 
```bash
PID=$(systemctl show monitor-disk --property=MainPID --value)
echo "PID saat ini: $PID"
journalctl -u monitor-disk -f &
JOURNAL_PID=$!
sudo kill -9 $PID
echo "Proses dengan PID $PID telah di-kill"
echo "Menunggu 10 detik untuk restart..."
sleep 10
journalctl -u monitor-disk -n 15 --no-pager
systemctl show monitor-disk | grep -E "NRestarts|Restart"
kill $JOURNAL_PID 2>/dev/null
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# PID=$(systemctl show monitor-disk --property=MainPID --value)
root@ubuntuser:~/praktikum-os/week12# echo "PID saat ini: $PID"
PID saat ini: 4414
root@ubuntuser:~/praktikum-os/week12# journalctl -u monitor-disk -f &
[2] 4440
root@ubuntuser:~/praktikum-os/week12# May 15 11:09:47 ubuntuser monitor-disk[4375]: Disk usage logged at 11:09:47
May 15 11:10:17 ubuntuser monitor-disk[4380]: Disk usage logged at 11:10:17
May 15 11:10:47 ubuntuser monitor-disk[4388]: Disk usage logged at 11:10:47
May 15 11:11:17 ubuntuser monitor-disk[4394]: Disk usage logged at 11:11:17
May 15 11:12:17 ubuntuser monitor-disk[4407]: Disk usage logged at 11:12:17
May 15 11:12:47 ubuntuser systemd[1]: monitor-disk.service: Main process exited, code=killed, status=9/KILL
May 15 11:12:47 ubuntuser systemd[1]: monitor-disk.service: Failed with result 'signal'.
May 15 11:12:47 ubuntuser systemd[1]: monitor-disk.service: Consumed 7.022s CPU time, 1.4M memory peak, 0B memory swap peak.
May 15 11:12:52 ubuntuser systemd[1]: monitor-disk.service: Scheduled restart job, restart counter is at 1.
May 15 11:12:52 ubuntuser systemd[1]: Started monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 11:13:52 ubuntuser monitor-disk[4444]: Disk usage logged at 11:13:52
May 15 11:13:52 ubuntuser monitor-disk[4444]: Disk usage logged at 11:13:52

root@ubuntuser:~/praktikum-os/week12# JOURNAL_PID=$!
root@ubuntuser:~/praktikum-os/week12# sudo kill -9 $PID
root@ubuntuser:~/praktikum-os/week12# May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Main process exited, code=killed, status=9/KILL
May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Main process exited, code=killed, status=9/KILL
May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Failed with result 'signal'.
May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Failed with result 'signal'.
May 15 11:14:25 ubuntuser systemd[1]: monitor-disk.service: Scheduled restart job, restart counter is at 2.
May 15 11:14:25 ubuntuser systemd[1]: monitor-disk.service: Scheduled restart job, restart counter is at 2.
May 15 11:14:25 ubuntuser systemd[1]: Started monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 11:14:25 ubuntuser systemd[1]: Started monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 11:14:25 ubuntuser monitor-disk[4456]: Disk usage logged at 11:14:25
May 15 11:14:25 ubuntuser monitor-disk[4456]: Disk usage logged at 11:14:25

root@ubuntuser:~/praktikum-os/week12# echo "Proses dengan PID $PID telah di-kill"
Proses dengan PID 4414 telah di-kill
root@ubuntuser:~/praktikum-os/week12# May 15 11:14:55 ubuntuser monitor-disk[4461]: Disk usage logged at 11:14:55
May 15 11:14:55 ubuntuser monitor-disk[4461]: Disk usage logged at 11:14:55

root@ubuntuser:~/praktikum-os/week12# echo "Menunggu 10 detik untuk restart..."
Menunggu 10 detik untuk restart...
root@ubuntuser:~/praktikum-os/week12# sleep 10
root@ubuntuser:~/praktikum-os/week12# systemctl status monitor-disk --no-pager
● monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2
     Loaded: loaded (/etc/systemd/system/monitor-disk.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 11:14:25 UTC; 1min 11s ago
       Docs: man:df(1)
   Main PID: 4451 (monitor-disk.sh)
      Tasks: 2 (limit: 4008)
     Memory: 592.0K (peak: 1.2M)
        CPU: 591ms
     CGroup: /system.slice/monitor-disk.service
             ├─4451 /bin/bash /usr/local/bin/monitor-disk.sh
             └─4472 sleep 30

May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Failed with …al'.
May 15 11:14:25 ubuntuser systemd[1]: monitor-disk.service: Scheduled re…t 2.
May 15 11:14:25 ubuntuser systemd[1]: Started monitor-disk.service - Mon…0.2.
May 15 11:14:25 ubuntuser monitor-disk[4456]: Disk usage logged at 11:14:25
May 15 11:14:55 ubuntuser monitor-disk[4461]: Disk usage logged at 11:14:55
Hint: Some lines were ellipsized, use -l to show in full.
root@ubuntuser:~/praktikum-os/week12# journalctl -u monitor-disk -n 15 --no-pager
May 15 11:10:47 ubuntuser monitor-disk[4388]: Disk usage logged at 11:10:47
May 15 11:11:17 ubuntuser monitor-disk[4394]: Disk usage logged at 11:11:17
May 15 11:12:17 ubuntuser monitor-disk[4407]: Disk usage logged at 11:12:17
May 15 11:12:47 ubuntuser systemd[1]: monitor-disk.service: Main process exited, code=killed, status=9/KILL
May 15 11:12:47 ubuntuser systemd[1]: monitor-disk.service: Failed with result 'signal'.
May 15 11:12:47 ubuntuser systemd[1]: monitor-disk.service: Consumed 7.022s CPU time, 1.4M memory peak, 0B memory swap peak.
May 15 11:12:52 ubuntuser systemd[1]: monitor-disk.service: Scheduled restart job, restart counter is at 1.
May 15 11:12:52 ubuntuser systemd[1]: Started monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 11:13:52 ubuntuser monitor-disk[4444]: Disk usage logged at 11:13:52
May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Main process exited, code=killed, status=9/KILL
May 15 11:14:20 ubuntuser systemd[1]: monitor-disk.service: Failed with result 'signal'.
May 15 11:14:25 ubuntuser systemd[1]: monitor-disk.service: Scheduled restart job, restart counter is at 2.
May 15 11:14:25 ubuntuser systemd[1]: Started monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 11:14:25 ubuntuser monitor-disk[4456]: Disk usage logged at 11:14:25
May 15 11:14:55 ubuntuser monitor-disk[4461]: Disk usage logged at 11:14:55
root@ubuntuser:~/praktikum-os/week12# systemctl show monitor-disk | grep -E "NRestarts|Restart"
Restart=always
RestartMode=normal
RestartUSec=5s
RestartSteps=0
RestartMaxDelayUSec=infinity
RestartUSecNext=5s
NRestarts=2
RestartKillSignal=15
root@ubuntuser:~/praktikum-os/week12# kill $JOURNAL_PID 2>/dev/null

[2]+  Terminated              journalctl -u monitor-disk -f
```

### 5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.
Input : 
```bash
sudo systemctl disable --now monitor-disk

sudo rm /etc/systemd/system/monitor-disk.service

sudo systemctl daemon-reload

sudo rm /usr/local/bin/monitor-disk.sh

sudo rm /var/log/monitor-disk.log

systemctl status monitor-disk 2>&1 | head -3

systemctl --failed
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo systemctl disable --now monitor-disk
Removed "/etc/systemd/system/multi-user.target.wants/monitor-disk.service".
root@ubuntuser:~/praktikum-os/week12# May 15 11:21:10 ubuntuser systemd[1]: Stopping monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2...
May 15 11:21:10 ubuntuser systemd[1]: monitor-disk.service: Deactivated successfully.
May 15 11:21:10 ubuntuser systemd[1]: Stopped monitor-disk.service - Monitor Disk Usage Service - Latihan 10.2.
May 15 11:21:10 ubuntuser systemd[1]: monitor-disk.service: Consumed 2.203s CPU time, 1.2M memory peak, 0B memory swap peak.

root@ubuntuser:~/praktikum-os/week12# sudo rm /etc/systemd/system/monitor-disk.service
root@ubuntuser:~/praktikum-os/week12# sudo systemctl daemon-reload
root@ubuntuser:~/praktikum-os/week12# sudo rm /usr/local/bin/monitor-disk.sh
root@ubuntuser:~/praktikum-os/week12# sudo rm /var/log/monitor-disk.log
root@ubuntuser:~/praktikum-os/week12# systemctl status monitor-disk 2>&1 | head -3
Unit monitor-disk.service could not be found.
root@ubuntuser:~/praktikum-os/week12# systemctl --failed
  UNIT            LOAD   ACTIVE SUB    DESCRIPTION
● quotaon.service loaded failed failed Enable File System Quotas

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization o>
        SUB    → The low-level unit activation state, values depend on unit >

1 loaded units listed.
```


## Latihan 10.3 Investigasi Log dan Keamanan SSH

Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.

### 1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l.
Input : 
```bash
journalctl -b -p err --no-pager > error-boot.txt
wc -l error-boot.txt
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# journalctl -b -p err --no-pager > error-boot.txt
root@ubuntuser:~/praktikum-os/week12# wc -l error-boot.txt
281 error-boot.txt
```

### 2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd -t, reload.
Input : 
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak

echo -e "\nPermitRootLogin no\nMaxAuthTries 3\nLoginGraceTime 30" | sudo tee -a /etc/ssh/sshd_config

sudo sshd -t && sudo systemctl reload ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
root@ubuntuser:~/praktikum-os/week12# echo -e "\nPermitRootLogin no\nMaxAuthTries 3\nLoginGraceTime 30" | sudo tee -a /etc/ssh/sshd_config

PermitRootLogin no
MaxAuthTries 3
LoginGraceTime 30
root@ubuntuser:~/praktikum-os/week12# sudo sshd -t && sudo systemctl reload ssh
```

### 3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
Input : 
```bash
systemctl status ssh --no-pager | head -3
ss -tlnp | grep ssh
sudo grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# systemctl status ssh --no-pager | head -3
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-15 07:53:18 UTC; 3h 35min ago
root@ubuntuser:~/praktikum-os/week12# ss -tlnp | grep ssh
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=3617,fd=3),("systemd",pid=1,fd=134))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=3617,fd=4),("systemd",pid=1,fd=141))
root@ubuntuser:~/praktikum-os/week12# sudo grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config
PermitRootLogin yes
PermitRootLogin no
MaxAuthTries 3
LoginGraceTime 30
```

### 4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
Input : 
```bash
sudo cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config
sudo sshd -t && sudo systemctl reload ssh
```

Output :
```bash
root@ubuntuser:~/praktikum-os/week12# sudo cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config
root@ubuntuser:~/praktikum-os/week12# sudo sshd -t && sudo systemctl reload ssh
```
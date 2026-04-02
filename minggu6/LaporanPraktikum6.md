# Laporan Praktikum 6

<h4>Nama : Yudhistira Putra Hartanto<h4>
<h4>Nim : 254107020083<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 6.1 — Melihat Proses dan Thread

1. Tampilkan semua proses yang berjalan:
```bash
ps aux
```
Output  :
```bash
root@ubuntuser:/home/yudhis# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.3  0.3  22112 13208 ?        Ss   13:47   0:00 /sbin/ini
root           2  0.0  0.0      0     0 ?        S    13:47   0:00 [kthreadd
root           3  0.0  0.0      0     0 ?        S    13:47   0:00 [pool_wor
root           4  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root           5  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root           6  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root           7  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root           8  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root           9  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          10  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          11  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          12  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          13  0.0  0.0      0     0 ?        I    13:47   0:00 [rcu_task
root          14  0.0  0.0      0     0 ?        I    13:47   0:00 [rcu_task
root          15  0.0  0.0      0     0 ?        I    13:47   0:00 [rcu_task
root          16  0.0  0.0      0     0 ?        S    13:47   0:00 [ksoftirq
root          17  0.0  0.0      0     0 ?        I    13:47   0:00 [rcu_pree
root          18  0.0  0.0      0     0 ?        S    13:47   0:00 [migratio
root          19  0.0  0.0      0     0 ?        S    13:47   0:00 [idle_inj
root          20  0.0  0.0      0     0 ?        S    13:47   0:00 [cpuhp/0]
root          21  0.0  0.0      0     0 ?        S    13:47   0:00 [cpuhp/1]
root          22  0.0  0.0      0     0 ?        S    13:47   0:00 [idle_inj
root          23  0.0  0.0      0     0 ?        S    13:47   0:00 [migratio
root          24  0.0  0.0      0     0 ?        S    13:47   0:00 [ksoftirq
root          25  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          26  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          27  0.0  0.0      0     0 ?        S    13:47   0:00 [cpuhp/2]
root          28  0.0  0.0      0     0 ?        S    13:47   0:00 [idle_inj
root          29  0.0  0.0      0     0 ?        S    13:47   0:00 [migratio
root          30  0.0  0.0      0     0 ?        S    13:47   0:00 [ksoftirq
root          31  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          32  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          33  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          34  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          35  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          36  0.0  0.0      0     0 ?        S    13:47   0:00 [kdevtmpf
root          37  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          38  0.0  0.0      0     0 ?        S    13:47   0:00 [kauditd]
root          39  0.0  0.0      0     0 ?        S    13:47   0:00 [khungtas
root          40  0.0  0.0      0     0 ?        S    13:47   0:00 [oom_reap
root          41  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          42  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          43  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          44  0.0  0.0      0     0 ?        S    13:47   0:00 [kcompact
root          45  0.0  0.0      0     0 ?        SN   13:47   0:00 [ksmd]
root          46  0.0  0.0      0     0 ?        SN   13:47   0:00 [khugepag
root          47  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          48  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          49  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          50  0.0  0.0      0     0 ?        S    13:47   0:00 [irq/9-ac
root          51  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          52  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          53  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          54  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          55  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          56  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          57  0.0  0.0      0     0 ?        S    13:47   0:00 [watchdog
root          58  0.1  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          59  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          60  0.3  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          61  0.0  0.0      0     0 ?        S    13:47   0:00 [kswapd0]
root          62  0.0  0.0      0     0 ?        S    13:47   0:00 [ecryptfs
root          63  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          64  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          65  0.0  0.0      0     0 ?        S    13:47   0:00 [scsi_eh_
root          66  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          67  0.0  0.0      0     0 ?        S    13:47   0:00 [scsi_eh_
root          68  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          69  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          70  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          71  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          72  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          73  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          74  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          75  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          76  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          78  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          84  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          85  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          87  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          88  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          89  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          90  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          94  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root          96  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root          97  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         106  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         131  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         158  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         159  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         166  0.0  0.0      0     0 ?        S    13:47   0:00 [scsi_eh_
root         167  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         212  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         256  0.0  0.0      0     0 ?        S    13:47   0:00 [jbd2/sda
root         257  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         279  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         323  0.1  0.4  50468 17420 ?        S<s  13:47   0:00 /usr/lib/
root         343  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         345  0.2  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         347  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         356  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         359  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         363  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         379  0.0  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/mul
root         389  0.0  0.2  28816  7588 ?        Ss   13:47   0:00 /usr/lib/
root         419  0.0  0.0      0     0 ?        S    13:47   0:00 [psimon]
root         437  0.1  0.0      0     0 ?        I    13:47   0:00 [kworker/
systemd+     443  0.0  0.2  19012  9544 ?        Ss   13:47   0:00 /usr/lib/
systemd+     480  0.0  0.3  21588 13052 ?        Ss   13:47   0:00 /usr/lib/
root         588  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         610  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root         625  0.0  0.0      0     0 ?        S    13:47   0:00 [irq/18-v
root         626  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
message+     628  0.0  0.1   9892  5656 ?        Ss   13:47   0:00 @dbus-dae
polkitd      647  0.0  0.2 308164  8108 ?        Ssl  13:47   0:00 /usr/lib/
root         660  0.0  0.2  18128  9012 ?        Ss   13:47   0:00 /usr/lib/
root         668  0.0  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libe
syslog       704  0.0  0.1 222508  6124 ?        Ssl  13:47   0:00 /usr/sbin
root         731  0.0  0.6 109688 23192 ?        Ssl  13:47   0:00 /usr/bin/
root         754  0.0  0.3 392100 12948 ?        Ssl  13:47   0:00 /usr/sbin
root         764  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/
root         767  0.0  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin
root         854  0.0  0.0   6824  2908 ?        Ss   13:47   0:00 /usr/sbin
root         861  0.0  0.2  12020  8220 ?        Ss   13:47   0:00 sshd: /us
root         866  0.0  0.1   6956  4924 tty1     Ss   13:47   0:00 /bin/logi
root         980  0.0  0.0      0     0 ?        S    13:47   0:00 [psimon]
yudhis       982  0.0  0.3  20076 11232 ?        Ss   13:47   0:00 /usr/lib/
yudhis       983  0.0  0.1  21152  3568 ?        S    13:47   0:00 (sd-pam)
yudhis       991  0.0  0.1   8656  5652 tty1     S    13:47   0:00 -bash
root         994  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root        1038  0.0  0.0      0     0 ?        I<   13:47   0:00 [kworker/
root        1040  0.0  0.2  16768  7408 tty1     S+   13:47   0:00 sudo su
root        1041  0.0  0.0  16768  2556 pts/0    Ss   13:47   0:00 sudo su
root        1042  0.0  0.1   9376  4492 pts/0    S    13:47   0:00 su
root        1043  0.0  0.1   7604  4496 pts/0    S+   13:47   0:00 bash
root        1050  0.0  0.2  12152  8640 ?        Ss   13:49   0:00 sshd: yud
yudhis      1052  0.2  0.2  13764  7484 ?        S    13:49   0:00 sshd: yud
yudhis      1053  0.0  0.1   5644  5080 pts/1    Ss   13:49   0:00 -bash
root        1062  0.1  0.1  13872  6976 pts/1    S+   13:49   0:00 sudo su
root        1063  0.0  0.0  13872  2596 pts/2    Ss   13:49   0:00 sudo su
root        1064  0.0  0.1   9376  4492 pts/2    S    13:49   0:00 su
root        1067  0.2  0.3  20092 11292 ?        Ss   13:49   0:00 /usr/lib/
root        1068  0.0  0.0  21160  3492 ?        S    13:49   0:00 (sd-pam)
root        1073  0.0  0.0      0     0 ?        S    13:49   0:00 [psimon]
root        1080  0.0  0.1   7736  4508 pts/2    S    13:49   0:00 bash
fwupd-r+    1090  2.3  0.8 440908 28568 ?        Ssl  13:51   0:00 /usr/bin/
root        1110  2.7  1.1 551776 41680 ?        Ssl  13:51   0:00 /usr/libe
root        1120  0.5  0.2 314136  9216 ?        Ssl  13:51   0:00 /usr/libe
root        1231 50.0  0.1  11012  4620 pts/2    R+   13:51   0:00 ps aux
```

2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (LightWeight Process ID):
```bash
ps aux -L
```

Output :  
```bash
USER         PID     LWP %CPU NLWP %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1       1  0.1    1  0.3  22112 13208 ?        Ss   13:47   0:00 /sbin/init splash noprompt noshell automatic-ubiquity
root           2       2  0.0    1  0.0      0     0 ?        S    13:47   0:00 [kthreadd]
root           3       3  0.0    1  0.0      0     0 ?        S    13:47   0:00 [pool_workqueue_release]
root           4       4  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-rcu_g]
root           5       5  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-rcu_p]
root           6       6  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-slub_]
root           7       7  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-netns]
root           9       9  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/0:1-cgroup_destroy]
root          11      11  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u6:0-ipv6_addrconf]
root          12      12  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-mm_pe]
root          13      13  0.0    1  0.0      0     0 ?        I    13:47   0:00 [rcu_tasks_kthread]
root          14      14  0.0    1  0.0      0     0 ?        I    13:47   0:00 [rcu_tasks_rude_kthread]
root          15      15  0.0    1  0.0      0     0 ?        I    13:47   0:00 [rcu_tasks_trace_kthread]
root          16      16  0.0    1  0.0      0     0 ?        S    13:47   0:00 [ksoftirqd/0]
root          17      17  0.0    1  0.0      0     0 ?        I    13:47   0:00 [rcu_preempt]
root          18      18  0.0    1  0.0      0     0 ?        S    13:47   0:00 [migration/0]
root          19      19  0.0    1  0.0      0     0 ?        S    13:47   0:00 [idle_inject/0]
root          20      20  0.0    1  0.0      0     0 ?        S    13:47   0:00 [cpuhp/0]
root          21      21  0.0    1  0.0      0     0 ?        S    13:47   0:00 [cpuhp/1]
root          22      22  0.0    1  0.0      0     0 ?        S    13:47   0:00 [idle_inject/1]
root          23      23  0.0    1  0.0      0     0 ?        S    13:47   0:00 [migration/1]
root          24      24  0.0    1  0.0      0     0 ?        S    13:47   0:00 [ksoftirqd/1]
root          26      26  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/1:0H-events_highpri]
root          27      27  0.0    1  0.0      0     0 ?        S    13:47   0:00 [cpuhp/2]
root          28      28  0.0    1  0.0      0     0 ?        S    13:47   0:00 [idle_inject/2]
root          29      29  0.0    1  0.0      0     0 ?        S    13:47   0:00 [migration/2]
root          30      30  0.0    1  0.0      0     0 ?        S    13:47   0:00 [ksoftirqd/2]
root          34      34  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u8:0-events_unbound]
root          35      35  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u9:0-events_unbound]
root          36      36  0.0    1  0.0      0     0 ?        S    13:47   0:00 [kdevtmpfs]
root          37      37  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-inet_]
root          38      38  0.0    1  0.0      0     0 ?        S    13:47   0:00 [kauditd]
root          39      39  0.0    1  0.0      0     0 ?        S    13:47   0:00 [khungtaskd]
root          40      40  0.0    1  0.0      0     0 ?        S    13:47   0:00 [oom_reaper]
root          41      41  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u7:1-events_unbound]
root          42      42  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u7:2-events_power_efficient]
root          43      43  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-write]
root          44      44  0.0    1  0.0      0     0 ?        S    13:47   0:00 [kcompactd0]
root          45      45  0.0    1  0.0      0     0 ?        SN   13:47   0:00 [ksmd]
root          46      46  0.0    1  0.0      0     0 ?        SN   13:47   0:00 [khugepaged]
root          47      47  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-kinte]
root          48      48  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-kbloc]
root          49      49  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-blkcg]
root          50      50  0.0    1  0.0      0     0 ?        S    13:47   0:00 [irq/9-acpi]
root          51      51  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-tpm_d]
root          52      52  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-ata_s]
root          53      53  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-md]
root          54      54  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-md_bi]
root          55      55  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-edac-]
root          56      56  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-devfr]
root          57      57  0.0    1  0.0      0     0 ?        S    13:47   0:00 [watchdogd]
root          58      58  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/1:1-events]
root          59      59  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/0:1H-kblockd]
root          61      61  0.0    1  0.0      0     0 ?        S    13:47   0:00 [kswapd0]
root          62      62  0.0    1  0.0      0     0 ?        S    13:47   0:00 [ecryptfs-kthread]
root          63      63  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-kthro]
root          64      64  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-acpi_]
root          65      65  0.0    1  0.0      0     0 ?        S    13:47   0:00 [scsi_eh_0]
root          66      66  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-scsi_]
root          67      67  0.0    1  0.0      0     0 ?        S    13:47   0:00 [scsi_eh_1]
root          68      68  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-scsi_]
root          72      72  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/1:2-events]
root          73      73  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/0:2-cgwb_release]
root          74      74  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-mld]
root          75      75  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-ipv6_]
root          76      76  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u6:1-ipv6_addrconf]
root          78      78  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/2:1H-kblockd]
root          84      84  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-kstrp]
root          85      85  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u9:1-events_power_efficient]
root          87      87  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/u10:0]
root          88      88  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/u11:0]
root          89      89  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/u12:0]
root          90      90  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/u13:0]
root          94      94  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u8:1-flush-8:0]
root          96      96  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-crypt]
root          97      97  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/2:2-cgroup_destroy]
root         106     106  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-charg]
root         131     131  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/1:1H-kblockd]
root         166     166  0.0    1  0.0      0     0 ?        S    13:47   0:00 [scsi_eh_2]
root         167     167  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-scsi_]
root         212     212  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-raid5]
root         256     256  0.0    1  0.0      0     0 ?        S    13:47   0:00 [jbd2/sda2-8]
root         257     257  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-ext4-]
root         279     279  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u9:2-events_power_efficient]
root         323     323  0.0    1  0.4  66860 17456 ?        S<s  13:47   0:00 /usr/lib/systemd/systemd-journald
root         343     343  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u9:3-events_power_efficient]
root         345     345  0.4    1  0.0      0     0 ?        I    13:47   0:02 [kworker/2:3-events]
root         347     347  0.0    1  0.0      0     0 ?        I    13:47   0:00 [kworker/u8:2-events_unbound]
root         356     356  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-kmpat]
root         359     359  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-kmpat]
root         379     379  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         379     392  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         379     393  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         379     394  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         379     395  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         379     396  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         379     397  0.0    7  0.7 288988 27324 ?        SLsl 13:47   0:00 /sbin/multipathd -d -s
root         389     389  0.0    1  0.2  28816  7588 ?        Ss   13:47   0:00 /usr/lib/systemd/systemd-udevd
root         419     419  0.0    1  0.0      0     0 ?        S    13:47   0:00 [psimon]
root         437     437  0.2    1  0.0      0     0 ?        I    13:47   0:01 [kworker/0:3-events]
systemd+     443     443  0.0    1  0.2  19012  9544 ?        Ss   13:47   0:00 /usr/lib/systemd/systemd-networkd
systemd+     480     480  0.0    1  0.3  21588 13052 ?        Ss   13:47   0:00 /usr/lib/systemd/systemd-resolved
root         588     588  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/2:2H-kblockd]
root         610     610  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-cfg80]
root         625     625  0.0    1  0.0      0     0 ?        S    13:47   0:00 [irq/18-vmwgfx]
root         626     626  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-ttm]
message+     628     628  0.0    1  0.1   9892  5656 ?        Ss   13:47   0:00 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-
polkitd      647     647  0.0    4  0.2 308164  8108 ?        Ssl  13:47   0:00 /usr/lib/polkit-1/polkitd --no-debug
polkitd      647     739  0.0    4  0.2 308164  8108 ?        Ssl  13:47   0:00 /usr/lib/polkit-1/polkitd --no-debug
polkitd      647     740  0.0    4  0.2 308164  8108 ?        Ssl  13:47   0:00 /usr/lib/polkit-1/polkitd --no-debug
polkitd      647     741  0.0    4  0.2 308164  8108 ?        Ssl  13:47   0:00 /usr/lib/polkit-1/polkitd --no-debug
root         660     660  0.0    1  0.2  18128  9012 ?        Ss   13:47   0:00 /usr/lib/systemd/systemd-logind
root         668     668  0.0    7  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root         668     687  0.0    7  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root         668     688  0.0    7  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root         668     694  0.0    7  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root         668     756  0.0    7  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root         668     776  0.0    7  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root         668    1264  0.0    7  0.3 468972 13608 ?        Ssl  13:57   0:00 /usr/libexec/udisks2/udisksd
syslog       704     704  0.0    4  0.1 222508  6124 ?        Ssl  13:47   0:00 /usr/sbin/rsyslogd -n -iNONE
syslog       704     735  0.0    4  0.1 222508  6124 ?        Ssl  13:47   0:00 /usr/sbin/rsyslogd -n -iNONE
syslog       704     736  0.0    4  0.1 222508  6124 ?        Ssl  13:47   0:00 /usr/sbin/rsyslogd -n -iNONE
syslog       704     737  0.0    4  0.1 222508  6124 ?        Ssl  13:47   0:00 /usr/sbin/rsyslogd -n -iNONE
root         731     731  0.0    2  0.6 109688 23192 ?        Ssl  13:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutd
root         731     833  0.0    2  0.6 109688 23192 ?        Ssl  13:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutd
root         754     754  0.0    4  0.3 392100 12948 ?        Ssl  13:47   0:00 /usr/sbin/ModemManager
root         754     782  0.0    4  0.3 392100 12948 ?        Ssl  13:47   0:00 /usr/sbin/ModemManager
root         754     784  0.0    4  0.3 392100 12948 ?        Ssl  13:47   0:00 /usr/sbin/ModemManager
root         754     787  0.0    4  0.3 392100 12948 ?        Ssl  13:47   0:00 /usr/sbin/ModemManager
root         767     767  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     769  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     770  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     771  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     772  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     774  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     777  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     778  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         767     780  0.0    9  0.1 293152  3764 ?        Sl   13:47   0:00 /usr/sbin/VBoxService
root         854     854  0.0    1  0.0   6824  2908 ?        Ss   13:47   0:00 /usr/sbin/cron -f -P
root         861     861  0.0    1  0.2  12020  8220 ?        Ss   13:47   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root         866     866  0.0    1  0.1   6956  4924 tty1     Ss   13:47   0:00 /bin/login -p --
root         980     980  0.0    1  0.0      0     0 ?        S    13:47   0:00 [psimon]
yudhis       982     982  0.0    1  0.3  20076 11232 ?        Ss   13:47   0:00 /usr/lib/systemd/systemd --user
yudhis       983     983  0.0    1  0.1  21152  3568 ?        S    13:47   0:00 (sd-pam)
yudhis       991     991  0.0    1  0.1   8656  5652 tty1     S    13:47   0:00 -bash
root         994     994  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/0:2H]
root        1038    1038  0.0    1  0.0      0     0 ?        I<   13:47   0:00 [kworker/R-tls-s]
root        1040    1040  0.0    1  0.2  16768  7408 tty1     S+   13:47   0:00 sudo su
root        1041    1041  0.0    1  0.0  16768  2556 pts/0    Ss   13:47   0:00 sudo su
root        1042    1042  0.0    1  0.1   9376  4492 pts/0    S    13:47   0:00 su
root        1043    1043  0.0    1  0.1   7604  4496 pts/0    S+   13:47   0:00 bash
root        1050    1050  0.0    1  0.2  12152  8640 ?        Ss   13:49   0:00 sshd: yudhis [priv]
yudhis      1052    1052  0.0    1  0.2  13764  7484 ?        S    13:49   0:00 sshd: yudhis@pts/1
yudhis      1053    1053  0.0    1  0.1   5644  5080 pts/1    Ss   13:49   0:00 -bash
root        1062    1062  0.0    1  0.1  13872  6984 pts/1    S+   13:49   0:00 sudo su
root        1063    1063  0.0    1  0.0  13872  2596 pts/2    Ss   13:49   0:00 sudo su
root        1064    1064  0.0    1  0.1   9376  4492 pts/2    S    13:49   0:00 su
root        1067    1067  0.0    1  0.3  20092 11292 ?        Ss   13:49   0:00 /usr/lib/systemd/systemd --user
root        1068    1068  0.0    1  0.0  21160  3492 ?        S    13:49   0:00 (sd-pam)
root        1073    1073  0.0    1  0.0      0     0 ?        S    13:49   0:00 [psimon]
root        1080    1080  0.0    1  0.1   7736  4512 pts/2    S    13:49   0:00 bash
root        1110    1110  0.6    6  1.2 685756 43608 ?        Ssl  13:51   0:02 /usr/libexec/fwupd/fwupd
root        1110    1114  0.0    6  1.2 685756 43608 ?        Ssl  13:51   0:00 /usr/libexec/fwupd/fwupd
root        1110    1115  0.0    6  1.2 685756 43608 ?        Ssl  13:51   0:00 /usr/libexec/fwupd/fwupd
root        1110    1116  0.0    6  1.2 685756 43608 ?        Ssl  13:51   0:00 /usr/libexec/fwupd/fwupd
root        1110    1117  0.0    6  1.2 685756 43608 ?        Ssl  13:51   0:00 /usr/libexec/fwupd/fwupd
root        1110    1119  0.0    6  1.2 685756 43608 ?        Ssl  13:51   0:00 /usr/libexec/fwupd/fwupd
root        1120    1120  0.0    4  0.2 314136  9364 ?        Ssl  13:51   0:00 /usr/libexec/upowerd
root        1120    1122  0.0    4  0.2 314136  9364 ?        Ssl  13:51   0:00 /usr/libexec/upowerd
root        1120    1123  0.0    4  0.2 314136  9364 ?        Ssl  13:51   0:00 /usr/libexec/upowerd
root        1120    1124  0.0    4  0.2 314136  9364 ?        Ssl  13:51   0:00 /usr/libexec/upowerd
root        1265    1265  200    1  0.1  11012  4640 pts/2    R+   13:57   0:00 ps aux -L
```

3. Lihat PID shell aktif dan detail prosesnya:
```bash
echo $$
ps -p $$ -f
```
Output :  
```bash
root@ubuntuser:/home/yudhis# echo $$
1080
root@ubuntuser:/home/yudhis# ps -p $$ -f
UID          PID    PPID  C STIME TTY          TIME CMD
root        1080    1064  0 13:49 pts/2    00:00:00 bash
```

4. Lihat hierarki proses secara visual:
```bash
pstree -p
```
Output:  
```bash
systemd(1)─┬─ModemManager(754)─┬─{ModemManager}(782)
           │                   ├─{ModemManager}(784)
           │                   └─{ModemManager}(787)
           ├─VBoxService(767)─┬─{VBoxService}(769)
           │                  ├─{VBoxService}(770)
           │                  ├─{VBoxService}(771)
           │                  ├─{VBoxService}(772)
           │                  ├─{VBoxService}(774)
           │                  ├─{VBoxService}(777)
           │                  ├─{VBoxService}(778)
           │                  └─{VBoxService}(780)
           ├─cron(854)
           ├─dbus-daemon(628)
           ├─fwupd(1110)─┬─{fwupd}(1114)
           │             ├─{fwupd}(1115)
           │             ├─{fwupd}(1116)
           │             ├─{fwupd}(1117)
           │             └─{fwupd}(1119)
           ├─login(866)───bash(991)───sudo(1040)───sudo(1041)───su(1042)───+
           ├─multipathd(379)─┬─{multipathd}(392)
           │                 ├─{multipathd}(393)
           │                 ├─{multipathd}(394)
           │                 ├─{multipathd}(395)
           │                 ├─{multipathd}(396)
           │                 └─{multipathd}(397)
           ├─polkitd(647)─┬─{polkitd}(739)
           │              ├─{polkitd}(740)
           │              └─{polkitd}(741)
           ├─rsyslogd(704)─┬─{rsyslogd}(735)
           │               ├─{rsyslogd}(736)
           │               └─{rsyslogd}(737)
           ├─sshd(861)───sshd(1050)───sshd(1052)───bash(1053)───sudo(1062)─+++
           ├─systemd(1067)───(sd-pam)(1068)
           ├─systemd(982)───(sd-pam)(983)
           ├─systemd-journal(323)
           ├─systemd-logind(660)
           ├─systemd-network(443)
           ├─systemd-resolve(480)
           ├─systemd-udevd(389)
           ├─udisksd(668)─┬─{udisksd}(687)
           │              ├─{udisksd}(688)
           │              ├─{udisksd}(694)
           │              ├─{udisksd}(756)
           │              └─{udisksd}(776)
           ├─unattended-upgr(731)───{unattended-upgr}(833)
           └─upowerd(1120)─┬─{upowerd}(1122)
                           ├─{upowerd}(1123)
                           └─{upowerd}(1124)
```  

  
### Latihan 6.1  

Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda lihat?  

Jawaban :

1. Total proses dapat dilihat dari jumlah baris di ps aux (kurangi satu baris header). PID terkecil biasanya adalah 1, yaitu init atau systemd (proses pertama yang dijalankan kernel).  
2. Jalankan pstree -p, cari bash dengan PID-nya. PPID-nya adalah proses yang menjadi induk, misalnya sshd jika masuk via SSH, atau systemd jika login lokal.  
3. ps aux menampilkan satu baris per proses. ps aux -L menampilkan satu baris per thread (LWP) sehingga jumlah baris lebih banyak karena proses dengan banyak thread akan muncul beberapa kali.  


## Praktikum 6.2 — Mengamati Siklus Hidup Proses

1. Buat proses di background dan amati kondisinya:
```bash
sleep 60 &
ps aux | grep sleep
```
Output :
```bash
root@ubuntuser:/home/yudhis# sleep 60 &
[1] 1283
root@ubuntuser:/home/yudhis# ps aux | grep sleep
root        1283  0.0  0.0   5684  2104 pts/2    S    14:07   0:00 sleep 60
root        1285  0.0  0.0   6544  2328 pts/2    S+   14:07   0:00 grep --color=auto sleep
```

2. Amati perubahan exit code dari perintah yang berhasil dan gagal:
```bash
ls / tmp
echo " Sukses : $?"
ls / direktori - tidak - ada
echo " Gagal : $?"
```
Output : 
```bash
root@ubuntuser:/home/yudhis# ls /tmp
snap-private-tmp
systemd-private-e883a04f257d4402b5ca3840da241f74-fwupd.service-NfBXJ8
systemd-private-e883a04f257d4402b5ca3840da241f74-ModemManager.service-uGfyK9
systemd-private-e883a04f257d4402b5ca3840da241f74-polkit.service-EFsXVL
systemd-private-e883a04f257d4402b5ca3840da241f74-systemd-logind.service-WLp0nl
systemd-private-e883a04f257d4402b5ca3840da241f74-systemd-resolved.service-cUPjRP
systemd-private-e883a04f257d4402b5ca3840da241f74-upower.service-iXFjhA
root@ubuntuser:/home/yudhis# echo "Sukses: $?"
Sukses: 0
[1]+  Done                    sleep 60
root@ubuntuser:/home/yudhis# ls /direktori-tidak-ada
ls: cannot access '/direktori-tidak-ada': No such file or directory
root@ubuntuser:/home/yudhis# echo "Gagal: $?"
Gagal: 2
```  

### Latihan 6.2  

1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi
apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?  
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit
code masing-masing. Pola apa yang Anda temukan?

Jawaban :  
1. Kolom STAT menunjukkan S (sleeping) karena proses sedang menunggu timer selesai dan tidak menggunakan CPU. Jika di-background, biasanya S.  
2. Perintah ```sukses → $? = 0```, Perintah ```gagal → $?``` bernilai bukan nol (misal 1, 2, 127, dll). Pola: nilai 0 selalu menandakan sukses, selain itu error.

 
## Praktikum 6.3 — Mengatur Prioritas Proses

1. Jalankan proses dengan prioritas rendah:
```bash
nice -n 10 sleep 300 &
```

Output :  
```bash
[1] 1768
```

2. Verifikasi nilai nice pada kolom NI:
```bash
ps aux | grep sleep
```

Output :  
```bash
root        1768  0.0  0.0   5684  2104 pts/2    SN   14:19   0:00 sleep 300
root        1774  0.0  0.0   6544  2332 pts/2    S+   14:20   0:00 grep --color=auto sleep
```

3. Ubah nilai nice proses yang sudah berjalan:
```bash
renice -n 15 -p <PID >
ps -p <PID > -o pid , ni , cmd
```

Output :  
```bash
root@ubuntuser:/home/yudhis# renice -n 15 -p 1794
1794 (process ID) old priority 10, new priority 15
root@ubuntuser:/home/yudhis# ps -p 1794 -o pid,ni,cmd
    PID  NI CMD
   1794  15 sleep 300
```

4. Bersihkan proses percobaan:
```bash
kill %1
```

Output :  
```bash
[1]+  Terminated              nice -n 10 sleep 300
```

### Latihan 6.3
1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan
ps.  
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.  
3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa Linux membatasi hal ini untuk user biasa?  

Jawaban :  
1.  
```bash
root@ubuntuser:/home/yudhis# nice -n 5 sleep 200 &
[1] 1808
root@ubuntuser:/home/yudhis# ps -o pid,ni,cmd
    PID  NI CMD
   1063   0 sudo su
   1064   0 su
   1080   0 bash
   1808   5 sleep 200
   1809   0 ps -o pid,ni,cmd
```
2.  
```bash
root@ubuntuser:/home/yudhis# renice -n 10 -p 1808
1808 (process ID) old priority 5, new priority 10
root@ubuntuser:/home/yudhis# ps -o pid,ni,cmd
    PID  NI CMD
   1063   0 sudo su
   1064   0 su
   1080   0 bash
   1808  10 sleep 200
   1811   0 ps -o pid,ni,cmd
```
3. Akan muncul pesan permission denied karena hanya root yang boleh menurunkan nilai nice (memberi prioritas lebih tinggi dari default 0). 


## Praktikum 6.4 — Mengirim Sinyal ke Proses
1. Buat proses percobaan:
```bash
sleep 500 &
sleep 600 &
sleep 700 &
ps aux | grep -v grep | grep sleep
```

Output :  
```bash
root@ubuntuser:/home/yudhis# sleep 500 &
[2] 1822
[1]   Done                    nice -n 5 sleep 200
root@ubuntuser:/home/yudhis# sleep 600 &
[3] 1826
root@ubuntuser:/home/yudhis# sleep 700 &
[4] 1827
root@ubuntuser:/home/yudhis# ps aux | grep -v grep | grep sleep
root        1822  0.0  0.0   5684  2104 pts/2    S    14:44   0:00 sleep 500
root        1826  0.0  0.0   5684  2104 pts/2    S    14:45   0:00 sleep 600
root        1827  0.0  0.0   5684  2108 pts/2    S    14:45   0:00 sleep 700
```

2. Hentikan satu proses dengan SIGTERM dan verifikasi:
```bash
kill <PID - sleep -500 >
ps aux | grep -v grep | grep sleep
```

Output :  
```bash
root@ubuntuser:/home/yudhis# kill 1822
root@ubuntuser:/home/yudhis# ps aux | grep -v grep | grep sleep
root        1826  0.0  0.0   5684  2104 pts/2    S    14:45   0:00 sleep 600
root        1827  0.0  0.0   5684  2108 pts/2    S    14:45   0:00 sleep 700
[2]   Terminated              sleep 500
```

3. Jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT:
```bash
kill - SIGSTOP <PID - sleep -600 >
ps aux | grep sleep # amati kolom STAT : berubah
menjadi T
kill - SIGCONT <PID - sleep -600 >
ps aux | grep sleep # STAT kembali ke S
```

Output :  
```bash
root@ubuntuser:/home/yudhis# kill -SIGSTOP 1826
root@ubuntuser:/home/yudhis# ps aux | grep sleep
root        1826  0.0  0.0   5684  2104 pts/2    T    14:45   0:00 sleep 600
root        1827  0.0  0.0   5684  2108 pts/2    S    14:45   0:00 sleep 700
root        1838  0.0  0.0   6544  2328 pts/2    S+   14:48   0:00 grep --color=auto sleep

[3]+  Stopped                 sleep 600
root@ubuntuser:/home/yudhis# kill -SIGCONT 1826
root@ubuntuser:/home/yudhis# ps aux | grep sleep
root        1826  0.0  0.0   5684  2104 pts/2    S    14:45   0:00 sleep 600
root        1827  0.0  0.0   5684  2108 pts/2    S    14:45   0:00 sleep 700
root        1840  0.0  0.0   6544  2328 pts/2    S+   14:48   0:00 grep --color=auto sleep
```

4. Hentikan semua proses sleep sekaligus:
```bash
pkill sleep
```

Output :  
```bash
root@ubuntuser:/home/yudhis# pkill sleep
root@ubuntuser:/home/yudhis# ps aux | grep sleep
root        1844  0.0  0.0   6544  2332 pts/2    S+   14:49   0:00 grep --color=auto sleep
[3]-  Terminated              sleep 600
[4]+  Terminated              sleep 700
```


### Latihan 6.4
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?

Jawaban :  
1. Kolom STAT berubah menjadi T (stopped). Proses dihentikan sementara dan tidak mendapat jatah CPU. 
```bash
root@ubuntuser:/home/yudhis# sleep 400 &
[1] 1857
root@ubuntuser:/home/yudhis# kill -SIGSTOP 1857
root@ubuntuser:/home/yudhis# ps aux | grep sleep
root        1857  0.0  0.0   5684  2104 pts/2    T    14:54   0:00 sleep 400
root        1859  0.0  0.0   6544  2332 pts/2    S+   14:54   0:00 grep --color=auto sleep

[1]+  Stopped                 sleep 400
```
2. STAT kembali ke S (sleeping) dan proses berjalan normal. 
```bash
root@ubuntuser:/home/yudhis# kill -SIGCONT 1857
root@ubuntuser:/home/yudhis# ps aux | grep sleep
root        1857  0.0  0.0   5684  2104 pts/2    S    14:54   0:00 sleep 400
root        1861  0.0  0.0   6544  2328 pts/2    S+   14:54   0:00 grep --color=auto sleep
```
3. SIGTERM digunakan terlebih dahulu karena memberi kesempatan proses menyimpan data dan keluar secara rapi. SIGKILL hanya digunakan jika proses tidak merespon SIGTERM atau benar-benar harus dihentikan paksa. 
```bash
root@ubuntuser:/home/yudhis# kill 1857
root@ubuntuser:/home/yudhis# ps aux | grep -v grep | grep sleep
[1]+  Terminated              sleep 400
```

## Praktikum 6.5 — Manajemen Job Foreground dan Background
1. Jalankan tiga job di background:
```bash
sleep 200 &
sleep 300 &
sleep 400 &
jobs
```

Output : 
```bash
root@ubuntuser:/home/yudhis# sleep 200 &
[1] 1874
root@ubuntuser:/home/yudhis# sleep 300 &
[2] 1875
root@ubuntuser:/home/yudhis# sleep 400 &
[3] 1876
root@ubuntuser:/home/yudhis# jobs
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```

2. Bawa job pertama ke foreground, jeda, lalu kembalikan ke background:
```bash
fg %1
# Tekan Ctrl +Z untuk menjeda
bg %1
jobs
```

Output : 
```bash
root@ubuntuser:/home/yudhis# fg %1
sleep 200
^Z
[1]+  Stopped                 sleep 200
root@ubuntuser:/home/yudhis# bg %1
[1]+ sleep 200 &
root@ubuntuser:/home/yudhis# jobs
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```

3. Hentikan semua job:
```bash
kill %1 %2 %3
jobs
```

Output : 
```bash
root@ubuntuser:/home/yudhis# kill %1 %2 %3
[1]   Terminated              sleep 200
[2]-  Terminated              sleep 300
[3]+  Terminated              sleep 400
root@ubuntuser:/home/yudhis# jobs
```


### Latihan 6.5
1. Jalankan top di foreground. Apa yang terjadi di terminal?
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q .

Jawaban :  

1. Terminal terisi penuh dengan tampilan top dan tidak bisa menerima perintah lain sampai top keluar. 
```bash
top - 15:07:20 up  1:20,  2 users,  load average: 0.00, 0.01, 0.00
Tasks: 134 total,   1 running, 133 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 95.1 id,  0.2 wa,  0.0 hi,  4.3 si,  0.
MiB Mem :   3422.4 total,   2269.6 free,    370.7 used,    944.3 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   3051.6 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+
    345 root      20   0       0      0      0 I   0.7   0.0   0:25.64
    256 root      20   0       0      0      0 S   0.3   0.0   0:00.26
    279 root      20   0       0      0      0 I   0.3   0.0   0:00.30
      1 root      20   0   22112  13268   9476 S   0.0   0.4   0:01.63
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.01
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
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.65
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.63
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.22
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     21 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     23 root      rt   0       0      0      0 S   0.0   0.0   0:00.43
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     26 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     27 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     28 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     29 root      rt   0       0      0      0 S   0.0   0.0   0:00.33
     30 root      20   0       0      0      0 S   0.0   0.0   0:00.28
     36 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     38 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     39 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     40 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     41 root      20   0       0      0      0 I   0.0   0.0   0:00.54
     43 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
```

2. Status menunjukkan Stopped karena top dijeda (dikirim SIGSTOP).
```bash
[1]+  Stopped                 top
root@ubuntuser:/home/yudhis# jobs
[1]+  Stopped                 top
```

3. Top tetap berjalan di background, tapi outputnya akan terus menulis ke terminal sehingga mengacaukan tampilan. Top kurang cocok di background karena interaktif. 
```bash
root@ubuntuser:/home/yudhis# bg %1
[1]+ top &

[1]+  Stopped                 top
```

4. Top kembali ke foreground, lalu tekan q untuk keluar dengan normal. 
```bash
top - 15:10:01 up  1:23,  2 users,  load average: 0.00, 0.00, 0.00
Tasks: 134 total,   1 running, 133 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.2 sy,  0.0 ni, 95.9 id,  0.0 wa,  0.0 hi,  3.9 si,  0.
MiB Mem :   3422.4 total,   2269.6 free,    370.7 used,    944.3 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   3051.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+
    345 root      20   0       0      0      0 I   0.7   0.0   0:26.82
    379 root      rt   0  288988  27324   8760 S   0.3   0.8   0:02.26
    437 root      20   0       0      0      0 I   0.3   0.0   0:06.91
   1880 root      20   0       0      0      0 I   0.3   0.0   0:00.08
   1883 root      20   0   11940   6012   3780 R   0.3   0.2   0:00.10
      1 root      20   0   22112  13268   9476 S   0.0   0.4   0:01.64
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.01
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
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.65
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.64
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.23
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     21 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     23 root      rt   0       0      0      0 S   0.0   0.0   0:00.44
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     26 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     27 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     28 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     29 root      rt   0       0      0      0 S   0.0   0.0   0:00.33
     30 root      20   0       0      0      0 S   0.0   0.0   0:00.28
     36 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     38 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     39 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     40 root      20   0       0      0      0 S   0.0   0.0   0:00.00
```


## Praktikum 6.6 — Pemantauan Proses
1. Temukan proses dengan penggunaan CPU dan memori tertinggi:
```bash
ps aux -- sort = -% cpu | head -10
ps aux -- sort = -% mem | head -10
```

Output ;  
```bash
root@ubuntuser:/home/yudhis# ps aux --sort=-%cpu | head -10
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1887  300  0.1  10884  4624 pts/2    R+   15:13   0:00 ps aux --sort=-%cpu
root         345  0.5  0.0      0     0 ?        I    13:47   0:28 [kworker/2:3-events]
yudhis      1052  0.3  0.2  13764  7484 ?        S    13:49   0:18 sshd: yudhis@pts/1
root         437  0.1  0.0      0     0 ?        I    13:47   0:07 [kworker/0:3-events]
root          72  0.1  0.0      0     0 ?        I    13:47   0:07 [kworker/1:2-events]
root        1110  0.0  1.2 685756 43676 ?        Ssl  13:51   0:03 /usr/libexec/fwupd/fwupd
root         379  0.0  0.7 288988 27324 ?        SLsl 13:47   0:02 /sbin/multipathd -d -s
root         767  0.0  0.1 293152  3764 ?        Sl   13:47   0:02 /usr/sbin/VBoxService
root        1120  0.0  0.2 314392  9732 ?        Ssl  13:51   0:02 /usr/libexec/upowerd
root@ubuntuser:/home/yudhis# ps aux --sort=-%mem | head -10
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1110  0.0  1.2 685756 43676 ?        Ssl  13:51   0:03 /usr/libexec/fwupd/fwupd
root         379  0.0  0.7 288988 27324 ?        SLsl 13:47   0:02 /sbin/multipathd -d -s
root         731  0.0  0.6 109688 23192 ?        Ssl  13:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         323  0.0  0.5  66860 17524 ?        S<s  13:47   0:00 /usr/lib/systemd/systemd-journald
root         668  0.0  0.3 468972 13608 ?        Ssl  13:47   0:00 /usr/libexec/udisks2/udisksd
root           1  0.0  0.3  22112 13268 ?        Ss   13:47   0:01 /sbin/init splash noprompt noshell automatic-ubiquity
systemd+     480  0.0  0.3  21588 13100 ?        Ss   13:47   0:00 /usr/lib/systemd/systemd-resolved
root         754  0.0  0.3 392100 12948 ?        Ssl  13:47   0:00 /usr/sbin/ModemManager
root        1067  0.0  0.3  20092 11292 ?        Ss   13:49   0:00 /usr/lib/systemd/systemd --user
```

2. Jalankan top dan eksplorasi shortcut-nya:
```bash
top
# Tekan M, P, 1 , u secara bergantian
# Tekan q untuk keluar
```

Output ;  
```bash
root@ubuntuser:/home/yudhis# top
top - 15:15:22 up  1:28,  2 users,  load average: 0.00, 0.00, 0.00
Tasks: 136 total,   2 running, 134 sleeping,   0 stopped,   0 zombie
%Cpu0  :  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.
%Cpu1  :  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.
%Cpu2  :  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.
MiB Mem :   3422.4 total,   2269.6 free,    370.7 used,    944.4 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   3051.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+
      1 root      20   0   22112  13268   9476 S   0.0   0.4   0:01.69
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.01
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
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.65
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.67
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.24
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     21 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     23 root      rt   0       0      0      0 S   0.0   0.0   0:00.45
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     26 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     27 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     28 root     -51   0       0      0      0 S   0.0   0.0   0:00.00
     29 root      rt   0       0      0      0 S   0.0   0.0   0:00.33
     30 root      20   0       0      0      0 S   0.0   0.0   0:00.29
     36 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     38 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     39 root      20   0       0      0      0 S   0.0   0.0   0:00.01
     40 root      20   0       0      0      0 S   0.0   0.0   0:00.00
     41 root      20   0       0      0      0 I   0.0   0.0   0:00.54
     43 root       0 -20       0      0      0 I   0.0   0.0   0:00.00
     44 root      20   0       0      0      0 S   0.0   0.0   0:00.59
```

3. Instal dan jalankan htop:
```bash
sudo apt install -y htop
htop
# Tekan F6 untuk pilih kolom pengurutan
# Tekan F10 atau q untuk keluar
```

Output ;  
```bash
root@ubuntuser:/home/yudhis# sudo apt install -y htop
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
htop is already the newest version (3.3.0-4build1).
0 upgraded, 0 newly installed, 0 to remove and 74 not upgraded.
root@ubuntuser:/home/yudhis# htop
```

### Latihan 6.6  
1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?  
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa
informasi ini berguna?  
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah.
Tekan F9 dan amati opsi sinyal yang tersedia.  

Jawaban :  

1.   
```bash
root@ubuntuser:/home/yudhis# ps aux --sort=-%mem | head -5
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1110  0.0  1.2 685756 43676 ?        Ssl  13:51   0:03 /usr/libexec/fwupd/fwupd
root         379  0.0  0.7 288988 27324 ?        SLsl 13:47   0:02 /sbin/multipathd -d -s
root         731  0.0  0.6 109688 23192 ?        Ssl  13:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         323  0.0  0.5  66860 17532 ?        S<s  13:47   0:00 /usr/lib/systemd/systemd-journald
```
2. Menampilkan penggunaan setiap core CPU secara terpisah. Berguna untuk melihat beban merata atau tidaknya.

3.  Akan muncul daftar sinyal yang bisa dikirim (SIGTERM, SIGKILL, SIGHUP, dll). Ini memudahkan tanpa perlu mengingat nomor sinyal.


## 1.8 Latihan
### Latihan 6.A
Eksplorasi Proses Sistem
1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa
nama dan fungsi proses tersebut dalam sistem Linux modern?
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang
dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian
besar proses di sistem berada dalam kondisi ini?

Jawaban :  

1. Proses tersebut bernama init (biasanya systemd di Linux modern), yang berfungsi sebagai proses pertama yang dijalankan kernel untuk menginisialisasi sistem dan menjadi induk dari semua proses lainnya.

 
```bash
root           1  0.4  0.3  21992 13284 ?        Ss   05:20   0:03 /sbin/ini
```
2. Proses milik root ada 92 (dihitung dari semua baris dengan USER=root, termasuk kernel threads seperti [kthreadd] dan seterusnya).
Proses milik user yudhis ada 4 (baris dengan USER=yudhis: PID 1029, 1030, 990, 991).
Root memiliki lebih banyak proses karena ia menjalankan semua layanan sistem, driver kernel, dan daemon yang diperlukan untuk operasi sistem.

3. Semua proses yang kolom STAT-nya diawali huruf S (misalnya Ss, S+, Ssl) berada dalam kondisi sleeping (dapat diinterupsi). Contohnya: PID 1 (/sbin/ini), PID 2 ([kthreadd]), PID 321 (/usr/lib/...), dll. Sebagian besar proses di sistem berada dalam kondisi S karena mereka sedang menunggu suatu event (seperti I/O, timer, atau sinyal) dan tidak membutuhkan CPU.  


### Latihan 6.B
Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di
background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan
ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job.
Berapa job yang tersisa?

Jawaban : 

1.  
```bash
root@ubuntuser:/home/yudhis# sleep 100 &
[1] 1165
root@ubuntuser:/home/yudhis# sleep 200 &
[2] 1166
root@ubuntuser:/home/yudhis# sleep 300 &
[3] 1168
root@ubuntuser:/home/yudhis# jobs
[1]   Done                    sleep 100
[2]-  Running                 sleep 200 &
[3]+  Running                 sleep 300 &
```
2.  
```bash
root@ubuntuser:/home/yudhis# fg %2
sleep 200
^Z
[2]+  Stopped                 sleep 200
root@ubuntuser:/home/yudhis# bg %2
[2]+ sleep 200 &
```
3.  
```bash
root@ubuntuser:/home/yudhis# kill %1
bash: kill: %1: no such job
[2]-  Done                    sleep 200
root@ubuntuser:/home/yudhis# jobs
[3]+  Running                 sleep 300 &
```


### Latihan 6.C
Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice
+15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10.
Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim
SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.

Jawaban :  

1.  
```bash
root@ubuntuser:/home/yudhis# nice -n 5 sleep 200 &
[1] 1253
root@ubuntuser:/home/yudhis# nice -n 15 sleep 200 &
[2] 1254
root@ubuntuser:/home/yudhis# ps -o pid,ni,cmd | grep sleep
   1253   5 sleep 200
   1254  15 sleep 200
   1256   0 grep --color=auto sleep
```
2. Proses yang lebih diprioritaskan scheduler adalah yang nilai nice-nya lebih kecil, yaitu proses dengan NI = 10 (karena 10 < 15).
```bash
root@ubuntuser:/home/yudhis# renice -n 10 -p 1253
1253 (process ID) old priority 5, new priority 10
root@ubuntuser:/home/yudhis# ps -o pid,ni,cmd | grep sleep
   1253  10 sleep 200
   1254  15 sleep 200
   1259   0 grep --color=auto sleep
``` 
3.
```bash
root@ubuntuser:/home/yudhis# kill -SIGSTOP 1253
root@ubuntuser:/home/yudhis# ps -o pid,stat,cmd | grep sleep
   1253 TN   sleep 200
   1254 SN   sleep 200
   1266 S+   grep --color=auto sleep

[1]+  Stopped                 nice -n 5 sleep 200
root@ubuntuser:/home/yudhis# kill -SIGCONT 1253
root@ubuntuser:/home/yudhis# ps -o pid,stat,cmd | grep sleep
   1253 SN   sleep 200
   1254 SN   sleep 200
   1268 S+   grep --color=auto sleep
root@ubuntuser:/home/yudhis# pkill sleep
[1]-  Terminated              nice -n 5 sleep 200
[2]+  Terminated              nice -n 15 sleep 200
```
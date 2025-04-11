# Tugas-SO-Manajemen-Proses

# Praktikum 6 - Linux Shell

Repositori ini berisi jawaban dari Praktikum 6 Linux Shell, khususnya bagian BAB E.

---

## Soal 1: Proses dan Hierarki

### A. Nama-nama proses yang bukan root
Gunakan perintah berikut:
```bash
ps -eo user,comm | grep -v '^root'
```
Ini akan menampilkan semua proses yang **tidak dijalankan oleh user root**.

### B. PID dan COMMAND dari proses yang paling banyak menggunakan CPU Time
Gunakan perintah berikut:
```bash
ps -eo pid,comm,etime,%cpu --sort=-%cpu | head -n 2
```
Baris kedua (setelah header) adalah proses dengan penggunaan CPU terbesar.

### C. Buyut Proses dan PID
Misalnya kamu menemukan PID 1234, jalankan perintah berikut untuk melacak sampai buyut:
```bash
ps -o ppid= -p 1234        # dapatkan parent
ps -o ppid= -p [parent1]   # dapatkan grandparent
ps -o ppid= -p [parent2]   # dapatkan buyut
```
Lalu ambil nama proses buyut dengan:
```bash
ps -p [buyutPID] -o pid,comm
```

### D. Contoh Proses Daemon
Beberapa contoh proses daemon:
- `systemd` – init system
- `cron` – penjadwal tugas
- `rsyslogd` – logging
- `sshd` – server SSH
- `cupsd` – layanan printer
- `bluetoothd`, `networkd`, dll

### E. Rantai Proses ke PPID = 1
Langkah di terminal:
```bash
$ csh
$ who
$ bash
$ ls
$ sh
$ ps
```
Ambil PID terbesar dan telusuri prosesnya ke atas menggunakan `ps -o ppid=` sampai PPID = 1. Ini menunjukkan urutan hierarki proses dari shell ke induk sistem.

### Screenshot:
![Screenshot Soal 1](soal1/screenshot.png)

---

## Soal 2: Menjalankan dan Memberhentikan Proses Background

### Script: `prog.sh`
```bash
#!/bin/sh
trap "echo Hello Goodbye" SIGTERM

echo "Program berjalan …"
while :
do
    sleep 1
done
```

### Langkah:
1. Jalankan program:
```bash
./prog.sh &
```
2. Catat PID yang muncul.
3. Hentikan proses:
```bash
kill -15 [PID]
```

### Screenshot:
![Screenshot Soal 2](soal2/screenshot.png)

---

## Soal 3: Menjalankan Script dengan Trap untuk Menghapus File

### Script: `myjob.sh`
```bash
#!/bin/sh
trap "rm -f berkas hasil; echo 'File dihapus karena proses dihentikan.'" SIGINT SIGTERM

i=1
while :
do
    find / -print > berkas 2>/dev/null
    sort berkas -o hasil
    echo "Proses selesai pada $(date)" >> proses.log
    sleep 60
done
```

### Screenshot:
![Screenshot Soal 3](soal3/screenshot.png)

---

## Struktur Direktori
```
praktikum-6-linux-shell/
├── README.md
├── soal1/
│   ├── jawaban.txt
│   └── screenshot.png
├── soal2/
│   ├── prog.sh
│   └── screenshot.png
├── soal3/
│   ├── myjob.sh
│   └── screenshot.png
```

Silakan gunakan struktur ini untuk membuat repositori GitHub. File skrip dan screenshot bisa dimasukkan ke dalam folder masing-masing sesuai soal.


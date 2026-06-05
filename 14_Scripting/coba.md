# <h1 align="center" style="font-family: 'Google Sans', sans-serif;">Laporan Praktikum Modul 14 <br> Scripting</h1>
<p align="center" style="font-family: 'Google Sans', sans-serif;">Marsella Dwi Julianti - 2311104004</p>

## Dasar Teori

Shell Scripting pada Linux adalah rangkaian perintah yang disimpan dalam file teks biasa (biasanya berekstensi `.sh`) untuk dieksekusi secara otomatis oleh interpreter command line seperti Bash (Bourne-Again Shell). 

Konsep dasar dalam pemrograman Bash meliputi:
1. **Shebang (`#!/bin/bash`)**: Baris pertama script yang menentukan path ke interpreter Bash.
2. **Variabel**: Tempat menyimpan data sementara (`nama=value`). Single quote (`'`) membaca karakter secara literal, sedangkan double quote (`"`) mendukung substitusi variabel.
3. **Command Substitution**: Menyimpan output perintah ke dalam variabel dengan sintaks `$(command)`.
4. **Command Line Argument**: Parameter luar yang ditangkap variabel spesial `$1` s.d `$9`, `$0` (nama script), dan `$#` (jumlah argumen).
5. **Struktur Kontrol**: Pengondisian (`if`, `case`) dan perulangan (`for`, `while`, `until`) untuk mengatur alur program.
6. **Function**: Blok kode terpisah untuk efisiensi penulisan ulang (*code reuse*).

---

## Guided

### 1. Struktur Dasar Bash Script (`myscript.sh`)
**Kode Program:**
```bash
#!/bin/bash
# Contoh komentar
echo "Hello World!"
```
> **Keterangan Screenshot:**
![alt text](image.png)

### 2. Variabel & Command Substitution
**Kode Program:**
```bash
#!/bin/bash
myvar='Hello World'
echo $myvar
newvar="More $myvar"
echo $newvar
newvar1='More $myvar'
echo $newvar1

myvar2=hello
var1=world
echo $myvar2 $var1

myvar_dir=$(ls /etc)
echo Terdapat file $myvar_dir di folder /etc
```
> **Keterangan Screenshot:**
![alt text](image-1.png)

### 3. Command Line Argument
**Kode Program:**
```bash
#!/bin/bash
echo "Argumen 1: $1"
echo "Argumen 2: $2"
echo "Nama script (\$0): $0"
echo "PID Script (\$\$): $$"
echo "Nama User (\$USER): $USER"
echo "Angka Random (\$RANDOM): $RANDOM"
```
> **Keterangan Screenshot:**
![alt text](image-2.png)

### 4. Input Pengguna (`read`)
**Kode Program:**
```bash
#!/bin/bash
echo Hello, Who are you?
read varname
echo Nice to meet you $varname

echo What cars do you like?
read car1 car2 car3
echo your first car: $car1
echo your second car: $car2
echo your third car: $car3
```
> **Keterangan Screenshot:**
![alt text](image-3.png)

### 5. Operasi Aritmatika (`let` dan `expr`)
**Kode Program:**
```bash
#!/bin/bash
let a=20+22
echo $a
let "a = 5 + 4"
echo $a
let a++
echo $a
let "a = $1 + 10"
echo $a

expr 5 + 4
expr "5 + 4"
expr 5+4
expr 5 \* $1
a=$(expr 10 - 3)
echo $a
```
> **Keterangan Screenshot:**
![alt text](image-4.png)

### 6. If dan Case Statement
**Kode Program:**
```bash
#!/bin/bash
if [ $1 -ge 17 ]
then
    echo Boleh melakukan pemilu
else
    echo Tunggu pemilu selanjutnya
fi

case $2 in
    start)
        echo Mulai
        ;;
    stop)
        echo Berhenti
        ;;
esac
```
> **Keterangan Screenshot:**
![alt text](image-5.png)

### 7. Perulangan (`for`, `while`, `until`)
**Kode Program:**
```bash
#!/bin/bash
echo "--- For Loop ---"
for value in {1..10}; do echo $value; done
for value in {10..0..2}; do echo $value; done

echo "--- While Loop ---"
counter=1
while [ $counter -le 10 ]
do
    echo $counter
    ((counter++))
done

echo "--- Until Loop ---"
counter_until=1
until [ $counter_until -gt 10 ]
do
    echo $counter_until
    ((counter_until++))
done
```
> **Keterangan Screenshot:**
![alt text](image-6.png)

### 8. Function
**Kode Program:**
```bash
#!/bin/bash
tampilkan_sesuatu(){
    echo Hello $1
}
tampilkan_sesuatu Mars
tampilkan_sesuatu Jupiter
```
> **Keterangan Screenshot:**
![alt text](image-7.png)

---

## Unguided

### 1. PERMULAAN — Menyapa User (`greeting.sh`)
**Kode Program:**
```bash
#!/bin/bash
echo "Hai User"
echo "Hari ini adalah $(date)"
echo "User yang sedang login saat ini adalah:"
who
```
> **Keterangan Screenshot:**
![alt text](image-8.png)

### 2. PENGONDISIAN — Waktu Jam Sistem (`greeting_1.sh`)
**Kode Program:**
```bash
#!/bin/bash
jam=$(date +%k | tr -d ' ')
echo "Sekarang jam $jam"

if [ $jam -gt 5 ] && [ $jam -le 10 ]; then
    echo "Selamat pagi User"
elif [ $jam -gt 10 ] && [ $jam -le 15 ]; then
    echo "Selamat siang User"
elif [ $jam -gt 15 ] && [ $jam -le 19 ]; then
    echo "Selamat sore User"
else
    echo "Selamat malam User"
fi
```
> **Keterangan Screenshot:**
![alt text](image-9.png)

### 3. PERULANGAN — Perhitungan Mundur (`countdown.sh`)
**Kode Program:**
```bash
#!/bin/bash
for value in {10..1}
do
    echo $value
done
echo "GO!"
```
> **Keterangan Screenshot:**
![alt text](image-10.png)

### 4. INPUT PENGGUNA (`countdown_1.sh`)
**Kode Program:**
```bash
#!/bin/bash
echo "Masukkan angka:"
read angka
echo "Mulai countdown!"

while [ $angka -ge 1 ]
do
    echo $angka
    let angka--
done
echo "GO!"
```
> **Keterangan Screenshot:**
![alt text](image-11.png)

### 5. PARAMETER SCRIPT (`countdown_2.sh`)
**Kode Program:**
```bash
#!/bin/bash
if [ $# -eq 0 ]; then
    echo "penggunaan: countdown_2.sh initial_value"
    exit 1
fi

angka=$1
while [ $angka -ge 1 ]
do
    echo $angka
    let angka--
done
echo "GO!"
```
> **Keterangan Screenshot:**
![alt text](image-12.png)

### 6. PENGONDISIAN DIRECTORY (`list_direktori.sh`)
**Kode Program:**
```bash
#!/bin/bash
for file in *
do
    echo "$file"
done
```
> **Keterangan Screenshot:**
![alt text](image-13.png)

---

## Referensi
1. `[IF] Modul Praktikum Sistem Operasi.pdf` - Laboratorium Informatika Universitas Telkom
2. `[REG] JURNAL MODUL 15.pdf` - Jurnal Praktikum Scripting Sistem Operasi
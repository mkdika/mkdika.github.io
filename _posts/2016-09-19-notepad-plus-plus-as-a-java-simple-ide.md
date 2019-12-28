---
layout      : post
title       : "Notepad++ as a Java Simple IDE"
date        : 2016-09-19 15:15:05 +0700
categories  : Java
tags        : [java, ide]
comments    : true
---
![Imgur](http://i.imgur.com/G3kzYFl.png)

Notepad++ adalah salah satu enhanced Text Editor yang sangat populer di OS Windows, lightweight, dengan dukungan plug-in yang banyak sehingga membuat Notepad++ menjadi aplikasi Text Editor yang powerful.

Sebagai lanjutan dari serangkaian tutorial untuk pemula mempelajari bahasa pemograman Java, pada tutorial kali ini kita akan memanfaatkan Notepad++ menjadi IDE Java sederhana kita. Gol nya adalah kita bisa men-compile dan men-run Java Code dari Editor Notepad++, sehingga tidak perlu lagi bolak balik ke `Command Line` secara terpisah. Asik kan? minimal hilang deh satu kerepotan :)

## Persiapan

- **Operating System**: Windows 7,8,10
- [**Notepad++**](https://notepad-plus-plus.org/repository/6.x/6.9.2/npp.6.9.2.Installer.exe) Download & install Notepad++ pada komputer/laptop Anda, pastikan install versi yang terbaru. Pada saat artikel ini ditulis versi terbaru dari Notepad++ adalah 6.9.2.
- **JDK**: Pastikan JDK telah terinstall terlebih dahulu dengan benar, cara instalasi JDK telah saya sharingkan untuk OS [Windows 7](/java/instalasi-jdk-pada-windows-7/) dan OS [Windows 10](/instalasi-jdk-pada-windows-10/). JDK yang saya pakai pada post ini adalah JDK 7 update 79. Pastikan command `javac` dan `java` telah ter-register di Windows Environment Variable, sehingga bisa dieksekusi dari folder manapun di `Command Line`.

## Instalasi Plug-In Notepad++

Supaya bisa compile & run Java Code dari Notepad++, kita perlu melakukan instalasi Plug-in khusus untuk kebutuhan ini, namanya `NppExec`. Pada Editor Notepad++, klik menu `Plugins`, kemudian pilih `Plugin Manager`, kemudian `Show Plugin Manager`.

![Imgur](http://i.imgur.com/VYqZKfT.png)

Kemudian pada tab `Available` cari plug-in `NppExec`. dicentang, kemudian klik tombol `Install`.

![Imgur](http://i.imgur.com/28ZC1y1.png)

Notepad++ akan melakukan download & instalasi, pastikan saat ini Anda terkoneksi dengan Internet. Apabila muncul popup konformasi instalasi, pilih `YES` saja, lanjutkan hingga selesai dan `restart` Notepad++ Anda.

### Langkah-langkah Menambah NppExec Execute

![Imgur](http://i.imgur.com/qRDcEhQ.png)

1. Pada editor Notepad++ tekan `F6` atau pilih dari menu `Plugins`.
2. kemudian `NppExec` dan `Execute..` untuk memunculkan execute editor.
3. Pastikan pada combobox yang terpilih adalah `<temporary script>` seperti pada gambar.
4. kemudian copy paste script berikut ke kolom `command(s)`.

```bash
NPP_SAVE

cd "$(CURRENT_DIRECTORY)"
"javac" $(FILE_NAME)
```

Kemudian klik tombol `save`. Masukan `Java-Compile` sebagai script name, dan `save`.

![Imgur](http://i.imgur.com/0EFkEf0.png)

Ulangi langkah 1,2,3. Kemudian copy paste script berikut ke kolom `command(s)`.

```bash
cd "$(CURRENT_DIRECTORY)"
"java"  -classpath "$(CURRENT_DIRECTORY)" "$(NAME_PART)"
```

Klik tombol `save`. Masukan `Java-Run` sebagai script name, dan `save`

![Imgur](http://i.imgur.com/5go73b6.png)

### Register Execute Script ke Macro

Klik menu `Plugins`, kemudian `NppExec`, kemudian `Advanced Options..` seperti pada gambar dibawah.

![Imgur](http://i.imgur.com/JjKlSuI.png)

Pada kolom `Associated script`, pilih `Java-Compile`, pastikan juga kolom `Item Name` berisi `Java-Compile`, dan klik tombol `Add/Modify`. Pastikan `Place to the Macros submenu` tercentang.

Ulangi hal yang sama untuk script `Java-Run`. Kemudian klik tombol `OK`.

![Imgur](http://i.imgur.com/WQTIMhb.png)

Restart Notepad++ Anda, apabila berhasil maka execute script `Java-Compile` dan `Java-Run` akan muncul di drop down menu `Macro`.

![Imgur](http://i.imgur.com/50lpInt.png)

Sampai sejauh ini sebenarnya kita telah dapat menjalankan `Java-Compile` ataupun `Java-Run` langsung dari editor Notepad++ dengan memilih menu macro diatas.

### Menambahkan Keyboard Shortcut

Ini adalah langkah terakhir untuk memudahkan kita dalam pemangilan NppExec script, yaitu dengan Keyboard Shortcut. Pada menu `Macro`, pilih `Modify Shortcut/Delete Macro...`.

![Imgur](http://i.imgur.com/zqLaZxj.png)

Klik tombol `Plugin commands`, kemudian cari baris `Java-Compile` dan `Java-Run` seperti tampak pada gambar dibawah ini. Kemudian klik tombol `Modify`.

![Imgur](http://i.imgur.com/rG4jKQT.png)

Keyboard Shortcut untuk `Java-Compile` dan `Java-Run` sebenarnya terserah Anda. Contoh kalau saya lebih nyaman `Ctrl + Shift + F5` untuk `Java-Compile` dan `Ctrl + Shift + F6` untuk `Java-Run`.

![Imgur](http://i.imgur.com/7uGJD7k.png)

![Imgur](http://i.imgur.com/aT5zQ3I.png)

Apabila shortcut telah terisi dengan benar, maka akan tampak seperti gambar dibawah, kemudian klik tombol `Close`.

![Imgur](http://i.imgur.com/yQI1a8R.png)

Restart Notepad++ Anda.

### Mencoba Java-Compile & Java-Run

Buka source code java Anda, simpan source code Anda, kemudian lakukan compile dengan shortcut keyboard yang telah kita buat sebelumnya. Sesuai contoh diatas tekan `Ctrl + Shift + F5` untuk `Java-Compile`. Akan muncul jendela `Console` seperti gambar dibawah.

![Imgur](http://i.imgur.com/m9Lu1WM.png)

Kemudian tekan `Ctrl + Shift + F6` untuk melakukan `Java-Run`. Hasil tampak seperti pada gambar dibawah.

![Imgur](http://i.imgur.com/MMAxGXM.png)

Jendala console akan mengantikan fungsi `cmd` yang biasa dipakai sebagai interaksi program Java yang kita jalankan. Semoga bermanfaat!

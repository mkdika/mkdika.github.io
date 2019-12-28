---
layout      : post
title       : "Instalasi JDK Pada Windows 10"
date        : 2016-08-28 15:15:05 +0700
categories  : Java
tags        : [java]
comments    : true
---
Berikut adalah step by step cara instalasi Java Development Kit (JDK) pada Operating System (OS) Windows 10. Tujuan dari posting ini adalah membantu para pemula dalam melakukan instalasi di JDK, dan mulai belajar Java. Pada saat akan melakukan instalasi JDK terdapat 2 opsi paket instalasi, opsi 1 mengunakan file Zip, opsi 2 mengunakan file instalasi `*.exe`. Supaya mempermudah kita akan mengunakan versi instlasi.

__Note:__ Untuk di Windows 8, langkah-langkah nya kurang lebih sama seperti di Windows 10.

## Persiapan

- Operating System: Windows 10
- JDK 8 update 144

Apabila ini adalah kali pertama Anda mulai belajar Java dan instalasi JDK, namun ternyata di komputer/Laptop Anda sebelumnya telah terdapat instalasi Java versi lain, sebaiknya di-uninstall terlebih dahulu dan kita mulai dari awal.

![Imgur](http://i.imgur.com/tlmezTJ.png)

## 1. Download dan Instalasi JDK sesuai arsitektur OS

Pada OS Windows terdapat type arsitektur 32-bit dan 64-bit, dan instalasi JDK tersedia untuk kedua type arsitektur Windows tersebut. Maka itu sebelum memulai download & install, pastikan dahulu versi arsitektur OS Windows Anda, cara pengecekan sbb:

Tekan tombol `Windows + E` untuk memunculkan File Explorer, kemudian klik icon `This PC` pada daftar di kiri, pada ribon menu diatas pilih Tab `Computer`, kemudian pilih `Properties`.

![Imgur](http://i.imgur.com/CopWKXN.png)

Perhatian nilai yang tertera pada kolom `System Type`. contoh punya saya adalah 64-bit.

![Imgur](http://i.imgur.com/BLc5g8H.png)

Jadi apabila pada `System Type` Anda adalah 64-bit, download JDK yang sesuai yaitu 64-bit. Begitu juga sebaliknya untuk yang 32-bit.

- [JDK 8 update 144 Windows 32-bit Installer](https://goo.gl/c9qisE)
- [JDK 8 update 144 Windows 64-bit Installer](https://goo.gl/EhUpkT)

Setelah itu lakukan instalasi dengan klik dobel icon file tersebut atau klik kanan `Open`.

![Imgur](http://i.imgur.com/BRlfcSx.png)

Klik Next dan ikutin langkah-langkah Instalasinya hingga selesai.

![Imgur](http://i.imgur.com/uct09LL.png)

Apabila terdapat window konfirmasi instalasi Java Runtime Environment (JRE) silakan di `NEXT` juga saja hingga selesai.

![Imgur](http://i.imgur.com/7LbatA8.png)

## 2. Pengecekan Hasil Instalasi

- Apabila JDK telah terinstall dengan sukses sesuai dengan type arsitektur OS, maka pada terdapat folder baru pada path `C:\Program Files\Java`.
- Selain itu pengecekan apakah JDK telah sukses terinstalasi bisa juga dengan Command line. Klik `START MENU`, kemudian ketik `cmd`.

![Imgur](http://i.imgur.com/TXPvfuz.png)

- Pada `cmd` ketik: `java -version`
- Apabila berhasil akan muncul informasi mengenai versi java yang terinstall seperti di bawah ini.

![Imgur](http://i.imgur.com/F4PA4Sp.png)

## 3. Setting JAVA_HOME & OS PATH ##

Sebelum bisa digunakan, langkah berikutnya adalah setting Windows Environment Variable untuk `JAVA_HOME` dan `PATH`.
Langkah-langkahnya sbb:

Buka `cmd` seperti cara diatas. ketik: `SETX JAVA_HOME "C:\Program Files\Java\jdk1.8.0_144"`

Dimana `JAVA_HOME` adalah nama untuk Windows Environment Variable. `C:\Program Files\Java\jdk1.8.0_144` adalah lokasi instalasi java kita.

![Imgur](http://i.imgur.com/a5WgEaO.png)

Dilanjutkan dengan ketik: `SETX PATH "%PATH%;%JAVA_HOME%\bin"`

![Imgur](http://i.imgur.com/mnSPXfG.png)

Setelah selesai, `RESTART` Windows Anda. Testing keberhasilan setting Windows Environment Variable dengan cara sbb, buka `cmd` seperti diatas, kemudian:

Ketik: `echo %JAVA_HOME%`

![Imgur](http://i.imgur.com/7qk8wSm.png)

Ketik: `javac`

![Imgur](http://i.imgur.com/9ehWMgH.png)

Akan muncul tampilan help & available parameter untuk `javac`

Selesai sampai disini dan semoga bermanfaat :)

### Baca Juga

- [**Instalasi JDK Pada Windows 7**](/java/instalasi-jdk-pada-windows-7/)
- [**Instalasi NetBeans IDE pada Windows**](/java/instalasi-netbeans-ide-pada-windows/)

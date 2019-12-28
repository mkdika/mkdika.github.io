---
layout      : post
title       : "ZK MVVM CRUD Hibernate JPA Example"
date        : 2016-05-27 08:25:05 +0700
categories  : Zk
tags        : [java, zk, spring, hibernate]
comments    : true
---
![alt text](https://i.imgur.com/MlEappM.jpg)

Pada post kali ini secara UI Layer, Business Layer dan Persistent Layer masih sama yaitu ZK Framework Style MVVM, Spring Framework dan Hibernate. Namun terdapat beberapa pergantian sbb:

1. Kali ini saya mengunakan file konfigurasi XML untuk Spring Framework.

2. Hibernate JPA yang dipakai sebagai DAO Layer

Tujuannya adalah untuk menunjukan perbedaan secara konfigurasi dan code dibanding project sebelumnya, secara code pengunaan Spring Data JPA mungkin relatif lebih singkat dibanding Hibernate JPA (dengan code yang lebih panjang), namun secara fungsional program aplikasi tetaplah sama. Adapun alasan lainnya adalah juga sebagai contoh project untuk mem-benchmark performance dengan cara yang "Sangat Sederhana" kedua pendekatan DAO Layer tersebut.

Silakan cek dan clone [**GitHub** saya berikut ini.](https://github.com/mkdika/zkmvvmcrudhbjpa){:target="_blank"}. Informasi mengenai *Change Logs/Perubahan*, cara instalasi, serta teknologi yang digunakan dan versinya dapat dibaca di [**README**](https://github.com/mkdika/zkmvvmcrudhbjpa/blob/master/README.md){:target="_blank"} project-nya.

### Screenshot Aplikasi

![Sceenshot-1](https://i.imgur.com/MYzyhuV.png)

![Sceenshot-2](https://i.imgur.com/eYS6DSq.png)

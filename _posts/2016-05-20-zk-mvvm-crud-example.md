---
layout      : post
title       : "ZK MVVM CRUD Example"
date        : 2016-05-20 12:15:05 +0700
categories  : Zk
tags        : [java, zk, spring, hibernate]
comments    : true
---
![Zk](https://i.imgur.com/eNMs7EI.png)

[ZK (ZKOSS)](https://www.zkoss.org){:target="_blank"} Framework adalah salah satu framework populer Java Web berbasis Server Side/Server Centric, dengan dukungan fitur dan komponennya yang sangat lengkap. Saya pribadi telah mengunakan ZK Framework sejak versi 3 ([sekitar tahun 2009](https://kurohide.wordpress.com/2010/02/19/my-java-development-stack/){:target="_blank"}), dan digunakan pada hampir setiap project Java Web saya. Saat ini versi yang saya gunakan sudah versi 7 (7.0.8).

Pada kesempatan ini saya men-sharingkan contoh program ZK dengan style [Model View ViewModel (MVVM)](http://books.zkoss.org/zk-mvvm-book/7.0/introduction_of_mvvm.html){:target="_blank"}, sebagai informasi selain style MVVM, ZK juga mendukung style sebelumnya yaitu [Model View Controller (MVC)](https://www.zkoss.org/wiki/ZK_Developer's_Reference/MVC){:target="_blank"}. Contoh ini telah lengkap dengan fitur transaksi data Create Read Update Delete, dengan model transaksi OneToMany (Head Detail) sebagai contohnya. Silakan cek dan clone [**GitHub** saya berikut ini.](https://github.com/mkdika/zkmvvmcrud){:target="_blank"}

Informasi mengenai *Change Logs/Perubahan*, cara instalasi, serta teknologi yang digunakan dan versinya dapat dibaca di [**README**](https://github.com/mkdika/zkmvvmcrud/blob/master/README.md){:target="_blank"} project-nya.

Project ini merupakan prototype & Proof of Concept (POC) dari beberapa hal yang ingin dicoba, sbb:

1. Mengunakan [Spring Framework](https://projects.spring.io/spring-framework/){:target="_blank"} di Business Layer, serta [Hibernate](http://hibernate.org/){:target="_blank"} di Persistent Layer.

2. Mengunakan [MAVEN](https://maven.apache.org/){:target="_blank"} sebagai Dependency Manager & Build System.

3. Mengunakan konfigurasi Spring Framework via Java, ketimbang cara konvensional via file XML. Saya ingin mencoba menkonversi parameter-parameter & config yang selama ini saya pakai di XML dianalogikan ke Java Config.

4. Mengunakan [Hibernate Validator](http://hibernate.org/validator/){:target="_blank"} di Entity Class sebagai standard Bean Validator ([JSR-303](http://beanvalidation.org/1.0/spec/){:target="_blank"}), konfigurasi Hibernate Validator ini nantinya akan diteruskan (diintegrasi) sebagai Form field validator ZK (UI Layer).

5. Mengunakan [Bidirectional Association Mapping](https://docs.jboss.org/hibernate/orm/3.3/reference/en/html/associations.html){:target="_blank"} pada Entity Class One To May, nantinya akan diteruskan ke ZK sebagai Collection View Model Binding. Hal memberikan akan mempermudah code di UI Layer nantinya.

6. Mengunakan [Spring Data JPA](http://docs.spring.io/spring-data/jpa/docs/current/reference/html/){:target="_blank"} sebagai Data Access Object (DAO). Spring Data JPA adalah teknologi yang cukup unik, karena mengunakan Naming Convension pada Method sebagai Logic Query yang akan dihasilkan. Jadi untuk kasus umum, kita tidak perlu lagi menuliskan method DAO yang sering digunakan.

7. Mengunakan hanya style [MVVM](http://books.zkoss.org/zk-mvvm-book/7.0/introduction_of_mvvm.html){:target="_blank"} pada ZK (UI Layer). Sebagai informasi kita juga bisa kombinasi mengunakan MVVM bersamaan dengan MVC.

8. Transaksi Create Read Update Delete (CRUD) di Form ZK dilengkapi dengan Form Logic dan Field Validator.

9. Mengunakan komponen Grid ZK untuk Direct Inline Editing. Inline Editing merupakan salah satu pendekatan perancangan UI yang lebih memudahkan dalam penginputan data. Biasanya pendekatan ini lebih banyak digunakan pada Desktop base.

10. Testing Performance dari komponen Grid ZK untuk menampilkan > 20 kolom dan > 100 baris data untuk Inline Editing.

11. Mengunakan ZK [ListModelList](http://books.zkoss.org/zk-mvvm-book/7.0/data_binding/collection_and_selection.html){:target="_blank"} untuk meningkatkan performance Add, Update, Delete pada komponen Grid ZK.

### Screenshot Aplikasi

![Sceenshot-1](https://i.imgur.com/MugWsId.png)

![Sceenshot-2](https://i.imgur.com/iWapORg.png)

![Sceenshot-3](https://i.imgur.com/WJxe6N3.png)

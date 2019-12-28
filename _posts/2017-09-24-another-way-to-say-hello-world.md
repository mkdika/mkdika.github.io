---
layout      : post
title       : "Another Way to say ‘Hello World’ with Spring Boot"
date        : 2017-09-24 15:15:05 +0700
categories  : Spring
tags        : [java , spring]
comments    : true
---
![Imgur](https://i.imgur.com/c5oud26.jpg)

As conventional programmer, it always start with the famous one, the `hello world` Project :)

Recently I do research and learn about Spring Framework, particularly on its latest version (5.0.0M3) and Spring Boot. Except, you are experience user to this framework, this is another way to give a try, one of the simplest. Moreover, a little bit awesome, and less common.

### Preparation

- You need to have installed JDK 8.
- Download Spring Boot CLI:
- [spring-boot-cli-1.5.6.RELEASE-bin.zip](http://repo.spring.io/release/org/springframework/boot/spring-boot-cli/1.5.6.RELEASE/spring-boot-cli-1.5.6.RELEASE-bin.zip)

Extract/uncompress the Spring Boot CLI, from command line or terminal, go to its `bin` folder. Type `spring --version` , the feedback should be:

![Imgur](https://i.imgur.com/CkVEetB.png)

### Hello World Project

Now we want to create simple web service which is return `Hello World` . The conventional way to start the Spring Boot project is by create the project files through Spring Initializer. Instead of those, this approach is going to use the groovy script, it quite similar to Java, except less boilerplate code. Furthermore, these methods are usually used for quickly prototype with Spring.

Create a new file, name it `Hello.groovy` , here the script:

```java
@RestController
class Hello {
    @RequestMapping("/")
    String index() {
        "Hello World :)"
    }
}
```

To run the file, in command line/terminal type `spring run <the-file-location>` as shown below:

![Imgur](https://i.imgur.com/5a5iWCM.png)

Make sure you have a proper Internet connection. Because Spring need to download the related dependencies. After that give a try by access to `http://localhost:8080` from web browser.

![Imgur](https://i.imgur.com/33DTwq1.png)

Congratulations, you have done to say `Hello World` with Spring Boot.

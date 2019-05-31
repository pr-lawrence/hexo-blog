---
title: JDK8에서 기본 GC(Garbage Collector)
date: 2019-05-31 22:51:04
category: Java
thumbnail: https://bloggceasy.files.wordpress.com/2016/08/garbage-collection.png
tags:
  - jdk
  - gc
---

JDK 8에서 기본 GC가 무엇인지 궁금해서 구글링을 해봤는데 [스택오버플로우에서 이런 글을](http://stackoverflow.com/questions/33206313/default-garbage-collector-for-java-8) 찾았다

글의 내용을 요약하면 머신에 따라 의존적이라는 것이다.

*  서버 클래스 머신일 경우 Parallel Collector
*  클라이언트 클래스 머신일 경우 Serial Collector

2가지를 구분하는 것은 물리적 프로세서의 갯수와 메모리의 크기, 32bit 윈도우즈 플랫폼이냐 하는 것인데
최근에는 머신에 멀티 코어 프로세서가 대부분 탑재 되므로 JVM이 항상 parallel collector를 선택한다고 한다.
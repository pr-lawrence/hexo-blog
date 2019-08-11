---
title: 엘라스틱서치 소개
date: 2019-08-08 23:29:26
category:
thumbnail:
tags: elasticsearch
---

## 서문

엘라스틱서치(Elasticsearch)는 루씬 기반의 검색 엔진이다. HTTP 프로토콜을 사용하여 스키마에 종속되지 않고 JSON 문서를 처리할 수 있다.

루씬은 역색인 구조를 통하여 빠른 검색 결과를 제공하였고, 이를 기반으로 한 엘라스틱서치 또한 빠르게 생태계에 안착하며 광범위하게 사용되어지는 오픈소스가 되었다. 현재 가장 최신 버전은 7.x 버전이다.

또 다른 특징으로 작게는 단독 머신에서 많게는 수천개의 머신에서 활용될 수 있도록 고안되었고 또한 멀티테넌트를 지원한다. 멀티테넌트란 그 용어에서 유추할 수 있듯 여러 사용자(tenant, 사용자)를 가진 아키텍처란 의미이다.

## 엘라스틱서치 설치하기

엘라스틱서치를 설치하는 가장 간단한 방법은 패키지매니저를 사용하는 것이다. yum, dnf, zypper, apt-get, homebrew까지 지원한다. 또한 OS별로 빌드된 바이너리도 함께 제공되니 다운로드하여 설치하는 방법도 있고, 컨테이너 환경에서 사용할 수 있도록 도커 이미지도 제공하고 있다.

[이 페이지](https://www.elastic.co/kr/downloads/elasticsearch)에 접속해보면 설치와 관련된 더 자세한 내용을 살펴볼 수 있다.

## 엘라스틱서치 활용처

기본적으로 엘라스틱서치는 오픈소스 검색엔진이며, 더불어 데이터도 쉽게 저장할 수 있다. 데이터를 저장하고, 질의하는 이 간단한 기능을 확장하여 엘라스틱서치의 활용도는 그야말로 무궁무진하다고 할 수 있다.

1. NoSQL 데이터베이스

엘라스틱서치는 HTTP 프로토콜을 통해 데이터를 생성, 삭제, 수정할 수 있다. 이 기능을 통해 NoSQL 데이터베이스로 활용될 수 있다. 한 가지 주의해야 할 점은 데이터가 '실시간'이 아니라는 점이다. 데이터베이스의 트랜젝션과 같은 기능은 기대할 수 없으며, 내부적으로 데이터를 처리하는데 복잡한 과정을 거치기 때문에 대략 1초 정도 뒤에나 질의가 가능해진다.

2. APM 서비스

APM은 Application Performance Management의 약자로 애플리케이션의 성능을 관리하는 서비스를 말한다. APM 서비스는 프로덕션 환경을 안정적으로 운영하는데 꼭 필요한 도구이며, 엘라스틱서치를 이에 활용할 수 있다.

엘라스틱서치에 로그와 시스템 메트릭을 보관하고 이를 시각화 할 수 있는 도구인 Kibana를 활용하는 것이다.

더 자세한 내용은 [이 페이지](https://www.elastic.co/kr/products/apm)에서 확인할 수 있다.

3. 전문 검색 시스템

엘라스틱서치는 문서가 입력했을 때 특정 타입을 갖는 필드에 대해 분석을 실시하며, 이를 통해 문서를 쉽게 검색할 수 있도록 한다. 이를 역색인(inverted index)이라 하며, 책의 마지막 페이지에 있는 찾아보기 페이지와 유사한 데이터 구조를 생성하는 것이다. 이를 통해서 문서의 일부만으로도 해당 단어가 포함된 전문을 검색할 수 있다.

4.

## 참고 :

- [엘라스틱서치 Wikipedia page](https://ko.wikipedia.org/wiki/%EC%9D%BC%EB%9E%98%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98)
- [엘라스틱서치 공식 가이드 문서](https://www.elastic.co/guide/index.html)
- [IT 용어풀이 - 멀티테넌트](http://www.itworld.co.kr/news/101255)
- [elasticsearch*적용 및 활용*정리](https://www.slideshare.net/JunyiSong1/elasticsearch-45936425)
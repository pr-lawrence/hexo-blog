---
title: Github Pages에 custom domain 설정하기
date: 2019-01-21 20:41:53
category: Frontend
thumbnail: https://cdn-images-1.medium.com/max/1600/1*pv5LukDtyQx5JXQee2uNgA.jpeg
tags:
  - hexo
  - blog
  - github pages
---

https://upload.wikimedia.org/wikipedia/commons/thumb/9/91/Electron_Software_Framework_Logo.svg/256px-Electron_Software_Framework_Logo.svg.png

Github pages에서 custom 도메인을 설정하는 방법이다.

1. Github에서 custom domain 사용하도록 설정한다.
2. 프로젝트 최상단에 CNAME 파일이 생성된 것을 확인한다.
3. 도메인을 구입한 사이트에서 CNAME 관련 설정을 진행한다.

### Github에서 custom domain 사용 설정하기

Github pages용 저장소에 Settings 메뉴로 들어가면 아래와 같은 메뉴가 있다.

![github-settings](./github-settings.png)

메뉴 중 Custom domain 부분에 원하는 도메인을 적는다. 이렇게 하면 프로젝트 루트에 CNAME이라는 이름으로 파일이 생성된다.

CNAME은 도메인 이름에 별칭 이름을 매핑하는 DNS 레코드 유형이다. CNAME 레코드는 일반적으로 www 또는 mail과 같은 하위 도메인과 이 하위 도메인의 콘텐츠를 호스팅하는 도메인을 매핑하는 사용된다.

### 도메인을 구입한 사이트에서 도메인 레코드 설정하기

나는 도메인을 가비아에서 구매했으므로 가비아 기준으로 설정하는 방법을 설명한다. CNAME과 A 레코드에 대한 설정을 추가해야 한다.

A 레코드는 또는 주소 레코드(호스트 레코드라고도 함)는 도메인을 IP 주소와 연결한다.

https://dns.gabia.com 로 접속해서 변경이 필요한 도메인을 클릭하면 아래와 같은 화면을 볼 수 있다.

![gabia-dns-settings](./gabia-dns-settings.png)

위에 화면에서 보이는 것과 같이 설정을 진행하자. A 레코드에는 `@` 호스트에 192.30.252.153, 192.30.252.154를 설정한다. CNAME 레코드에는 `blog` 호스트에 소유하고 있는 도메인 + . 을 입력한다.

### 결론

github pages를 생성하고 나면 `*.github.io`로 끝나는 주소로 접근할 수 있지만 이 글에서 알아본 것 처럼 설정하면 `blog.*`로 시작하는 주소로 연결할 수 있다. `www`로 시작하거나, 도메인주소로만 접근하도록 설정하는 방법을 알고 싶다면 Github에서 제공하는 [이 문서](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)를 참고하자.

#### Reference

[Github Custom Domain](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)
[CNAME 레코드 정보](https://support.google.com/a/answer/112037?hl=ko)
[A 레코드 정보](https://support.google.com/a/answer/2576578?hl=ko)
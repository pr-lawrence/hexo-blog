---
title: Git 한글에서 영어로 바꾸기
date: 2020-01-04 23:55:01
category: [Git]
thumbnail: 2020-01-04-git-language/git.png
tags:
  - git
  - git-config
  - git-language-setting
---

MAC에서 brew 패키지매니저를 사용하여 Git을 설치하다가 특정 버전 이후에(아마도 2.19이상)는 git에 대한 명령줄에서 한글을 만날 수 있다.
원인은 brew에서 git을 설치할 때 `gettext`라는 라이브러리를 필수로 넣으면서 자동 번역이 되는 것이다.

다시 영어로 출력되게 하는 방법은 git을 삭제 했다가 설치 옵션을 바꿔 다시 설치해야 한다.

1. git 삭제

```
$ brew uninstall git
```

2. git 설치 옵션 변경

```
$ brew edit git

<<<
- depends_on "gettext"
+ depends_on "gettext" => :optional
<<<
- args = %W[
+ ENV["NO_GETTEXT"] = "1" if build.without? "gettext"
+
+ args = %W[
<<<
:wq

```

3. 재 설치

```
$ brew install -s git
```


## Reference

[Stackover flow - git-cli-in-russian-after-brew-upgrade](https://stackoverflow.com/questions/52426922/git-cli-in-russian-after-brew-upgrade/52592260#52592260)
[mac 에서 git 언어 변경되는 문제](https://kyubot.tistory.com/125)
[Clien - 맥의 터미널 git 언어가 한국어로 바뀌었네요? 어떻게 되돌리죠?](https://www.clien.net/service/board/cm_mac/12884754)
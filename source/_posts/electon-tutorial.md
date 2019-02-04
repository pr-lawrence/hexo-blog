---
title: electon-tutorial
date: 2019-02-04 22:24:55
tags: 
  - electron
---

![Electron-first-page](./electron-first-page.png)

### Electron 소개

HTML과 JAVASCRIPT, CSS에 익숙한 개발자라면 손쉽게 네이티브 애플리케이션을 개발할 수 있다. 처음 이런 내용을 접하는 사람이라면 의아해 할 것이다. Web 기반 기술로 네이티브 애플리케이션을 가능하게 하는 것은 바로 [Electron](https://electronjs.org/)이다.

Electon은 Github이 주도 해서 개발하고 있는 오픈소스로 2013년에 처음 릴리즈 되어 올해로 벌써 6년째 개발 및 유지보수가 진행 중이다.

Electron으로 개발된 유명한 앱은 Github의 Atom Editor, MS의 Visual Studio Code 를 비롯하여 Slack, Skype, Whats App 등이 있다. [이 페이지](https://electronjs.org/apps)에서 Electron으로 개발된 더 많은 앱을 확인할 수 있다.

Electron으로 개발하게 되면 Node.js의 백엔드와 Chromium 프론트엔드 기술을 사용하여 네이티브앱이 구동되도록 되어있다.

### Electron 설치하기

Electron은 총 3 종류로 릴리즈를 하고 있으며, 각각을 `latest`, `beta`, `nightly`라고 부른다. `latest`는 안정적인 가장 최신버전의 앱을 가리키며, `beta`는 곧 변경될 기능을 사용할 수 있는 버전이고, `nightly`는 실험적인 기능까지 사용할 수 있는 버전이다.

각각을 설치하는 방법은 아래와 같다.

```bash
$ npm i -D electron@latest
$ npm i -D electron@beta
$ npm i -D electron-nightly
```

Electron에 첫 페이지에 가면 아래와 같이 버전도 명시가 되어 있고, [Releases](https://electronjs.org/releases/stable) 페이지에 가면 각 버전별로 기능, 버그수정, 변경점 등을 함께 확인할 수도 있다.

![electron-release](./electron-release.png)

### Electron Demo App 살펴보기

Electron은 API 기능을 살펴볼 수 있는 Demo App을 제공하고 있다. 이를 살펴보면 Electron을 이해하는데 큰 도움을 받을 수 있다. 아래 명령어를 순서대로 실행하면 Demo App이 실행된다.

```bash
$ git clone https://github.com/electron/electron-api-demos
$ cd electron-api-demos
$ npm install
$ npm start
```

실행된 Demo App은 아래와 같은 형상이며, 좌측에 메뉴, 오른쪽에 해당 기능에 대한 설명이 코드와 함께 있으며, 몇몇 메뉴는 View Demo버튼으로 직접 실행되는 것도 확인할 수 있다.

![electron-demo-app](./electron-demo-app.png)

### 결론

이 포스팅에서는 Electron이 무엇인지 알아보고 Demo App을 통해 어떤 기능이 있는지 확인해보았다.
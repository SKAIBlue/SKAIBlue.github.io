---
layout: post
title: Meteor AWS에 배포하기[Deploying Meteor App to AWS]
description: >
  Meteor 웹 App을 (AWS)아마존 웹 서비스에 배포하는 방법을 알아본다.
tags: [web]
---

Meteor를 이용해서 웹 앱을 만들고 있었다. AWS를 통해 배포를 하려고 계획 중 이었는데, 이미지 업로드 기능 때문에 테스트를 위해 생각보다 빨리 AWS를 사용하게 되었다. AWS를 사용해 본 적이 없어서 배포를 위해 어떻게 설정해야 하는지 전혀 몰랐다. 그래서 AWS에 가입하고 로그인 한 단계 부터 AWS에 Meteor App을 배포하는 과정까지 모두 알아보았다. 관련 자료를 찾기 힘들기 때문에 이 포스트가 도움이 되었으면 좋겠다.

## AWS 인스턴스 생성
회원가입과 로그인 과정은 생략하고 Meteor App을 위한 EC2 인스턴스를 생성하는 과정부터 시작한다.

로그인을 하면 가장 먼저 아래 화면이 보일 것이다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/1.png "AWS Service list")

가장 먼저 해 줘야 할 일은 AWS 인스턴스의 서버 지역을 설정해 주는 것이다.
오른쪽 상단에서 자신의 사용자 이름의 오른쪽`빨간 박스`에 현재 설정된 지역 이름이 있다.
클릭 하면 설정 지역을 변경할 수 있으며, `서울에도 서버가 있다`. 물론 자신의 서버가 서비스 할 지역에 가까울 수록 좋기때문에 무조건 서울이 좋은것은 아니므로 자신의 상황에 맞게 지역 설정을 하도록 한다.

다음은 `파란색 박스` 안에 있는 EC2를 클릭한다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/2.png "AWS Resource group")

이전에 이미 생성한 인스턴스가 있다면 `빨간색 박스` 안의 인스턴스를 클릭해 이전에 생성해 두었던 인스턴스 목록을 볼 수 있다.<br>
생성한 인스턴스가 없다면 `파란색 박스` 안의 인스턴스 시작 버튼을 누러 인스턴스를 생성하는 페이지로 넘어간다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/3.png "AWS Image")

사용할 운영체제 이미지를 선택하는 화면이다. 우분투 16.04를 사용할 생각이므로 `우분투 16.04의 선택` 버튼을 눌러 다음으로 넘어간다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/4.png "AWS Select Instance type")

AWS의 성능을 결정하는 페이지이다. 나중에 변경할 수 있으므로 무료로 사용할 수 있는 기본값으로 그대로 놔두고 오른쪽 하단의 `다음: 인스턴스 세부정보 구성` 버튼을 누른다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/5.png "AWS Auto Scaling")

해당 페이지는 Auto Scaling을 설정하는 페이지이다. Auto Scaling은 동일한 인스턴스를 여러개 생성하여 어떤 인스턴스에 오류가 발생한 경우 자동으로 다른 인스턴스로 교체하는 기능으로 보인다. 아직 필요한 기능이 아니라 자세히 알아보지 않았으므로 나중에 알아본 후 설정을 변경하도록 한다. 역시 오른쪽 하단의 `다음: 스토리지 추가` 버튼을 누른다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/6.png "AWS Add Storage")

이 페이지는 저장소를 설정하는 페이지이다. 최대 30GB까지 무료로 쓸 수 있으므로 팍팍 활용하도록 한다. 기본값 8GB로 설정되어 있으니 30GB로 변경한 후 `다음: 테그 추가` 버튼을 누른다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/7.png "AWS IP Port settings")

보안 그룹을 설정하는 화면이다. 접속IP와 포트를 설정하여 허가되지 IP와 포트의 접속을 막는다. 웹 앱을 배포하기 위해 인스턴스를 생성하기 때문에 다음 세 가지 규칙을 추가한다.

> SSH:TCP:22:내IP

SSH 접속으로 원격 관리를 위해 필요하다. 또한 Meteor deploy 에 ssh를 사용한다.

> HTTP:TCP:80:위치 무관

> HTTPS:TCP:443:위치 무관

위 두 프로토콜은 당연히 웹 페이지 접속을 위해서 추가한다.

규칙 추가를 누른 후 유형만 변경하면 프로토콜과 포트 번호는 자동으로 설정된다.
유형 선택 후 소스만 변경하자. `검토 및 시작` 버튼을 누른다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/8.png "AWS examine")

설정이 잘못된것은 없는지 잘 확인 한 후 `시작` 버튼을 눌러 시작하자.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/9.png "AWS Keypair settings")

이전 단계에서 시작 버튼을 누르면 키페어 설정이 나온다. 역시 보안을 위해 아무나 SSH 접속을 못하도록 키를 가지고 있는 사용자만 SSH에 접속할 수 있도록 한다. 키페어가 없다면 `새 키페어 생성` 을 선택한 후 원하는 키페어 이름을 설정하여 `키페어 다운로드`를 누른다. 또는 생성해 둔 키페어가 있다면 기존에 가지고 있던 키페어를 사용할 수 도 있다.
다운받은 키페어는 안전한곳에 소중하게 보관해두자

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/10.png "AWS state Start")

인스턴스가 시작되는 동안 시간이 걸릴 수 있다.
`인스턴스 보기`를 클릭하여 인스턴스 목록 페이지로 이동한다.

![](https://skaiblue.github.io/assets/img/posts/meteor/awsdeploy/11.png "AWS Instance list")

인스턴스 상태가 running이면 사용 가능한 상태가 된 것이다. 아마존에서 인스턴스 생성 과정은 끝났다. 아래 설명에 `퍼블릭 DNS(IPv4)`와 `IPv4 퍼블릭 IP`는 나중에 필요하므로 기록해 두도록 한다.

## Meteor AWS 배포하기

### SSH 접속하기
사실 배포하는 과정에 자신의 인스턴스에 SSH로 접속할 필요는 없지만 필요한 사람을 위해 방법을 작성한다. `리눅스`와 `맥OS` 기준으로 접속하는 방법이다.

SSH 접속을 위해 가장 먼저 할 일은 다운받은 키페어의 권한 설정이다. 키페어가 있는 위치로 이동하여 다음 명령어를 사용해 권한을 변경한다.

```
chmod 400 키페어이름.pem
```
권한 변경후 다음 명령어로 접속할 수 있다.
```
ssh -i "키페어이름.pem" ubuntu@퍼블릭 DNS(IPv4)
```

처음 접속하면 뭔가 물어보는데 yes를 입력하면 성공적으로 접속된다.

### 배포하기
이 과정은 본인의 컴퓨터에서 실행 해야 하며, AWS에 접속해서 하는 과정이 아니다.

원격 서버에 배포하기 위해서는 시스템에 `mup`이라는 패키지를 설치해야 한다. 
콘솔을 이용해 다음 명령어로 mup 패키지를 설치할 수 있다.

```
meteor npm install mup -g
```

설치가 완료되면 다음은 배포할 미티어 프로젝트에 찾아가야 한다. `cd` 명령어를 이용해 미티어 프로젝트 폴더로 이동한다.

배포할 미티어 프로젝트 폴더로 이동했다면 mup을 초기화 해야 한다.
다음 명령어를 사용하면 `mup.json` 파일이 생성된다.
```
meteor mup init
```

생성된 mup.json 파일을 열어보면 다음과 같은 구조로 되어있다.
```js
module.exports = {
  servers: {
    one: {
      // TODO: set host address, username, and authentication method
      host: '<IPv4 퍼블릭 IP>',
      username: 'ubuntu',
      pem: '<다운받은 키페어 경로(ex /User/Anonymous/sign/keypair.pem)>'
      // password: 'server-password'
      // or neither for authenticate from ssh-agent
    }
  },

  app: {
    // TODO: change app name and path
    name: '<앱 이름>',
    path: '../<프로젝트 폴더 이름>',

    servers: {
      one: {},
    },

    buildOptions: {
      serverOnly: true,
    },

    env: {
      // TODO: Change to your app's url
      // If you are using ssl, it needs to start with https://
      ROOT_URL: '<퍼블릭 DNS(IPv4)>',
      MONGO_URL: 'mongodb://localhost/meteor',
    },

    // ssl: { // (optional)
    //   // Enables let's encrypt (optional)
    //   autogenerate: {
    //     email: 'email.address@domain.com',
    //     // comma separated list of domains
    //     domains: 'website.com,www.website.com'
    //   }
    // },

    docker: {
      // change to 'abernix/meteord:base' if your app is using Meteor 1.4 - 1.5
      image: 'abernix/meteord:node-8.4.0-base',
    },

    // Show progress bar while uploading bundle to server
    // You might need to disable it on CI servers
    enableUploadProgressBar: true
  },

  mongo: {
    version: '3.4.1',
    servers: {
      one: {}
    }
  }
};

```

변경해야 할 값은 아래 다섯 가지다.
- host: '`<IPv4 퍼블릭 IP>`'
- pem: '`<다운받은 키페어 경로(ex /User/Anonymous/sign/keypair.pem)>`'
- name: '`<앱 이름>`'
- path: '../`<프로젝트 폴더 이름>`'
- ROOT_URL: '`<퍼블릭 DNS(IPv4)>`'

위 값을 변경 후에 아래 명령어를 실행하면 AWS 서버에 배포하기 위한 설정을 한다
```
meteor mup setup
```
여러가지 설정과정이 끝나면 AWS에 배포할 준비가 끝난것이다.
다음 명령어를 실행하면 현재 프로젝트의 파일들을 AWS에 배포한다.

```
meteor mup deploy
```
배포 과정이 끝난 후 브라우저에 `퍼블릭 DNS(IPv4)`를 입력하고 접속하면 자신의 Meteor 앱이 정상적으로 배포된 것을 확인할 수 있을것이다.
---
layout: post
title: 3!2! 퓨전! 개발과 심사 후기
description: >
  3!2! 퓨전! 개발과 심사 후기
  Guideline 2.1때문에 바이너리가 거부되었다면 아래 나와있는 위반 항목에 대해서 설명하면 된다.
tags: [projects]
---

이번에 모바일 게임을 출시 한것은 두 번째이다.

첫 번째 게임을 출시 한 지는 2년이 조금 넘었다.

당시에 개발한 게임은 개발 비용이 약 50만원(앱스토어 개발자 계정, 구글, 각종 리소스 구매 비용)이 들어갔고, 수익 구조는 리워드를 주는 Unity Ads와 캐릭터를 구매하는 인앱 결제를 채용했다.

배너 광고가 게임의 미관을 상당히 헤친다고 생각하기 때문에 플레이어가 원할때만 광고를 실행하여 리워드를 주는 광고만 사용했었다.

홍보를 한건 커뮤니티에 게임을 개발했다고 글 쓴것과 구글에 광고 비용으로 5만원 쓴게 전부였는데, 결과는 수익이 0으로 완전 망했다.

그래서 이번에는 쓸 수 있는 돈이 많지 않기 때문에 망하더라도 리스크도 줄이기 위해서 저예산으로 게임을 만들고 싶어졌다. 

배경음악도 필요 없고, 복잡한 리소스를 사용하지 않으며, 빠르게 개발할 수 있는 게임.

그 게임이 3!2! 퓨전!이다.

인앱 결제가 없는 대신 광고는 Admob의 배너와 전면 광고를 사용했다.

광고가 게임 미관을 헤친다는 생각은 변함이 없지만 나도 먹고는 살아야 하기 때문에 타협해서 배너 광고를 넣었다.

생존>>>>>>>>>>>>>>>>게임미관

물론 게임을 플레이 할 때는 배너 광고가 숨겨지도록 구현했다.

이번에는 공식 페이스북이나 트위트 계정을 만들어서 홍보도 조금씩 해보려고 게임 내에 사이트 연결 버튼도 만들고, 설치 유도를 위해 점수를 공유하는 기능도 추가했다.

여러가지 고려하면서 틈틈히 개발해서 25일 정도 걸렸는데, 테스트 하다가 버그를 발견해서 이틀 정도 더 소모되었다 ㅠㅠ

심사를 위해 앱을 제출하고 하루 뒤에 심사 결과가 나왔는데 바이너리가 거부되어서 기겁했다 ㅠㅠ

첫 번째 게임은 한 방에 통과가 됐었는데, 심사가 거부된건 또 처음이라 어떻게 해야하는지 몰라서 당황스러웠다.

애플 심사팀에게서 받은 메세지는 아래와 같았다.

```
Guideline 2.1 - Information Needed


This type of app has been identified as one that may violate one or more of the following App Store Review Guidelines. Specifically, these types of apps often:

1.1.6 - Include false information, features, or misleading metadata
2.3.0 - Undergo significant concept changes after approval
2.3.1 - Have hidden or undocumented features, including hidden "switches" that redirect to a gambling or lottery website
3.1.1 - Use payment mechanisms other than in-app purchase to unlock features or functionality in the app
3.2.1 - Do not come from the financial institution performing the loan services
4.3.0 - Are a duplicate of another app or are conspicuously similar to another app
5.2.1 - Were not submitted by the legal entity that owns and is responsible for offering any services provided by the app
5.2.3 - Facilitate illegal file sharing or include the ability to save, convert, or download media from third party sources without explicit authorization from those sources
5.3.4 - Do not have the necessary licensing and permissions for all the locations where the app is used

Before we can continue with our review, please confirm that this app does not violate any of the above guidelines. You may reply to this message in Resolution Center or the App Review Information section in App Store Connect to verify this app’s compliance. 

Given the tendency for apps of this type to violate the aforementioned guidelines, this review will take additional time. If at any time we discover that this app is in violation of these guidelines, the app will be rejected and removed from the App Store, and it may result in the termination of your Apple Developer Program account.

Should you choose to resubmit this app without confirming this app’s compliance, the next submission of this app will still require a longer review time. Additionally, this app will not be eligible for an expedited review until we have received your confirmation.
```

[앱 심사 한글 가이드라인 링크](https://developer.apple.com/kr/app-store/review/guidelines/#accurate-metadata) 참고

항목을 살펴보니 도박이 어쩌고, 금융이 어쩌고, 외부 결제 시스템이 어쩌고 하는데 내가 제출한 게임은 문제될 내용이 없었다.

어떻게 해야하나 고민을 하다가 각 항목에 대해서 아래와 같이 작성해서 답변을 보냈다.

```
Thank you for your reply.

1.1.6 - My game does not provide these features or information.
2.3.0 - After receiving the results of the review, I added the name of the trade representative contact information. but this game is free and does not offer in-app purchases.
2.3.1 - My game has no hidden switches. Most switches are drawn large enough on the screen.
3.1.1 - This game does not offer in-app purchases.
3.2.1 - This app is game. There is no financial function.
4.3.0 - This game combines the rules of two games I played. If there are similar apps, please let me know which apps.
5.2.1 - The resources used in this game are purchased from the Unity Asset Store or i created.
5.2.3 - The only sharing feature supported in this game is score and link to download app.
5.3.4 - This is not a gambling game.

Please reply if you need more information.
```
요약하면 각 항목에 대해 **'내 게임은 어쩌구 저쩌구해서 이 항목을 위반하지 않았다.'** 를 작성해 보냈더니

![](https://skaiblue.github.io/assets/img/projects/1.png 'apple reply')

승인 메일이 왔다 ㅠㅠㅠㅠㅠ

앱 출시를 앞두고 있는 많은 개인 개발자분들 만약 나와 같은 이유로 앱 심사가 거부되었을때 도움이 되었으면 좋겠다.
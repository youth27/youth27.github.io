---
layout: post
title: 2019 네이버 테크콘서트 - iOS
tags: conference 네이버테크콘서트 iOS
categories: Story
---

> 7월 12일에 그린팩토리에서 진행하는 네이버 테크콘서트에 다녀왔습니다. 오랜만의 컨퍼런스이기도 했고, 주제가 너무 어렵지 않고 도움되는 주제라서 재미있었습니다. 같이 공부했던 동료들도 만날 수 있어서 더 좋았습니다.(거의 동창회 수준으로 아는 사람이 많았던...ㅋㅋㅋ) 그 유명한 그린팩토리 도서관도 들어가봤는데 좋더군요 ㅜ_ㅜ 네이버 임직원 & 정자 주민들 부럽습니다...

- [공식 영상 링크](https://tv.naver.com/v/9140435/list/486582)

## 1. 네이버지도 SDK-네이버 지도 밑그림을 그리는 SDK개발자가 하는 일
- [발표자료](https://www.slideshare.net/NaverEngineering/techcon-2019-mobile-ios1-sdk)
- 새롭게 출시한 네이버 지도2.0의 개선사항에 대한 전반적인 설명이었습니다. 개인적으로는 SDK개발자가 어떻게 일을 하는지 좀 더 구체적으로 알고싶었는데, 거의 홍보..? 성과보고에 가까운 발표여서 개인적으로 조금 아쉬웠습니다.
- 맵박스라는 오픈소스 라이브러리를 사용해서 개발했다는게 의외였음. (다 만들었을 줄 알아았는데..)
  - 포크 & 재개발 : 잘 되어있는 것을 제외한 수정이 필요한부분은 전부 수정했다고 함
- 오픈소스 라이브러리를 써서 협업이 더 용이했다.



## 2. 들숨에 협업 날숨에 클린코드
- [발표자료](https://www.slideshare.net/NaverEngineering/techcon-2019-mobile-ios2)
- 사내 컨벤션/협업/아키텍쳐/TDD에 관한 내용
- 다양한 관점을 가진 여럿이 모여서 일의 효율성을 높이기 위해서는 코드스타일을 통합할 필요가 있다. 다만 모든 룰을 적용할때는 합의를 바탕으로 하는 것이 필수이고, 공통의 룰로 판단하는 기준은 이 구문의 의도와 역할이 무엇인지에 초점
- SwiftLint라는 라이브러리가 있는데, 이를 통해서 띄어쓰기나 indent 등 개발자가 놓치기 쉬운 사소한 것들은 자동화하여 보정, 개발자는 비즈니스 로직에만 집중할 수 있도록 해줌
  - SwiftLint는 스위프트 개발자들이 가장 많이 쓰는 컨벤션 도구입니다. 제가 개인 프로젝트를 만들때 사용하는 라이브러리이기도 합니다. 처음에 적용했을땐 Swift컨벤션에 안맞으면 warning도 아니고 error가 떠서 빌드조차 할 수 없는데, 툴이 맞춰주는  규칙으로 차츰 개선해나가다보면 공식 컨벤션에 맞는 코드를 만들 수 있어서 좋았습니다. 특히 발표에서 설명한대로 indent나 공백 등에 신경쓰지 않고 로직에만 집중 할 수 있어서 좋았습니다.
  - [SwiftLint](https://github.com/realm/SwiftLint/blob/master/README_KR.md)

### MVC탈출기

- 코코아터치 프레임워크의 MVC는 사실 컨트롤러가 컨트롤러의 역할만 하기 힘든 구조입니다. iOS의 MVC 아키텍쳐의 가장 큰 단점으로는 Massive View Controller 이슈가 있는데, 이의 단점을 이야기하고 MVVM과 Rx를 접목해서 아키텍쳐를 변형한 후기를 들을 수 있어서 흥미로웠습니다.
- 코코아터치 프레임워크의 MVC는 사실 단점이 많다. 컨트롤러는 사실 뷰와 너무나 밀접하게 연관되어있다. 개발하다보면 순식간에 뷰의 모든 델리게이트를 선언해서 관리하고 네트워크 요청까지 보내게 되면서 점점 massive하게 변화하게된다. 단위테스트도 힘들어진다. 뷰의 라이프사이클까지 더해지면 완전... hell.
- MVVC을 채택 : 코코아 의존도를 최대한 줄이고 순수한 비즈니스 로직을 가져야한다는 목적으로 시작.
- 뷰모델 <-> 뷰와 느슨한 종속성 / 바인딩을 용이하게 해주는 Rx를 채택.
- View == 예쁜 껍데기 : layout(), attribute() 그리고 뷰모델과의 바인딩만 하는 것으로 역할 제한
- ViewBindable: 뷰에서 발생할 수 있는 이벤트를 핸들링할수잇도록 연결하는 역할
- ViewModel: 뷰의 액션이 일어났을때 어떻게 처리하는지 구현
- Model: 네트워크 등 연결, Business Logic만을 전담



## 3. 쉽고 재미있는 iOS디버깅 - LLDB Command
- [발표자료](https://www.slideshare.net/NaverEngineering/techcon-2019-mobile-ios3i-os-debug)
- LLDB는 Xcode툴에 내장되어있는 디버거입니다. 다양한 LLDB 명령어를 통해 쉽고 편리하게 디버깅하는 방법을 알 수 있었습니다.
- 지금도 개발할때 breakpoint와 LLDB명령어를 통해서 디버깅하곤했는데, 좀 더 효율적이고 다양하게 디버깅 할 수 있는 방법을 알게되어 앞으로 많이 응용할 것 같습니다. 한번에 커맨드를 외워서 사용하진 못하겠지만, 어떤 좋은 방법이 있는지도 몰라서 아예 찾아보지도 않고 사용도 못하는거랑 이런게 있대~ 쯤은 알고 필요할때 찾아서 쓸수 있는거랑 천지차이인 것 같아요. 이런 의미에서 저에게 굉장히 도움되는 세션 중에 하나였습니다!  (디버깅 커맨드가 필요할때 앞으로 계속 발표자료를 챙겨 볼 것 같네요...!)



## 4. ARKit, CoreML, Turi Create 삼형제
- [발표자료](https://www.slideshare.net/NaverEngineering/techcon-2019-mobile-ios42arkit-coreml-turi-create)
- CoreML프레임워크를 이용해서 미니 프로젝트 한 후기를 설명하면서 머신러닝 모델을 세팅할때 어떤 점을 주의해야하는지, 쉽고 가볍게 쓰기엔 어떤 툴을 사용했는지 설명하는 세션이었습니다. 지폐에 얼굴을 합성하면 재밌겠다는 아이디어로 시작되어 머신러닝 모델링에 시행착오를 겪은 이야기, 결국에 더 모델링에 효과적인 방법을 적용해서 성공했다는 이야기를 듣고 나니 어렵게만 느껴졌던 머신러닝이 좀 더 친숙(?)해지는 계기가 되었습니다!
- ARKit: 애플이 제공하는 증강현실 프레임워크
  - https://developer.apple.com/documentation/arkit
- Create ML: 머신러닝 모델 제공 프레임워크
  - https://developer.apple.com/documentation/createml
- Turi Create: 커스텀 머신러닝 모델을 간단하게 발달시킬 수 있게 하는 라이브러리
  - https://github.com/apple/turicreate




## 5. 사용자 경험을 높이는 애니메이션 만들기
- [발표자료](https://www.slideshare.net/NaverEngineering/techcon-2019-mobile-ios5-155527315)
- 애니메이션이 왜 필요할까? 부터 시작해서 애니메이션의 기능, 각 기능을 자연스럽 구현하기 위해서 어떤 메소드를 사용하면 좋을지 안내하는 세션이었습니다.
  - 형태는 기능을따른다(Louis H. Sullivan) - 디자인을 할때는 이게 어디에 쓰일것인지 미리 결정하고 그 이후에 형태와 용도에맞는 디자인과 애니메이션을 선택해야한다.
  - 애플의 HIG문서에 따르면 애니메이션은 컨텐츠를 이해하기 쉽게 만들기 위한 도구. 따라서 컨텐츠와 맥락을 잘 표현할 수 있도록 정제된 애니메이션을 넣는게 필요하다.
    - HIG: Human Interface Guideline
  - 애니메이션의 요소를 파악하면 쉽게 접근 할 수 있다.
    - 3 요소: 트리거/타겟/타임
    - 특정 이벤트(트리거)가 발생했을때 UI요소(타겟)를 시간에 따라(타임) 변화시키는 것
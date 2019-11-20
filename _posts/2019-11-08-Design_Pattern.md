---
title:  "[Design Pattern] MVP, MVC, and MVVM"
excerpt: "디자인 패턴 이해"

categories:
  - Design Pattern

last_modified_at: 2019-11-08T18:30:00
---

- 계층을 분리하여 코드의 재활용성을 높이고, 중복 제거
- 화면에 보여주는 로직과 실제 데이터 처리 로직 분리
- Model : Application에서 사용되는 Data 및 Data를 처리하는 부분
- View : 사용자에게 제공되는 UI (Ex. CSS/HTML/XML/XAML)
- Model - View 의존성 제어에 따라 패턴 분류


![Design Pattern types](/assets/images/posts/191108/design_pattern.png)

### MVC (Model - View - Controller)
- 입력은 controller에서 처리
- controller는 입력에 해당하는 model 업데이트 후 model을 나타낼 view 선택 
- 하나의 controller가 여러 view 선택하여 model 나타낼 수 있음 (n:n = controller:view)
- controller는 view를 지정만 해주고, view가 model을 이용해 업데이트
- model을 직접 사용 / model에서 view에게 notify / view에서 polling을 통해 model 변화 인지
- view - model 간의 의존성
- ex) 대부분의 웹 개발

### MVP (Model - View - Presenter)
- 입력은 view에서 처리
- presenter는 view, model의 인스턴스 소유 (1:1 = presenter:view)
- presenter는 view와 model 사이의 이벤트 처리 및 데이터 업데이트를 담당
- model과 view의 완벽한 분리(의존성 X)
- view - presenter 간의 의존성
- ex) 안드로이드 개발

### MVVM (Model - View - ViewModel)
- 입력은 view에서 처리
- view model은 view를 표현하기 위해 만든 view를 위한 model (1:n = view model:view)
- view로 들어온 action은 command 패턴으로 view model에 action 전달
- view model은 model에게 데이터 요청 후 model에게 응답 받고 데이터 가공하여 저장
- view는 view model과 data binding하여 화면에 표시
- view - model 의존성 X
- view - view model 의존성 X (command pattern, data binding)
- ex) WPF 

----
**ref :**  
[[WPF] MVC, MVP, MVVM 차이점](https://hackersstudy.tistory.com/71)  
[[디자인패턴] MVC, MVP, MVVM 비교](https://beomy.tistory.com/43)  
[MVC vs. MVP vs. MVVM](https://academy.realm.io/kr/posts/eric-maxwell-mvc-mvp-and-mvvm-on-android/)


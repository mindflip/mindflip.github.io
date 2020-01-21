---
title:  "[Andorid] Gradle"
excerpt: "안드로이드 Gradle 개념 및 특징"

categories:
  - Android

last_modified_at: 2019-08-28T18:30:00
---

## 새로운 빌드 시스템의 채택
- gradle은 빌드를 위한 도구

1. 빌드 스크립트가 'programming language'의 모습
- 자바와 같이 JVM 위에서 동작하는 groovy 라는 언어로 작성

2. 빌드 스크립트가 일률적이지 않음
- DSL(Domain Specific Language)라는 모습으로 server side gradle script와 android를 위한 script 모습이 전혀 다름

3. 다수의 빌드 지원 파일로 구성
- `settings.gradle` / `build.gradle`(project) / `builde.gradle`(module) / `gradle.properties` / `local.properties`

## 구글은 왜 그레이들을 채택했을까?
- 모듈화 개발 (modular development)
- one source multi APK
- 라이브러리 의존성 관리

### settings.gradle / build.gradle
- settings.gradle
  - 사용하는 모듈 추가 

- build.gradle (project)
  - 안드로이드 그레이들 플러그인 정보 설정
  - ex) `classpath 'com.android.tools.build:gradle:3.5.0'`
  - allprojects 설정

- build.gradle (app)
  - apply plugin
  - android
    - AndroidManifest.xml 재정의 목적 (우선순위 높음)
  - dependencies
    - 외부 라이브러리 관리


----
**ref :**  
[구글은 왜 그레이들을 채택했을까](https://brunch.co.kr/@yudong/67)
[구성요소로 바라본 그레이들](https://brunch.co.kr/@yudong/70)
[그레이들 의존성 관리](https://brunch.co.kr/@yudong/73)

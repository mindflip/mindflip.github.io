---
title: "[Javascript] Bundling, babel, polyfilling"
excerpt: "js를 배포하기 위해서 필요한 작업들"

categories:
  - Javascript

last_modified_at: 2021-12-27T14:00:00
---

### Bundling

- 여러 개의 파일 중, 종속성이 존재하는 파일을 하나의 파일로 묶어 패키징하는 과정
- 컴포넌트, helper 클래스 등 모듈화된 기능들을 하나의 파일로 번들링하여 웹을 빠르게 불러올 수 있도록 함
- 네트워킹 요청 횟수가 줄어들고, 중복된 소스코드 최적화 등의 효과

### Parcel (bundler)

- parcel을 이용해 간단하게 웹에서 사용되는 모든 자원(assets)을 번들링
- 설정이 필요 없는 zero-configuration 번들러
- 빠른 빌드 속도를 위한 캐싱 및 병렬 처리

### babel

- cross browsing을 해결하기 위해 필요한 js 컴파일러 (transcompiler)
- ES6 이상의 문법 코드들을 호환 안 되는 브라우저에서도 동작할 수 있도록 변환
- 구문 변환, polyfill, 소스코드 변환

### polyfilling

- ES5에 존재하지 않는 ES6의 Map, Promise 등의 문법을 번역하기 위해 필요
- babel-polyfill 모듈은 deprecated 됨
- core-js, regenerator-runtime 두 모듈을 이용하여 polyfill 가능
- core-js : ES5에 존재하지 않는 ES6 메서드, 생성자 등을 지원
- regenerator-runtime : runtime support for compiled.transpiled `async` functions

---

**ref :**  
[parcel](https://parceljs.org/){:target="\_blank"}  
[babel](https://babeljs.io/){:target="\_blank"}  
[core-js](https://github.com/zloirock/core-js/blob/master/README.md){:target="\_blank"}  
[regenerator-runtime](https://www.npmjs.com/package/regenerator-runtime){:target="\_blank"}

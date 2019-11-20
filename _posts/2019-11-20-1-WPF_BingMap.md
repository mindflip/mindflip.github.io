---
title:  "[C#] WPF - UI Design Bing Map"
excerpt: "Bing map 을 이용한 UI design"

categories:
  - C#

last_modified_at: 2019-11-20T18:30:00
---

![bingmap](/assets/images/posts/191120/bingmap.png)

### Required
1. Nuget Package - Material Design Themes [Click Here](https://www.nuget.org/packages/MaterialDesignThemes/3.0.0-ci778)
2. Bing Maps WPF Control SDK [Click Here](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=27165)
3. Bing Map Credentials [Click Here](https://www.bingmapsportal.com/)

----

- Nuget Solution을 이용해 `Material Design Themes` 패키지를 설치  
- `Bing Map WPF Control SDK` 를 위의 링크로 들어가 설치  
- 프로젝트 우클릭 Add -> Reference 클릭 후, SDK 설치한 폴더의 라이브러리에서 `Microsoft.Maps.MapControl.WPF.dll` 파일 선택
- Bing Map 사이트에 가입 후 Dev key 생성
- XAML를 이용해 UI 구성 후 Map `CredentialsProvide` 에 Key 입력


### [Source code (Click to github)](https://github.com/mindflip/WPF-UI-Bing-Map)

----
**ref :**  
[Bing Maps WPF Control](https://docs.microsoft.com/en-us/previous-versions/bing/wpf-control/hh750210(v=msdn.10))


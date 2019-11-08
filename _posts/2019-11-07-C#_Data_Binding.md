---
title:  "[C#] WPF - Data Binding"
excerpt: "데이터가 UI 에 바인딩 되는 방식의 이해"

categories:
  - C#

last_modified_at: 2019-11-07T18:30:00
---


![Data Binding](/assets/images/posts/191107/basic-data-binding-diagram.png)

- UI와 Data를 동기화시켜주는 기술
- 앱이 UI를 표현하고 Data와 상호작용하는 것을 단순화
- 컨트롤(Control)의 Property와 내가 지정한 객체의 Property를 연결 (Target ↔ Source)
- Bingding을 위해 BindingContext 속성이 반드시 소스객체를 참조
- XAML에서 Binding 마크업을 사용해 설정

----

![Data Binding](/assets/images/posts/191107/data-binding-updatesource-trigger.png)

- Binding 마크업은 Path, Mode 속성이 있음
- Path : 바인딩하고자 하는 원본객체의 속성명
- Mode : 속성 값의 변화가 영향을 줄 방향
  - `OneWay` 소스에서 타깃으로만 변경사항이 반영 (Default)
  - `TwoWay` 양방향으로 적용. 소스와 타깃객체가 항상 동기화
  - `OnwWayToSource` 타깃에서 소스로만 변경사항이 반영. 주로, 읽기전용의 바인딩 속성에 사용.
  - `OneTime` 생성자에서 초기화될 때, 한 번만 소스에서 타깃으로 반영
- PropertyChanged를 이용해 속성 변경에 이벤트 발생

----
### 코드 예제

```html
<StackPanel>
    <!-- Textbox is the target-->
    <TextBox Name="MyTextBox" Width="100" Margin="50" Text="{Binding ElementName=MySlider, Path=Value, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"></TextBox>
    <!-- Slider is binding source-->
    <Slider IsSnapToTickEnabled="True" Name="MySlider" Minimum="0" Maximum="100"></Slider>
</StackPanel>
```

- 텍스트와 슬라이드 동기화
- UpdateSourceTrigger 속성을 이용해 값 변경에 이벤트 발생

----
**ref :**  
[Data binding overview in WPF](https://docs.microsoft.com/en-us/dotnet/desktop-wpf/data/data-binding-overview)  
[Xamarin.Forms 데이터 바인딩 1/3](http://chanlee.github.io/2016/10/27/introduction-to-data-binding/)


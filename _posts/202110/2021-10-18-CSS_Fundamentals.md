---
title: "[CSS] Fundamentals"
excerpt: "Class, Selector, Box, Postioning 등 css 기초 정리"

categories:
  - CSS

last_modified_at: 2021-10-18T22:00:00
---

### Class and ID Selectors

```css
/* Class selector */
.related-author {
  font-size: 18px;
}

/* ID selector */
#copyright {
  font-size: 16px;
}

/* 
Class : use for gving multiple elemnts the same name
ID : for only used once

실제로는 ID는 사용하지 않음
Class를 사용함으로써 미래를 대비할 수 있음
*/
```

### Colors

- 기본적으로 RGB 모델을 사용 (0 ~ 255)
- RGB / RGBA notation
  - `rgb(0, 255, 255)`
  - `rgba(0, 255, 255, 0.3)`
- Hexadecimal notation
  - `#00ffff` (0 to ff)
  - `#0ff` (shorthand)
- Shades of GREY
  - When colors in all 3 channels are the same, we get a grey color
  - `rgb(0, 0, 0)` `#000000` `#000`
  - `rgb(69, 69, 69)` `#444444` `#444`
  - `rgb(255, 255, 255)` `#ffffff` `#fff`

### Pseudo-classes / Pseudo-elements

- Pseudo-class : 특정 상태의 요소를 선택하는 selector
  - first-child, hover 등
  - `article p:first-child {}`
- Pseudo-element : markup에 새로운 HTML을 추가한 것처럼 동작
  - first-line, before, after
  - `article p::first-line {}`

### Conflicts between selectors

- Highest priority to Lowest priority

```
- Declarations marked `!important`
- Inline style (style attribute in HTML)
- ID (#) selector
- Class (.) or pseudo-class (:) selector
- Element selector (p, div, li, etc.)
- Universal selector (\*)
```

### Inheritance

- Parent element의 proprties가 child element에도 적용
- 주로 text와 관련된 prop만 상속

### CSS box model

- Content, Border, Padding, Margin, Fill area
- Final element width = left border + legt padding + width + right padding + right border
- Final element hight = top border + top padding + height + bottom padding + bottom border

### Type of boxes

- Block-level elements
  - formatted visually as blocks
  - 100% of parent element's width
  - stacked vertically
  - applies as showed earlier
  - css: `display : inline`
- Inline elements
  - necessary for its content
  - no line-breaks
  - height, width do not apply
  - padding, margin are applied only hotizontally
- Inline-Block boxes
  - 외부는 inline, 내부는 block처럼 적용
  - css: `display: inline-block`

### Absolute positioning

- out of flow
- element들이 overlap 될 수 있음
- relatively positioned container에서 top, bottom, left, right offset 적용
- css: `position: absolute`
- container가 relative인 상태에서 elemet에 absolute 적용해서 offset 적용

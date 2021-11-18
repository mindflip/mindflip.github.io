---
title: "[OOP] Polymorphism 다형성"
excerpt: "객체지향프로그래밍 - 다형성"

categories:
  - OOP

last_modified_at: 2021-11-18T12:30:00
---

### 다형성 (Polymorphism)

- 부모 클래스에서 선언된 `가상 함수(virtual functions)`가 자식 클래스에서 다른 기능으로 `오버라이드(Override)`되어 런타임에 부모나 형제들과 다른 기능을 보이는 현상

```cpp
class Figure {
  public:
    virtual string draw() = 0;
};

class Triangle : public Figure {
  public:
    string draw() { return "Draw Triangle"; }
};

class Square : public Figure {
  public:
    string draw() { return "Draw Square"; }
};

int main() {
  Figure* F1 = new Triangle;
  Figure* F2 = new Square;

  cout << F1->draw() << "\n";
  cout << F2->draw() << "\n";

  /*
  출력 :
  Draw Triangle
  Draw Square
  */

  return 0;
}

```

---

**ref :**  
[다형성의 기본 개념](https://ansohxxn.github.io/cpp/chapter12-1/){:target="\_blank"}  
[C++ 프로그래밍, 다형성](https://micropilot.tistory.com/3072){:target="\_blank"}  
[상속과 다형성](https://pacs.tistory.com/entry/C-%EC%83%81%EC%86%8D%EA%B3%BC-%EB%8B%A4%ED%98%95%EC%84%B1-Inheritance-Polymorphism){:target="\_blank"}

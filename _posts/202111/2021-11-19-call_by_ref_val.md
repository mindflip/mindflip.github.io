---
title: "[C++] Call by value, Call by reference"
excerpt: "함수 호출 형태의 차이"

categories:
  - C++

last_modified_at: 2021-11-19T09:30:00
---

### Call by value

- 값에 의한 호출
- 함수 인자로 넘기는 값을 복사해서 새로운 함수에 전달
- 값을 인자로 전달하는 함수 호출 방식

```cpp
void swap(int a, int b) {
  int temp = a;
  a = b;
  b = temp;
}

int main() {
  int num1 = 1;
  int num2 = 2;

  cout << num1 << " ";
  cout << num2 << "\n";

  swap(num1, num2);

  cout << num1 << " ";
  cout << num2 << "\n";

  /*
  출력 :
  1 2
  1 2
  */

  return 0;
}
```

### Call by reference

- 참조에 의한 호출
- 주소 값을 인자로 전달하는 함수 호출

```cpp
void swap(int *a, int *b) {
  int temp = *a;
  *a = *b;
  *b = temp;
}

int main() {
  int num1 = 1;
  int num2 = 2;

  cout << num1 << " ";
  cout << num2 << "\n";

  swap(num1, num2);

  cout << num1 << " ";
  cout << num2 << "\n";

  /*
  출력 :
  1 2
  2 1
  */

  return 0;
}
```

### 참조자를 이용한 Call by reference

- C++에서는 함수 외부에 선언된 변수에 접근하는 방식이 두 가지
- 주소 값을 이용한 Call-by-reference (Call-by-address)
- 참조자를 이용한 Call-by-reference
- 참조자는 같은 데이터 공간을 가리키는 변수지만 이름만 다름
- 선언되는 변수 앞에 `&`가 붙으면 참조자

```cpp
void swap(int &a, int &b) {
  int temp = a;
  a = b;
  b = temp;
}
```

---

**ref :**  
[call-by-value, call-by-ref](https://musket-ade.tistory.com/entry/C-Call-by-Value-Call-by-reference){:target="\_blank"}

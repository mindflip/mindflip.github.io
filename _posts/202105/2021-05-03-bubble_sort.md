---
title:  "[Algorithm] Bubble Sort"
excerpt: "버블 소트"

categories:
  - Algorithm
  - Sort

last_modified_at: 2021-05-03T18:30:00
---

- 인접한 두 원소의 대소를 비교
- 조건에 맞지 않다면 자리를 교환하며 정렬
- 원소의 이동이 거품이 수면 위로 올라오는 듯한 모습


### Implementation

```cpp
for (int i = 0; i < SIZE; ++i) {
    for (int j = 1; j < SIZE - i; ++j) {
        if (arr[j - 1] > arr[j]) {
            int temp = arr[j];
            arr[j] = arr[j - 1];
            arr[j - 1] = temp;
        }
    }
}
```

- Time Complexity : O(n^2)
- Space Complexity : O(n)
- Execution Time (sec) : 1.908 (원소 30000개 기준)

### 장점
- 구현이 매우 간단하고, 소스코드가 직관적이다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않다. => 제자리 정렬(in-place sorting)
- 안정 정렬(Stable Sort) 이다.

### 단점
- 시간복잡도가 최악, 최선, 평균 모두 O(n^2)으로, 굉장히 비효율적이다.
- 정렬 돼있지 않은 원소가 정렬 됐을때의 자리로 가기 위해서, 교환 연산(swap)이 많이 일어나게 된다.


### [C++ 코드](https://github.com/mindflip/algorithm/blob/main/sort/00_bubbleSort.cpp)

----
**ref :**  
[버블정렬참고1](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)  
[버블정렬참고2](https://gyoogle.dev/blog/algorithm/Bubble%20Sort.html)


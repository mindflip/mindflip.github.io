---
title:  "[Algorithm] Insertion Sort"
excerpt: "삽입 정렬"

categories:
  - Algorithm
  - Sort

last_modified_at: 2021-05-04T18:40:00
---

- 2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정
- 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입 하여 정렬
- 모두 정렬이 되어있는 경우(Optimal)한 경우, 한번씩 밖에 비교를 안하므로 O(n) 의 시간복잡도
- 이미 정렬되어 있는 배열에 자료를 하나씩 삽입/제거하는 경우에는, 현실적으로 최고의 정렬 알고리즘

### Implementation

```cpp
for (int i = 1; i < SIZE; ++i) {
    int temp = arr[i];
    int prev = i - 1;
    while (prev >= 0 && arr[prev] > temp) {
        arr[prev + 1] = arr[prev];
        prev--;
    }
    arr[prev + 1] = temp;
}
```

- Time Complexity : O(n^2)
- Space Complexity : O(n)
- Execution Time (sec) : 0.428 (원소 30000개 기준)


### 장점
- 알고리즘이 단순하다.
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. => 제자리 정렬(in-place sorting)
- 안정 정렬(Stable Sort) 이다.
- Selection Sort나 Bubble Sort과 같은 O(n^2) 알고리즘에 비교하여 상대적으로 빠르다.


### 단점
- 평균과 최악의 시간복잡도가 O(n^2)으로 비효율적이다.
- Bubble Sort와 Selection Sort와 마찬가지로, 배열의 길이가 길어질수록 비효율적이다.


### [C++ 코드](https://github.com/mindflip/algorithm/blob/main/sort/02_insertionSort.cpp)

----
**ref :**  
[삽입정렬](https://gyoogle.dev/blog/algorithm/Insertion%20Sort.html)  


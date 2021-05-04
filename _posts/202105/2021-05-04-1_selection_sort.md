---
title:  "[Algorithm] Selection Sort"
excerpt: "선택 정렬"

categories:
  - Algorithm
  - Sort

last_modified_at: 2021-05-04T18:30:00
---

- 위치 먼저 선정
- 해당위치에 원소들간의 대소비교를 통한 적절한 값 선택


### Implementation

```cpp
int idxMin, temp;
for (int i = 0; i < SIZE - 1; ++i) {
    idxMin = i;
    for (int j = i + 1; j < SIZE; ++j) {
        if (arr[j] < arr[idxMin]) {
            idxMin = j;
        }
    }

    temp = arr[idxMin];
    arr[idxMin] = arr[i];
    arr[i] = temp;
}
```

- Time Complexity : O(n^2)
- Space Complexity : O(n)
- Execution Time (sec) : 0.917 (원소 30000개 기준)


### 장점
- Bubble sort와 마찬가지로 알고리즘이 단순하다.
- 정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적이다.
- Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. => 제자리 정렬(in-place sorting)


### 단점
- 시간복잡도가 O(n^2)으로, 비효율적이다.
- 불안정 정렬(Unstable Sort) 이다.


### [C++ 코드](https://github.com/mindflip/algorithm/blob/main/sort/01_selectionSort.cpp)

----
**ref :**  
[선택정렬](https://gyoogle.dev/blog/algorithm/Selection%20Sort.html)  


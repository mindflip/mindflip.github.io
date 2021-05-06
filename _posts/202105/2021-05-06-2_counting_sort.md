---
title:  "[Algorithm] Counting Sort"
excerpt: "계수 정렬"

categories:
  - Algorithm
  - Sort

last_modified_at: 2021-05-06T19:00:00
---

- counting 배열을 생성
- 정렬하고자 하는 배열을 순회하여 couting 배열의 해당하는 index에 1씩 증가
- counting 배열 순회하며 0이 아닌 index를 counting 수만큼 출력


### Implementation

```cpp
for (int i = 0; i < SIZE; ++i) {
    countingArr[arr[i]]++;
}

int arrSize = 0;
for (int i = 1; i < SIZE + 1; ++i) {
    if (countingArr[i] == 0) continue;
    int cnt = countingArr[i];
    while (cnt--) {
        arr[arrSize++] = i;
    }
}
```

- Time Complexity : O(n)



### [C++ 코드](https://github.com/mindflip/algorithm/blob/main/sort/06_countingSort.cpp)

----
**ref :**  
[계수정렬](https://gyoogle.dev/blog/algorithm/Counting%20Sort.html)  


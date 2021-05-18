---
title:  "[Algorithm] Binary search"
excerpt: "이분 탐색"

categories:
  - Algorithm

last_modified_at: 2021-05-18T19:00:00
---

- 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 알고리즘
- Time Complexity : O(logN)


### Operation
- 리스트를 오름차순으로 정렬
- left, right로 mid 값 설정
- mid와 구하고자 하는 target 값 비교
- mid 값이 target 값보다 크면, 왼쪽 구간만 다시 탐색
- mid 값이 target 값보다 작으면, 오른쪽 구간만 다시 탐색


### Implementation

- Iterative Version

```cpp
int binary_search(int* arr, int length, int value) {

    if (arr == nullptr || length < 0)
        return -1;

    int left = 0;
    int right = length - 1;
    int mid;

    while(left <= right) {
        mid = left + (right - left) / 2;

        if(arr[mid] == value) {
            return mid;
        } else if (arr[mid] < value) {
            left = mid + 1;
        } else if (arr[mid] > value) {
            right = mid - 1;
        }
    }

    return -1;
}
```

- Reculsive Version

```cpp
int binary_search(int* arr, int value, int left, int right) {

    if(left > right) {
        return -1;
    }

    int mid = left + (right - left) / 2;

    if (arr[mid] == value)
        return mid;
    else if (arr[mid] > value) {
        binary_search_reculsive(arr, value, left, mid - 1);
    } else {
        binary_search_reculsive(arr, value, mid + 1, right);
    }

}
```

----
**ref :**  
[C++ 이진 탐색(Binary Search) 구현 및 흔히 발생하는 오류](https://blog.weirdx.io/post/3121)  


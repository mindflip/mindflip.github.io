---
title:  "[Algorithm] Heap Sort"
excerpt: "힙 정렬"

categories:
  - Algorithm
  - Sort

last_modified_at: 2021-05-06T18:30:00
---

- 완전 이진 트리를 기본으로 하는 힙(Heap) 자료구조를 기반으로한 정렬 방식
- 완전 이진 트리 : 삽입할 때 왼쪽부터 차례대로 추가하는 이진 트리
- 정렬 과정
  - 최대 힙을 구성
  - 현재 힙 루트는 가장 큰 값이 존재함. 루트의 값을 마지막 요소와 바꾼 후, 힙의 사이즈 하나 줄임
  - 힙의 사이즈가 1보다 크면 위 과정 반복


### Implementation

```cpp
void heapify(int* arr, int n, int i) {
	int p = i;
	int l = i * 2 + 1;
	int r = i * 2 + 2;

	if (l < n && arr[p] < arr[l]) {
		p = l;
	}

	if (r < n && arr[p] < arr[r]) {
		p = r;
	}

	if (i != p) {
		int temp = arr[p];
		arr[p] = arr[i];
		arr[i] = temp;
		heapify(arr, n, p);
	}

}

void heapSort(int* arr) {
	int n = SIZE;

	// max heap 초기화
	for (int i = n / 2 - 1; i >= 0; --i) {
		heapify(arr, n, i);
	}

	// 최대값 추출, root에서 맨 뒤에 넣고 다시 heap 생성
	for (int i = n - 1; i > 0; --i) {
		int temp = arr[0];
		arr[0] = arr[i];
		arr[i] = temp;
		heapify(arr, i, 0);
	}
}
```

- Time Complexity : O(nlogn)
- Execution Time (sec) : 0.014 (원소 30000개 기준)



### [C++ 코드](https://github.com/mindflip/algorithm/blob/main/sort/05_heapSort.cpp)

----
**ref :**  
[힙정렬](https://gyoogle.dev/blog/algorithm/Heap%20Sort.html)  


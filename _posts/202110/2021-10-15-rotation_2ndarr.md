---
title: "[Algorithm] 2차원 배열의 회전"
excerpt: "90도, 180도, 270도 회전"

categories:
  - Algorithm

last_modified_at: 2021-10-15T16:00:00
---

- 알고리즘 문제에서 구현을 할 때 가끔 배열을 회전해야하는 경우가 있다.
- 간단하게 코드로 정리하고 원리를 이해해보자.

### rotation implementation

```cpp
// 시계방향 90도 회전
int board[n][n];

int rotate(){
    int temp[n][n];
    for (int i = 0; i < n; ++i){
        for (int j = 0; j < n; ++j) {
            temp[j][n - 1 - i] = board[i][j];
        }
    }
}

/*
// 시계방향 기준
temp[j][n - 1 - i] = board[i][j];   // 90도
temp[n - 1 - i][n - 1 - j] = board[i][j];   // 180도
temp[n - 1 - j][i] = board[i][j];   // 270도
temp[n - 1 - i][j] = board[i][j];   // 상하 반전
temp[i][n - 1 - j] = board[i][j];   // 좌우 반전
*/
```

- 90도만 알아도 된다. (180, 270도는 2번, 3번 씩 회전해주면 된다)
- 회전 후 행 == 회전 전 열
- 회전 후 열 == n - 1 - 회전 전 행

---

**ref :**  
[2차원 배열 회전](https://shoark7.github.io/programming/algorithm/rotate-2d-array)

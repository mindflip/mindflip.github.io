---
title:  "[Git] merge vs. rebase"
excerpt: "merge와 rebase의 특징과 차이점"

categories:
  - Git

last_modified_at: 2021-01-28T18:00:00
---

- 두 브랜치를 합칠 때 사용하는 merge, rebase
- 각각은 어떤 특징을 갖고, 어떤 상황에서 쓰이는 게 좋을까?

### Merge
- branch를 병합
- master, sub branch가 있을 때, master에서 sub branch를 병합
  - (master) git merge sub
- sub 브랜치는 유지되고 master에 새로운 커밋해시가 생기면서 병합
- 변경 부분이 겹칠 경우 conflict 날 수 있음 (수정 후 다시 커밋)

### Rebase
- Base를 재정렬
- Base : branch를 생성할 때, 기준이 되는 커밋 이력
- master, sub branch가 있을 때, sub에서 master를 rebase
  - (sub) git rebase master
- 기존 base에서 master branch의 모든 커밋 이력을 base로 재정렬 후, 이전 base 이후의 커밋 이력를 이어줌
- 이후 master에서 fast-forward merge 가 가능해짐
- master에서 sub를 rebase **안 하는 게 좋음**
  - master의 커밋 이력이 변하여 새로운 해시id가 부여됨

### 결론
- 여러 개발자들이 같은 브랜치를 공유할 때, Pull & Rebase 가 히스토리를 깔끔하게 유지하는데 유리
- 완료된 기능 브랜치를 다시 합칠 때는 Merge를 사용
- 기능 브랜치에 부모 브랜치의 변경 내용을 반영하고 싶을 때
  - **Rebase가 유리한 경우**
  - 이 브랜치를 다른 곳에 푸시한 적 없는 경우
  - (Mercurial 이 아닌) Git을 사용하고 다른 사람이 이 기능브랜치를 체크아웃할 일이 없을 것이라 확신하는 경우
  - **이 외의 상황에는 머지가 유리**

----
**ref :**  
[Merge vs Rebase 차이](https://dongminyoon.tistory.com/9)  
[Git Merging 과 Rebase 의 상황별 사용법](https://elegantcoder.com/git-merge-or-rebase/)  

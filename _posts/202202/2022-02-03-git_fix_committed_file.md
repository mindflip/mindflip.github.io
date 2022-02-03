---
title: "[Git] 과거의 커밋 파일 수정하기"
excerpt: "이미 예전에 커밋한 파일을 수정해야할 때"

categories:
  - Git

last_modified_at: 2021-02-03T16:00:00
---

- 개발 중 테스트를 위해 임시로 API키를 바로 소스코드에 삽입하고는 commit을 해버렸다
- 근데 commit이 몇 개 더 쌓이고 알아채버린 것
- 지금 수정해봤자 커밋으로 기록이 남기 떄문에, 그 커밋 자체를 수정해야하는 상황
- `git rebase --interactive` 와 `git --amend` 를 이용해서 해결할 수 있다

### sloution

- git log를 통해 수정할 커밋의 이전 커밋을 target으로 지정
  - `git rebase --interactive [commit hash]`
- target을 기준으로 이후의 커밋에 대한 수정 여부를 정할 수 있음
  - 수정하고 싶은 커밋 앞에 `pick` 을 `edit` 으로 수정
- rebase가 시작되면 필요한 부분을 수정
  - 수정 후 add 하여 staging
  - staging 된 상태에서 `git --amend`를 통해 기존의 커밋에 수정된 파일을 추가
- `git rebase --continue`를 통해 수정 마무리

### issue

- 원격 저장소에 이미 푸쉬된 상태라면, `-f` 옵션을 이용해서 덮을 수 있음
- 하지만 이런 방식은 협업하는 프로젝트라면 권장하지 않는 방향

---

**ref :**  
[Git 과거의 특정 커밋 수정하기](https://homoefficio.github.io/2017/04/16/Git-%EA%B3%BC%EA%B1%B0%EC%9D%98-%ED%8A%B9%EC%A0%95-%EC%BB%A4%EB%B0%8B-%EC%88%98%EC%A0%95%ED%95%98%EA%B8%B0/){:target="\_blank"}  
[git rebase활용해서 이전 commit 내용 수정](https://mizzo-dev.tistory.com/entry/git-commit-edit){:target="\_blank"}

---
title: "[Git] 커밋된 파일 .gitignore 적용"
excerpt: "git rm --cached ."

categories:
  - Git

last_modified_at: 2021-01-12T00:10:00
---

- `.gitignore`을 이용하여 커밋에 제외하고 싶은 파일을 정할 수 있음
- 하지만 깜빡하고 이미 커밋 후 제외하고픈 파일이 생길 수 있다

### --cached keyword

- Use this option to unstage and remove paths only from the index.
- Working tree files, whether modified or not, will be left alone.

```s
$ git rm -r --cached .
$ git add .
$ git commit -m "Apply .gitignore"
$ git push
```

- 캐시를 지우고 `.gitignore` 적용

---

**ref :**  
[수정하고 저장소에 저장하기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0){:target="\_blank"}

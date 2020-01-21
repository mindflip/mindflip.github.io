---
title:  "[Unity] Coroutine"
excerpt: "Coroutine 의미와 사용법"

categories:
  - Unity

last_modified_at: 2020-01-17T19:20:00
---

- Unity는 single thread만 지원하면서, multi thread 흉내를 내고 싶었음 (multi thread에서 신경써야할 다양한 문제 배제)
- Coroutine 함수가 IEnumerator를 반환하는 방식으로 구현
- yield return 사용, 그 위치를 기억하고, 값 반환 후 다음 작업 실행
- update 함수는 1 frame에 한 번 호출, yield로 진입점을 다양하게 하여 순차적으로 프로세스 처리

### Example
```c#
void Fade() 
{
    for (float ft = 1f; ft >= 0; ft -= 0.1f) 
    {
        Color c = renderer.material.color;
        c.a = ft;
        renderer.material.color = c;
    }
}
```
- 점차 색이 바래는 효과를 위한 함수이지만, 한 프레임에 모두 작업이 완료
- 이런 종류의 작업에 coroutine 사용

```c#
void Update()
{
    if (Input.GetKeyDown("f")) 
    {
        StartCoroutine("Fade");
    }
}

IEnumerator Fade() 
{
    for (float ft = 1f; ft >= 0; ft -= 0.1f) 
    {
        Color c = renderer.material.color;
        c.a = ft;
        renderer.material.color = c;
        yield return new WaitForSeconds(.1f);
    }
}
```
- 기본적으로 coroutine은 프레임 생성 후 다시 시작
- WaitForSeconds를 사용해 시간 지연 도입



----
**ref**  
[Coroutine(Unity Doc)](https://docs.unity3d.com/kr/2019.3/Manual/Coroutines.html)  
[코루틴의 이해](https://teddy.tistory.com/22)  
[Coroutine(코루틴)과 Update](https://m.blog.naver.com/PostView.nhn?blogId=hana100494&logNo=221626194462&proxyReferer=https%3A%2F%2Fwww.google.com%2F)

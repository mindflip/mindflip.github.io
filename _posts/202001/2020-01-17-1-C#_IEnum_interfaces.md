---
title:  "[C#] IEnumerable & IEnumerator"
excerpt: "두 열거형 반복 인터페이스의 이해 및 비교"

categories:
  - C#

last_modified_at: 2020-01-17T18:30:00
---

- 컬렉션에서 foreach를 이용해 단순하게 반복할 수 있는 이유는 IEnumerable/IEnumerator 인터페이스를 상속했기 때문

### IEnumerable
- 컬렉션을 단순하게 반복할 수 있도록 지원하는 열거자를 노출
- method : GetEnumerator() (IEnumerator 타입)
- 객체의 형식을 규정하여 IEnumerator 구현

### IEnumerator
- 컬렉션을 단순하게 반복할 수 있도록 지원
- prop : Current
- method : MoveNext(), Reset()
- 객체의 인덱스에 해당하는 요소 반환, 인덱스를 넘기는 메소드 구현

```c#
/*********** IEnumerable ***********/
//create IEnumerable of string 
IEnumerable<string> iEnumerableOfString = (IEnumerable<string>)Month;  
  
//If we want to retrieve all the items from this IEnumerable object, we can use a foreach loop. 
foreach(string AllMonths in iEnumerableOfString)
{  
   Console.WriteLine(AllMonths);  
} 

/*********** IEnumerator ***********/
//Create IEnumerator of string.
IEnumerator<string> iEnumeratorOfString = Month.GetEnumerator(); //to convert list into IEnumerator we can invoke the GetEnumerator method  
  
//To retrieve all the items from the above IEnumerator object, we cannot use foreach loop instead of that we need to invoke MoveNext() Boolean method.  
while(iEnumeratorOfString.MoveNext())
{
    Console.WriteLine(iEnumeratorOfString.Current); 
} 
```

- 컬렉션을 통해 연속적으로 반복문을 동작하고 싶을 때 IEnumerable 사용
- 현재 커서 위치와 데이터를 이용해야할 때는 ㄴIEnumerator 사용

----

### yield return/break
- `yield`는호출자에게 컬렉션 데이터를 하나씩 리턴
- return은 데이터를 하나씩 리턴할 때, break는 반복에서 벗어날 때 사용
- yield return 위치 기억하고, 처리 후에, 이후의 작업 진행

```c#
while(true)
{
    _start++;
    if (max < _start)
    {
        yield break;
    }

    yield return _start;
}
```


----
**ref**  
[IEnumerable 인터페이스(MS Doc)](https://docs.microsoft.com/ko-kr/dotnet/api/system.collections.ienumerable?view=netframework-4.8)  
[IEnumerator 인터페이스(MS Doc)](https://docs.microsoft.com/ko-kr/dotnet/api/system.collections.ienumerator?view=netframework-4.8)  
[IEnumerator, IEnumerable의 의미](https://kwangyulseo.com/2016/10/16/ienumerator-ienumerable%EC%9D%98-%EC%9D%98%EB%AF%B8/)  
[IEnumerable VS IEnumerator in C#](https://www.c-sharpcorner.com/UploadFile/219d4d/ienumerable-vs-ienumerator-in-C-Sharp/)
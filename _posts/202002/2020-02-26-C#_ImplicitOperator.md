---
title:  "[C#] Implicit/Explicit Operator"
excerpt: "사용자 정의 전환 연산자"

categories:
  - C#

last_modified_at: 2020-02-26T18:30:00
---

- 다른 형식에서 또는 다른 형식으로 사용자 지정 암시적 또는 명시적 변환을 정의
- 쉽게 말해, 특정 형식(클래스/구조체)이 다른 타입으로 사용될 수 있도록 함 (반대로도 가능)
- 특별한 구문 호출 X
- 할당과 메서드 호출과 같은 다양한 상황에서 발생 가능

### Ex Source Code
```c#
using System;

public readonly struct Digit
{
    private readonly byte digit;

    public Digit(byte digit)
    {
        if (digit > 9)
        {
            throw new ArgumentOutOfRangeException(nameof(digit), "Digit cannot be greater than nine.");
        }
        this.digit = digit;
    }

    public static implicit operator byte(Digit d) => d.digit;
    public static explicit operator Digit(byte b) => new Digit(b);

    public override string ToString() => $"{digit}";
}

public static class UserDefinedConversions
{
    public static void Main()
    {
        var d = new Digit(7);
        
        byte number = d;  // implicit operator
        Console.WriteLine(number);  // output: 7

        Digit digit = (Digit)number;  // explicit operator
        Console.WriteLine(digit);  // output: 7
    }
}
```
- implicit operator로 Digit을 **byte**로 return
- explicit operator로 byte를 **Digit**으로 return


----
**ref**  
[사용자 정의 전환 연산자(MS DOC)](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/operators/user-defined-conversion-operators)  

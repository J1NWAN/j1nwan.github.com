---
title: "Java String(문자열)"
excerpt: "Information processing"

categories:
    - Information processing
tags:
    - JAVA
last_modified_at: 2021-03-04T00:09:00-05:00
---

# [ 문자열 ]

자바에서 문자열에 해당하는 자료형은 **String** 이다.
``` java 
String a = "Happy java";
String b = new String("Happy java");
```

**new** 라는 키워드는 객체를 만들 때 사용한다.

**객체**란 추가적으로 글을 작성할 것이지만 **새로 생성된 자료형** 정도의 의미라고 생각하면 된다.<br><br>

> 문자열을 표현할 때는 가급적 첫번째 방식(literal 표기)을 사용하는 것이 좋다.<br>
> 가독성에 이점이 있고 컴파일 시 최적화에 도움을 준다.

---
<br>

## primitive(원시) 자료형

<span style="color:coral">primitive</span> 자료형이란 
<span style="color:hotpink">int, float, char</span> 등을 말한다.<br>
이런 자료형은 new 키워드로 생성할 수 없다.

그렇다면 <span style="color:hotpink">String</span>은 
<span style="color:coral">primitive</span> 자료형인가?<br>

그것은 아니다 <span style="color:hotpink">String</span>은 리터럴로 표기가 가능하지만 <span style="color:coral">primitive</span> 자료형은 아니다.<br>
String은 리터럴 표현식을 사용할 수 있도록 자바에서 특별 대우 해주는 자료형이다.

String 자료형에는 몇가지 유용한 메소드들이 있는데 자주사용되는 몇가지만 알아보자.

---
<br>

## [ 문자열 메소드 ]
 <details>
 <summary style="color:"> equals </summary>
 <div markdown ="1">

> equals는 문자열의 값을 비교할때 사용한다.

``` java
String a = "hello"
String b = "java"
String c = "hello"
System.out.println(a.equals(b)); // false
System.out.println(a.equals(c)); // true
```

"=="와는 다른 의미이다.

``` java
String a = "hello"
String b = new String("hello");
System.out.println(a==b) // false
```

"=="는 두개의 자료형이 동일한 객체인지를 판별할 때 사용하는 연산자 이다.
</div>
</details>

 <details>
 <summary style="color:"> indexOf </summary>
 <div markdown ="1">

> 문자열에서 특정 문자가 시작되는 인덱스를 리턴한다.

``` java
String a = "Hello java";
System.out.println(a.indexOf("java")); // 6
```
</div>
</details>

 <details>
 <summary style="color:"> replaceAll</summary>
 <div markdown ="1">

> replaceAll은 문자열 중 특정 문자를 다른 문자로 바꾸고 싶을 경우에 사용한다.

``` java
String a = "Hello java";
String b = "World";
System.out.println(a.replaceAll("java", "World")); // Hello World
System.out.println(a.replaceAll("java", b)); // Hello World
```
</div>
</details>

 <details>
 <summary style="color:"> substring </summary>
 <div markdown ="1">

> 문자열 중 특정 부분을 뽑아낼 경우에 사용한다.

``` java
String a = "Hello java";
System.out.println(a.substring(0, 4)); // Hell
```

* substring(시작위치, 끝위치)와 같이 사용한다.<br>
* 끝 위치는 포함이 안된다. (수학의 식과 비슷하다.)<br>
* (시작위치 <= a < 끝위치)<br>

</div>
</details>

 <details>
 <summary style="color:"> toUpperCase, toLowerCase </summary>
 <div markdown ="1">

> 문자열을 모두 대문자로 변경하고자 할 때 사용한다.

``` java
String a = "Hello java";
System.out.println(a.toUpperCase()); // HELLO JAVA
System.out.println(a.toLowerCase()); // hello java
```
</div>
</details>

---
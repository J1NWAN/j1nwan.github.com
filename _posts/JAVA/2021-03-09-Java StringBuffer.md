---
title: "Java StringBuffer"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, String
last_modified_at: 2021-03-09T00:09:00-05:00
---

# [ StringBuffer ]

StringBuffer는 문자열을 추가하거나 변경 할 때 주로 사용하는 자료형이다.

---
<br>

## [ append ]
> StringBuffer 자료형은 append 라는 메소드를 이용하여 계속해서 문자열을 추가해 나갈 수 있다.
>그리고 toString() 메소드를 이용하면 String 자료형으로 변경할 수 있다.

``` java
StringBuffer sb = new StringBuffer();
sb.append("hello");
sb.append(" ");
sb.append("java");
System.out.println(sb.toString()); // hello java
```

String 자료형만 가지고도 표현할 수 있다.

``` java
String temp = "";
temp += "hello";
temp += " ";
temp += "java";
System.out.println(temp); // hello java
```

두 개의 예제 모두 결과는 동일하지만 내부적으로 객체가 생성되고 메모리가 사용되는 과정은 다르다.

* 1번 예제의 경우 StringBuffer 객체는 단 <span style="color:hotpink">**한번만**</span> 생성된다.
* 2번 예제의 경우 <span style="color:hotpink">**+**</span> 연산이 있을 때마다 새로운 String 객체가 생성된다. 총 4개의 객체가 만들어지게 된다.<br><br>

> 문자열간 <span style="color:hotpink">**+**</span> 연산이 있는 경우 자바는 자동으로 새로운 String 객체를 만들어 낸다.

<br>

그렇다고 무조건 StringBuffer를 사용하는것이 바람직한 방법은 아니다.

* StringBuffer 자료형은 String 자료형보다 무거운 편에 속한다.
* new StringBuffer()로 객체를 생성하는 것은 일반 String을 사용하는 것보다 메모리 사용량도 많고 속도도 느리다.<br><br>

> 문자열 추가나 변경등의 작업이 많을 경우에는 StringBuffer를

> 문자열 변경 작업이 거의 없는 경우에는 그냥 String을 사용하는 것이 좋다.

---
<br>

## [ insert ]
> insert 메소드는 특정 위치에 원하는 문자열을 삽입할 수 있다.

``` java
StringBuffer sb = new StringBuffer();
sb.append("java world");
sb.insert(0, "hello ");
System.out.println(sb.toString()); // hello java world
```

insert는 insert(삽입위치, 삽입 할 내용) 이다.

---
<br>

## [ substring ]
> substirng 메소드는 String 자료형의 substring 메소드와 사용법이 동일하다.

``` java
StringBuffer sb = new StringBuffer();
sb.append("Hello java world");
System.out.println(sb.substring(0, 4)); // Hell
```

substirng(시작위치, 끝위치)와 같이 사용하면 StringBuffer 객체의 시작위치에서 끝위치까지의 문자를 뽑아내게 된다.

---
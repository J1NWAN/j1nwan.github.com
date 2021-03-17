---
title: "Java Method"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Method
last_modified_at: '2021-03-11 21:30:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

# 메소드 (Method)

보통 다른언어에는 **함수**라는 것이 별도로 존재한다.<br>
하지만 자바는 클래스를 떠나 존재하는 것은 있을 수 없기 때문에 자바의 함수는 따로 존재하지 않고 클래스 내에 존재한다.<br>

> 자바는 이 클래스 내의 함수를 메소드라고 부른다.

<br>
메소드 구조

``` java
public 리턴자료형 메소드명(매개변수) {
	...
	return 리턴값; // 단 리턴자료형이 void 인 경우에는 return 문이 필요없다.
}
```

메소드는 입출력 유무에 따라 4가지로 분류할 수 있다.

<details>
<summary> 입력과 출력이 모두 있는 메소드 </summary>
<div markdown="1">

``` java
public int sum(int a, int b) {
	return a+b;
}
```

</div>
</details>

<details>
<summary> 입력과 출력이 모두 없는 메소드 </summary>
<div markdown="1">

``` java
public void say() {
	System.out.println("HI");
}
```

</div>
</details>

<details>
<summary> 입력은 없고 출력은 있는 메소드 </summary>
<div markdown="1">

``` java
public int say() {
	return "HI";
}
```

</div>
</details>

<details>
<summary> 입력은 있고 출력은 없는 메소드 </summary>
<div markdown="1">

``` java
public void sum(int a, int b) {
	System.out.println(a + b);
}
```

</div>
</details>

---
<br>

## [ Return ]

위의 코드를 보고 리턴에 대한 궁금증이 있을 것이다.<br>

뜻 그대로 "반환", "복귀", "돌려주다" 라는 의미이다.

무엇을 돌려주나?<br>
해당 메소드의 결과값을 돌려준다.

메소드내의 변수는 해당 메소드 안에서만 쓰이는 변수이지 메소드 밖의 변수가 아니기 때문에 결과값이 생각했던 값 이랑 다를 것이다.<br>

**return**은 현재 메소드의 결과값을 밖에서도 사용할 수 있도록 해준다.

---
<br>

## [ 객체를 이용한 메소드 사용 ]

``` java
public class Method_Main {

	int a;
	
	public int sum_2(int a) {
		a++;
		return a;
	}
	
	public static void main(String[] args) {
		
		Method_Main num = new Method_Main();
		num.a = 1;
		
		System.out.println(num.sum_2(num.a)); // 2 
	}
}
```
---
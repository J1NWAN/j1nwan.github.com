---
title: "Java Constructor"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Constructor
last_modified_at: 2021-03-17T00:09:00-05:00
---

# 생성자

> 메소드명이 클래스명과 동일하고 리턴 자료형이 없는 메소드를 생성자(Constructor)라고 말한다.

``` java
// HouseDog.java
public HouseDog(String name) {
		this.setName(name);
}
```

생성자의 규칙
1. 클래스명과 메소드명이 동일하다.
2. 리턴타입을 정의하지 않는다.

생성자는 객체가 생성될 때 호출된다.<br>
객체가 생성될 때는 **new**라는 키워드로 객체가 만들어질 때이다.
``` java
new 클래스명(매개변수)
```
생성자를 생성하고 매개변수를 입력하면 객체를 생성할 때 **무조건** 생성자값에 매개변수 타입에 맞는 값을 넣어줘야한다.

생성자를 활용하는 코드를 보자.
``` java
public class HouseDog extends Dog {

	public HouseDog(String name) {
		this.setName(name);
	}
	
	public void sleep() {
		System.out.println(this.name + " zzz in house");
	}
	
	public void sleep(int hour) {
		System.out.println(this.name + " zzz in house" + hour + "hours");
	}
	
	public static void main(String[] args) {
		HouseDog dog = new HouseDog("구름이");
		System.out.println(dog.name); // 구름이
	}
}
```
---
<br>

## default 생성자
``` java
public class Dog extends Animal {
	public Dog() { // defalut 생성자

	}
}
```
생성자의 입력 항목(매개변수)가 없고 생성자 내부에 아무 내용이 없는 생성자를 **defalut 생성자**라고 부른다.

* defalut 생성자는 매개변수, 생성자 내부에 아무 내용이 없는 생성자를 의미함.
* 클래스에 생성자가 하나도 없다면 컴파일러는 자동으로 defalut 생성자를 추가함.

> 이러한 이유로 위에서 살펴본 HouseDog 클래스에 name을 입력으로 받는 생성자를 만든 후에 **new HouseDog()** 는 사용할 수 없게 되는 것이다.

---
<br>

## 생성자 오버로딩

생성자도 하나의 클래스에 매개변수가 다른 여러개의 생성자를 만들 수 있다.

``` java
public class HouseDog extends Dog {

	public HouseDog(String name) {
		this.setName(name);
	}
	
	public HouseDog(int type) {
		if(type == 1) {
			this.setName("yorkshire");
		}else if(type == 2) {
			this.setName("bulldog");
		}
	}
	public void sleep() {
		System.out.println(this.name + " zzz in house");
	}
	
	public void sleep(int hour) {
		System.out.println(this.name + " zzz in house" + hour + "hours");
	}
	
	public static void main(String[] args) {
		HouseDog cloud = new HouseDog("구름이");
		HouseDog yorkshire = new HouseDog(1);
		
		System.out.println(cloud.name); // 구름이
		System.out.println(yorkshire.name); // yorkshire
	}
}
```
---
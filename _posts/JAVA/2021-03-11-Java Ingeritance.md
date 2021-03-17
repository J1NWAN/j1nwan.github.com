---
title: "Java Ingeritance"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Ingeritance
last_modified_at: '2021-03-15 21:00:00 +0800'
---

# 상속 (Ingeritance)

상속은 말 그대로 자식이 부모로부터 무언가를 물려받는 것이다.

* 상속을 사용하려면 2개(부모, 자식)의 자바파일이 필요하다.
* 자식클래스 extends 부모클래스 로 사용한다.

예시
* Animal.java(부모)
  * Dog.java(자식)

``` java
// Animal.java

public class Animal {
	String name;
	
	public void setName(String name) {
		this.name = name;
	}
	
	public static void main(String[] args) {
	
	}
}
```
``` java
// Dog.java

public class Dog extends Animal {

}
```

Dog 클래스는 Animal 클래스를 상속하게 되었다.

Dog 클래스에 **name** 이라는 객체변수와 **setName** 이라는 메소드를 만들지 않았지만
Animal 클래스를 상속 받았기 때문에 사용 가능하다.<br>

상속 받은것을 활용 해보자. 
``` java
public class Dog extends Animal {

	public static void main(String[] args) {
		Dog dog = new Dog();
		dog.setName("구름");
		System.out.println(dog.name); // 구름
	}
}
```

이렇게 보통 부모 클래스를 상속받은 자식 클래스는 부모 클래스의 기능에 더하여 좀 더 많은 기능을 갖도록 설계한다.

---
<br>

## [ 메소드 오버라이딩 ]

> 부모클래스의 메소드를 자식클래스가 동일한 형태로 또 다시 구현하는 행위를 **메소드 오버라이딩**(Method Overriding)이라고 한다. (메소드 덮어쓰기)

``` java
// Dog.java

public class Dog extends Animal {

	public void sleep() {
		System.out.println("zzz");
	}
	
	public static void main(String[] args) {
		Dog dog = new Dog();
		dog.setName("구름");
		System.out.println(dog.name);
	}
}
```
``` java
// houseDog.java

public class HouseDog extends Dog {

	public void sleep() {
		System.out.println(this.name + " zzz in house");
	}
	
	public static void main(String[] args) {
		HouseDog houseDog = new HouseDog();
		houseDog.setName("happy");
        houseDog.sleep(); // happy zzz in house
	}
}
```

동일한 입출력 형태의 메소드가 구현되면 현재 클래스의 메소드가 우선순위를 갖게 된다.

---
<br>

## [ 메소드 오버로딩 ]

> 입력항목이 다른 경우 동일한 이름의 메소드를 만들 수 있는데 이것을 **메소드 오버로딩**(Method Overloading) 이라고 부른다.

``` java
public class HouseDog extends Dog {

	public void sleep() {
		System.out.println(this.name + " zzz in house");
	}
	
	public void sleep(int hour) {
		System.out.println(this.name + " zzz in house" + hour + "hours");
	}
	
	public static void main(String[] args) {
		HouseDog houseDog = new HouseDog();
		houseDog.setName("happy");
		houseDog.sleep(); // happy zzz in house
		houseDog.sleep(3); // happy zzz in house for 3 hours
	}
}
```
---
---
title: "Java Polymorphism"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Polymorphism
last_modified_at: '2021-03-18 21:30:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

# 다형성

하나의 객체가 여러개의 자료형 타입을 가질 수 있는 것을 객체지향 세계에서는<br>
다형성, 폴리모피즘(Polymorphism)이라고 부른다.

전 포스트에 이용했었던 동물 파일들을 이용할 것이고, 다향성을 이용할 것이다.
``` java
// Bouncer.java
public class Bouncer {
	public void barkAnimal(Animal animal) {
		if(animal instanceof Tiger) { // animal 객체가 new Tiger로 만들어졌는가?
			System.out.println("어흥");
		} else if (animal instanceof Lion) { // animal 객체가 new Lion로 만들어졌는가?
			System.out.println("으르렁");
		}
	}

	public static void main(String[] args) {
		Tiger tiger = new Tiger();
		Lion lion = new Lion();

		Bouncer bouncer = new Bouncer();
		bouncer.barkAnimal(tiger); // 어흥
		bouncer.barkAnimal(Lion); // 으르렁
	}
}
```

> **instanceof**는 특정 객체가 특정 클래스의 객체인지를 조사할 때 사용되는 자바의 내장 키워드이다. **animal instanceof Tiger**는 "animal 객체가 **new Tiger**로 만들어진 객체인가?"를 묻는 조건식이다.<br><br>

만약 위의 코드에 새로운 동물들이 추가된다면 조건문을 늘려가야한다.<br>
이 방법대신 인터페이스를 이용하여 바꿔보자.<br>

---
<br>

## 인터페이스 작성
``` java
// Barkable.java
public interface Barkable {
	public void bark()
}
```

그리고 동물클래스에 Barkable 인터페이스를 구현하도록 변경 해 보자.

---
<br>

## 인터페이스 구현
``` java
public class Tiger extends Animal implements Predator, Barkable {

	public String getFood() {
		return "apple";
	}
	
	public void bark() {
		System.out.println("어흥");
	}
}
```
``` java
public class Lion extends Animal implements Predator, Barkable {

	public String getFood() {
		return "banana";
	}
	
	public void bark() {
		System.out.println("으르렁");
	}
}
```

> 인터페이스는 (**,**)를 이용하여 여러개를 implements 할 수 있다.

동물클래스에 bark 메소드를 구현했으면 Bouncer 클래스의 barkAnimal 메소드를 수정하자.<br><br>
- 바뀌기 전
``` java
public void barkAnimal(Animal animal) {
		if(animal instanceof Tiger) {
			System.out.println("어흥");
		} else if(animal instanceof Lion) {
			System.out.println("으르렁");
		}
	}
```

- 바뀐 후
``` java
public void barkAnimal(Barkable animal) {
		animal.bark();
	}
```

> 폴리모피즘을 이용하면 위의 예에서 보듯이 복잡한 if else 의 조건문을 간단하게 처리할 수 있는 경우가 많다.

바뀐점은 이러하다.
* 메소드 매개변수 Animal -> Barkable
* 메소드 내부 조건문(if) -> animal.bark()

위 예제에서 사용한 동물 객체는 각각 개인의 객체이면서 부모(Animal) 클래스의 객체이기도 하고 두 개의 인터페이스 이기도하다.<br>
이러한 이유로 메소드의 매개변수를 Animal에서 Barkable로 바꾸어 사용할 수 있는 것이다.<br>
즉 Tiger 클래스의 객체는 다음과 같이 여러가지 자료형으로 표현할 수 있다.

``` java
Tiger tiger = new Tiger();
Animal animal = new Tiger();
Predator predator = new Tiger();
Barkable barkable = new Tiger();
```

여기서 알아두어야 할 사항은 Predator와 Barkable로 선언된 객체는 각각 구현된 메소드만 사용할 수 있다.<br>

두 인터페이스의 메소드를 모두 사용하는 방법도 있다.
1. 두 개의 인터페이스를 구현한 동물클래스(Tiger) 로 선언된 동물(tiger) 객체를 사용
2. 두 개의 인터페이스의 메소드를 모두 포함하는 새로운 인터페이스를 만들어 사용

``` java
// Bouncer.java
// 두개의 인터페이스를 구현한 동물클래스 로 선언된 동물 객체를 사용
public static void main(String[] args) {
	tiger.bark();
	System.out.println(tiger.getFood());
}
```
``` java
// BarkablePredator.java
// 두 개의 인터페이스의 메소드를 모두 포함하는 새로운 인터페이스
public interface BarkablePredator {
	public void bark();
	public String getFood();
}
```

미리 만들어둔 인터페이스를 사용할 경우 아래 코드처럼 새로운 인터페이스를 만들고 상속을 받을 수도 있다.
``` java
public interface BarkablePredator extends Predator, Barkable {

}
```

> 인터페이스는 **extends** 를 이용하여 다중 상속이 지원된다.<br>
> 일반 클래스는 단일 상속만 가능하다.

---
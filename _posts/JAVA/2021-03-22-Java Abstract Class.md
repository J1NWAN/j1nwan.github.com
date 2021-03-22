---
title: "Java Abstract Class"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Abstract, Class
last_modified_at: '2021-03-22 21:30:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

# 추상클래스
> 추상 클래스(abstract class)란 하나 이상의 추상 메소드(abstract method)를 포함하는 클래스이다.

* 추상 메소드는 선언만 있고 본체는 없는 함수이며 선언부에 "**abstract**" 라는 키워드를 붙인다. 
* 추상 메소드가 포함되었다면 클래스도 추상 클래스이므로 클래스명 앞에도 "**abstract**"키워드를 붙여야 한다.

인터페이스 포스트에서 사용한 Predator 클래스를 추상클래스로 변경해보자.
``` java
public abstract class Predator extends Animal {
	public abstract String getFood();
}
```
<br>

바뀐점은 이러하다.
* public interface Predator -> public abstract class Predator extends Animal 
* public String getFood() -> public abstract String getFood()
<br><br>

인터페이스 메소드를 사용하던 파일들을 추상클래스 메소드를 사용하는 파일로 바꿔줘야 한다.

``` java
// Tiger.java
public class Tiger extends Predator implements Barkable {

	public String getFood() {
		return "apple";
	}
	
	public void bark() {
		System.out.println("어흥");
	}
}
```
``` java
// Lion.java
public class Lion extends Predator implements Barkable {

	public String getFood() {
		return "banana";
	}
	
	public void bark() {
		System.out.println("으르렁");
	}
}
```
<br>

바뀐점은 이러하다.
``` java
// 추상클래스 변경전(인터페이스 상태)
public class Tiger extends Animal implements Predator, Barkable{...}
public class Lion extends Animal implements Predator, Barkable{...}

// 추상클래스 변경후
public class Tiger extends Predator implements Barkable {...}
public class Lion extends Predator implements Barkable {...}
```
<br>

추상클래스는 인터페이스와 마찬가지로 추상클래스를 상속하는 클래스에서 반드시 메소드를 구현해야 한다.<br>

추상클래스는 두 가지를 기억해야 한다.
1. 추상클래스 파일(.java)에 추상메소드 선언만 한 경우 추상클래스를 상속하는 클래스에 반드시 메소드를 구현해야 한다.
2. 추상클래스 파일(.java)에 추상메소드를 선언과 동시에 내부(몸통)도 만들 수 있다.<br><br>

만약 2번으로 추상클래스를 만든 경우 상속받는 객체에서 메소드를 사용할 수 있다.<br>
예시를 한번 만들어보자!

``` java
// isPredator.java
public abstract class isPredator extends Animal {
	public abstract String getFood();
	
	public boolean isPredator() {
		System.out.println("isPredator On!");
		return true;
	}
}


// Tiger.java
public class Tiger extends isPredator implements Barkable {
	public String getFood() {
		return "apple";
	}
	
	public void bark() {
		System.out.println("어흥");
	}
}
```
``` java
// Bouncer.java
public class Bouncer {
	
	public void barkAnimal(Barkable animal) {
		animal.bark();
	}
	
	public static void main(String[] args) {
		Tiger tiger = new Tiger();
		Tiger.isPredator(); // isPredator On!
	}
}
```
<br>
정상적으로 출력되는 것을 볼 수 있다.

---
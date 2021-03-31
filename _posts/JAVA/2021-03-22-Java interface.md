---
title: "Java Interface"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Interface
last_modified_at: '2021-03-17 21:30:00 +0800'
---

# 인터페이스

우선 코드를 보자

``` java
// Tiger.java
public class Tiger extends Animal{

}
```
``` java
// Lion.java
public class Lion extends Animal {

}
```
``` java
// ZooKeeper.java
public class ZooKeeper {

	public void feed(Tiger tiger) {
		System.out.println("feed apple");
	}
	
	public void feed(Lion lion) {
		System.out.println("feed banana");
	}
	
	public static void main(String[] args) {
		ZooKeeper zooKeeper = new ZooKeeper();
		Tiger tiger = new Tiger();
		Lion lion = new Lion();
		zooKeeper.feed(tiger); // feed apple
		zooKeeper.feed(lion); // feed banana
	}
}
```

상속만 준 클래스 파일 2개와 동물들의 먹이에 관한 파일 하나가 존재한다.<br>
ZooKeeper 코드를 보면 각 동물들의 관한 메소드가 존재한다.<br>

동물들이 더 추가된다면 추가될 때마다 메소드를 추가해야 한다.<br>
이 귀찮은 작업을 **인터페이스**를 이용하여 작성해보자.

``` java
// Predator.java
public interface Predator {

}
```
위 코드와 같이 인터페이스는 class가 아닌 **interface** 라는 키워드를 이용하여 작성한다.<br>

``` java
// Tiger.java
public class Tiger extends Animal implements Predator {

}
```

``` java
// Lion.java
public class Lion extends Animal implements Predator {

}
```
인터페이스 구현은 위 코드와 같이 **implements** 라는 키워드를 사용한다.<br>
그러면 Tiger, Lion은 각각 Tiger, Lion의 객체이기도 하지만,<br> 
Predator 인터페이스의 객체이기도 하기 때문에 **Predator를 자료형의 타입**으로 사용할 수 있다.<br>

* tiger - Tiger 클래스의 객체, Predator 인터페이스의 객체
* lion - Lion 클래스의 객체, Predator 인터페이스의 객체

코드를 실행해보자.
``` java
public class ZooKeeper {

	public void feed(Predator predator) {
		System.out.println("feed apple");
	}
	
	public static void main(String[] args) {
		ZooKeeper zooKeeper = new ZooKeeper();
		Tiger tiger = new Tiger();
		Lion lion = new Lion();
		zooKeeper.feed(tiger); // feed apple
		zooKeeper.feed(lion); // feed apple
		
	}
}
```

두 동물의 결과가 같은것을 확인할 수 있다.<br>
그런데 동물들 마다 먹는 먹이가 다르다 Predator 인터페이스에 메소드를 추가하여 각 동물 파일에서 사용할 수 있도록 해보자.<br>

``` java
// Predator
public interface Predator {

	public String getFood();
}
```
여기서 이상한점이 있을 것이다 메소드에 몸동이 없다.<br>

* 인터페이스의 메소드는 메소드의 이름과 입출력에 대한 정의만 있고 내용은 없다.
* 몸통 부분은 Implements한 클래스들이 구현해야 한다.<br>

``` java
public class Tiger extends Animal implements Predator {

	public String getFood() {
		return "apple";
	}
}
```
``` java
public class Lion extends Animal implements Predator {

	public String getFood() {
		return "banana";
	}
}
```
``` java
// ZooKeeper.java
public void feed(Predator predator) {
	System.out.println("feed " + predator.getFood());
}
```

각 동물 클래스 파일에 **getFood** 메소드의 몸통을 구현했고,<br>
출력하는(Main) ZooKeeper 클래스에 feed 메소드에 predator 인터페이스의 메소드를 출력하는 코드를 작성했다.

결과는 각 동물의 메소드안에 먹이값을 리턴 받는다.
``` java
feed apple
feed banana
```

> 인터페이스의 중요함은 메소드의 갯수가 줄어들었다는 점이 아니라 각 클래스 종류와 상관없는 독립적인 클래스가 되었다는 점이다.<br>



| 물리적세계                  | 자바세계       |
| --------------------------- | -------------- |
| 컴퓨터                      | ZooKeeper      |
| USB 포트                    | Predator       |
| 하드디스크, 디지털카메라... | Tiger, Lion... |
> USB 포트에는 전자기기들이 지켜야만 하는 각종 규칙들이 있다. (인터페이스의 메소드)
---

**Info Notice:**
dd
{: .notice--info}

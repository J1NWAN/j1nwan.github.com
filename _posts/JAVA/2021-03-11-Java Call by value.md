---
title: "Java Call by value"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Method
last_modified_at: '2021-03-11 21:30:00 +0800'
---

# Call by value

메소드로 객체를 전달할 경우 메소드에서 객체의 객체변수(속성) 값을 변경할 수 있게 된다.

``` java
class Updater {
    public void update(int count) {
        count++;
    }
}

public class Counter {
    int count = 0;  // 객체변수
    public static void main(String[] args) {        
        Counter myCounter = new Counter();        
        System.out.println("before update:" + myCounter.count); // 0

        Updater myUpdater = new Updater();
        myUpdater.update(myCounter.count);
        System.out.println("after update:" + myCounter.count); // 0
    }
}
```

> 위 코드에 클래스가 2개가 등장했는데 Java는 하나의 파일에 여러개의 클래스를 선언 할 수 있다. 단 파일명이 Counter.java라면 Counter라는 클래스는 public 으로 선언하라는 규칙이 있다.

Updater 메소드는 count를 증가 시키는 메소드인데 적용이 안되는 모습이다.<br>
이유는 int 자료형을 전달 받았기 때문이다.


객체의 객체변수 값을 변경 가능하게 코드를 작성해보자.
``` java
class Updater {
	public void update(Counter counter) {
		counter.count++;
	}
}

public class Counter {
	int count = 0;
	
	public static void main(String[] args) {
		
		Counter myCounter = new Counter();
		System.out.println("before update: " + myCounter.count); // 0
		
		Updater myUpdater = new Updater();
		myUpdater.update(myCounter);
		System.out.println("after update: " + myCounter.count); // 1
	}
}
```

이렇게 메소드의 입력으로 객체를 전달받는 경우에는 메소드가 입력받은 객체를 그대로 사용하기 때문에 메소드가 객체의 속성값을 변경하면 메소드 수행 후 객체의 변경된 속성값이 유지되게 된다.

---
---
title: "Java Class"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Class
last_modified_at: 2021-03-11T00:09:00-05:00
---

# 클래스 (Class)

클래스는 과자를 만드는 과자틀과 과자라고 생각하면 된다.
* 과자틀 -> 클래스(Class)
* 과자틀에 의해서 만들어진 과자들 -> 객체(Object)<br>

하나의 클래스로 무수히 많은 객체를 만들 수 있다.

클래스는 자바를 처음 배울 때 부터 존재했다.

``` java
public class practice_Java {

}
```

위 코드가 클래스 이다.<br>
위 클래스는 선언만 있고 내용이 없는 껍데기 클래스이다.<br>
하지만 이 껍데기뿐인 클래스도 아주 중요한 기능인 **객체(Object)** 를 만드는 기능이 있다.<br>

``` java
practice_Java student = new practice_Java();
```

위 코드가 객체를 만드는 코드이고 **new** 는 객체를 생성할 때 사용하는 키워드이다.<br>
이렇게 하면 practice_Java 클래스의 인스턴스(instance)인 **"student"**, 즉 pratice_Java의 객체가 만들어진다.<br>

---
<br>

## [ 객체 변수 ]

메소드가 아닌 클래스에서 선언된 변수를 **객체 변수** 라고 부른다.
> 인스턴스 변수, 멤버 변수, 속성이라고도 말한다.

``` java
public class practice_Java {
	String name; // 객체 변수
}
```

객체 변수에 접근하기 위해서는 도트연산자 **.** 을 이용하여 접근할 수 있다.

``` java
student.name = "김이름"; // 객체.객체 변수
```

<br>

아래 코드는 간단한 객체 변수값 출력 코드이다.

``` java
public class practice_String {
	String name;
	
	public static void main(String[] args) {
		
		practice_String student = new practice_String();
		student.name = "김이름"; // 객체 : student, 객체변수 : name
		System.out.println(student.name); // 김이름
	}
}
```

---
<br>

## [ 메소드 ]

객체 변수에 값을 대입하는 방법에는 여러가지가 있을 수 있지만 가장 보편적인 방법인 메소드를 이용하는 방법에 대해서 알아보자.

> 메소드에 대해는 자세하게 포스트 할 예정이다.

``` java
public class practice_String {
	String name;

	public void setName(String name) {
		this.name = name;
	}
	
	public static void main(String[] args) {
		
		practice_String student = new practice_String();
		student.setName("boby");
		System.out.println(student.name);
	}
}
```

위 코드를 해석 해보면 이러하다.<br>
* String name : 객체 변수
* setName(String name) : setName(메소드 이름), String name(매개변수)
  * this.name = name : this.name(객체 변수를 가르킴), name(매개변수로 받는 값)
* main : 메인 함수
  * practice_String student = new practice_String() : practice_String 클래스의 student 객체를 생성
  * student.setName("body") : student 객체의 name에 boby 적용
  * System.out.println(student.name) : student 객체의 name값 출력
<br><br>

여기서 중요한것은 **"this.name"** 부분이다.<br>
현재 객체가 하나밖에 없어서 this 는 student 객체를 지칭하게된다.<br>
만약 객체가 하나 더 생성되어 똑같이 setName 메소드를 사용하게 된다면 어떻게 될까?<br>

---
<br>

## [ 객체 변수는 공유되지 않는다 ]

``` java
public class practice_String {
	String name;

	public void setName(String name) {
		this.name = name;
	}
	
	public static void main(String[] args) {
		
		practice_String student = new practice_String();
		practice_String people = new practice_String();
		
		student.setName("boby");
		people.setName("홍길동");
		System.out.println(student.name + " " + people.name); // boby 홍길동
	}
}
```

위 결과값을 보면 "**boby 홍길동**" 이렇게 출력이 되었다.<br>

즉, 객체 변수는 공유 되지 않는다는 것을 확인할 수 있다.

> 참고. 객체 변수의 값은 공유되지 않지만 static을 이용하게 되면 객체 변수를 공유하도록 만들 수도 있다.
---
---
title: "Java Input"
excerpt: "Information processing"

categories:
    - JAVA
tags:
    - JAVA, Input
last_modified_at: '2021-03-29 21:30:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

# 콘솔 입출력

> 콘솔 입출력은 키보드로 값을 입력하고 그 값을 콘솔창에 출력되는 것이다.

JAVA에는 다양한 콘솔 입력 방법이 존재한다.

## Console Input(콘솔 입력)

JAVA의 **System.in**을 이용하면 콘솔 입력을 얻을 수 있다.
``` java
import java.io.InputStream; // 입력 도구 InputStream을 사용하기 위해 불러옴

public class test1 {

	public static void main(String[] args) throws Exception { // 예외처리
		InputStream in = System.in;
		
		int a;
		a = in.read(); // 1byte
		
		System.out.println(a); // 입력값이 a면 97이 출력됨
	}
}
```
 
a를 입력했는데 결과가 정수 97로 출력이 되었다.<br>
이유는 이러하다.<br>
* InputStream의 **read** Method는 1byte의 사용자의 입력을 받는다.
* **read**로 읽은 1byte의 데이터는 byte 자료형으로 저장되는 것이 아니라 int 자료형으로 저장된다.
* 저장된 int 값은 0~255 정수값으로 **ASCII CODE** (**아스키 코드**)값이다.

> 아스키코드의 자세한 내용은 구글링으로 찾아보자.

<br>

위의 코드는 1 byte의 입력값만 전달되기 때문에 "**abc**", <br>
이렇게 연속적으로 값을 입력하게 되면 첫 문자 "**a**"의 아스키코드값 97만 출력된다.<br>

여러개를 입력하고 출력 받고 싶은경우 배열을 이용하면 된다.<br>
``` java
import java.io.InputStream;

public class test1 {

	public static void main(String[] args) throws Exception {
		InputStream in = System.in;
		
		byte[] a = new byte[3];
		in.read();
		
		System.out.println(a[0]); // a -> 97
		System.out.println(a[1]); // b -> 98
		System.out.println(a[2]); // c -> 99
	}
}
```

위의 코드는 아스키코드를 해석을 해야하기 때문에 너무 불편하다.<br>
바이트 대신 문자로 입력 스트림을 읽는 방법을 이용해보자.<br>

---
<br>

## InputStreamReader
``` java
import java.io.InputStream;
import java.io.InputStreamReader;

public class test1 {

	public static void main(String[] args) throws Exception {
		InputStream in = System.in;
		InputStreamReader reader = new InputStreamReader(in);
		char[] a = new char[3];
		reader.read(a);
		
		System.out.println(a);
	}
}
```

아스키코드로 입력 받는것 보단 편하지만 여전히 불편하다.<br>
사용자가 엔터키를 입력할 때 까지 사용자의 입력을 전부 받아들이는 방법을 사용해보자.<br>

---
<br>

## BufferedReader

``` java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;

public class test1 {

	public static void main(String[] args) throws Exception {
		InputStream in = System.in;
		InputStreamReader reader = new InputStreamReader(in);
		BufferedReader br = new BufferedReader(reader);
		
		String a = br.readLine(); // Hello Java World
		System.out.println(a); // Hello Java World
	}
}
```

사용자가 엔터키를 입력할 때까지 입력했던 문자열 전부를 읽을 수 있게 된다.<br>
스트림에 대해 헷갈리는 경향이 많이 있다. 이렇게 기억하면 좋을 것 같다.<br>

* InputStream - byte
* InputStreamReader - character
* BufferedReader - String

> 코드 부분에 예외처리(throws Exception)을 사용한 부분이 있다.
> InputStream으로 부터 값을 읽어들일 때는 IOExeption이 발생할 수 있기 때문에 예외처리를 하는데 throws로 그 예외처리를 뒤로 미루게 한 것이다.

---
<br>

## Scanner

Java 2 버전부터 Scanner를 사용할 수 있게 되었다.<br>
``` java
import java.util.Scanner;

public class Test {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println(sc.next());
	}
}
```
* next - 단어
* nextLine - 라인
* nextInt - 정수

> 간단하게 사용이 가능하지만 BufferedReader 보다 느리다.

---
<br>

# Console Print(콘솔 출력)

``` java
System.out.print - 출력 후 줄바꿈 X
System.out.println - 출력 후 줄바꿈 O
System.err.println - 에러메세지 출력 후 줄바꿈
```
---
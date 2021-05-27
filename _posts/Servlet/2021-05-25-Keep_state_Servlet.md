---
title: Servlet 상태유지
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories: Web
toc: true
toc_sticky: true
toc_label: 목차
description: 사용자에게 전달받은 값을 종료되기 전 까지 유지하는 방법을 배운다.
article_tag1: Application Method를 이용한 상태유지
article_tag2: Session Method를 이용한 상태유지
article_tag3: Cookie Method를 이용한 상태유지
article_section: 사용자를 구분하고 전달받은 값을 사용자가 종료하기 전 까지 상태유지
meta_keywords: Servlet, Application, Session, Cookie
last_modified_at: '2021-05-25 00:00:00 +0800'
---

# 클라이언트에서 전달받은 데이터를 유지

## Servlet Context

- **ServletContext** 클래스는 톰캣 컨테이너 실행 시 각 컨텍스트(웹 애플리케이션)마다 한 개의 **ServletContext**객체를 생성한다.
- 톰캣 컨테이너가 종료되면 ServletContext 객체는 소멸된다.

<br>

### ServletContext 클래스의 특징
- ```javax.servlet.ServletContext```로 정의 되어 있다. 
- 서블릿과 컨테이너 간의 연동을 위해서 사용한다.
- 컨텍스트(웹 애플리케이션)마다 하나의 ServletContext가 생성된다.
- 서블릿끼리 자원(데이터)를 공유하는 데 사용한다.
- 컨테이너 실행시 생성되고 컨테이너 종료시 소멸된다.

<hr><br>

## Application

- Application은 서블릿 Context로, 서블릿들 간의 문맥을 저장할 수 있는 곳이자, 자원을 공유할 수 있는 저장소이다.
- Application은 누구나 상태 값을 서버(웹 애플리케이션)에 Application 객체를 저장하여 사용하도록 한다.
  - 사용 범위 : **전역 범위**에서 사용하는 저장 공간
  - 생명 주기 : WAS가 시작해서 종료할 때까지
  - 저장 위치 : WAS 서버의 메모리
<br><br>

### Application 구현

- ```import javax.servlet.ServletContext;```
  - **ServletContext**의 생성자를 이용하여 구현한다.
  - ```ServletContext application = request.getServletContext();```

<br>

- 상태유지를 위한 데이터 저장
  - ```application.setAttribute("key", value);```
    - **setAttibute**는 ("**key**", **value**)로 사용한다.
      - key : 저장한 데이터(value)의 열쇠
      - value : 저장해야 할 데이터 값

<br>

- 저장한 데이터 불러오기
  - ```application.getAttribute("key");```
    - **getAttibute**는 ("key")로 사용한다.
      - 저장한 데이터의 위치에 존재한 **key**를 사용하여 불러온다.

<br>

<hr><br>

## Session

> Session은 **서버에 생성**하고 서버의 기존 연결정보를 저장함으로써 클라이언트와 서버가 지속적으로 연결을 유지 할 수 있도록 도와준다.

- Session의 원리
  - 세션ID를 서버에서 클라이언트로 발급해 준다.
  - 서버에서 클라이언트로 발급해준 세션 ID를 쿠키를 사용해 저장한다.
  - 클라이언트는 다시 접속시, 이 쿠키 및 **localstorage**를 이용해서 세션 ID값을 전달한다.
<br><br>

- Session의 장점
  - 각 클라이언트에게 고유 ID를 부여한다.
  - 세션 ID를 클라이언트를 구분해서 클라이언트의 요구에 맞는 서비스를 제공할 수 있다.
  - 사용해봤던 정보들을 서버에 저장하기에 보안성이 높다.
<br><br>

- Session의 단점
  - 서버에 저장하기에 처리를 요구하는 부하와 저장 공간을 필요로 한다.
<br><br>

- HTTP 세션 동작 순서
  - **client가** 서버로 접속을 시도
  - 서버는 접근한 클라이언트의 **request-header filed**인 쿠키를 확인해 클라이언트가 해당 **session-id**를 보내왔는지 확인한다.
  - 만약 클라이언트로부터 발송된 **session-id**가 없다면, 서버는 session-id를 생성해 클라이언트에게 response-head field인 set cookie 값으로 sesion-id 발행한다.
<br><br>

- Session 사용시 주의사항
  - Session은 사용자가 같아도 웹 브라우저가 다르면 다른 사용자로 인식한다.
  - **같은 종류**의 웹 브라우저는 같은 사용자로 인식한다.
<br><br>

### Session 구현

- Session을 사용하기 위해 **HttpSession** 인터페이스를 사용한다.
  - 인터페이스 사용을 위한 ```import```를 한다.
  - ```import javax.servlet.http.HttpSession;```
<br><br>

- HttpSession 객체를 사용을 위한 선언을 해준다.
  - ```HttpSession session = request.getSession();```
  - 요청 받은 데이터를 유지시켜야 하므로 **request**를 사용한다.
<br><br>

- 상태유지를 위한 데이터 저장
  - ```session.setAttribute("key", value);```
  - **setAttibute**는 ("**key**", **value**)로 사용한다.
    - key : 저장한 데이터(value)의 열쇠
    - value : 저장해야 할 데이터 값
<br><br>

- Session에 저장되어 있는 데이터 불러오기
  - ```session.getAttribute("key");```
    - 저장한 데이터의 위치에 존재한 **key**를 사용하여 불러온다.

<hr><br>

## 쿠키

- 쿠키는 **클라이언트**(웹 브라우저, 사용자 컴퓨터) 측에 저장되어 사용됩니다.
- 쿠키의 **기본 생명주기는 브라우저가 닫히기 전** 까지입니다.
	- 기간을 값을 설정하면 그 기간 동안 값을 설정합니다.
<br>

- 사용 범위
	- 웹 브라우저 별 및 경로 범주 공간
- 생명주기
	- 웹 브라우저에 전달한 시간부터 종료 시간
- 저장 위치
	- 웹 브라우저의 메모리 또는 파일
< BR > < BR >

- 쿠키의 인터페이스를 사용하는 경우 import 해야한다.
	- ```javax.servlet.http.Cookie```
<br>

### Cookie 저장하는 방법

``` java 
// 쿠키 객체를 생성하고 쿠키에 속성(저장할 데이터) 값을 설정
Cookie cookie = new Cookie("Key", String_value);

// 클라이언트측으로 전송해 값을 저장
response.addCookie(cookie);
```
<br>

- Cookie는 **key** 값과 **value** 값으로 저장한다.
	- value 값은 문자(String)로만 저장이 가능하다.
	- 저장해야 할 value가 문자(String)가 아니라면 ```String.valueOf()```를 이용하여 변환한다.
<br>

### Cookie 받아오기
- Cookie를 받아오려면 ```request.getCookie()```라는 Method를 이용한다.
	- Method 이름을 보면 예상가능하듯 **여러개의 Cookie**를 가져와야 하기 때문에 **배열로 얻는다**.
	- 받아온 Cookie는 배열에 저장되어 있으므로 배열안에 원하는 Cookie를 찾기 위해 반복문으로 비교하며 가져온다.
	- **Cookie[] 변수 = request.getCookies();**
	-  Ex) ```Cookie[] cookies = request.getCookies();```
<br>

### Cookie 이름 얻기
- **String 변수 = 받아온 변수.getCookies();**
- Ex) ```String c = cookies.getName();```
<br>

### Cookie 값을 얻기
- **String 변수 = 받아온 변수.getValue();**
- Ex) ```String c = cookies.getValue();```
<br>

### Cookie 받아오기 부터 값을 얻기 까지의 정리
- 모든 Cookie를 받아오기 때문에 **"배열"**로 받는다.
- 수 많은 Cookie중 원하는 값을 얻기위해 **반복하여** 꺼내온 이름들을 **체크(비교)**하는 형태로 필요한 쿠키를 찾아야 한다.
- Ex)
``` java
// 모든 쿠키를 배열로 받아온다. 
Cookie[] cookies = request.getCookies(); 

// 값을 저장할 변수 
String c = ""; 

// 배열에 값이 존재하는 경우 true 
if(cookies != null) { 
	// 반복 횟수는 cookies의 끝 까지 
	for(Cookie cookie : cookies) { 
		// 배열에서 받아온 이름(key)이 동일한 경우 true 
		if(cookie.getName.equals("key1")) { 
		// 이름(key)값에 저장되어 있는 데이터를 저장 
			c = cookie.getValue(); 
			}
		}
	} 
// 위 주석과 동일 
if(cookies != null) { 
	for(Cookie cookie : cookies) { 
		if(cookie.getName.equals("key2")) { 
			c_ = cookie.getValue(); 
		} 
	} 
}
```
<br><br>

### Cookie의 생명 주기(Life Cycle)

- Cookie의 생명 주기는 기본적으로 **클라이언트(웹 브라우저)가 닫히면 소멸**된다.
- 생명 주기를 설정하면 **설정한 만큼 사용이 가능**하며, **초 단위로 설정**해야 한다.
	- 생명 주기는 해당 **Cookie를 얻은 후 부터 설정한 값 까지**이며, 설정된 시간이 경과 되기 전까지 Cookie는 유지 된다.
	- 사용 방법은 **받아온 변수.setMaxAge(초);**로 사용한다.
	- Ex)  ```cookies.setMaxAge(86400);``` or ```cookies.setMaxAge(24 * 60 * 60);```

<hr><br>

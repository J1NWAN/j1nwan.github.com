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

### Application 예제

- 사용자의 입력을 받은 Calculator
  - Java
``` java
// ServletContext - 데이터 공유 시작
ServletContext application = request.getServletContext();
response.setCharacterEncoding("UTF-8");
response.setContentType("text/html; charset=UTF-8");
		
String v_ = request.getParameter("v");
String op = request.getParameter("operator");
		
int v = 0;
		
if(!v_.equals("")) v = Integer.parseInt(v_);
		
if(op.equals("=")) {
  // 저장한 데이터 key값으로 불러오기
	int x = (Integer)application.getAttribute("value");
	int y = v;

	String operator = (String)application.getAttribute("op");
	int result = 0;
	
  // 계산식
  if(operator.equals("+"))
  	  result = x+y;
  else
		  result = x-y;
			
      // 웹 브라우저로 결과 출력
  	  response.getWriter().printf("result is %d\n", result);
}
else {
  // 데이터 저장
	application.setAttribute("value", v);
	application.setAttribute("op", op);	
}
```

<br>

- HTML
``` HTML
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form action="calc2" method="post">
		<div>
			<label>입력 : </label> 
			<input type="text" name="v"/>
		</div>
		<div>
			<input type="submit" name="operator" value="+" />
			<input type="submit" name="operator" value="-" />
			<input type="submit" name="operator" value="=" />
		</div>
		<div>
			결과 : 0
		</div>
	</form>
</body>
</html>
```
<hr><br>
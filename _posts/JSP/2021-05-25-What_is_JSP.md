---
title: JSP란 (Java Server Pages)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories: JSP
toc: true
toc_sticky: true
toc_label: 목차
description: JSP의 개념과 문법을 이해한다.
article_tag1: JSP의 개념, 동작 과정, 특징과 문법을 이해한다.
article_tag2: JSP에서 동적인 코드를 호출하는 6가지 전략
article_tag3: Action 태그와 JSP EL, Scriptlet 태그와 JSTL
article_section: Java 언어를 기반으로 하는 Server Side 스크립트 언어에 대해 배운다.
meta_keywords: Servlet, Application, Session, Cookie
last_modified_at: '2021-05-25 00:00:00 +0800'
---

# JSP(Java Server Pages)란

> Java 언어를 기반으로 하는 Server Side 스크립트 언어
<br>

- HTML 코드에 Java 코드를 넣어 동적인 웹 페이지를 생성하는 웹 어플리케이션 도구
  - JSP를 통해 정적인 HTML과 동적으로 생성된 Contents(HTTP 요청 파라미터)를 혼합하여 사용할 수 있다.
  - 즉, 사용자가 입력한 Contents에 맞게 동적인 웹 페이지를 생성한다.
<br>

![jsp-example](https://user-images.githubusercontent.com/61576254/120657832-d2d67600-c4bf-11eb-9a88-6223b146c708.png)

<br>

- Servlet 기술의 확장
  - Servlet을 보완한 스크립트 방식 표준
  - Servlet의 모든 기능 + 추가적인 기능
<br>

![jsp-definition](https://user-images.githubusercontent.com/61576254/120657933-f13c7180-c4bf-11eb-8686-29df22e2e954.png)

<br>

### JSP의 내부적인 동작 과정

> JSP 문서는 백 그라운드에서 Servlet으로 자동으로 변환된다.

![jsp-process](https://user-images.githubusercontent.com/61576254/120658130-1f21b600-c4c0-11eb-8f41-e93ec28a71fc.png)

<br>

1. JSP가 실행되면 WAS는 내부적으로 JSP 파일을 Java Servlet(.java)으로 변환한다.
2. WAS는 이 변환한 Servlet을 동작하여 필요한 기능을 수행한다.
   - WAS는 사용자 요청에 맞는 적절한 Servlet 파일을 컴파일(.class 파일 생성)한다.
   - .class 파일을 메모리에 올려 Servlet 객체를 만든다.
   - 메모리에 로드될 때 Servlet 객체를 초기화하는 **init()** 메서드가 실행된다.
   - WAS는 Request가 올 때 마다 **thread를 생성하여** 처리한다.
   - 각 thread는 Servlet의 단일 객체에 대한 **service()** 메서드를 실행한다.
   - service() 메서드는 요청에 맞는 적절한 메서드(doGet, doPost 등)을 호출한다.
3. 수행 완료 후 생성된 데이터를 웹 페이지와 함께 클라이언트로 응답한다.
<br><br>

### JSP의 특징

- 스크립트 언어이기 때문에 자바 기능을 그대로 사용할 수 있다.
- Tomcat(WAS)이 이미 만들어놓은 객체(predefined values)를 사용한다.
  - Ex. request, response, session 등
- 사용자 정의 태그(custom tags)를 사용하여, 보다 효율적으로 웹 사이트를 구성할 수 있다.
  - **JSTL**(JSP Standard Tag Library, JSP 표준 태그 라이브러리)사용
- HTML 코드안에 Java 코드가 있기 때문에 HTML 코드를 작성하기 쉽다.
- Servlet과 다르게 JSP는 수정된 경우 재배포할 필요 없이 Tomcat(WAS)이 알아서 처리해준다.
<br><br>

#### 참고1 Predefined Values(또는 Implicit Object)

- 미리 정의된 객체로, WAS가 제공하는 객체를 의미한다.
  - request: the HttpServletRequest Object
  - response: the HttpServletResponse Object
  - session: the HttpSession Object
  - out: the PrintWriter Object
  - application: the ServletContext Object
- 구체적인 내용은 www.javatpoint.com 참고
<hr>

# JSP 문법

### 1. JSP Expression

```<%= expression %>```
<br>

- JSP Expression elements는 **String으로 변환되어** Servlet의 출력에 삽입된다.
- 동적인 페이지를 생성한다.
- 끝에 세미콜론(;)을 붙이지 않는다.
<br>

![jsp-expression-example](https://user-images.githubusercontent.com/61576254/120658185-2e086880-c4c0-11eb-94ef-0364f50a2475.png)

<br>

### 2. JSP Scriptlet

```<% code fragment %>```
<br>

- 간단한 값이 아닌 조금 더 복잡한 것을 수행하고자 할 때 JSP Scriptlet을 사용한다.
- 임의의 Java 코드를 삽일할 수 있다.
- JSP Scriptlet Tag는 메서드가 아닌 변수만 선언할 수 있다.
<br>

![jsp-scriptlet-example](https://user-images.githubusercontent.com/61576254/120658315-47111980-c4c0-11eb-8404-b7aeb9fc907b.png)

<br>

### 3. JSP Declaration

```<%! declaration %>```
<br>

- JSP Declaration을 사용하면 Servlet 클래스에 삽입되는 메서드나 필드를 정의할 수 있다.
- JSP Scriptlet Tag와 달리 JSP Declaration Tag는 메서드와 변수 모두 선언할 수 있다.
<br>

![jsp-declaration-example](https://user-images.githubusercontent.com/61576254/120658637-90616900-c4c0-11eb-83f7-e26d3ec14c56.png)

<br>

### 4. JSP Comment

```<%-- comments --%>```
<br>

- 주석의 개념
<br>

### 5. JSP Directive

```<%@ directive %>```
<br>

- JSP 페이지의 전체적인 구조에 영향을 미친다.
- 전체 구조에 대해 WAS에 지시를 내린다.
- 지시어에 들어가는 것: **page**, **include**, **taglib**
<br>

![jsp-directive-example](https://user-images.githubusercontent.com/61576254/120658376-585a2600-c4c0-11eb-9c8f-18683bf0494f.png)

<br>

1. page
   - ```<%@ page attribute = "value" %>```
   - page 지시어는 Container에 명령을 제공하는데 사용된다.
2. include
   - ```<%@ include file = "relative_url" %>```
   - include 지시어는 변환 단계에서 다른 외부 파일의 내용을 현재 JSP에 병합하도록 Container에 지시한다.
3. taglib
   - ```<%@ taglib uri = "uri" prefix = "prefixOfTag" %>
   - JSP API를 사용하면 HTML 또는 XML 태그처럼 보이는 사용자 정의 태그(custom tags)를 정의할 수 있다.
     - JSTL(JSP Standard Tag Library, JSP 표준 태그 라이브러리)사용
   - tag library는 사용자가 정의한 동작을 구현한 사용자 정의(user-defined)태그 집합이다.
<br>

### 6. JSP Action

- JSP Action XML 구문 안의 구조들을 사용하여 WAS의 동작을 제어한다.
1. ```<jsp:forward>``` action
   - 다른 리소스(JSP, html 또는 Servlet과 같은 정적 페이지)로 요청을 전달하는데 사용한다.
2. ```<jsp:include>``` action
   - 현재 JSP 페이지에 다른 리소스를 포함시키는데 사용한다.
3. ```<jsp:useBean>``` action
   - 해당하는 Bean(자바 객체)이 이미 존재하는지 확인한다.
   - 객체가 없으면 지정된 객체를 생성한다.
4. ```<jsp:setProperty>``` action
   - Bean(자바 객체)의 속성을 설정한다.
5. ```<jsp:getProperty>``` action
   - 주어진 속성값을 가져오는데 사용되며 이를 문자열로 변환하고 동적인 웹 페이지를 생성하는데 해당 내용을 사용할 수 있다.
<br>

- 용도
  - 동적으로 파일을 삽입하고
  - JavaBeans 구성 요소를 재사용하고
  - 사용자를 다른 페이지로 전달(forward)할 수 있다.
- 예시
<br>

  ![jsp-action-example](https://user-images.githubusercontent.com/61576254/120658439-67d96f00-c4c0-11eb-8c58-8008fbbe6de3.png)
  - 구체적인 예시는 www.javapoint.com 참고
<hr><br>

> 주기적으로 추가할 예정
> 출처: https://gmlwjd9405.github.io/2018/11/03/jsp.html

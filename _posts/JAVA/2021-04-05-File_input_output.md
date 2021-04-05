---
title: Java File Input, Output(파일 입출력)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories: JAVA
toc: true
toc_sticky: true
toc_label: 목차
description: Java로 파일을 읽고 쓰는 방법을 이해한다.
article_tag1: 파일 쓰기
article_tag2: 파일에 내용 추가하기
article_tag3: 파일 읽기
article_section: Java를 이용한 파일 읽고 쓰기
meta_keywords: Java, FileInputOutput
last_modified_at: '2021-04-05 22:00:00 +0800'
---

# 파일 쓰기

## 파일에 내용쓰기
Java로 파일을 쓰는 방법은 여러가지 방법이 존재한다. <br>
- FileOutStream 이용하기 <br>


``` java
import java.io.FileWriter;
import java.io.IOExeption;

public class FileWrite {
  public static void main(String[] args) throws IOException {
    FileOutputStream output = new FileOutputStream("파일 생성할 경로");
    for(int i=1; i<11; i++) {
      String data = i+" 번째 줄입니다.\n";
      output.writer(data.getBytes());
    }
    output.close();
  }
}
```
- 위 방법은 Byte(바이트) 단위로 데이터를 처리하는 클래스이다. <br><br>

- FileWriter 이용하기 <br>


``` java
import java.io.FileWriter;
import java.io.IOException;

public class FileWrite {
  public static void main(String[] args) throws IOException {
    FileWriter fw = new FileWriter("파일 생성할 경로");
    for(int i=1; i<11; i++) {
      String data = i+" 번째 줄입니다.\n";
      fw.writer(data);
    }
    fw.close();
  }
}
```
- 위 방법은 Byte(바이트) 대신 문자열을 직접 파일에 쓸 수가 있다. <br><br>

- PrintWriter 이용하기 <br>


```java
import java.io.PrintWriter;
import java.io.IOException;

public class FileWrite {
  public static void main(String[] args) throws IOException {
    PrintWriter pw = new PrintWriter("파일 생성할 경로");
    for(int i=1; i<11; i++) {
      String data = i+" 번째 줄입니다.";
      pw.writer(data);
    }
    pw.close();
  }
}
```
- 위 방법은 문자열을 직접 파일에 쓰는 방식이다.
- `System.out.println`와 같은 의미이고 콘솔대신 파일로 출력하는 방법이다.

---
<br>

## 파일에 내용 추가하기

이미 작성된 파일을 다시 **추가모드**로 열어 내용을 추가하는 방식이다. <br>

- FileWriter 방식 <br>


``` java
import java.io.FileWriter;
import java.io.IOException;

public class FileWrite {
    public static void main(String[] args) throws IOException {
        // 파일 생성 및 쓰기
        FileWriter fw = new FileWriter("파일 생성 경로");
        for(int i=1; i<11; i++) {
            String data = i+" 번째 줄입니다.\r\n";
            fw.write(data);
        }
        fw.close();

        // 파일 내용 추가
        FileWriter fw2 = new FileWriter("파일이 존재한 경로", true);
        for(int i=11; i<21; i++) {
            String data = i+" 번째 줄입니다.\r\n";
            fw2.write(data);
        }
        fw2.close();
    }
}
```
- new FileWrite(파일명, 추가모드구분)
  - 추가모드구분은 Boolean 타입이다. <br><br>

- PrintWrite 방식 <br>


``` java
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;

public class FileWrite {
    public static void main(String[] args) throws IOException {
        PrintWriter pw = new PrintWriter("파일 생성 경로");
        for(int i=1; i<11; i++) {
            String data = i+" 번째 줄입니다.";
            pw.println(data);
        }
        pw.close();


        PrintWriter pw2 = new PrintWriter(new FileWriter("파일이 존재한 경로", true));
        for(int i=11; i<21; i++) {
            String data = i+" 번째 줄입니다.";
            pw2.println(data);
        }
        pw2.close();
    }
}
```
- `FileWrite`와 다른점은 생성자 뿐이다.

---
<br>

# 파일 읽기

> 작성된 파일을 **Console** 창에 나타내주는 방법이다.
>> 방법은 2가지가 존재한다. <br>


- FileInputStram 방식 <br>


``` java
import java.io.FileInputStream;
import java.io.IOException;

public class FileRead {
    public static void main(String[] args) throws IOException {
        byte[] b = new byte[1024];
        FileInputStream input = new FileInputStream("파일이 존재한 경로");
        input.read(b);
        System.out.println(new String(b));
        input.close();
    }
}
```
- 위 방법은 byte(바이트) 배열을 이용하여 파일을 읽는다.
  - 이 방법은 정확한 길이를 모를 경우에는 불편한 방법이다. <br><br>

- BufferedReader 방식 <br>


``` java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileRead {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("파일이 존재한 경로"));
        while(true) {
            String line = br.readLine();
            if (line==null) break;
            System.out.println(line);
        }
        br.close();
    }
}
```
- 위 방법은 라인단위로 파일을 읽을 수 있다.
  - **FileReader**와 **BufferedReader**의 조합
  - BufferedReader의 **readLine** Method는 더이상 읽을 라인이 없을 경우 **null**을 리턴한다.

---
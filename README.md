# PHP (Professional HTML Preprocessor)

## 목차

- [PHP? JSP? ASP?](#php-jsp-asp)
- [PHP의 시작과 끝](#php의-시작과-끝)   
- [PHP에서의 주석처리](#php에서의-주석처리)
- [출력문](#출력문)


<br><br>

-----

## PHP? JSP? ASP?   

```
- PHP (Personal Hypertext Preprocessor)   

: PHP는 1994년 Rasmus Lerdort가 개인 홈페이지를 만들기 위해 처음 고안하였으며 현재 세계에서 가장 많이 사용하고 있는 아파치 웹 서버에 모듈형태로 장착되어 활용되고 있다.
PHP는 서버의 운영체제가 윈도우뿐만 아니라 유닉스와 리눅스 운영체제에서도 사용이 가능한 서버측 스크립트 언어이다.

PHP는 JSP의 JDBC나 ASP의 ODBC와 같은 보조적인 메커니즘을 사용하지 않고 함수를 통하여 바로 처리될 수 있는 방식을 채택하고 있어 초보자가 웹 언어를 배우기에 가장 적합한 장점을 지니고 있다.
그리고 모든 데이터베이스에 대해 자체 라이브러리를 지원하고 있기 때문에 다양한 데이터베이스(Oracle, MySQL, dbase, Informix, unix dbm 등)를 활용할 수 있다.

PHP는 C언어를 기반으로 만들어져 서버에서 실행되는 스크립트언어로 C언어에 자신있는 개발자들에게는 보다 쉽게 접근할 수 있다는 장점이 있지만, 컴포넌트를 사용할 수 없는 점과 취약한 보안을 강구해야 하는 단점이 존재한다.
그렇지만, 빠른 생산성과 저렴한 유지비용으로 프로그래밍 속도를 높여준다는 매력적인 부분 또한 존재하기 때문에 많이 사용되고 있다.
```

<br>

```
- JSP (Java Server Page)

: JSP는 Sun Microsystems사에서 만든 웹 언어이며 순수한 자바를 기반으로 한 스크립트 언어이다.
기존의 HTML에 프로그램 언어를 사용할 수 있게 하는 기술을 접목하여 컴파일 등의 역할을 서버 측에서 담당하도록 하는 방식으로 구현된다.

JSP는 일반적인 웹 페이지의 형태를 나타내는 HTML 태그로 구현되는 부분과 웹 페이지를 동적으로 생성하는 서버측 프로그램 즉, 서블릿을 수행하도록 JSP 태그로 구현되는 부분으로 소스가 생성되어 처리된다.
또한, JavaBeans 지원기증을 사용하여 정보를 최종 사용자에게 보여주는 프레젠테이션과 사용자들에게 보여주기 위해 사용되는 코드의 프로그램 구현이 완벽하게 분리될 수 있으며 Java 언어를 활용하여 동적 컨텐츠를 구현할 수 있다.

JSP는 서블릿 기술을 활용한 수행 흐름으로 서버에서의 수행능력이 뛰어나며 플랫폼과 웹 서버에 독립적으로 구현 가능하다는 장점이 있다.
또한, 컴포넌트를 활용하여 프레젠테이션 부분과 프로그램 기능 구현 부분으로 분리하여 개발 할 수 있으며 자바의 특징을 그대로 사용할 수 있다는 장점이 있는 반면, 코딩이 어렵고 ASP에 비해 코드를 입력해야 하는 양이 1.5배가량 더 많다는 단점이 존재한다.
그렇지만, JVM(Java Virtual Machine)이라는 프로그램이 운영체제 위에 설치되어 가동되면 모든 운영체제(유닉스, 리눅스, 윈도우)에서 사용할 수 있기 때문에 코딩이 어려워도 많이 사용되고 있는 추세이다. 
```

```
- ASP (Active Server Page)

: ASP는 Microsoft사에서 개발한 웹 언어로서 윈도우용에서만 제작 가능한 플랫폼을 지원하고 있으며 윈도우 2000 서버의 IIS(Internet Information Server) 또는 윈도우 98/ME의 PWS(Personal Web Server)만을 지원한다.
사용되는 언어로는 비주얼베이직이나 자바이며 OLE(Object Linking and Embedding) 데이터베이스를 기반으로 ADO(Active Data Objects)의 연결은 MS-SQL 데이터베이스를 사용한다.

ASP는 Microsoft사에서 만든 Visual Basic 언어를 기반으로 스크립트 방식을 사용하여 동적인 웹페이지를 작성할 수 있도록 지원한다.
쉽게 표현하면 서버에서 실행하는 스크립트 언어를 의미하며 ActiveX를 제공하는 컴포넌트를 사용하거나 직접 개발하기 위한 기능도 제공한다.

ASP의 장점은 적당히 빠른 생산성과 편리성을 들 수 있으며 MS사에서 개발한 MS-SQL을 적용하기가 편리하다.
윈도우 운영체제 기반에서 구동되므로 유지보수 측면에서는 수월하며 비즈니스 로직을 구현하기에도 편리함을 제공한다.

하지만, ASP는 구축과정에서 높은 비용을 투자해야 한다는 단점이 있다.
그 이유는 특정한 기능을 구현하려면 컴포넌트를 구입해야 한다는 점이다.
무엇보다도 ASP의 치명적인 단점을 꼽는다면 특정 플랫폼과 특정 웹 서버(IIS)에서만 동작한다는 부분과 PHP보다 코딩양이 많다는 점이다.
```

<br>

-----

## 웹 서버와 클라이언트

<br>

-----

## PHP의 시작과 끝

### - php의 시작

```
<?php
```

-> php의 시작을 나타낸다.

### - php의 끝 

```
?>
```

-> php의 끝을 나타낸다.   
-> php만 단독으로 쓰일 땐 생략 가능하다. 

<br>

*참고

```
1. <? ... ?>  // 보편적인 방법

2. <?php ... ?>  // XML이나 XHTML 안에 PHP 코드를 내장시켜 사용할 때의 방법

3. <script language = "php"> ... </script>  // PHP가 스크립트 언어임을 표현하는 방법
```

-> XML이나 XHTML 안에 PHP 코드를 내장시켜 사용하고자 할 때는 확실한 구분을 위해 <?php ...?>형을 사용하는 것이 좋다.


<br>

-----


## PHP에서의 주석처리

### - 한 줄 주석

```
// 한 줄 주석입니다.
# 한 줄 주석입니다.
```

### - 여러 줄 주석

```
/*
여러 줄 주석입니다.
여러 줄 주석입니다.
여러 줄 주석입니다.
여러 줄 주석입니다.
여러 줄 주석입니다.
*/
```

<br>

-----

## 출력문

```
### - echo
### - print
```

-> C언어의 printf() 함수와 같은 의미로, 대소문자를 구별하지 않는다.

<br>

-----


---
title: DAO & DTO
date: 2018-08-22 22:26:20
tags:
- DAO
- DTO
categories:
- Programing
- JDBC
---

* #### DTO, Data Transmission Object
 (프레임워크 단에서 주로 쓰이는 용어)
 - 데이터 전송 객체
 - VO (Value Object)  
 - 계층간 데이터 교환을 위한 자바 클래스
   ( Java Beans:  , JAVA EE(EnterPrise : 웹이나 대규모 플젝할 때 쓰임, (JAVA SE (기본))) - 이쪽에서  주로 사용하는 용어)

 - DTO 클래스 명은 테이블의 이름과 같게 하는 것이 좋다
 - 멤버 필드는 모두 private
	(데이터베이스 테이블의 컬럼명과 같게 하는 것이 좋다)
 - 메소드는 getter, setter, toString() 만 작성


  *** __VO__ : 데이터로만 이뤄진 객체
  &nbsp;&nbsp;&nbsp;&nbsp;__DTO__ :  VO 랑 거의 같은 의미. 전송을 목적으로 했을 때 DTO 라고 씀 *


* #### DAO, Data Access Object
	- Database의 데이터에 접근하기 위한 객체
	- 데이터베이스에 수행할 SQL 문을 하나의 메소드의 기능으로 구현하여 모아놓은 객체

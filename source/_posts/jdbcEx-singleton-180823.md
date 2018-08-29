---
title: Singleton Pattern을 이용한 Ojdbc 활용 예제 _0823
date: 2018-08-23 14:16:56
tags:
- Singleton
categories:
- Programing
- JDBC
---

이전 포스팅에서 DTO, DAO를 이용하여 Ojdbc를 활용한 DB작업을 했었다.

아래는 이전 포스팅의 UserDaoImpl 클래스 생성자의 한 부분이다.

{% codeblock UserDaoImpl.java lang:java %}
// 드라이버 로드
Class.forName(DRIVER);
// DB 연결
conn = DriverManager.getConnection(URL, USERNAME, PASSWORD);
{% endcodeblock %}

만약 여러 DAO 클래스를 작성한다면,
위의 코드가(DB 연결객체 생성 코드) 계속 중복해서 쓰이기 때문에 DAO 클래스의 개수만큼 DB와의 연결이 수립된다.
-> __싱글톤 패턴으로 해결한다__

{% codeblock DBConn.java lang:java %}
package dbutil;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DBConn {
	// DB 연결 정보
	public static final String DRIVER = "oracle.jdbc.driver.OracleDriver";
	public static final String URL = "jdbc:oracle:thin:@localhost:1521:xe";
	public static final String USERNAME = "scott";
	public static final String PASSWORD = "tiger";

	// DB 연결객체
	private static Connection conn = null;

	// private 생성자
	private DBConn(){
	}

	// Connection 객체 반환 = Singleton Pattern
	public static Connection getConnection() {

		// DB 연결이 안되어있을 때만 동작
		if (conn == null) {
			try {
				Class.forName(DRIVER); //드라이버 로드

				// DB 연결객체 생성
				conn = DriverManager.getConnection(URL, USERNAME, PASSWORD);
			} catch (ClassNotFoundException e) {
				e.printStackTrace();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return conn;
	}
}
{% endcodeblock %}

위 처럼 DB 연결객체를 싱글톤으로 사용할 수 있도록 따로 클래스를 만들어 준다.

이제 아래의 클래스처럼 객체를 싱글톤으로 얻어 사용하면 된다.

{%codeblock UserDaoImpl2.java lang:java %}
public class UserDaoImpl2 implements UserDao{

	// DB 연결 객체 -> 싱글톤
	private static Connection conn = DBConn.getConnection();

	// JDBC 객체
	private PreparedStatement ps;
	private ResultSet rs;

	// ...(생략)...
}
{% endcodeblock %}

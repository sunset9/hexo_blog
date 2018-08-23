---
title: Ojdbc 활용 예제(USER) _0822
date: 2018-08-23 12:26:42
tags:
categories:
- Programing
- JDBC
---

JDBC를 이용해 USERTEST테이블에 접근하여 몇 가지 쿼리를 수행한다.

이전 포스팅의 예제에서는 main 함수가 있는 클래스에 DB 연결, SQL 문 수행 등 모든 작업이 한 번에 이루어 졌었다.
이번에는 __DAO를 이용하여__ 코드를 작성하였다.

[패키지 구성]
 user
	├ dao
	│   ├ UserDao.java (인터페이스)
	│   └ UserDaoImpl.java
	│
	├ dto
	│   └ User.java
	└ ex
	&nbsp;&nbsp;&nbsp;&nbsp;└ UserEx.java
		   

		 
### UserDao 인터페이스
```java
package user.dao;

import java.util.List;

import user.dto.User;

public interface UserDao {

	//UserTest 테이블 전체 조회
	//	idx 정렬
	public List<User> selectAll();
	
	// idx를 이용한 UserTest 조회
	//	1명이 조회되도록 한다
	public User selectByIdx(int idx);
	
	// User 삽입
	public void insertUser(User insertUser);
	
	// idx를 이용한 UserTest 삭제
	public void deleteByIdx(int idx);	
}
```

### UserDaoImpl.java
```java
package user.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import user.dto.User;

public class UserDaoImpl implements UserDao{
	
	// DB 연결 정보
	private final String DRIVER = "oracle.jdbc.driver.OracleDriver";
	private final String URL = "jdbc:oracle:thin:@localhost:1521:xe";
	private final String USERNAME = "scott";
	private final String PASSWORD = "tiger";
	
	// DB 연결 객체
	private Connection conn;
	// JDBC 객체
	private PreparedStatement ps;
	private ResultSet rs;
	
	public UserDaoImpl() {
		try {
			// 드라이버 로드
			Class.forName(DRIVER);
			
			conn = DriverManager.getConnection(URL, USERNAME, PASSWORD);
			
			// 오토커밋 설정(기본값 : true)
			// 오토커밋 시 중간에 에러나서 프로그램종료되면 자동커밋, 데이터 깨질 수 있음
			conn.setAutoCommit(false); 
			// 이러면 commit, rollback 관리를 명시적으로 해줘야함
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	
	@Override
	public List<User> selectAll() {
		String sql = "SELECT * FROM userTest ORDER BY idx";
		List<User> userList = new ArrayList<>();
		
		try {
			ps = conn.prepareStatement(sql);
			rs = ps.executeQuery();
			
			while(rs.next()) {
				User user = new User();
				
				user.setIdx(rs.getInt("idx"));
				user.setUserid(rs.getString("userid"));
				user.setName(rs.getString("name"));
				
				userList.add(user);
			}
			
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				rs.close();
				ps.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return userList;
	}

	@Override
	public User selectByIdx(int idx) {
		String sql = "SELECT * FROM userTest WHERE idx = ?";
		User user = null;
		
		try {
			ps = conn.prepareStatement(sql);
			
			ps.setInt(1, idx);
			rs = ps.executeQuery();
			
			user = new User();
			if(rs.next()) {
				user.setIdx(rs.getInt("idx"));
				user.setName(rs.getString("name"));
				user.setUserid(rs.getString("userid"));
			} else {
				System.out.println("** 조회: 해당 IDX에 해당하는 유저가 없습니다.");
				return null;
			}
			
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				rs.close();
				ps.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return user;
	}

	@Override
	public void insertUser(User insertUser) {
		String userId = insertUser.getUserid();
		String userName = insertUser.getName();
		String sql = "INSERT INTO userTest(idx, userid, name) VALUES (userTest_SQ.nextval,?,?)";
		String sql2 = "SELECT COUNT(*) FROM userTest WHERE userid = upper(?)";
		
		try {
			// 중복 아이디 체크
			PreparedStatement ps2 = conn.prepareStatement(sql2);
			ps2.setString(1, userId);
			rs = ps2.executeQuery();
			rs.next();
			// 해당 아이디가 있다면 추가 X
			if(rs.getInt(1) > 0) {
				System.out.println("** 삽입: 같은 ID 가 존재합니다.");
			} else {
				// user 추가
				ps = conn.prepareStatement(sql);
				ps.setString(1, userId);
				ps.setString(2, userName);
				
				ps.executeUpdate();
			}
			
			conn.commit(); // 명시적으로 커밋하기
			
		} catch (SQLException e) {
			e.printStackTrace();
			
			try {
				conn.rollback(); // 예외 발생 시 롤백 
			} catch (SQLException e1) {
				e1.printStackTrace();
			}
		} finally {
			try {
				rs.close();
				ps.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}

	@Override
	public void deleteByIdx(int idx) {
		String sql = "DELETE userTest WHERE idx = ?";
		
		try {
			ps = conn.prepareStatement(sql);
			ps.setInt(1, idx);
			
			if( ps.executeUpdate() == 0) {
				System.out.println("** 삭제: 해당 IDX에 해당하는 유저가 없습니다.");
			}
			
			conn.commit(); // 명시적으로 커밋하기
			
		} catch (SQLException e) {
			e.printStackTrace();
			
			try {
				conn.rollback(); // 예외 발생 시 롤백 
			} catch (SQLException e1) {
				e1.printStackTrace();
			}
		} finally { 
			try {
				ps.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}
}
```

** 메소드 안의 catch문에서 자원 해제할 때 conn.close() 는 하면 안된다. 연결 객체를 해제해버리면 다른 메소드에서 접근 할 수 없다.
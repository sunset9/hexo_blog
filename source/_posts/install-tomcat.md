---
title: 톰캣 설치 및 적용
date: 2018-08-27 21:45:43
tags:
- Tomcat
categories:
- Programing
- Web
---

톰캣 서버를 설치하고 이클립스에 올려 실행하고자 한다.
기존에 이클립스를 Standard 버전을 쓰고 있었는데 해당 버전은 웹 프로젝트에 대한 지원이 안되기 때문에 톰캣 설치에 앞서 우선 이클립스 EE 버전을 새로 설치하려고 한다.

* __Eclipse IDE for Java EE Developers 다운로드__
-> 오른쪽 위에 ! 가 떠 있으면 선택해서 update 진행 (설치 후 installer 종료하면 update 다시 해야 함)
-> ! 사라지면 EE 버전 다운로드 진행

![](https://user-images.githubusercontent.com/42576587/44789210-f6fe1d80-abd6-11e8-8157-de574b5abc9a.png)
나는 SE 버전을 설치한지 몇 달 됐기 때문에 그 사이에 업데이트 사항이 생겨서..이 과정을 해줘야 했다.

이제 톰켓 웹 서버를 다운받아보자.
* __톰켓 웹 서버 다운로드__
<http://tomcat.apache.org/>
\- 왼쪽 Download 항목에서 Tomcat 9 클릭
\- 아래쪽 9.0.11 항목에서
	Core:
	&nbsp;&nbsp;&nbsp;&nbsp;64-bit Windows zip 클릭해서 다운

윈도우에 올려서 사용하는게 아니라 이클립스에 올려서 사용할 예정이다.
그러므로 톰캣 다운받을 때 ZIP 파일로 받아야한다. (WINDOW INSTALLER 이 아닌)

이제 마지막으로 다운 받은 톰캣을 이클립스에 올려보자.

* __이클립스에 Server Runtime 추가__
Window 메뉴
\- Preferences 항목
&nbsp;&nbsp;&nbsp;&nbsp;\- Server 항목
&nbsp;&nbsp;&nbsp;&nbsp;\- Runtime Environments
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Add... 버튼 클릭
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Apache Tomcat v9.0 선택
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- Browser 버튼 -> 압축해제한 Tomcat Directory 선택하고 완료

해당 톰캣 폴더가 이클립스 내부 폴더로 복사됨
서버가 설치된게 아니라 서버를 만들 수 있는 환경(서버 실행 환경)이 구축된 것이다.

* 이제 __New -> Server__ -> Tomcat v9.0 Server 을 선택해 완료하면 하나의 서버가 만들어진다!

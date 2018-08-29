---
title: Web Project와 서버 연결하기
date: 2018-08-27 23:01:41
tags:
categories:
- Programing
- Web
---

Dynamic Web Project를 서버에서 실행시키기 위해서 서버와 프로젝트를 연결시켜줘야 한다.

__방법1.__

![](https://user-images.githubusercontent.com/42576587/44795744-68919800-abe6-11e8-8ca7-49cbae653ef3.png)
Server 뷰에서 원하는 톰캣 서버를 우클릭하여 'Add and Remove' 을 누른다.

![](https://user-images.githubusercontent.com/42576587/44794497-9c1ef300-abe3-11e8-8e7a-d7919d13c33d.png)
후에 원하는 프로젝트를 'Add' 해준다. (Front라는 이름의 프로젝트이다.)


__방법2.__
![](https://user-images.githubusercontent.com/42576587/44795070-cc1ac600-abe4-11e8-8aeb-a4868c43e578.png)
Server 뷰에서 원하는 톰캣 서버를 더블클릭한다.
노란색 박스로 표시된 'Add Web Module...'을 클릭하면 위와 같은 창이 뜬다.

__\* Document Base:__ 실제 파일이 저장된 경로
__\* Path:__ 논리적인 URL 에서 인정되는 경로

브라우저에서 Path에 작성해놓은 경로를 치면 Document Base에 작성된 프로젝트 안에서 파일을 찾는다.
ex) Path 를 /lala 로 해놓았고 Front라는 프로젝트의 hi.html을 로드하려면,
웹 브라우저의 url에 localhost:port번호/lala/hi.html 라고 작성하면 된다.

방법1로 추가시켰을 경우에는 Path가 자동으로 Document Base와 똑같이 설정된다.

\* Modules 설정 변경했으면, 서버를 재실행 시켜줘야한다.

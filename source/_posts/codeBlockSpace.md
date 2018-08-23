---
title: 코드블럭 스타일 바꾸기 (수정예정)
date: 2018-08-23 10:17:45
tags:
---

* ### 코드블럭의 탭 간격 바꾸기
_config.yml 파일에서
```
highlight:
	tab_replace: '    '
```
tab_replace 에 원하는 만큼의 간격을 넣어준다.

간단하게 바꿀 수 있는 거였는데, 별로의 스타일 파일을 넣어주거나 하는 식의 방식으로 하는 줄알고 엄청 헤맸다.

* ### 코드블럭의 하이라이트 스타일 바꾸기
현재 HUEMAN 테마를 사용 중이다.

themes\hueman\_config.yml 파일을 열어
```
highlight theme: 
```
를 바꿔준다. 바꿔주려는 명은 css\highlight에 존재하는 파일명중 하나로 바꿔주면 된다.
 
하이라이트 스타일을 바꾸는 방법은 HUEMAN공식 문서에 존재?한다.

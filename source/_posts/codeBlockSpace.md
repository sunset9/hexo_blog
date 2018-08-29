---
title: 코드블럭 스타일 바꾸기
date: 2018-08-23 10:17:45
tags:
---

* ### 코드블럭의 탭 간격 바꾸기
_config.yml 파일에서
```
highlight:
	tab_replace: '    '
```
`tab_replace:`에 원하는 만큼의 간격을 넣어준다.

간단하게 바꿀 수 있는 거였는데, 별로의 css 파일을 수정하거나 플러그인을 따로 설치하는건가 싶어 엄청 헤맸다..

* ### 코드블럭의 하이라이트 스타일 바꾸기
현재 HUEMAN 테마를 사용 중이다.

themes\hueman\\_config.yml 파일을 열어
```
customize:
	highlight:
```
`highlight:` 에 원하는 스타일명을 넣어주면 된다. 바꿔주려는 명은 css\highlight에 존재하는 파일명중 하나로 바꿔주면 된다.

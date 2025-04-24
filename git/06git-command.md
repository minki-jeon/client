
	2) git 명령어
	  - `git branch` : 브랜치 목록, (* 표시 = 현재 브랜치)
``` //* 브랜치 실습
	$ git branch
	master
	* second
	$ git checkout master
	$ git branch
	* master
	second
	$ git checkout second
	$ git branch
	master
	* second
```

	  - `git log --oneline --all --graph` : 커밋 기록을 그래프 형식으로 출력
	  - `git switch {브랜치명}`	: 브랜치 이동 (= checkout 명령어 동일)
	  - `git switch -c {브랜치명}` : 브랜치 만들고 이동

``` //* 커밋 로그 그래프형 실습
	$ git log --oneline --all --graph
	* 31a440e (HEAD -> second) 555 추가
	* 9b89231 444 추가
	| * 530d489 (master) eee 추가
	| * e79da7b ddd 추가
	|/
	* e4738a7 CCC 추가
	* 86d8501 BBB 추가
	* ef7effd first commit	
	$ git switch master
	$ git switch second
```

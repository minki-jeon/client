
	7) log reader 조작키
	  - [J],[K],[화살표위/아래] : 텍스트 화면 위 아래 이동
	  - [Q]	: 빠져나가기
	8) log 옵션
	  - git log -{숫자}	: 커밋 로그 출력 개수
	  
	9) 3way merge : 서로 다른 길을 간 두 브랜치의 통합
					, 두 브랜치가 가리키는 두 커밋을 부모로 두는 새 커밋 (merge commit)이 생성
					//* 3개의 커밋을 관여하는 merge

```	//* 3way merge 실습
	$ git log --oneline --all --graph -5
	* 50cb261 (HEAD -> feat2) add c
	* 5046b5a add b
	| * 8401a0c (feat1) add b
	| * 8aa19d8 add a
	|/
	* 1b85947 (master) 88 추가
	$ git switch master
	Switched to branch 'master'
	$ git merge feat2
	Updating 1b85947..50cb261
	Fast-forward
	 b.txt | 2 ++
	 1 file changed, 2 insertions(+)
	$ git log --oneline --all --graph -5
	* 50cb261 (HEAD -> master, feat2) add c
	* 5046b5a add b
	| * 8401a0c (feat1) add b
	| * 8aa19d8 add a
	|/
	* 1b85947 88 추가
	$ git branch -d feat2
	Deleted branch feat2 (was 50cb261).
	$ git log --oneline --all --graph -5
	* 50cb261 (HEAD -> master) add c
	* 5046b5a add b
	| * 8401a0c (feat1) add b
	| * 8aa19d8 add a
	|/
	* 1b85947 88 추가
	$ git merge feat1		//* 3way merge 발생(커밋메시지 작성을 위한 편집기 자동실행)
	Merge made by the 'ort' strategy.
	 a.txt | 2 ++
	 1 file changed, 2 insertions(+)
	$ git log --oneline --all --graph -6
	*   4a8ee25 (HEAD -> master) Merge branch 'feat1', 특정 기능 통합함
	|\
	| * 8401a0c (feat1) add b
	| * 8aa19d8 add a
	* | 50cb261 add c
	* | 5046b5a add b
	|/
	* 1b85947 88 추가
	$ git branch -d feat1
	Deleted branch feat1 (was 8401a0c).
	$ git log --oneline --all --graph -6
	*   4a8ee25 (HEAD -> master) Merge branch 'feat1', 특정 기능 통합함
	|\
	| * 8401a0c add b
	| * 8aa19d8 add a
	* | 50cb261 add c
	* | 5046b5a add b
	|/
	* 1b85947 88 추가
	$ git cat-file -p 4a8ee25		//* merge-commit 정보 확인 (parent 등)
	tree c45095215b060885ba857b96213ff49c1735b40f
	parent 50cb261b58e26dfd8c3fbe8fec5b644eb1472941
	parent 8401a0c6cc12c8a15267b42a705c31b8beaf8ea8
	author minki-jeon <minki.jeon.study@gmail.com> 1745461558 +0900
	committer minki-jeon <minki.jeon.study@gmail.com> 1745461558 +0900
	
	Merge branch 'feat1', 특정 기능 통합함
```	

``` //* 3way-merge 개인실습(복습)
	$ git switch master
	$ git log --oneline --all --graph -1
	$ git branch bug1
	$ git branch bug2
	$ git log --oneline --all --graph -1
	*   4a8ee25 (HEAD -> master, bug2, bug1) Merge branch 'feat1', 특정 기능 통합함
	|\
	$ git switch bug1
	$ echo aaa111 >> a.txt
	$ git add .
	$ git commit -m 'add aaa111 to a.txt'
	$ echo aaa222 >> a.txt
	$ git add .
	$ git commit -m 'add aaa222 to a.txt'
	$ git log --oneline --all --graph -3
	* c2a56ed (HEAD -> bug1) add aaa222 to a.txt
	* 6d8c5d5 add aaa111 to a.txt
	*   4a8ee25 (master, bug2) Merge branch 'feat1', 특정 기능 통합함
	|\
	$ git switch bug2
	$ echo bbb111 >> b.txt
	$ git add .
	$ git commit -m 'add bbb111 to b.txt'
	$ echo bbb222 >> b.txt
	$ git add .
	$ git commit -m 'add bbb222 to b.txt'
	$ git log --oneline --all --graph -5
	* 0f5c3e1 (HEAD -> bug2) add bbb222 to b.txt
	* a655483 add bbb111 to b.txt
	| * c2a56ed (bug1) add aaa222 to a.txt
	| * 6d8c5d5 add aaa111 to a.txt
	|/
	*   4a8ee25 (master) Merge branch 'feat1', 특정 기능 통합함
	|\
	$ git switch master
	$ git merge bug1
	Updating 4a8ee25..c2a56ed
	Fast-forward
	 a.txt | 2 ++
	 1 file changed, 2 insertions(+)
	$ git log --oneline --all --graph -5
	$ git branch -d bug1
	Deleted branch bug1 (was c2a56ed).
	$ git log --oneline --all --graph -5
	* 0f5c3e1 (bug2) add bbb222 to b.txt
	* a655483 add bbb111 to b.txt
	| * c2a56ed (HEAD -> master) add aaa222 to a.txt
	| * 6d8c5d5 add aaa111 to a.txt
	|/
	*   4a8ee25 Merge branch 'feat1', 특정 기능 통합함
	|\
	$ git merge bug2
	Merge made by the 'ort' strategy.
	 b.txt | 2 ++
	 1 file changed, 2 insertions(+)
	$ git log --oneline --all --graph -6	
	 *   6c54e73 (HEAD -> master) Merge branch 'bug2', merge to 'bug1'
	 |\
	 | * 0f5c3e1 (bug2) add bbb222 to b.txt
	 | * a655483 add bbb111 to b.txt
	 * | c2a56ed add aaa222 to a.txt
	 * | 6d8c5d5 add aaa111 to a.txt
	 |/
	 *   4a8ee25 Merge branch 'feat1', 특정 기능 통합함
	 |\
```
	
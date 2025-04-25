1) Git 명령어 - 커밋메시지 수정
	  - `git commit --amend -m '{커밋메시지}'`
			: 마지막 커밋 메시지 수정
	    - [커밋번호]도 변경
	  - `git branch {브랜치명} {커밋번호}`
			: 메시지 수정 이전의 커밋을 브랜치 지정하여 불러오기 (이후 merge명령어를 사용하여 복원)
	  
``` //* 커밋메시지 수정 실습
$ git commit -am 'aaddd d'

$ git log --oneline
d5bfe5d (HEAD -> master) aaddd d
3f85d90 add c
4291e63 add b
636193d a

$ git commit --amend -m 'add d'
[master 0492284] add d
 Date: Fri Apr 25 09:21:15 2025 +0900
 1 file changed, 1 insertion(+)

$ git log --oneline
0492284 (HEAD -> master) add d
3f85d90 add c
4291e63 add b
636193d a
```
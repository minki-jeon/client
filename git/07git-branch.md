	3) 브랜치(Branch) :: 브랜치 각각의 최종 버전의 커밋을 지칭하고 있다.
      - 종류 : 통합브랜치(master, main), 기능브랜치(그외)
	    - 통합브랜치: 잘 돌아가는 버전 용도
        - 기능브랜치: 기능 추가, 버그 수정, 테스트 코드 용도
	4) Merge(통합,병합) : 기능브랜치를 통합브랜치에 Merge
	  - 통합브랜치 이동 `git switch master`
	  - 기능브랜치 통합 `git merge {브랜치}`
	5) 기능 브랜치 삭제(지우기)
	  - `git branch -d {브랜치}`
```	//* [Fast-Forward] Merge 실습
	$ cd /c/learn-git
	$ mkdir repo7
    $ cd repo7
    $ git init
    $ echo a > a.txt
    $ git add .
    $ git commit -m 'a 추가'
    $ echo b >> a.txt
    $ git add .
    $ git commit -m 'b 추가'
    $ git log --oneline
	3f20de8 (HEAD -> master) b 추가
	828c85b a 추가
    $ git branch feat1
    $ git log --oneline
	3f20de8 (HEAD -> master, feat1) b 추가
	828c85b a 추가
    $ git switch feat1
    $ git log --oneline
    $ echo 1 >> a.txt
    $ git add .
    $ git commit -m '1 추가'
    $ echo 2 >> a.txt
    $ git add .
    $ git commit -m '2 추가'
    $ git log --oneline
	35129ef (HEAD -> feat1) 2 추가
	1166492 1 추가
	3f20de8 (master) b 추가
	828c85b a 추가
    $ git switch master
    $ git merge feat1
	Updating 3f20de8..35129ef
	Fast-forward
	a.txt | 2 ++
	1 file changed, 2 insertions(+)
	$ git log --oneline
	35129ef (HEAD -> master, feat1) 2 추가
	1166492 1 추가
	3f20de8 b 추가
	828c85b a 추가
	$ git branch -d feat1
	$ git log --oneline
	35129ef (HEAD -> master) 2 추가
	1166492 1 추가
	3f20de8 b 추가
	828c85b a 추가
```


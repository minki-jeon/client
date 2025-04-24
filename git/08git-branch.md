


		- `git switch -c {생성브랜치} {커밋지점}` : master커밋지점에서 브랜치 생성하고 이동
		```git switch -c feat4 master```


	6) 브랜치 강제 삭제
		- `git branch -D {브랜치}`

``` //* 병합되지 않은 브랜치 삭제, 복원 실습
	$ git branch
	$ git switch master
	$ git switch -c feat3
	Switched to a new branch 'feat3'
	$ echo 34 >> a.txt
	$ git add .
	$ git commit -m '34 추가'
	$ echo 45 >> a.txt
	$ git add .
	$ git commit -m '45 추가'
	$ git log --oneline
	5cd64a0 (HEAD -> feat3) 45 추가
	628602a 34 추가
	fed667d (master) bb 추가
	0291fd9 aa 추가
	35129ef 2 추가
	1166492 1 추가
	3f20de8 b 추가
	828c85b a 추가
	$ git switch -c feat4 master	//* master커밋지점에서 feat4브랜치 생성, 이동
	Switched to a new branch 'feat4'
	$ git log --oneline
	fed667d (HEAD -> feat4, master) bb 추가
	0291fd9 aa 추가
	35129ef 2 추가
	1166492 1 추가
	3f20de8 b 추가
	828c85b a 추가
	$ echo 99 >> a.txt
	$ git add .
	$ git commit -m '99 추가'
	$ echo 88 >> a.txt
	$ git add .
	$ git commit -m '88 추가'
	$ git log --oneline
	1b85947 (HEAD -> feat4) 88 추가
	43a7902 99 추가
	fed667d (master) bb 추가
	0291fd9 aa 추가
	35129ef 2 추가
	1166492 1 추가
	3f20de8 b 추가
	828c85b a 추가
	$ git switch master
	Switched to branch 'master'
	$ git log --oneline --all --graph
	* 1b85947 (feat4) 88 추가
	* 43a7902 99 추가
	| * 5cd64a0 (feat3) 45 추가
	| * 628602a 34 추가
	|/
	* fed667d (HEAD -> master) bb 추가
	* 0291fd9 aa 추가
	* 35129ef 2 추가
	* 1166492 1 추가
	* 3f20de8 b 추가
	* 828c85b a 추가
	$ git merge feat4
	Updating fed667d..1b85947
	Fast-forward
	 a.txt | 2 ++
	 1 file changed, 2 insertions(+)
	$ git log --oneline --all --graph
	* 1b85947 (HEAD -> master, feat4) 88 추가
	* 43a7902 99 추가
	| * 5cd64a0 (feat3) 45 추가
	| * 628602a 34 추가
	|/
	* fed667d bb 추가
	* 0291fd9 aa 추가
	* 35129ef 2 추가
	* 1166492 1 추가
	* 3f20de8 b 추가
	* 828c85b a 추가
	$ git branch -d feat4
	Deleted branch feat4 (was 1b85947).
	$ git branch -d feat3		//* Merge되지 않은 브랜치 삭제 시 error
	error: the branch 'feat3' is not fully merged
	$ git branch -D feat3		//* Merge되지 않은 브랜치 강제 삭제
	Deleted branch feat3 (was 5cd64a0).		//* 삭제되는 브랜치의 커밋번호
	$ git branch feat9 5cd64a0			//* 삭제된 커밋번호를 feat9 브랜치명으로 생성(복원)
	$ git log --oneline --all --graph
	* 1b85947 (HEAD -> master) 88 추가
	* 43a7902 99 추가
	| * 5cd64a0 (feat9) 45 추가
	| * 628602a 34 추가
	|/
	* fed667d bb 추가
	* 0291fd9 aa 추가
	* 35129ef 2 추가
	* 1166492 1 추가
	* 3f20de8 b 추가
	* 828c85b a 추가	
```
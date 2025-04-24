


		13) 브랜치 이동(git switch/checkout) 전에 변경된 파일이 있는 경우, 변경된 파일을 잃을 수 있으므로 이동이 되지 않는다.
			- 브랜치 이동하려는 'master', 'feat1'가 서로 같은 커밋 지점의 경우에는 브랜치 이동 가능하다.
			- `git status`로 clean 상태 확인하여 커밋이 완료된 상황에서만 브랜치 이동하도록한다.
			
```	//* Working Dirctory 내의 변경된 파일이 존재한 상황에서 'master'에서 'feat1'으로 브랜치 이동할 때 error 발생
	$ git switch feat1
	error: Your local changes to the following files would be overwritten by checkout:
			a.txt
	Please commit your changes or stash them before you switch branches.
	Aborting
```

		14) 파일의 상태 : (1)tracked(git에서 변경사항을 추적하는 상태), (2)untracked(git에서 추적하지 않는 상태)
		- Ref: "https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository"
		`Remember that each file in your working directory can be in one of two states: tracked or untracked. `
		- (1) 파일 수정 : tracked(unmodified) -> tracked(modified)
		- (2) stage 등록(업로드) : tracked(modified) -> tracked(staged)
		- (3) commit : tracked(staged) -> tracked(unmodified)
		- (4) 파일 생성 : untracked
		- (5) stage 업로드 : untracked -> tracked(staged)
		- (6) commit : tracked(staged) -> tracked(unmodified)
```	//* a.txt는 수정된 파일로서 tracked상태이며, c.txt는 생성한 파일로서 untracked상태
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
			c.txt

	no changes added to commit (use "git add" and/or "git commit -a")

```
``` //* a.txt와 c.txt를 stage영역에 등록하면, 두 파일 모두 tracked상태가 된다.
	$ git add .
	warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
	warning: in the working copy of 'c.txt', LF will be replaced by CRLF the next time Git touches it

	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   a.txt
			new file:   c.txt
```
``` //* stage에 등록된 파일들을 commit하고나면 tracked의 Unmodified 상태가 된다.
	$ git commit -m 'a, c'
	[master 8447fe7] a, c
	 2 files changed, 2 insertions(+)
	 create mode 100644 c.txt
```
``` //*	파일을 수정하면 tracked의 modified상태가 된다.
	$ echo c >> c.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   c.txt

	no changes added to commit (use "git add" and/or "git commit -a")
```
		15) `git commit -a`
			`git commit -a -m {커밋메시지}`
			`git commit -am {커밋메시지}`
			: tracked 파일을 모두 add하고 커밋 (untracked 파일은 불가)

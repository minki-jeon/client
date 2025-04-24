
	11) Git Repository Project Directory 구성: [Working Directory] / [Staging Area] / [.git directory]
		- Ref: "git-scm.com/book/en/v2/Getting-Started-What-isGit%3F"
`This leads us to the three main sections of a Git project: the working tree, the staging area, and the Git directory.`

	12) `git status` : 현재 상태보기 (영역 3구역이 모두 같으면 clean 상태)
		- working directory(working tree)
		- stage(index, staging area)
		- git repository(저장소, 오브젝트 저장소)
		- `git add 파일명` : Working-Tree의 파일을 Stage에 복사
		- `git commit` : Stage에 있는 내용을 repo에 복사, 커밋 생성, 브랜치 이동, HEAD 이동
		- `git add {파일명1} {파일명2} : 여러 파일 Stage 등록
		- `git add .` : 수정된 모든 파일 Stage 등록

```//* git status 실습
	$ cd /c/learn-git
	$ mkdir repo8
    $ cd repo8
    $ git init
	$ echo aa >> a.txt
	$ git add .
	$ git commit -m 'aa 추가'
	$ git status
	On branch master
	nothing to commit, working tree clean
	
	$ echo bb >> a.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ git add a.txt
	warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   a.txt
	$ git commit -m 'bb 추가'
	[master 7b44fa6] bb 추가
	 1 file changed, 1 insertion(+)
	$ git status
	On branch master
	nothing to commit, working tree clean
```
```//* git status 실습2
	$ echo aaaa >> a.txt
	$ echo bbbb >> b.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt
			modified:   b.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ git add a.txt
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   a.txt

	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   b.txt
	$ git commit -m 'add aaaa to a.txt'
	[master 15418c9] add aaaa to a.txt
	 1 file changed, 1 insertion(+)
	$ git commit -m 'add aaaa to a.txt'
	[master 15418c9] add aaaa to a.txt
	 1 file changed, 1 insertion(+) 
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   b.txt

	no changes added to commit (use "git add" and/or "git commit -a") 
	$ git add b.txt
	warning: in the working copy of 'b.txt', LF will be replaced by CRLF the next time Git touches it 
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   b.txt
	$ git commit -m 'add bbbb to b.txt'
	[master 92d6649] add bbbb to b.txt
	 1 file changed, 1 insertion(+)
	$ git status
	On branch master
	nothing to commit, working tree clean 
```

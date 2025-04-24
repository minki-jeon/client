


	- `git restore --staged {파일명}` : 등록된 Stage 내리기
									= git repository의 파일을 stage에 있는 파일에 붙여넣기(복원)
	- `git restore {파일명}` : (Working Dirctory에서) 변경된 파일을 되돌리기(복원하기)
									= git stage 영역의 파일을 working Directory에 변경된 파일에 붙여넣기
``` //* git restore 실습
	$ git status
	On branch master
	nothing to commit, working tree clean
	$ cat b.txt
	11
	22
	bbbb
	33
	$ echo 3333 >> b.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   b.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ cat b.txt
	11
	22
	bbbb
	33
	3333
	$ git add b.txt
	warning: in the working copy of 'b.txt', LF will be replaced by CRLF the next time Git touches it
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   b.txt
	$ git restore --staged b.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   b.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ cat b.txt
	11
	22
	bbbb
	33
	3333
	$ git restore b.txt
	$ git status
	On branch master
	nothing to commit, working tree clean
	$ cat b.txt
	11
	22
	bbbb
	33
```

``` //* stage에 등록되어있는 파일을 추가로 변경(수정)했을 때
	$ echo 11 >> a.txt
	$ cat a.txt
	aa
	bb
	cc
	aaaa
	dd
	11
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ git add a.txt
	$ echo 22 >> a.txt
	$ cat a.txt
	aa
	bb
	cc
	aaaa
	dd
	11
	22
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   a.txt

	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt
	$ git restore a.txt
	$ cat a.txt
	aa
	bb
	cc
	aaaa
	dd
	11
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
			modified:   a.txt
	$ git restore --staged a.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ git restore a.txt
	$ git status
	On branch master
	nothing to commit, working tree clean
	$ cat a.txt
	aa
	bb
	cc
	aaaa
	dd
```
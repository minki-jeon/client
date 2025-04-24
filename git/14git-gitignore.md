
		16) .gitignore 파일 : 이 파일에 명시된 파일은 untracked(추적하지 않음)
				- untracked에서 tracked로 변경되지 않도록 적용
```
	$ touch .gitignore
	$ git add .
	$ git commit -m '.gitignore 추가'
	$ echo 486 >> secret.txt

	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   .gitignore

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
			secret.txt

	no changes added to commit (use "git add" and/or "git commit -a")

	$ echo secret.txt >> .gitignore
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   .gitignore

	no changes added to commit (use "git add" and/or "git commit -a")

	$ git commit -am 'add secret.txt'
	warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches it
	[master 93f51d5] add secret.txt
	 1 file changed, 1 insertion(+)
	 
	$ echo 987 >> secret.txt

	$ git status
	On branch master
	nothing to commit, working tree clean

	$ echo a.txt >> .gitignore

	$ cat .gitignore
	secret.txt
	a.txt

	$ echo secretaaaa >> a.txt

	$ git status					//* .gitignore에 파일 추가했더라도 이미 tracked 파일은 계속 추적한다.
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   .gitignore
			modified:   a.txt

	no changes added to commit (use "git add" and/or "git commit -a")

	$ rm a.txt

	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add/rm <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   .gitignore
			deleted:    a.txt

	no changes added to commit (use "git add" and/or "git commit -a")

	$ git add .

	$ git status
	On branch master
	nothing to commit, working tree clean

	$ git log -5 --oneline
	d43e18b (HEAD -> master) delete a.txt
	93f51d5 add secret.txt
	6f06731 .gitignore 추가
	a8b4991 b, c수정
	cd3b9ce z수정					//* .gitignore 존재하지 않는 지점

	$ git branch second cd3b9ce

	$ git switch second
	Switched to branch 'second'

	$ echo abcde >> a.txt

	$ git status
	On branch second
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   a.txt

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
			secret.txt

	no changes added to commit (use "git add" and/or "git commit -a")

	$ ls -al
	total 18
	drwxr-xr-x 1 minmi 197609  0  4월 24 16:29 ./
	drwxr-xr-x 1 minmi 197609  0  4월 24 14:02 ../
	drwxr-xr-x 1 minmi 197609  0  4월 24 16:29 .git/
	-rw-r--r-- 1 minmi 197609 30  4월 24 16:29 a.txt
	-rw-r--r-- 1 minmi 197609 28  4월 24 16:29 b.txt
	-rw-r--r-- 1 minmi 197609  6  4월 24 16:29 c.txt
	-rw-r--r-- 1 minmi 197609  3  4월 24 16:00 e.txt
	-rw-r--r-- 1 minmi 197609  8  4월 24 16:25 secret.txt
	-rw-r--r-- 1 minmi 197609  2  4월 24 16:15 z.txt
```
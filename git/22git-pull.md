

	 - fetch와 merge를 동시에 하기 : `git pull`
		//* `git fetch` + `git merge origin/{브랜치명}`
		//* merge 단계에서 conflict 발생 가능성이 있으므로 fetch를 별도로 먼저 사용 권장
				
	
``` //* github에 repository 생성부터 push 작업까지 실습
minmi@MinKi-Book2Pro MINGW64 /c/learn-git
$ cd repo13

minmi@MinKi-Book2Pro MINGW64 /c/learn-git/repo13
$ git init
Initialized empty Git repository in C:/learn-git/repo13/.git/

(master)
$ echo a >> a.txt

(master)
$ git add .
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it

(master)
$ git commit -m 'add a to a.txt'
[master (root-commit) 3bcda09] add a to a.txt
 1 file changed, 1 insertion(+)
 create mode 100644 a.txt

(master)
$ echo b >> a.txt

(master)
$ git commit -am 'add b'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[master 8ea37d6] add b
 1 file changed, 1 insertion(+)

(master)
$ git log --oneline --all --graph
* 8ea37d6 (HEAD -> master) add b
* 3bcda09 add a to a.txt

(master)
$ git remote add origin https://github.com/minki-jeon/repo13.git

(master)
$ echo c >> a.txt

(master)
$ git commit -am 'add c'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[master 2f62db3] add c
 1 file changed, 1 insertion(+)

(master)
$ git status
On branch master
nothing to commit, working tree clean

(master)
$ git log --oneline --all --graph
* 2f62db3 (HEAD -> master) add c
* 8ea37d6 add b
* 3bcda09 add a to a.txt

(master)
$ git push -u origin master
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (9/9), 634 bytes | 634.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/minki-jeon/repo13.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.

(master)
$ git log --oneline --all --graph
* 2f62db3 (HEAD -> master, origin/master) add c
* 8ea37d6 add b
* 3bcda09 add a to a.txt

(master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

(master)
$ echo d >> a.txt

(master)
$ git commit -am 'add d'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[master e0dfda1] add d
 1 file changed, 1 insertion(+)

(master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

(master)
$ git log --oneline --all --graph
* e0dfda1 (HEAD -> master) add d
* 2f62db3 (origin/master) add c
* 8ea37d6 add b
* 3bcda09 add a to a.txt

(master)
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 245 bytes | 245.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/minki-jeon/repo13.git
   2f62db3..e0dfda1  master -> master

(master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

(master)
$ git log --oneline --all --graph
* e0dfda1 (HEAD -> master, origin/master) add d
* 2f62db3 add c
* 8ea37d6 add b
* 3bcda09 add a to a.txt
```




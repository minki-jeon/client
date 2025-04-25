
	  - Github(remote)의 Git커밋정보를 로컬(local)로 가져오기 - `git fetch`
	    //* local 파일에 영향을 주지 않음
```$ git fetch```


	  - 원격 브랜치(remote branch) 반영하기 - `git push origin {브랜치명}
```$ git push origin {브랜치명}```
	  
``` //* 다른 브랜치 추가 업로드 (push; local -> remote(github))
(master)
$ git branch feat1

(master)
$ git switch feat1
Switched to branch 'feat1'

(feat1)
$ echo 1 >> b.txt

(feat1)
$ git add .
warning: in the working copy of 'b.txt', LF will be replaced by CRLF the next time Git touches it

(feat1)
$ git commit -m 'add 1 to b.txt'
[feat1 5458c98] add 1 to b.txt
 1 file changed, 1 insertion(+)
 create mode 100644 b.txt

(feat1)
$ git push origin feat1	

(feat1)
$ git log --oneline --graph --all
* 88984d3 (HEAD -> feat1, origin/feat1) add 2 to b.txt
* 5458c98 add 1 to b.txt
* d397f9e (origin/master, master) add b
* fe24b91 add a		
```


     - remote에 push하고 upstream(track; 추적) 설정 : `git push -u origin {브랜치명}`
        //* -u : --set-upstream 약자
        
     - upstream 설정 : `git branch -u origin/{브랜치명}`
        //* branch 'master' set up to track 'origin/master'
        //* git status 명령어로, remote와의 비교하여 버전 차이를 알려줄 수 있다.
        
     - upstream 설정된 원격브랜치에 올리기 : `git push`
        //* upstream 상태에서는 `git push` 명령어 뒤에 생략하고 사용 가능하다.


``` //* 브랜치 push+upstream 실습
(master)
$ git switch -c second

(second)
$ echo 88 >> a.txt

(second)
$ git commit -am '88 to a.txt'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[second 8f59d05] 88 to a.txt
 1 file changed, 1 insertion(+)

(second)
$ git status
On branch second
nothing to commit, working tree clean

(second)
$ git push -u origin second
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 270 bytes | 270.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'second' on GitHub by visiting:
remote:      https://github.com/minki-jeon/repo12/pull/new/second
remote:
To https://github.com/minki-jeon/repo12.git
 * [new branch]      second -> second
branch 'second' set up to track 'origin/second'.

(second)
$ echo 99 >> a.txt

(second)
$ git commit -am '99 to a.txt'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[second 10b95a9] 99 to a.txt
 1 file changed, 1 insertion(+)

(second)
$ git status
On branch second
Your branch is ahead of 'origin/second' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

(second)
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 269 bytes | 269.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/minki-jeon/repo12.git
   8f59d05..10b95a9  second -> second

(second)
$ git status
On branch second
Your branch is up to date with 'origin/second'.

nothing to commit, working tree clean

```


``` //* remote -> local 실습 (fetch, merge)
$ git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 903 bytes | 150.00 KiB/s, done.
From https://github.com/minki-jeon/repo12
   00771ae..b877d51  third      -> origin/third

(third)
$ git status
On branch third
Your branch is behind 'origin/third' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean

(third)
$ git log --oneline --graph --all -5
* b877d51 (origin/third) 77 to a.txt
* 00771ae (HEAD -> third) add mmm
* 1b14be9 add nnn
| * 10b95a9 (origin/second, second) 99 to a.txt
| * 8f59d05 88 to a.txt
|/

(third)
$ git merge origin/third
Updating 00771ae..b877d51
Fast-forward
 a.txt | 1 +
 1 file changed, 1 insertion(+)

(third)
$ git status
On branch third
Your branch is up to date with 'origin/third'.

nothing to commit, working tree clean

(third)
$ git log --oneline --graph --all -5
* b877d51 (HEAD -> third, origin/third) 77 to a.txt
* 00771ae add mmm
* 1b14be9 add nnn
| * 10b95a9 (origin/second, second) 99 to a.txt
| * 8f59d05 88 to a.txt
|/
```

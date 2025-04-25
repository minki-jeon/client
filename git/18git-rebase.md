	
	4) Git 명령어 - 특정브랜치를 다른 브랜치 위에 잇기 -> `pick`
	  - `git rebase -i {브랜치명}
	  
``` //* 브랜치 잇기 실습
	//* 3way-merge 대신 커밋 브랜치 라인을 하나로 만들기
	//* comflict 발생하지 않도록 서로 다른 파일로 사용하여 커밋
(master)
$ git branch bug1

(master)
$ git branch bug2

(master)
$ git log --graph --all --oneline -3
* 6715266 (HEAD -> master, bug2, bug1) add 1, 2, 3 complete
* 09d7389 add x, y, z complete
* c3798b3 Complete Work

(master)
$ git switch bug1
Switched to branch 'bug1'

(bug1)
$ echo bug1 a >> a.txt

(bug1)
$ git commit -am 'add a'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[bug1 9c89967] add a
 1 file changed, 1 insertion(+)

(bug1)
$ echo bug1 aa >> a.txt

(bug1)
$ git commit -am 'add aa'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[bug1 5297faa] add aa
 1 file changed, 1 insertion(+)

(bug1)
$ echo bug1 aaa >> a.txt

(bug1)
$ git commit -am 'add aaa'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[bug1 cf14cae] add aaa
 1 file changed, 1 insertion(+)

(bug1)
$ git switch bug2
Switched to branch 'bug2'

(bug2)
$ echo bug2 b >> b.txt

(bug2)
$ git commit -am 'add b'
warning: in the working copy of 'b.txt', LF will be replaced by CRLF the next time Git touches it
[bug2 2cb1354] add b
 1 file changed, 1 insertion(+)

(bug2)
$ echo bug2 bb >> b.txt

(bug2)
$ git commit -am 'add bb'
warning: in the working copy of 'b.txt', LF will be replaced by CRLF the next time Git touches it
[bug2 5efc422] add bb
 1 file changed, 1 insertion(+)

(bug2)
$ echo bug2 bbb >> b.txt

(bug2)
$ git commit -am 'add bbb'
warning: in the working copy of 'b.txt', LF will be replaced by CRLF the next time Git touches it
[bug2 1804df1] add bbb
 1 file changed, 1 insertion(+)

(bug2)
$ git log --graph --oneline --all -7
* 1804df1 (HEAD -> bug2) add bbb
* 5efc422 add bb
* 2cb1354 add b
| * cf14cae (bug1) add aaa
| * 5297faa add aa
| * 9c89967 add a
|/
* 6715266 (master) add 1, 2, 3 complete

(bug2)
$ git status
On branch bug2
nothing to commit, working tree clean

(bug2)
$ git switch bug1
Switched to branch 'bug1'

(bug1)
$ git rebase -i master
  //* 시작 커밋(master) 'pick', 병합할 커밋 3개는 각각 'squash'로 작성
[detached HEAD 5f1e0bc] add a,aa, aaa complete (squash 3)
 Date: Fri Apr 25 11:55:10 2025 +0900
 1 file changed, 3 insertions(+)
Successfully rebased and updated refs/heads/bug1.

(bug1)
$ git log --graph --oneline --all -5
* 5f1e0bc (HEAD -> bug1) add a,aa, aaa complete (squash 3)
| * 1804df1 (bug2) add bbb
| * 5efc422 add bb
| * 2cb1354 add b
|/
* 6715266 (master) add 1, 2, 3 complete

(bug1)
$ git switch bug2
Switched to branch 'bug2'

(bug2)
$ git rebase -i master
  //* 시작 커밋(master) 'pick', 병합할 커밋 3개는 각각 'squash'로 작성
[detached HEAD 79f9eda] add b, bb, bbb complete (squash 3)
 Date: Fri Apr 25 11:56:20 2025 +0900
 1 file changed, 3 insertions(+)
Successfully rebased and updated refs/heads/bug2.

(bug2)
$ git log --graph --oneline --all -3
* 79f9eda (HEAD -> bug2) add b, bb, bbb complete (squash 3)
| * 5f1e0bc (bug1) add a,aa, aaa complete (squash 3)
|/
* 6715266 (master) add 1, 2, 3 complete

(bug2)
$ git switch master
Switched to branch 'master'

(master)
$ git merge bug1
Updating 6715266..5f1e0bc
Fast-forward
 a.txt | 3 +++
 1 file changed, 3 insertions(+)

(master)
$ git log --graph --oneline --all -3
* 79f9eda (bug2) add b, bb, bbb complete (squash 3)
| * 5f1e0bc (HEAD -> master, bug1) add a,aa, aaa complete (squash 3)
|/
* 6715266 add 1, 2, 3 complete

(master)
$ git switch bug2
Switched to branch 'bug2'

(bug2)
$ git rebase -i master
  //* bug2를 master 다음 커밋버전으로 잇기 => 'pick'
Successfully rebased and updated refs/heads/bug2.

(bug2)
$ git log --graph --oneline --all -3
* 568ab82 (HEAD -> bug2) add b, bb, bbb complete (squash 3)
* 5f1e0bc (master, bug1) add a,aa, aaa complete (squash 3)
* 6715266 add 1, 2, 3 complete

(bug2)
$ git switch master
Switched to branch 'master'

(master)
$ git merge bug2
Updating 5f1e0bc..568ab82
Fast-forward
 b.txt | 3 +++
 1 file changed, 3 insertions(+)

(master)
$ git log --graph --oneline --all -3
* 568ab82 (HEAD -> master, bug2) add b, bb, bbb complete (squash 3)
* 5f1e0bc (bug1) add a,aa, aaa complete (squash 3)
* 6715266 add 1, 2, 3 complete

(master)
$ git branch -d bug1
Deleted branch bug1 (was 5f1e0bc).

(master)
$ git branch -d bug2
Deleted branch bug2 (was 568ab82).

(master)
$ git log --graph --oneline --all -3
* 568ab82 (HEAD -> master) add b, bb, bbb complete (squash 3)
* 5f1e0bc add a,aa, aaa complete (squash 3)
* 6715266 add 1, 2, 3 complete
```


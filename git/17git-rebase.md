
	3) Git 명령어 - 커밋 하나로 합치기(병합)
	  - `git rebase -i HEAD~{합치려는 커밋개수}`
	  
``` //* 커밋 합치기 실습 (rebase)
(master)
$ git branch feat2

(master)
$ git log --graph --all --oneline
* d57f8e4 (HEAD -> master, feat2) complete func (rebase -i HEAD~5)
* e14b69c add a

(master)
$ git switch feat2
Switched to branch 'feat2'

(feat2)
$ git log --graph --all --oneline
* d57f8e4 (HEAD -> feat2, master) complete func (rebase -i HEAD~5)
* e14b69c add a

(feat2)
$ echo AAA >> a.txt

(feat2)
$ git commit -am 'working 1'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[feat2 e1853bc] working 1
 1 file changed, 1 insertion(+)

(feat2)
$ echo BBB >> a.txt

(feat2)
$ git commit -am 'working 2'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[feat2 52dc60b] working 2
 1 file changed, 1 insertion(+)

(feat2)
$ echo CCC >> a.txt

(feat2)
$ git commit -am 'working 3'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[feat2 9438011] working 3
 1 file changed, 1 insertion(+)

(feat2)
$ echo DDD >> a.txt

(feat2)
$ git commit -am 'working 4'
warning: in the working copy of 'a.txt', LF will be replaced by CRLF the next time Git touches it
[feat2 c3ef1ae] working 4
 1 file changed, 1 insertion(+)

(feat2)
$ cat a.txt
a
b
c
d
e
ee
AAA
BBB
CCC
DDD

(feat2)
$ git log --graph --all --oneline
* c3ef1ae (HEAD -> feat2) working 4
* 9438011 working 3
* 52dc60b working 2
* e1853bc working 1
* d57f8e4 (master) complete func (rebase -i HEAD~5)
* e14b69c add a

(feat2)
$ git status
On branch feat2
nothing to commit, working tree clean

(feat2)
$ git rebase -i HEAD~4

//////..open editor, edit work
[File: git-rebase-todo]
pick e1853bc working 1
squash 52dc60b working 2
squash 9438011 working 3
squash c3ef1ae working 4
//* squash: 이전 커밋에 병합
///////////////////////////
//////..open editor, edit commit-msg
[File: COMMIT_EDITMSG]
{커밋메시지}
///////////////////////////

[detached HEAD c3798b3] Complete Work
 Date: Fri Apr 25 10:53:59 2025 +0900
 1 file changed, 4 insertions(+)
Successfully rebased and updated refs/heads/feat2.

(feat2)
$ git status
On branch feat2
nothing to commit, working tree clean

(feat2)
$ git log --graph --all --oneline
* c3798b3 (HEAD -> feat2) Complete Work
* d57f8e4 (master) complete func (rebase -i HEAD~5)
* e14b69c add a

(feat2)
$ git switch master
Switched to branch 'master'

(master)
$ git log --graph --all --oneline
* c3798b3 (feat2) Complete Work
* d57f8e4 (HEAD -> master) complete func (rebase -i HEAD~5)
* e14b69c add a

(master)
$ git merge feat2
Updating d57f8e4..c3798b3
Fast-forward
 a.txt | 4 ++++
 1 file changed, 4 insertions(+)

(master)
$ git log --graph --all --oneline
* c3798b3 (HEAD -> master, feat2) Complete Work
* d57f8e4 complete func (rebase -i HEAD~5)
* e14b69c add a

(master)
$ git branch -d feat2
Deleted branch feat2 (was c3798b3).

(master)
$ git log --graph --all --oneline
* c3798b3 (HEAD -> master) Complete Work
* d57f8e4 complete func (rebase -i HEAD~5)
* e14b69c add a

(master)
$ git status
On branch master
nothing to commit, working tree clean

```


	
	4) Git 명령어 - 특정브랜치를 다른 브랜치 위에 잇기 -> `pick`
	  - `git rebase -i {브랜치명}
	  
``` //* 브랜치 잇기 실습
	//* 3way-merge 대신 커밋 브랜치 라인을 하나로 만들기
	//* comflict 발생하지 않도록 서로 다른 파일로 사용하여 커밋
(master)
$ git log --graph --all --oneline -5
*   18b3efc (HEAD -> master) Merge branch 'feat2'
|\
| * 7afbfd1 (feat2) add 1, 2, 3 complete
* | 09d7389 add x, y, z complete
|/
* c3798b3 Complete Work (rebase -i HEAD~4)

(master)
$ git reset --hard HEAD~
HEAD is now at 09d7389 add x, y, z complete

(master)
$ git log --graph --all --oneline -5
* 09d7389 (HEAD -> master) add x, y, z complete
| * 7afbfd1 (feat2) add 1, 2, 3 complete
|/
* c3798b3 Complete Work (rebase -i HEAD~4)

(master)
$ git switch feat2
Switched to branch 'feat2'

(feat2)
$ git rebase -i master
Successfully rebased and updated refs/heads/feat2.

(feat2)
$ git log --graph --all --oneline -3
* 6715266 (HEAD -> feat2) add 1, 2, 3 complete
* 09d7389 (master) add x, y, z complete
* c3798b3 Complete Work (rebase -i HEAD~4)

(feat2)
$ git switch master
Switched to branch 'master'

(master)
$ git merge feat2
Updating 09d7389..6715266
Fast-forward
 b.txt | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 b.txt

(master)
$ git log --graph --all --oneline -3
* 6715266 (HEAD -> master, feat2) add 1, 2, 3 complete
* 09d7389 add x, y, z complete
* c3798b3 Complete Work (rebase -i HEAD~4)
```


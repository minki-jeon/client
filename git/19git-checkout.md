
	5) Git 명령어 - 다른 커밋에 있는 특정 파일 불러오기
	  - `git checkout {커밋번호|브랜치명} -- {파일명} |{파일명}|...`
      
	6) Git 명령어 - 모든 수정 원복 (Repository 영역의 파일을 Working-Dir에 덮어쓰기)(*주의해서 사용)
	  - `git checkout . `
	  //* Working Directory에 파일이 없더라도 .git 폴더만 있으면 위 명령어로 원복 가능

```	//* 다른 커밋에 있는 파일을 가져온 후 다시 원복
(master)
$ cat b.txt
1
2
3
bug2 b
bug2 bb
bug2 bbb

(master)
$ git log --graph --oneline --all -5
* 568ab82 (HEAD -> master) add b, bb, bbb complete (squash 3)
* 5f1e0bc add a,aa, aaa complete (squash 3)
* 6715266 add 1, 2, 3 complete
* 09d7389 add x, y, z complete
* c3798b3 Complete Work

(master)
$ git checkout 6715266 -- b.txt

(master)
$ cat b.txt
1
2
3

(master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   b.txt


(master)
$ git restore --staged b.txt

(master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   b.txt

no changes added to commit (use "git add" and/or "git commit -a")

(master)
$ git restore b.txt

(master)
$ git status
On branch master
nothing to commit, working tree clean
```

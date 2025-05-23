
	2) Git 명령어 - 커밋 롤백
	  - `git reset --soft {커밋번호}`
			: 해당 커밋번호의 내용을 Repository까지만 덮어쓰기 (Stage, Working-Dir 영역의 파일은 유지)
	  - `git reset --mixed {커밋번호}`
			: 해당 커밋번호의 내용을 Repository와 Stage영역까지 덮어쓰기 (Working-Dir 영역의 파일은 유지)
	  - `git reset --hard {커밋번호}`
			: 해당 커밋번호의 내용을 Repository, Stage, Working-Directory 영역 모두 덮어쓰기
	  - `git branch {브랜치명} {커밋번호}
			: reset --hard에 의해 삭제된 최종 버전 커밋을 브랜치 지정하여 불러오기 (이후 merge명령어를 사용하여 복원)
			
	  - HEAD
			: 현재 위치
	  - HEAD^, HEAD~, HEAD^1, HEAD~1 : 부모(상위)커밋
	  - HEAD^^, HEAD~~, HEAD~2
			: 부모의 부모(상위의 상위) 커밋
	  - HEAD^^^, HEAD~~~, HEAD~3
			: 부모의 부모(상위의 상위) 커밋
	  - HEAD^2
            : 3way-merge 커밋의 두번째 부모(상위)
			  - 3way-merge 직전에 HEAD가 지칭했던 커밋이 첫번째 부모(상위)
              //* 아래 실습에서 부연 설명

``` //* 커밋 롤백하고 되돌리기 실습
$ git log --oneline --all --graph
* 74975fa (HEAD -> master) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d a

$ git reset --soft 3f85d90

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt

$ git log --oneline
3f85d90 (HEAD -> master) add c
4291e63 add b
636193d a

$ git commit -m 'add d'
[master 28620c7] add d
 1 file changed, 1 insertion(+)
 
$ git status
On branch master
nothing to commit, working tree clean

$ git log --oneline
28620c7 (HEAD -> master) add d
3f85d90 add c
4291e63 add b
636193d a
$ git reset --mixed 3f85d90
Unstaged changes after reset:
M       a.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git log --oneline
3f85d90 (HEAD -> master) add c
4291e63 add b
636193d a

$ git commit -am 'add d'
[master e33c635] add d
 1 file changed, 1 insertion(+)
 
$ git status
On branch master
nothing to commit, working tree clean

$ git log --oneline
e33c635 (HEAD -> master) add d
3f85d90 add c
4291e63 add b
636193d a

$ git reset --hard 3f85d90
HEAD is now at 3f85d90 add c

$ git status
On branch master
nothing to commit, working tree clean

$ git log --oneline
3f85d90 (HEAD -> master) add c
4291e63 add b
636193d a

$ git branch temp-branch e33c635

$ git log --oneline --all --graph
* e33c635 (temp-branch) add d
* 3f85d90 (HEAD -> master) add c
* 4291e63 add b
* 636193d a

$ git merge temp-branch
Updating 3f85d90..e33c635
Fast-forward
 a.txt | 1 +
 1 file changed, 1 insertion(+)
 
$ git log --oneline --all --graph
* e33c635 (HEAD -> master, temp-branch) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d a

$ git branch -d temp-branch
Deleted branch temp-branch (was e33c635).

$ git log --oneline --all --graph
* e33c635 (HEAD -> master) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d a
```			


``` //* HEAD ^ ~ 사용하여 reset 실습
$ git log --oneline --all --graph
* e33c635 (HEAD -> master) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d a

$ git branch second

$ git log --oneline --all --graph
* e33c635 (HEAD -> master, second) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d a

$ git status
On branch master
nothing to commit, working tree clean

$ git reset --hard HEAD^
HEAD is now at 3f85d90 add c

$ git log --oneline --all --graph
* e33c635 (second) add d
* 3f85d90 (HEAD -> master) add c
* 4291e63 add b
* 636193d a

$ git status
On branch master
nothing to commit, working tree clean

$ git reset --hard HEAD~2
HEAD is now at 636193d a

$ git log --oneline --all --graph
* e33c635 (second) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d (HEAD -> master) a

$ git status
On branch master
nothing to commit, working tree clean

$ git merge second
Updating 636193d..e33c635
Fast-forward
 a.txt | 3 +++
 1 file changed, 3 insertions(+)
 
$ git log --oneline --all --graph
* e33c635 (HEAD -> master, second) add d
* 3f85d90 add c
* 4291e63 add b
* 636193d a

$ git status
On branch master
nothing to commit, working tree clean 
```

``` //* HEAD를 사용한 reset 실습
	//* 'second'브랜치와 3-way Merge 한 상태 + 'third'브랜치 지정
$ git log --oneline --all --graph
*   2f486c8 (HEAD -> master, third) Merge branch 'second'
|\
| * e33c635 (second) add d		//* => `HEAD^2` 현재HEAD의 두번째 부모(상위)를 지칭 
| * 3f85d90 add c				//* => `HEAD^2~` 현재HEAD의 두번째 부모의 부모를 지칭
| * 4291e63 add b				//* => `HEAD^2~2`
* | b1b5990 add 33				//* => `HEAD~1`	현재HEAD의 첫번째 부모(상위)를 지칭
* | 9447dd9 add 22				//* => `HEAD^^` 현재HEAD의 첫번째 부모의 부모를 지칭
* | b62006c add 11				//* => `HEAD~~~`
|/
* 636193d a
```



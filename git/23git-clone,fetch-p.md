	
	 - 원격 repository 로컬에 가져오기 : `git clone {remote-address} {폴더명}`
	    //* 동작과정 :
			새폴더 생성하고, remote-repository의 .git 폴더 복사하고,
			통합브랜치(master)를 checkout, local브랜치 upstream 설정
```
$ pwd
/c/learn-git

$ git clone https://github.com/minki-jeon/repo13.git repo13-copy
Cloning into 'repo13-copy'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 12 (delta 0), reused 12 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (12/12), done.
```

	 - 원격에서 삭제된 브랜치 정보 포함 가져오기 : `git fetch --prune`, `git fetch -p`
	
``` //* Local에서 Branch 생성하고 Remote PUSH
$ git branch feat1

$ git switch feat1
Switched to branch 'feat1'

$ echo 1 >> a.txt

$ git commit -am 'add 1'

$ git log --oneline --all --graph
* 83dd29e (HEAD -> feat1) add 1
* cf464c8 (origin/master, origin/HEAD, master) add 3 to b.txt
* 60cd6aa add 2 to b.txt
* e97ff0c add 1 to b.txt
* d04d050 add e
* e0dfda1 add d
* 2f62db3 add c
* 8ea37d6 add b
* 3bcda09 add a to a.txt

$ git push origin feat1
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 277 bytes | 277.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote:
remote: Create a pull request for 'feat1' on GitHub by visiting:
remote:      https://github.com/minki-jeon/repo13/pull/new/feat1
remote:
To https://github.com/minki-jeon/repo13.git
 * [new branch]      feat1 -> feat1
 
$ git log --oneline --all --graph
* 83dd29e (HEAD -> feat1, origin/feat1) add 1
* cf464c8 (origin/master, origin/HEAD, master) add 3 to b.txt
* 60cd6aa add 2 to b.txt
* e97ff0c add 1 to b.txt
* d04d050 add e
* e0dfda1 add d
* 2f62db3 add c
* 8ea37d6 add b
* 3bcda09 add a to a.txt
```


``` //* Github에서 생성한 branch를 master브랜치에 merge 요청하기
  1) github repository -> [Pull requests] -> [New pull request]
	 -> Compare changes 아래 [base:master]<-[compare:master] 에서 [compare:{작업브랜치명}]으로 지정
	 -> [Create pull request] -> {write message} -> [Create pull request]
			//* pull(merge) 요청
  2) [Merge pull request] -> [Confirm merge] -> [Delete branch]
			//* 요청 승인, merge 완료(3way merge), 기능 브랜치 삭제
```

``` //* github에서 merge 이후 fetch, pull(merge)
(feat2)
$ git fetch
remote: Enumerating objects: 2, done.
remote: Counting objects: 100% (2/2), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (2/2), 1.72 KiB | 294.00 KiB/s, done.
From https://github.com/minki-jeon/repo13
   cf464c8..4a0e072  master     -> origin/master

(feat2)   
$ git log --oneline --all --graph
*   4a0e072 (origin/master, origin/HEAD) Merge pull request #2 from minki-jeon/feat2
|\
| * 0903f1e (HEAD -> feat2, origin/feat2) add aaaaa to a.txt
* | 98d5bce Merge pull request #1 from minki-jeon/feat1
|\|
| * 83dd29e (origin/feat1, feat1) add 1
|/
* cf464c8 (master) add 3 to b.txt

(feat2)
$ git switch master

(master)
$ git fetch -p
From https://github.com/minki-jeon/repo13
 - [deleted]         (none)     -> origin/feat2
 
(master)
$ git pull
	//* 또는 `git merge origin/master`로 할 수 있다.
 
(master)
$ git branch -d feat2
```
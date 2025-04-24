git 복습
```
    $ cd /c/learn-git/
    $ ls
    $ mkdir repo5
    $ cd repo5
    $ ls -al
    $ git init
    $ git log --oneline
	fatal: your current branch 'master' does not have any commits yet	
    $ echo aaa >> a.txt
    $ cat a.txt
    $ git add .
    $ git commit -m 'aaa 추가'
    $ git log --oneline
    4caac2a (HEAD -> master) aaa 추가
    $ echo bbb >> a.txt
    $ git add .
    $ git commit -m 'bbb 추가'
    $ git log --oneline
    f47ae62 (HEAD -> master) bbb 추가
	//	4caac2a aaa 추가
    $ echo ccc >> a.txt
    $ git add .
    $ git commit -m 'ccc 추가'
    $ git log --oneline
	5001ef9 (HEAD -> master) ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git branch second
	$ git log --oneline
	5001ef9 (HEAD -> master, second) ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ echo ddd >> a.txt
	$ git add .
	$ git commit -m 'ddd 추가'
	$ git log --oneline
	b2719ae (HEAD -> master) ddd 추가
	5001ef9 (second) ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git checkout second
	$ cat a.txt
	aaa
	bbb
	ccc
	$ git log --oneline
	5001ef9 (HEAD -> second) ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git log --oneline --all
	b2719ae (master) ddd 추가
	5001ef9 (HEAD -> second) ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ echo 111 >> a.txt
	$ cat a.txt
	aaa
	bbb
	ccc
	111
	$ git add .
	$ git commit -m '111 추가'
	$ git log --oneline
	97cd89e (HEAD -> second) 111 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git log --oneline --all
	97cd89e (HEAD -> second) 111 추가
	b2719ae (master) ddd 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git checkout master
	$ git log --oneline
	b2719ae (HEAD -> master) ddd 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git log --oneline --all
	97cd89e (second) 111 추가
	b2719ae (HEAD -> master) ddd 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ echo eee >> a.txt
	$ git add .
	$ git commit -m 'eee 추가'
	$ git log --oneline
	e7b3c69 (HEAD -> master) eee 추가
	b2719ae ddd 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git checkout second
	$ echo 222 >> a.txt
	$ git add .
	$ git commit -m '222 추가'
	$ git log --oneline
	218b94b (HEAD -> second) 222 추가
	97cd89e 111 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
	$ git log --oneline --all
	218b94b (HEAD -> second) 222 추가
	e7b3c69 (master) eee 추가
	97cd89e 111 추가
	b2719ae ddd 추가
	5001ef9 ccc 추가
	f47ae62 bbb 추가
	4caac2a aaa 추가
```
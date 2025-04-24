
	10) 같은 파일의 merge (커밋충돌, CONFLICT)
	  - `code .` : conflict 상태에서 편집기에서 소스 편집
``` //* CONFLICT 실습
	MINGW64 /c/learn-git/repo7 (master)
	$ git branch feat3
	$ git branch feat4
	$ git switch feat3
	$ echo bbb123 >> b.txt
	$ cat b.txt
	bb
	b
	c
	bbb111
	bbb222
	bbb123
	$ echo bbb123 > b.txt
	$ cat b.txt
	bbb123
	$ git add .
	$ git commit -m 'bbb123 to b.txt'
	$ echo bbb456 >> b.txt
	$ git add .
	$ git commit -m 'add bbb456 to b.txt'
	$ git log --oneline --all --graph -3
	* 3465176 (HEAD -> feat3) add bbb456 to b.txt
	* f500b00 bbb123 to b.txt
	*   ea4d4eb (master, feat4) feat1 branch 반영
	|\
	$ git switch feat4
	$ cat b.txt
	bb
	b
	c
	bbb111
	bbb222
	$ echo bbbABC > b.txt
	$ cat b.txt
	bbbABC
	$ git add .
	$ git commit -m 'bbbABC to b.txt'
	$ echo bbbDEF >> b.txt
	$ git add .
	$ git commit -m 'add bbbDEF to b.txt'
	$ git log --oneline --all --graph -5
	* 88a1abc (HEAD -> feat4) add bbbDEF to b.txt
	* b859414 bbbABC to b.txt
	| * 3465176 (feat3) add bbb456 to b.txt
	| * f500b00 bbb123 to b.txt
	|/
	*   ea4d4eb (master) feat1 branch 반영
	|\
	$ cat b.txt
	bbbABC
	bbbDEF
	$ git switch master
	$ cat b.txt
	bb
	b
	c
	bbb111
	bbb222
	$ git merge feat3
	Updating ea4d4eb..3465176
	Fast-forward
	 b.txt | 7 ++-----
	 1 file changed, 2 insertions(+), 5 deletions(-)
	$ cat b.txt
	bbb123
	bbb456
	$ git merge feat4
	Auto-merging b.txt
	CONFLICT (content): Merge conflict in b.txt
	Automatic merge failed; fix conflicts and then commit the result.
	$ code .
	//* 편집기를 통해 conflict 소스 수정
	$ git add .
	$ git commit -m 'merge feat4'
	[master 9052e4f] merge feat4
	$ cat b.txt
	bbb123ABC
	bbb456DEF
	$ git log --oneline --all --graph -6
	*   9052e4f (HEAD -> master) merge feat4
	|\
	| * 88a1abc (feat4) add bbbDEF to b.txt
	| * b859414 bbbABC to b.txt
	* | 3465176 (feat3) add bbb456 to b.txt
	* | f500b00 bbb123 to b.txt
	|/
	*   ea4d4eb feat1 branch 반영
	|\
	$ git branch -d feat3
	$ git branch -d feat4
	$ git log --oneline --all --graph -6
	*   9052e4f (HEAD -> master) merge feat4
	|\
	| * 88a1abc add bbbDEF to b.txt
	| * b859414 bbbABC to b.txt
	* | 3465176 add bbb456 to b.txt
	* | f500b00 bbb123 to b.txt
	|/
	*   ea4d4eb feat1 branch 반영
	|\
```

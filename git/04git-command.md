
       - git 명령어
         - `git checkout {커밋번호}` : 커밋번호의 지점으로 파일 불러오기
``` //* git checkout 실습
    $ git checkout a660c5f
    $ cat a.txt
    $ git checkout 3eed969
    $ cat a.txt
```

     - git log로 기록을 볼 때 현재 커밋 지점(HEAD)에서부터 이전버전기록만 볼 수 있음
       - git 명령어
         - `git log --all` : 모든 커밋 기록 보기
         - `git log --all --oneline` : 모든 커밋 기록 한줄로 보기
     - branch : 커밋의 별칭
        - 커밋별칭을 커밋번호 대신 사용 가능 (명령어ex: git checkout / git branch)
        - 특별한 이유가 없다면 커밋번호 대신 branch명(별칭)으로 지정하여 사용할 것(checkout)
        - git 명령어
           - `git branch {별칭} {커밋번호}` : 특정 커밋번호에 별칭 지정 ({커밋번호} Default = 현재지점의 커밋번호)

``` //* git log/branch 실습
    $ git log --all --oneline
    $ git checkout 6b8e31e
    $ branch first a660c5f
    $ log --all --oneline
    $ git branch second 6b8e31e
    $ git branch last
    $ git log --all --oneline
    $ git checkout second
    $ cat a.txt
    $ git checkout last
    $ cat a.txt
    $ git branch third master
    $ git log --oneline
    d3bf95e (HEAD -> last) 4444를 a.txt에 추가
    3eed969 (third, master) 3333 추가
    6b8e31e (second) 2222를 a.txt에 추가
    a660c5f (first) 1111를 a.txt에 추가
```

       - detached HEAD : branch(별칭)을 가리키지 않는 HEAD 
          - 별칭아닌 커밋번호로 커밋이동(checkout)한 경우 
          - HEAD : 현재 지점
```//* HEAD 지점 이동 확인 실습
    $ echo 5555 >> a.txt
    $ git add .
    $ git commit -m '5555를 추가'
    $ git log --oneline
    9ce3aad (HEAD -> last) 5555를 추가
    d3bf95e 4444를 a.txt에 추가
    3eed969 (third, master) 3333 추가
    6b8e31e (second) 2222를 a.txt에 추가
    a660c5f (first) 1111를 a.txt에 추가
```
       - 커밋할 때, 새 커밋이 생기고 HEAD가 가리키는 Branch(별칭)가 새 커밋으로 이동하고 HEAD는 이동한  Branch 따라감
       - `git cat-file -p {커밋번호}` : 해당 커밋지점의 커밋정보
          - 커밋 번호 생성은 [누가/커밋작업자], [언제/커밋일시], [왜/커밋메시지], [부모(이전버전)커밋번호]를 기반으로 생성된다.
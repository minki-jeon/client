
       - Linux 기본 명령어
          (1) `pwd` (print working directory) : 현재 디렉터리 위치 출력
          (2) `ls` (list) : 현재 디렉터리에 저장되어 있는 파일 목록 출력
          (3) `clear` , [CTRL+L] : 화면 초기화
          (4) `ls -al` : 파일 목록 상세 출력 (숨김 파일 포함)
          (5) `cd {디렉터리명}`(change directory) : 디렉터리 이동
               - `cd ..` : 상위 디렉터리로 이동
               - `cd ~` : 사용자 디렉터리로 이동
               - `cd - ` : 이전 위치로 이동
          (6) `mkdir {디렉터리명} : 새 디렉터리 생성
          (7) [TAB] : 파일명 자동완성
          (8) [화살표 위/아래] : 이전 명령어 반환
          (9) `rm -d {디렉터리명}` : 디렉터리 삭제
          (10) `touch {파일명}` : 새 파일 생성
          (11) `rm {파일명}` : 파일 삭제
          (12) `cat {파일명}` : 파일 내용 보기
          (13) `echo "{텍스트}" ` : 텍스트 출력
          (14) `echo {텍스트} >> {파일명}` : 텍스트를 파일에 추가 입력 (기존 텍스트 다음줄에 입력)
          (15) `echo {텍스트} > {파일명}` : 텍스트를 파일에 새로 입력 (덮어쓰기)
``` //* 리눅스 명령어 실습
    $ mkdir learn-git
    $ cd learn-git/
    $ mkdir repo1
    $ rm -d repo1
    $ mkdir repo1
    $ cd repo1
    $ touch a.txt
    $ rm a.txt
 
    $ cd ../..
    $ cd learn-git
    $ mkdir repo2
    $ touch b.txt
    $ cat b.txt
    $ echo hello >> b.txt
    $ cat b.txt
    $ echo javascript >> b.txt
    $ cat b.txt
 
    $ touch c.txt
    $ echo hi >> c.txt
    $ echo git >> c.txt
    $ cat c.txt
 
    $ mkdir repo3
    $ cd repo3
```
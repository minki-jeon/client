
       - git 명령어
         - `git init` : 현재 위치의 디렉터리에 git repository 생성 (현재 디렉터리 내용을 버전관리)
         - `git add . ` : 변경된 파일 Stage 올리기
         - `git commit` : 현재 상태 저장 (커밋 메시지 입력을 위한 Editor Program Open)
                - Editor에서 1번째 라인에 커밋 메시지 (커밋하려는 이유) 작성
                ## git Editor 연결 ##
                - `git config --global core.editor "code --wait" `  # vscode 연결
                - `git config --global core.editor "vim" `  # vim 연결  
``` //* git add/commit 실습
    $ git init
    $ touch a.txt
    $ echo aaaaa >> a.txt
    $ echo bbbbb >> b.txt
    $ cat a.txt
    $ cat b.txt
    $ git add .
    $ git commit
```
       - git 명령어
          - `git log` : 커밋 기록 보기
          - `git log --oneline` : 커밋 기록 1줄씩 보기
          - `git commit -m "{커밋메시지}" : 현재 지점 커밋메시지와 저장
``` //* git log/commit -m 실습
    $ git log
    $ echo 2222 >> a.txt
    $ cat a.txt
    $ git add .
    $ git commit
    $ git log
    $ echo 3333 >> a.txt
    $ git add .
    $ git commit
    $ echo 4444 >> a.txt
    $ git add .
    $ git commit -m "4444를 a.txt에 추가"
    $ git log
    $ git log --oneline

    $ cd /c/learn-git
    $ mkdir repo4
    $ cd repo4
    $ pwd
```

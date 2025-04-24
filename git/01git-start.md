GIT 시작하기
       - 설치 / 설정 / 명렁 / .. 등
       - 'Windows Terminal' 설치
       - Git "https://git-scm.com" > Download for Windows > Click here to download
       - [Set up > Select Components]  "(NEW!) Add a Git Bash Profile to Windows Terminal" << Check !
          - Select to "Use Visual Studio Code as Git's default editor" 
          - < Installing >
       - [Windows Terminal (터미널)] > [설정] > [기본 프로필] Git Bash 선택 > 저장
       - Git 프로필 설정 : 
```
    $ git config --global user.name "{user-id}"
    $ git config --global user.email "{user-email}"
    $ git config --list
```
# **Git Cheat Sheet**
## **Setup**
깃 사용 시 기록에 남길 이름 및 이메일 초기 설정
```bash
$ git config --global user.name [name]   # 이름 설정
                      user.email [email] # 이메일 설정
```

## **Start**
로컬 저장소 초기화
```bash
$ git init (directory-name)  # 새 로컬 저장소 생성
$ git clone [repo-URL]  # 원격저장소 새로 내려받기
```

## **Commit**
파일 스테이징
```bash
$ git add [file]
$ git commit -m "commit message"
or
$ git commit -am "commit message"
```

## **Define**
작업 위치(브랜치) 및 원격 저장소 정의<br>

`origin` - 기본 원격 저장소 별칭<br>
`main` - 기본 개발 브랜치<br>
`HEAD` - 마지막 커밋<br>
`HEAD^` - 마지막 직전(부모) 커밋<br>
`HEAD~2` - 2개 위 부모 커밋

## **Upload**
파일 업로드
```bash
$ git push -u [repo-alias] [branch-name]
```
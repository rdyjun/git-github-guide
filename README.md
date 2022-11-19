# **Git Cheat Sheet**
## **Setup**
**깃 사용 시 기록에 남길 이름 및 이메일 초기 설정**
```bash
$ git config --global user.name [name]   # 이름 설정
                      user.email [email] # 이메일 설정
```

## **Start**
**로컬 저장소 초기화(준비)**

`init` 명령으로 새로운 저장소를 초기화하고<br>
```bash
$ git init <directory-name>  # 새 로컬 저장소 생성
```

`clone` 명령으로 기존 저장소를 가져온다.
```bash
$ git clone [repo-URL]  # 원격저장소 새로 내려받기
```

## **Update**
**로컬 저장소를 원격 저장소의 상태로 최신화합니다.**

`pull` 명령으로 로컬저장소를 최신화한다.
```bash
$ git pull <repo-URL>  #저장소 최신화
```

`fetch` 명령으로 원격 저장소의 최신 상태를 가져오며,<br>
현재 로컬 저장소와 병합 여부를 결정할 수 있다.
```bash
$ git fetch <repo-URL>
```

## **Remote-Repository**
**원격 저장소 연결**

원격 저장소 목록 확인
```bash
$ git remote -v
```

원격 저장소 추가(연결)
```bash
$ git remote add [repo-alias] [repo-URL]
```

원격 저장소 제거
```bash
$ git remote remove [repo-alias]
$ git remote rename [repo-alias] [new-alias]
```


## **Branch**
**각 기능(작업) 별 흐름**

브랜치 생성<br>
checkout과 switch를 통해 생성 즉시 이동 가능
```bash
$ git branch <new-branch>  # 브랜치 생성
$ git checkout -b [branch-name]  # 브랜치 생성 후 이동
$ git switch -c [branch-name]  # 브랜치 생성 후 이동
```

브랜치 삭제<br>
강제 삭제 시 수정 사항 존재 여부를 무시하고, 삭제
```bash
$ git branch -d [branch-name]
$ git branch -D [branch-name]  # 강제 삭제
```

브랜치 이동
```bash
$ git checkout [branch-name]  # 브랜치 변경
$ git switch [branch-name]  # 브랜치 변경
```

## **Staging**
**파일 스테이징**
```bash
$ git add [file]  # 파일 스테이징
$ git commit -m "commit message"  # 커밋 진행

$ git commit -am "commit message"  # add 실행 후 commit
```

## **Commit**
**작업 위치<브랜치> 및 원격 저장소 명칭**<br>

`origin` - 기본 원격 저장소 별칭<br>
`main` - 기본 개발 브랜치<br>
`HEAD` - 마지막 커밋<br>
`HEAD^` - 마지막 직전<부모> 커밋<br>
`HEAD~2` - 2개 위 부모 커밋

## **Merge**
**브랜치 상태에 따라 `3way`, `fast-forward` 방식 자동적용**
- 한 브랜치의 HEAD가 다른 브랜치의 조상 커밋이라면 `fast-forward` 방식 적용
- 그렇지 않다면 `3way` 방식 자동 적용
> ※ 3way는 각 병합한 결과를 새로운 커밋으로 생성한다.<br>
> ※ fast-forward는 파생된 브랜치의 커밋을 메인 브랜치에 이어준다.
```bash
$ git merge [branch-name]
# --no-ff 옵션 사용 시 3way 방식으로 병합
```

## **Rebase**
rebase 시 메인 브랜치의 HEAD가<br>
파생된 브랜치의 조상이 된다.
> ※ 파생된 브랜치의 커밋 기록 재정렬

```bash
$ git rebase main  # 현재 브랜치에 main 브랜치 수정사항 병합
$ git rebase -i HEAD  # 대화형으로 rebase 실행
```

## **Upload**
**파일 업로드**
```bash
$ git push [repo-alias] <branch-name>
```

## **Remove & Undo**
**삭제 및 되돌리기**
```bash
$ git rm [file-name]  # 파일 삭제
$ git rm --cached [file-name]  # 스테이징된 해당 파일 삭제

$ git reset HEAD~2  # 2개 전 커밋으로 돌아가며 뒤 커밋 제거
$ git revert HEAD~2  # 2개 전 커밋을 지우는 커밋 생성
```

## **Status**
**로컬 저장소 작업 상태 확인**
```bash
$ git status
$ git diff <commit1_ID> <commit2_ID>
# --staged 옵션은 sa-HEAD, HEAD 옵션은 wd-HEAD
$ git log
# --oneline 한 줄 요약, --graph 커밋 그래프 보기
```

## **Stash**
**작업중이던 내용 임시저장**<br>

워킹 디렉터리 & 스테이지의 `수정사항`을 임시 저장소로 이동시킴
```bash
$ git stash
$ git stash --keep-index  # 스테이지 상태는 그대로 유지
```
stash 목록을 유지한 상태로 불러오기
> ※ --index 옵션으로 스테이지 내용까지 불러오기
```bash
$ git stash apply
```
stash 목록에서 제거한 상태로 불러오기
> ※ --index 옵션으로 스테이지 내용까지 불러오기
```bash
$ git stash apply
```
브랜치 생성 후 해당 브랜치에 stash 내용 불러오기
```bash
$ git stash branch [branch-name]
```
stash 목록 전체 제거
```bash
$ git stash clear
```
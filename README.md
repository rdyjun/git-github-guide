# **Git Cheat Sheet**
## **Setup**
**깃 사용 시 기록에 남길 이름 및 이메일 초기 설정**
```bash
$ git config --global user.name [name]   # 이름 설정
                      user.email [email] # 이메일 설정
```

## **Start**
**로컬 저장소 초기화**
```bash
$ git init <directory-name>  # 새 로컬 저장소 생성
$ git clone [repo-URL]  # 원격저장소 새로 내려받기
```

## **Remote-Repository**
```bash
$ git remote -v
$ git remote add [repo-alias] [repo-URL]
$ git remote remove [repo-alias]
$ git remote rename [repo-alias] [new-alias]
```

## **Branch**
**각 기능<작업> 별 흐름**
```bash
$ git branch <new-branch>  # 브랜치 생성
# -d 브랜치 삭제, -D 브랜치 강제 삭제
$ git checkout [branch-name]  # 브랜치 변경
# -b 브랜치 생성
$ git switch [branch-name]  # 브랜치 변경
# -c 브랜치 생성
```

## **Staging**
**파일 스테이징**
```bash
$ git add [file]
$ git commit -m "commit message"
or
$ git commit -am "commit message"
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
```bash
$ git merge [branch-name]
# --no-ff 3way 방식으로 병합
```

## **Rebase**

```bash
$ git rebase main  # 현재 브랜치에 main 브랜치 수정사항 병합
$ git rebase -i HEAD  # 
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
$ git revert HEAD~2  # 2개 전 커밋을 자우는 커밋 생성
```

## **Status**
**로컬 저장소 작업 상태 확인**
```bash
$ git status
$ git diff <commit1_ID> <commit2_ID>
# --staged sa-HEAD, HEAD wd-HEAD
$ git log
# --oneline 한 줄 요약, --graph 그래프 보기
```
# **:page_with_curl: git-command**
각종 깃 명령어 정리

## **:outbox_tray: 로컬 저장소에서 원격 저장소로 보내기**
### **git add**
지정한 working directory의 수정사항을 스테이지로 올린다.
```bash
git add .  # [.]은 현재 폴더 내 전체 파일을 의미
```

### **git commit**
스테이지에 올라온 수정사항을 고유번호를 지정해 저장<br>
`-am` 속성으로 add를 같이 할 수 있다.
> ※ -am 사용 시 untracked 파일은 add되지 않는다.<br>
> ※ 별도로 `git add` 을 해주어야 함.
```bash
git commit -m "커밋 메시지"
git commit -am "커밋 메시지"
```

### **git push**
커밋한 기록들(수정사항)을 원격 저장소로 보냅니다.<br>
`-u(--set-upstream)` 옵션을 통해 별칭 및 브랜치명을 작성하지 않고도 push할 수 있다.
```bash
git push [원격 저장소 별칭] [브랜치명]
git push -u [원격 저장소 별칭] [브랜치명]
git push  # 위 -u를 포함한 명령이 선행되어야 실행가능
```

## **:white_check_mark: 작업상태 확인**
### **git log**
여태 진행한 커밋 기록을 확인합니다.
```bash
git log
git log [commit ID]  # 특정 커밋 확인
git log --oneline  # 커밋 기록을 한 줄로 출력
git log -[Num]  # 최근 커밋 2개 출력
git log --graph  # 커밋 기록을 브랜치에 따른 그래프 확인 가능
```

### **git show**
커밋의 상세정보(수정사항)을 확인합니다.
```bash
git show  # 이전 커밋과의 수정사항을 출력합니다.
git show [commit ID]  # 선택한 커밋과 제일 최신 커밋(HEAD)을 비교합니다.
```

### **git diff**

```bash
git diff           # wd와 sa의 차이 확인
git diff HEAD      # wd와 head 커밋 차이 확인
git diff --cached  # sa와 head 커밋 차이 확인
git diff --staged  # cached와 동일
```

<br>

## **:inbox_tray: 저장소 내려받기**
### **git clone**
원격 저장소로부터 파일을 로컬 저장소로 내려받습니다.<br>
`-o` 옵션 사용 시 원격 저장소의 별칭을 지정할 수 있습니다.
> ※ `-o` 옵션을 사용하지 않으면 `origin` 으로 지정됩니다.

```bash
git clone [원격 저장소 URL]
git clone [원격 저장소 URL] -o [별칭]
```

### **git pull**
로컬 저장소에 원격 저장소의 파일이 있으나,<br>
로컬 저장소의 파일이 원격 저장소의 파일보다 버전이 낮을 때 최신화합니다. 
```bash
git pull
```

### **git fetch**
pull과 마찬가지로 저장소를 최신화 하지만, 이를 바로 적용하지 않고,<br>
임시 브랜치에 저장됩니다. 이때, [merge](#병합-merge) 해주어야 적용됩니다.
```bash
git fetch [원격저장소 URL]
```

<br>

## **✨ 병합**
### **git merge**
메인 브랜치의 헤드가 파생된 브랜치의 조상 커밋이 아니라면, 3way로 자동 적용됩니다.<br>
메인 브랜치의 헤드가 파생된 브랜치의 조상 커밋이라면, fast-forward 방식이 적용됩니다.
> ※ --no-ff 옵션으로 fast-forward 상황에서 3way 방식으로 적용할 수 있습니다.<br>
> ※ 3way 방식은 두 브랜치를 합친 새로운 커밋을 생성하는 방식입니다.<br>
> ※ fast-forward 방식은 메인 브랜치가 병합할 브랜치의 커밋을 가지는 방식입니다.<br>
```bash
git merge [브랜치명]  # 자동으로 3way, fast-forward 구분해서 실행
git merge [브랜치명] --no-ff  # 3way 방식으로 실행
```

### **git rebase**
파생된 브랜치의 조상을 메인 브랜치의 헤드로 옮기고 병합합니다.
```bash
git rebase [브랜치명]  
git rebase --continue  # 충돌 발생 시 충돌을 해결하고 continue를 통해 rebase 적용
git rebase --abort  # rebase를 취소
git rebase -i HEAD~3  # 3개의 커밋 묶기
```

<br>

## **브랜치 - 작업흐름**
### git branch
프로젝트에서 각 기능별 흐름을 나타내는 브랜치를 표시합니다.<br>
`-d` 옵션 사용 시 브랜치를 삭제하지만, 수정사항이 남아있다면 삭제되지 않습니다.<br>
`-D` 사용 시 해당 브랜치의 수정사항 여부에 관계없이 삭제합니다.
```bash
git branch  # 브랜치 목록 출력
git branch -d  # 삭제
git branch -D  # 강제삭제
git branch [브랜치명]  # 브랜치 생성
```

### **git checkout**
현재 브랜치를 떠나 새로운 브랜치로 이동합니다.
```bash
git checkout [브랜치명]  # 해당 브랜치로 이동
git checkout -- [파일명]  # 해당 파일로 이동
git checkout -b  # 새 브랜치를 생성하고 이동
```

### **git switch**
```bash
git switch [브랜치명]  # 해당 브랜치로 이동
git switch -c [브랜치명] # 새 브랜치를 생성하고 이동
```

<br>

## **커밋 취소**
### **reset**
직접적으로 기존의 커밋을 제거하고, 전의 커밋을 헤드로 가집니다.
- `-soft` 옵션은 커밋 기록만 지우고 브랜치가 이전 커밋을 가리키지만,<br>
- 파일은 전으로 돌아가지 않습니다.
- `-mixed` 옵션은 soft와 같이 브랜치가 이전 커밋을 가리키며,<br>
- 작업중인 working directory는 두고, staging area만 전으로 돌아갑니다.
- `hard` 옵션은 커밋 기록과 그 기록 속 수정사항들을 모두 삭제합니다.
```bash
git reset [옵션] [commit ID]  # 해당 커밋까지 되돌리기
git reset HEAD~  # -mixed 옵션을 사용해서 리셋
git reset -soft HEAD~
git reset -mixed HEAD~
git reset -hard HEAD~
git reset –merge HEAD~  # 병합된 커밋 취소
```

### **revert**
reset과 다르게 커밋 기록이 전으로 돌아가지 않고,<br>
취소하고자 하는 커밋 기록에 대한 수정사항을 `적용하지 않은 커밋`을 새로 생성합니다.
```bash
git revert [commit ID]  # 해당 커밋 삭제
git revert [commit ID] .. [commit ID]  # 커밋 범위를 지정해 삭제
git revert --mainline [Number] [merge-commit ID]  # 병합 취소
```



<br>

## **작업 스테이지 임시저장**
### **git stash**

커밋할 필요 없이 파일의 변경 사항을 숨기거나 비밀리에 저장할 수 있는 도구

- `git log --all` 로 확인 시 stash 정보도 나온다.

```bash
git stash                    # wa, sa 임시 저장 및 wd, sa 수정 사항 지우기
git stash -u                 # untracked 파일까지 임시 저장
git stash list               # stash 목록 확인
git stash show               # stash와 현재 디렉터리의 차이
git stash show -p            # 차이를 더 자세히 보기
git stash show -p stash@{1}  # 1번째 index의 stash 와 wd 차이 보기

# pop
git stash pop                # 임시로 저장한 wd 불러오기 (stash 목록에서 빠짐)
git stash pop --index        # wd와 sa 까지 이동 적용

# apply
git stash apply              # 임시로 저장한 wd 불러오기 (stash 목록 유지)
git stash apply --index      # wd와 sa 까지 복사 적용

# keep index
git stash --keep-index       # sa는 유지하고 wd만 복사함

git stash branch [브랜치명]    # 브랜치 생성 및 해당 브랜치에 wd, sa, ut 복사

git stash clear              # stash list 삭제
```

### **git clean**

```bash
git clean     # ut 파일 삭제 (삭제 안됨)
git clean -f  # ut 파일 강제 삭제
git clean -n  # ut 파일 목록 확인g
git clean -i  # 대화모드로 삭제
# Would remove the following item:
# [삭제 목록]
# *** Commands ***
# 1: clean                2: filter by pattern    3: select by numbers
# 4: ask each             5: quit                 6: help
# What now>
```
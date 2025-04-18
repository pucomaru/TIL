
# 📌 Git 명령어 정리: branch, switch, stash

## 🌿 git branch
브랜치 관련 작업을 할 때 사용하는 명령어

| 명령어 | 설명 |
|--------|------|
| `git branch` | 현재 존재하는 브랜치 목록 확인 |
| `git branch <브랜치명>` | 새로운 브랜치 생성 (체크아웃은 안 됨) |
| `git branch -d <브랜치명>` | 브랜치 삭제 (병합된 브랜치만 삭제됨) |
| `git branch -D <브랜치명>` | 강제 브랜치 삭제 |

---

## 🔄 git switch
브랜치를 **이동**하거나 **생성 + 이동**할 때 사용

| 명령어 | 설명 |
|--------|------|
| `git switch <브랜치명>` | 다른 브랜치로 이동 |
| `git switch -c <새_브랜치명>` | 브랜치 생성 + 이동 (= git checkout -b) |
| `git switch -` | 직전에 있던 브랜치로 이동 |

> 💡 `git checkout` 명령어를 `switch`/`restore`로 나눠서 더 명확하게 사용 가능

---

## 🧳 git stash
작업 중인 변경사항을 **임시로 저장(숨김)**해두는 명령어

| 명령어 | 설명 |
|--------|------|
| `git stash` | 수정된(tracked) 파일만 임시 저장 |
| `git stash -u` | 수정된 파일 + 추적되지 않은(untracked) 새 파일까지 저장 |
| `git stash -a` | 수정된 파일 + untracked + .gitignore된 파일까지 전부 저장 |
| `git stash list` | 저장해둔 stash 목록 확인 |
| `git stash apply` | 가장 최근 stash를 다시 적용 (stash는 그대로 유지됨) |
| `git stash pop` | 가장 최근 stash를 적용하고 목록에서 삭제 |
| `git stash drop` | 특정 stash를 삭제 |
| `git stash clear` | stash에 저장된 모든 항목 삭제 |

### ❗️왜 `stash`를 써야 할까?

- `git pull`, `git switch` 등을 하려면 **작업 중이던 파일이 깔끔해야 함**  
  → 하지만 아직 커밋하기 애매한 상태면 잠깐 저장해야 할 필요가 있음
- 그럴 때 `git stash`를 사용해서  
  **변경사항을 임시로 보관하고, 브랜치를 이동하거나 병합할 수 있음**

> 즉, **작업 중이던 내용을 날리지 않고 안전하게 숨겨두는 안전장치!**

---

### 📎 `git stash -u`를 왜 써야 해?

- 기본 `git stash`는 **수정된 파일(tracked)**만 저장함
- **새로 만든 파일(아직 git add 안 한 파일)**은 포함되지 않음
- 이럴 때 `-u` 옵션(`--include-untracked`)을 쓰면 **추적되지 않은 파일도 함께 stash** 됨

```bash
git stash -u  # 수정 + 새 파일까지 모두 안전하게 임시 저장
```

> 💡 실무에서 새 파일도 같이 작업 중이라면 `-u` 옵션은 거의 필수!

---

## ✅ 협업 중 develop 브랜치가 업데이트되었을 때

```bash
git switch feature/dayea        # 내가 작업 중이던 브랜치로 이동
git stash -u                    # 현재 작업 내용 + 새 파일까지 임시 저장
git pull origin develop         # 최신 develop 내용 병합
git stash pop                   # 작업 다시 복원
```

> 💡 stash 안 하고 pull 하면 충돌날 수도 있고, Git이 거부할 수도 있음!


---

# 🚀 GitHub로 협업하는 그룹 프로젝트 가이드

팀 프로젝트에서 Git과 GitHub를 활용해 효율적으로 협업하는 방법을 정리한 문서입니다.

---

## 1️⃣ 프로젝트 환경 설정

### ✅ GitHub 저장소 생성 및 연결

- **GitHub에 저장소가 이미 존재할 경우**

```bash
git clone <원격 저장소 URL>
cd <프로젝트 폴더>
```

- **로컬에서 먼저 작업한 경우**

```bash
git init
git remote add origin <원격 저장소 URL>
```

> 📌 `clone`은 원격 저장소 전체를 복사해오며 자동으로 연결까지 해줍니다.  
> 📌 `remote add`는 로컬 저장소를 나중에 원격 저장소에 연결할 때 사용합니다.

---

## 2️⃣ 브랜치 전략

### 🧾 브랜치 역할

| 브랜치명             | 역할 설명 |
|----------------------|-----------|
| `main` / `master`    | 최종 배포용 브랜치 (유저가 보는 완성본) |
| `develop`            | 개발자들이 작업하는 메인 브랜치 |
| `feature/기능이름`   | 실제 기능 구현을 위한 개별 브랜치 |

> ❗ `main`에서는 직접 작업하지 않습니다.  
> `develop`에서 `feature` 브랜치를 따서 작업하고, merge 과정을 통해 `main`까지 올립니다.

### ✅ 로컬에서 브랜치 생성 및 푸시

```bash
git branch feature/기능이름
git push --set-upstream origin feature/기능이름
```

---

## 3️⃣ `main` 브랜치 보호 설정

> ⚙️ GitHub → `Settings` → `Branches` → `Add branch protection rule`

- `main` 브랜치를 직접 푸시하지 못하도록 보호
- Pull Request를 통해서만 merge 가능하게 설정

**추천 설정:**
- ✅ Require pull request before merging
- ✅ Require status checks to pass
- ✅ Include administrators

---

## 4️⃣ GitHub Projects로 업무 보드 생성

> GitHub → `Projects` → `New Project` → Kanban 보드 선택

- 각 업무를 **Issue로 전환**해 관리
- Issue에서 브랜치를 바로 생성 가능 (`develop` 기준 브랜치 사용)

```bash
git fetch origin
git switch <브랜치명>
```

---

## 5️⃣ 기능 브랜치 개발

- 브랜치명: `feature/login`, `feature/api`, `fix/bug-name` 등
- 커밋은 **작업 단위로 작게**, 커밋 메시지는 명확하게 작성

```bash
git add .
git commit -m "feat: 로그인 페이지 구현"
git push origin feature/login
```

---

## 6️⃣ Pull Request(PR) 생성

> GitHub에서 `feature` 브랜치를 `develop` 브랜치로 PR 생성  
> 팀원들이 코드 리뷰 후 승인 시 merge

**PR 제목 예시:**

```
[feat] 로그인 기능 구현
```

**본문 예시:**

- 작업 내용: 로그인 로직 구현, 세션 저장 처리
- 관련 이슈: #3
- 테스트 완료 여부: ✅

---

## 7️⃣ 충돌 해결 전략

- 충돌은 **`feature` 브랜치에서 `develop`을 merge**하여 해결  
  (**반대로 develop에서 feature로 merge 금지**)

```bash
git checkout feature/기능이름
git pull origin develop  # 최신 develop 코드 가져오기
# 충돌 해결 후
git add .
git commit -m "resolve: merge conflict with develop"
```

---

## 8️⃣ 최종 배포

- `develop` 브랜치의 기능과 테스트가 모두 완료되면,
- `develop` → `main`으로 Pull Request 생성 후 배포

```bash
git switch main
git merge develop
git push origin main
```

---

## ✅ 협업 체크리스트

- [ ] 항상 `develop`에서 브랜치를 따온다
- [ ] 브랜치명, 커밋명은 명확하고 일관되게
- [ ] PR 시 리뷰어 지정, 설명 작성
- [ ] `main` 브랜치는 직접 수정 금지
- [ ] 기능 단위로 커밋 & PR


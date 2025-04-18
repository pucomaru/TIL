
# 🧰 유용한 CLI 명령어 모음

개발하면서 자주 사용하는 CLI 명령어들을 정리한 문서입니다.  
간결하게 커밋 로그를 확인하거나, 자주 쓰는 명령어를 줄여서 쓰고 싶을 때 유용합니다!

---

## 📌 1. 커밋 로그 간단히 보기

```bash
git log --oneline
```

### ✅ 설명
- 커밋 로그를 **한 줄 요약 형식**으로 출력해줌
- 커밋 해시 + 메시지 간단하게 확인 가능
- 많은 커밋 내역을 **빠르게 확인**하고 싶을 때 유용


## 🧠 2. 자주 쓰는 명령어 alias 등록하기

```bash
git config --global alias.st status
```

### ✅ 설명
- `git st` 입력만으로 `git status` 실행 가능
- `alias.<단축어> <원래명령어>` 형식으로 설정
- `--global` 옵션을 주면 **전체 환경에서 적용됨**

### 🔧 자주 쓰는 alias 예시

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm 'commit -m'
git config --global alias.last 'log -1 HEAD'
```

---

## 🌱 alias 확인 및 관리

### 🔍 등록된 alias 확인
```bash
git config --get-regexp alias
```

### 🧹 alias 삭제
```bash
git config --global --unset alias.st
```

---


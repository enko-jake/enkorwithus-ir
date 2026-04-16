---
name: update-ir
description: enkorwithus-ir 레포의 변경사항을 요약 커밋 메시지로 main에 푸시합니다. pat.txt의 토큰을 인증에 사용하고, 푸시 완료 후 배포 링크를 안내합니다. 트리거 - "/update-ir", "IR 업데이트", "IR 배포"
---

# Update IR Skill

enkorwithus-ir 프로젝트의 변경 사항을 커밋하고 main 브랜치에 푸시하여 GitHub Pages 배포를 트리거합니다.

## 사전 조건

- 현재 작업 디렉토리가 `enkorwithus-ir` 레포의 루트여야 함
- 프로젝트 루트에 `pat.txt` 파일이 존재하고, 유효한 GitHub Personal Access Token(한 줄)이 저장돼 있어야 함
- `pat.txt`는 `.gitignore`에 포함돼 있어야 함 (커밋 금지)

## 실행 절차

### 1. 변경사항 확인

```bash
git status --short
git diff --stat
```

- 변경된 파일이 없으면 "변경사항이 없다" 알리고 종료
- `pat.txt`가 staged 혹은 변경 후보로 잡혀 있으면 **즉시 중단**하고 사용자에게 경고 (토큰 유출 방지)

### 2. 커밋 메시지 작성

- `git diff`의 핵심 변경을 한 줄 요약 (conventional commit 스타일)
- 예시 형식: `feat: ~~ 추가`, `fix: ~~ 수정`, `docs: ~~ 업데이트`, `style: ~~ 디자인 조정`
- 메세지에 author 등 변경 요약 내용 외에 불필요한 내용 포함 금지
- **간결하게**, 70자 이내

### 3. 토큰 읽기

```bash
TOKEN=$(cat pat.txt | tr -d '\n' | tr -d ' ')
```

- 토큰은 메모리상에서만 사용, 로그/출력에 절대 노출 금지

### 4. 커밋 & 푸시

```bash
git add -A
git commit -m "<요약 메시지>"
git push "https://${TOKEN}@github.com/enko-jake/enkorwithus-ir.git" main
```

- 푸시 시 URL에 토큰이 들어가므로, 출력에서 토큰 부분은 마스킹하거나 명령어 자체를 사용자에게 보여주지 말 것
- 사용자에게는 "푸시 중..." 정도로만 안내

### 5. 결과 안내

푸시가 성공하면 아래 형식으로 알림:

```
업데이트 완료! 🚀
커밋: <메시지>
1~2분 뒤 https://ir.enko.kr/ 에 반영됩니다.
```

푸시가 실패하면 원인(인증 실패 / 네트워크 / 충돌)을 짧게 알리고 해결 방향 제시.

## 주의사항

- `pat.txt`는 **절대** `git add`로 포함되면 안 됨. `.gitignore` 확인 필수
- 푸시 명령어의 토큰 포함 URL을 히스토리나 출력에 남기지 말 것
- `index.html`의 `data-i18n` 텍스트를 직접 수정한 변경이 섞여 있으면 주의 (CLAUDE.md 규칙)
- rebase / force-push 금지, 일반 push만 수행

## 실패 처리

- `403`/`401`: 토큰이 만료됐거나 권한 부족. GitHub에서 PAT 재발급 후 `pat.txt` 교체 안내
- `non-fast-forward`: 원격이 앞서 있음. `git pull --rebase origin main` 후 재시도 제안
- pre-commit hook 실패: 에러 그대로 보여주고 사용자 판단 요청

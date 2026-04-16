---
name: setup-vibe-coding
description: 새 macOS PC에서 IR 레포 작업을 이어가기 위한 최소 개발 환경(homebrew, git)을 점검/설치합니다. 트리거 - "/setup-vibe-coding", "새 PC 세팅", "환경 세팅"
---

# Setup Vibe Coding Skill

새 macOS 환경에서 enkorwithus-ir 프로젝트 작업을 바로 시작할 수 있게 기본 도구(homebrew, git)를 확인하고 없으면 설치합니다.

## 실행 절차

### 1. Homebrew 확인

```bash
which brew
```

- 있으면: 버전 확인 (`brew --version`)만 출력하고 다음 단계로
- 없으면: 설치 진행

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

설치 중 sudo 비밀번호 입력이 필요할 수 있음을 사용자에게 미리 알림.
설치 후 Apple Silicon(M시리즈)인 경우 PATH 추가 안내:

```bash
# Apple Silicon (M1/M2/M3/M4 등)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# Intel Mac
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

### 2. Git 확인

```bash
which git && git --version
```

- 있으면: 버전만 출력
- 없으면: `brew install git` 실행

### 3. Git 사용자 정보 점검 (권장)

```bash
git config --global user.name
git config --global user.email
```

둘 중 하나라도 비어있으면 사용자에게 텍스트로 질문:
- "git user.name / user.email이 설정돼 있지 않다용. 기존 PC와 동일하게 `Jake-enkor` / `jonghyeon.jun@enkor.kr` 로 설정할까용?"

동의 시:
```bash
git config --global user.name "Jake-enkor"
git config --global user.email "jonghyeon.jun@enkor.kr"
```

### 4. 결과 보고

- 각 도구의 설치 여부/버전을 표로 정리해 보고
- 추가로 필요한 작업(Claude Code 설치, PAT 파일 준비 등)은 `SETUP.md` 혹은 대화로 안내

## 주의사항

- Homebrew 설치는 네트워크/권한에 따라 수 분 소요될 수 있음 — 백그라운드로 실행 후 진행 상황 모니터링 권장
- 사용자가 Intel Mac인지 Apple Silicon인지 `uname -m` 로 확인 후 PATH 지시
- 이미 설치돼 있으면 **건드리지 말 것** (버전 업그레이드 금지)

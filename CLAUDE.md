# Enkorwithus IR One-Pager

## 프로젝트 개요

엔코위더스(Enkostay) Series A 투자 유치용 IR 웹페이지.
GitHub Pages로 호스팅되며, 단일 `index.html` 파일로 구성됨.

- **배포 URL**: https://enko-jake.github.io/enkorwithus-ir/
- **레포지토리**: https://github.com/enko-jake/enkorwithus-ir
- **GitHub Pages 설정**: `main` 브랜치 / `/ (root)` 경로

## 파일 구조

```
enkorwithus-ir/
├── CLAUDE.md      ← 이 문서
└── index.html     ← IR 웹페이지 (CSS, JS, SVG 로고 모두 인라인)
```

## 기술 구조

### 단일 파일 구성
- CSS, JavaScript, SVG 로고가 모두 `index.html` 안에 인라인으로 포함
- 외부 의존성: Google Fonts (Noto Sans KR, Inter), YouTube 썸네일 이미지 (hqdefault.jpg)
- 별도 빌드 과정 없음

### 한/영 전환 (i18n)
- `<script>` 내부의 `i18n` 객체에 `en`, `kr` 키로 텍스트 관리
- HTML 요소에 `data-i18n="키이름"` 속성으로 바인딩
- `switchLang('en')` / `switchLang('kr')` 함수로 전환
- 기본 언어: EN

### 디자인
- 원본 PDF(`Enkorwithus One pater.pdf`)의 디자인을 그대로 재현
- 컬러 테마: 올리브(#3E3C1F) 헤더/다크섹션, 골드(#F8E585) 강조, 크림(#FFF9E8) 배경
- 로고: enkostay 공식 SVG를 흰색으로 변환하여 인라인 삽입

### 반응형
- PC (900px 이상): PDF 원본과 동일한 레이아웃
- 태블릿 (768px 이하): 타이틀 숨김, 팀 2열
- 모바일 (480px 이하): 스탯바 3+2 줄바꿈, 마켓 세로 스택, 팀 2x2
- 소형 모바일 (360px 이하): 추가 축소

### 섹션 구성 (순서)
1. 올리브 헤더 (로고 + tagline + Series A 배지 + KR/EN 토글)
2. 스탯바 ($20.7M, $5.2M, 258%, 18x, 13%+)
3. Executive Summary (Problem / Solution / Revenue)
4. Traction (GMV 바 차트, Q1'24 ~ Q1'26)
5. Unit Economics (CAC $22, LTV $406, ROI 18x, Repurchase 57%)
6. Market (TAM $113B, SAM $23B, SOM $3B)
7. Competitive Moats (5개 항목)
8. The Ask ($7M Series A, 2026 목표, 자금 사용)
9. Team (CEO, CTO, COO, IT Advisor)
10. Backed By (투자자 + 파트너)
11. CEO Interview (YouTube 썸네일 + 재생 버튼, 클릭 시 YouTube 이동)
12. 하단 스탯바 (40K+ Members, 10K+ Listings, 500K Nights, 7K+ Hosts)
13. 푸터 (연락처, LinkedIn, enko.kr)

### YouTube 영상
- 해당 영상(W2nHHiIWuqk)은 소유자가 외부 임베드를 차단함
- iframe 대신 썸네일 이미지(`hqdefault.jpg`) + 재생 버튼 → 클릭 시 YouTube로 이동하는 방식

## 수정 후 배포 방법

```bash
# 1. 레포 클론 (최초 1회)
git clone https://github.com/enko-jake/enkorwithus-ir.git
cd enkorwithus-ir

# 2. index.html 수정

# 3. 커밋 & 푸시
git add index.html
git commit -m "변경 내용 설명"
git push origin main

# push 후 1~2분 내에 자동 배포됨
```

## 수정 시 주의사항

- `data-i18n` 속성이 있는 요소의 텍스트를 직접 수정하면 안 됨. `<script>` 내부 `i18n` 객체의 `en`/`kr` 값을 수정해야 함.
- 수치나 텍스트 변경 시 `en`, `kr` 양쪽 모두 수정할 것.
- SVG 로고는 인라인이므로 변경 시 HTML 내부의 SVG 코드를 직접 수정해야 함.

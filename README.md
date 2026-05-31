# 5×5 강함

StrongLifts 5×5 프로그램 기반 스트렝스 훈련 트래커 PWA.

## 개요

바벨 3대 운동(스쿼트, 벤치프레스, 데드리프트)을 StrongLifts 5×5 메커니즘에 따라 기록하고 진행상황을 추적하는 모바일 웹앱.

## 기능

### 훈련 흐름
- 훈련 시작 전 준비 화면 — 다음 훈련 무게 및 연속 실패 현황 표시
- 세트 체크 (한 방향, 취소 불가)
- 종목별 **성공 / 실패** 직접 선택
- 저장 전 결과 미리보기 (다음 훈련 무게 확인)

### StrongLifts 5×5 메커니즘
- 스쿼트 / 벤치프레스: 매 훈련 성공 시 **+2.5kg** 증량
- 데드리프트: 초반 **+5kg**, 첫 실패 이후 **+2.5kg**으로 자동 전환
- 데드리프트는 **1×5** (1세트)
- 실패 시 무게 유지
- **3연속 실패 시 10% 디로드** (자동 계산 및 적용)

### 기록 & 통계
- 훈련 히스토리 (날짜, 무게, 성공/실패 여부)
- 종목별 개인 최고 기록 (PR) 자동 추적
- 총 훈련 횟수, 이번 달 횟수, 완전 성공률
- 현재 연속 실패 카운트

### 기타
- 모든 데이터 localStorage 로컬 저장
- 홈화면 추가 시 앱처럼 실행 (PWA 메타태그)

## 기술 스택

- HTML / CSS / JavaScript — 단일 파일 (`index.html`)
- [Alpine.js v3](https://alpinejs.dev) (MIT) — 선언적 상태 관리 및 DOM 바인딩
- [Lucide Icons](https://lucide.dev) (MIT) — 아이콘
- [DM Sans + DM Mono](https://fonts.google.com) (Google Fonts, OFL) — 폰트
- `localStorage` — 데이터 저장

> **단일 파일 전략**: 산출물 관리 편의상 HTML·CSS·JS를 `index.html` 하나로 통합. Alpine.js, Lucide, 폰트는 CDN 참조 (온라인 환경 전제).

## 아키텍처

초기 Vanilla JS로 `renderXxx()` 함수 기반 DOM 직접 조작 방식으로 작성했다가 Alpine.js로 리팩터링.

- **이전**: 상태 변경 시 `document.getElementById` + `innerHTML` 직접 조작
- **이후**: `x-data`, `x-for`, `x-show`, `:class`, `x-text` 선언적 바인딩으로 교체
- JS는 `app()` 함수 하나에 순수 로직만 담당, DOM 조작 코드 제거
- 리팩터링 결과 1046줄 → 705줄 (-32%)

## 디자인

- 라이트 모드 / 플랫 디자인
- 흰색 베이스, 종목별 컬러 포인트 (스쿼트 오렌지 / 벤치 블루 / 데드 퍼플)
- 헤더·네비 블러 효과
- 모바일 퍼스트, safe-area-inset 대응

## 파일 구조

```
index.html   # 앱 전체 (HTML + CSS + JS + Alpine.js 바인딩)
README.md
DEPLOY.md
```

## 제작 방식

Claude (Anthropic)와의 대화로 전체 기획 및 개발 진행. 코드를 직접 작성하지 않고 요구사항을 대화로 전달하는 방식으로 제작.

### 주요 대화 흐름
1. 앱 기획 — 운동 종목, 플랫폼(PWA), 핵심 기능 결정
2. StrongLifts 5×5 메커니즘 리서치 — Claude가 웹 검색 후 정확한 규칙 확인 및 공유
3. 기능 반복 개선 — 훈련 흐름, 성공/실패 판정 방식, 세트 입력 UX 수정
4. 디자인 리뉴얼 — 라이트 플랫 디자인, Lucide 아이콘, DM Sans 폰트 적용
5. Alpine.js 리팩터링 — 선언적 상태 관리로 전환, 코드 경량화
6. 배포 설정 — GitHub Pages 배포 방법 가이드

### 사용 AI 도구
- **Claude Sonnet (Anthropic)** — 기획, 코드 생성, 디자인, 문서 작성 전반

## 개선 시 참고

- 데이터 스키마: `localStorage` 키 `fx5_v3`
- 상태 구조: `weights`, `fails`, `history`, `deadBig`, `workoutActive`, `inProgress`
- 히스토리 항목: `{ id, date, num, weights, tapped, results }`
- 종목 키: `squat`, `bench`, `dead`
- Alpine 상태: `app()` 함수 내 `return {}` 객체가 단일 진실 공급원
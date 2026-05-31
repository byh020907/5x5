# 배포 가이드 (GitHub Pages)

## 배포 정보

| 항목 | 내용 |
|---|---|
| 플랫폼 | GitHub Pages (무료) |
| 저장소 | `{유저명}/5x5` (Public) |
| URL | `https://{유저명}.github.io/5x5/` |
| 브랜치 | `main` |

---

## 최초 배포 절차

### 1. GitHub 저장소 생성
1. [github.com](https://github.com) 로그인
2. 우상단 **+** → **New repository**
3. Repository name: `5x5`
4. Description: `StrongLifts 5x5 strength training tracker PWA`
5. **Public** 선택
6. **Create repository** 클릭

### 2. 파일 업로드
1. 로컬에서 `5x5-strength.html` → `index.html` 로 rename
2. 저장소 페이지 → **uploading an existing file** 클릭
3. `index.html` 드래그 업로드
4. Commit message: `Add 5x5 training app`
5. **Commit changes** 클릭

### 3. GitHub Pages 활성화
1. 저장소 → **Settings** 탭
2. 왼쪽 사이드바 → **Pages**
3. Source → **Deploy from a branch**
4. Branch → **main** / `/(root)`
5. **Save** 클릭
6. 1~2분 후 URL 활성화 확인

### 4. 홈화면에 추가 (PWA)
- **iOS Safari**: 공유 버튼(□↑) → 홈 화면에 추가
- **Android Chrome**: 메뉴(⋮) → 앱 설치 또는 홈 화면에 추가

---

## 이후 업데이트 방법

### GitHub 웹에서 직접 수정
1. 저장소 → `index.html` 클릭
2. 연필 아이콘(Edit this file) 클릭
3. 내용 수정 후 **Commit changes**
4. 30초~1분 후 자동 배포

### 로컬에서 수정 후 업로드
1. `index.html` 수정
2. 저장소 → `index.html` → 연필 아이콘
3. 전체 내용 교체 후 Commit

---

## 주의사항

- 저장소가 **Public**이어야 GitHub Pages 무료 사용 가능
- 데이터는 각 기기의 localStorage에 저장 — 기기 간 동기화 없음
- 앱 삭제(홈화면에서 제거)해도 데이터는 브라우저 localStorage에 남아 있음
- 브라우저 데이터 삭제 시 기록 초기화됨
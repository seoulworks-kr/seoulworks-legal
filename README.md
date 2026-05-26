# GitHub Pages 호스팅 가이드

이 폴더의 파일들을 GitHub Pages에 올려서 무료로 호스팅하는 방법.

---

## 결과물 미리보기

호스팅 완료 후 URL:
- 인덱스: `https://[your-username].github.io/seoulworks-legal/`
- Privacy Policy: `https://[your-username].github.io/seoulworks-legal/privacy.html`
- Terms: `https://[your-username].github.io/seoulworks-legal/terms.html`

위 URL이 Play Console / AdMob / 앱 내 링크에 들어갈 주소.

---

## 사전 준비

- GitHub 계정 (없으면 https://github.com/signup 에서 무료 가입)
- 본인 PC에 Git 설치 (선택: 웹에서만 해도 됨)

---

## 방법 A: 웹브라우저로만 (제일 쉬움, 추천)

### 1. 새 Repository 만들기

1. https://github.com 로그인
2. 우측 상단 `+` → `New repository` 클릭
3. 입력:
   - **Repository name**: `seoulworks-legal`
   - **Description**: `Privacy Policy and Terms for Seoul Works apps`
   - **Public** 선택 (Private이면 GitHub Pages 무료 안 됨)
   - `Add a README file` ✅ 체크
4. `Create repository`

### 2. 파일 업로드

1. 새로 만든 repo 페이지에서 `Add file` → `Upload files`
2. 아래 4개 파일을 끌어다 놓기:
   - `index.html`
   - `privacy.html`
   - `terms.html`
   - `privacy-policy.md` (선택, 참고용)
   - `terms-of-service.md` (선택, 참고용)
3. 하단 `Commit changes` 버튼 클릭

### 3. GitHub Pages 활성화

1. repo 페이지 상단 `Settings` 클릭
2. 좌측 메뉴 `Pages` 클릭
3. `Source` 섹션:
   - Branch: `main`
   - Folder: `/ (root)`
   - `Save` 클릭
4. 1~2분 기다리면 페이지 상단에 URL 표시됨:
   ```
   Your site is live at https://[username].github.io/seoulworks-legal/
   ```

### 4. 동작 확인

브라우저로 URL 접속해서:
- ✅ index.html 정상 표시
- ✅ Privacy Policy 링크 클릭 → privacy.html 정상 표시
- ✅ Terms 링크 클릭 → terms.html 정상 표시
- ✅ 모바일 브라우저에서도 잘 보임

---

## 방법 B: Git CLI로 (개발자 익숙하면)

```bash
# 1. 로컬에서 폴더 만들고 파일 복사
mkdir seoulworks-legal && cd seoulworks-legal
# (이 폴더의 파일들을 여기에 복사)

# 2. Git 초기화
git init
git add .
git commit -m "Initial: Privacy Policy and Terms"

# 3. GitHub에서 빈 repo 만든 후 연결
git remote add origin https://github.com/[username]/seoulworks-legal.git
git branch -M main
git push -u origin main

# 4. GitHub Settings → Pages → main / root 선택
```

---

## 출시 전 해야 할 것

호스팅 후 **반드시** 아래 텍스트를 실제 값으로 교체:

### 1. 날짜 placeholder 교체 (HTML + MD 양쪽)

`[INSERT LAUNCH DATE]` → 실제 출시일 (예: `July 1, 2026`)

교체할 파일:
- `privacy.html` — 2곳 (Effective Date + Last Updated)
- `terms.html` — 2곳 (Effective Date + Last Updated)
- `privacy-policy.md` — 2곳 (참고용 md 파일도 함께 올릴 경우)
- `terms-of-service.md` — 2곳

찾기 쉽게 검색:
```bash
grep -rn "INSERT LAUNCH DATE" .
```

### 2. Privacy Policy URL 교체

`terms-of-service.md` 안의 `[INSERT PRIVACY POLICY URL — e.g., ...]`를 실제 호스팅 URL로 교체:

```text
https://[your-username].github.io/seoulworks-legal/privacy.html
```

(HTML 파일들은 이미 상대 경로 `privacy.html`로 링크되어 있어 자동 작동함)

### 3. 한 번에 검증

모든 placeholder 교체 후 확인:
```bash
grep -rn "INSERT" .
# 출력이 비어 있으면 OK
```

---

## 앱 / Play Console에서 사용할 URL

호스팅 완료 후 이 URL들을 메모:

| 용도 | URL |
|---|---|
| **Privacy Policy** (Play Console / AdMob 필수) | `https://[username].github.io/seoulworks-legal/privacy.html` |
| **Terms of Service** (앱 내 설정 화면) | `https://[username].github.io/seoulworks-legal/terms.html` |
| **인덱스 (선택)** | `https://[username].github.io/seoulworks-legal/` |

이 URL을 사용할 곳:

1. **Google Play Console** → 앱 콘텐츠 → Privacy Policy URL 입력
2. **AdMob 콘솔** → 앱 설정 → Privacy Policy URL 입력
3. **앱 내 설정 화면** → Privacy / Terms 링크 (DEV_FLAGS 끄고 별도 화면 만들 때)

---

## 나중에 수정하려면

GitHub repo 페이지에서:

1. 수정할 파일 클릭 (예: `privacy.html`)
2. 우측 상단 ✏️ 연필 아이콘 클릭
3. 수정 후 하단 `Commit changes`
4. 1분 내 자동 반영

---

## 사용자 정의 도메인 (선택, 나중에)

회사 도메인 (예: `seoulworks.com`)을 산 후:
1. GitHub Settings → Pages → Custom domain에 입력
2. 도메인 등록처에서 CNAME 레코드 설정
3. `https://seoulworks.com/privacy` 같은 깔끔한 URL 사용 가능

V1.0 출시 후 V1.1 즈음 작업 권장.

---

## 문제 해결

**Q. Page Not Found가 뜬다**
A. 5~10분 기다려라. 첫 배포는 시간 걸림. 그래도 안 되면 Settings → Pages 다시 확인.

**Q. 폰트가 깨진다**
A. 브라우저 캐시 문제. 강제 새로고침 (Ctrl+Shift+R / Cmd+Shift+R)

**Q. 한 번 더 손보고 싶다**
A. 위 "나중에 수정하려면" 섹션 참고. 자유롭게 수정 가능.

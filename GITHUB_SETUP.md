# GitHub 저장소 설정 가이드

## 1. GitHub에서 새 저장소 생성

1. [GitHub](https://github.com)에 로그인
2. 우측 상단의 "+" 버튼 클릭 → "New repository" 선택
3. 저장소 이름 입력 (예: `nahyun-blog`)
4. Public 또는 Private 선택
5. "Create repository" 클릭

## 2. 로컬 Git 초기화 및 GitHub 연결

```bash
# 현재 디렉토리에서 Git 초기화
git init

# 원격 저장소 추가 (YOUR_USERNAME과 REPO_NAME을 실제 값으로 변경)
git remote add origin https://github.com/YOUR_USERNAME/REPO_NAME.git

# 파일들을 스테이징
git add .

# 첫 번째 커밋
git commit -m "Initial commit: Next.js Notion Starter Kit setup"

# main 브랜치로 푸시
git branch -M main
git push -u origin main
```

## 3. Vercel 배포 설정

### 3.1 Vercel 계정 생성
1. [Vercel](https://vercel.com)에 가입
2. GitHub 계정으로 로그인

### 3.2 프로젝트 배포
1. Vercel 대시보드에서 "New Project" 클릭
2. GitHub 저장소 선택
3. 프로젝트 설정:
   - Framework Preset: Next.js
   - Root Directory: `./` (기본값)
   - Build Command: `npm run build`
   - Output Directory: `.next`
   - Install Command: `npm install`

### 3.3 환경 변수 설정 (선택사항)
Vercel 프로젝트 설정에서 다음 환경 변수들을 추가할 수 있습니다:

- `NEXT_PUBLIC_FATHOM_ID`: Fathom Analytics ID
- `NEXT_PUBLIC_POSTHOG_ID`: PostHog Analytics ID
- `REDIS_HOST`: Redis 호스트 (캐싱 사용시)
- `REDIS_PASSWORD`: Redis 비밀번호 (캐싱 사용시)

## 4. Notion 페이지 설정

### 4.1 Notion 페이지 공개 설정
1. Notion에서 블로그로 사용할 페이지 생성
2. 페이지 우측 상단의 "Share" 버튼 클릭
3. "Share to web" 활성화
4. "Copy link" 클릭하여 URL 복사

### 4.2 페이지 ID 추출
복사한 URL에서 페이지 ID를 추출:
```
https://www.notion.so/페이지제목-페이지ID
```

예: `https://www.notion.so/My-Blog-7875426197cf461698809def95960ebf`
페이지 ID: `7875426197cf461698809def95960ebf`

### 4.3 site.config.ts 업데이트
```typescript
rootNotionPageId: 'YOUR_PAGE_ID_HERE'
```

## 5. 커스터마이징

### 5.1 메타데이터 수정
`site.config.ts`에서 다음 항목들을 수정:
- `name`: 블로그 이름
- `domain`: 도메인 (Vercel 도메인 사용시 `your-project.vercel.app`)
- `author`: 작성자 이름
- `description`: 블로그 설명
- 소셜 미디어 계정들

### 5.2 스타일 커스터마이징
- `styles/global.css`: 전역 스타일
- `styles/notion.css`: Notion 콘텐츠 스타일
- `components/`: 컴포넌트 수정

## 6. 배포 확인

1. Vercel에서 자동 배포 완료 확인
2. 제공된 URL로 접속하여 블로그 확인
3. Notion 페이지 수정 후 자동 업데이트 확인

## 7. 도메인 연결 (선택사항)

### 7.1 커스텀 도메인 설정
1. Vercel 프로젝트 설정 → Domains
2. "Add Domain" 클릭
3. 도메인 입력 및 DNS 설정 안내 따르기

### 7.2 site.config.ts 도메인 업데이트
```typescript
domain: 'your-custom-domain.com'
```

## 문제 해결

### 빌드 오류
- Node.js 버전 확인 (>= 18 필요)
- 의존성 재설치: `npm install`
- 캐시 클리어: `npm run build -- --no-cache`

### Notion 연결 오류
- 페이지가 공개로 설정되어 있는지 확인
- 페이지 ID가 정확한지 확인
- Notion API 제한 확인

### 배포 오류
- Vercel 로그 확인
- 환경 변수 설정 확인
- 빌드 명령어 확인 
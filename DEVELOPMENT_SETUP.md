# Obsidian Custom Frames - 개발 환경 설정 및 진행 상황

> **다른 LLM을 위한 안내**: 이 문서는 Obsidian Custom Frames 플러그인 fork 후 개발 환경 설정 과정과 현재 상태를 정리한 문서입니다. 모든 기본 설정이 완료되어 기능 개발을 시작할 수 있는 상태입니다.

## 📋 현재까지 완료된 작업 (2024-07-30)

### 1. Fork 및 클론 완료
- ✅ GitHub에서 `Ellpeck/ObsidianCustomFrames`를 `Uwaang/ObsidianCustomFrames`로 fork
- ✅ 로컬에 클론: `/d/custom/obsidian-plugin-dev/ObsidianCustomFrames`
- ✅ Remote 설정 완료:
  - `origin`: https://github.com/Uwaang/ObsidianCustomFrames.git
  - `upstream`: https://github.com/Ellpeck/ObsidianCustomFrames.git

### 2. 개발 환경 설정 완료
- ✅ Node.js v22.17.0, npm v10.9.2 확인
- ✅ 의존성 설치: `npm install` 완료
- ✅ 빌드 테스트: `npm run build` 성공 (main.js 생성)

### 3. 개발용 플러그인 설치 완료
- ✅ 개발용 디렉토리 생성: `/d/custom/obsvault/.obsidian/plugins/obsidian-custom-frames-dev/`
- ✅ 빌드 파일 복사: `main.js`, `manifest.json`, `styles.css`
- ✅ **완료**: manifest.json ID/이름 수정 완료
  - ID: `"obsidian-custom-frames"` → `"obsidian-custom-frames-dev"`
  - 이름: `"Custom Frames"` → `"Custom Frames (Dev)"`

## ✅ 개발 환경 설정 완료!

모든 기본 설정이 완료되었습니다. 이제 기능 개발을 시작할 수 있습니다.

### 📁 프로젝트 위치 변경됨
- **이전**: `/d/custom/obsidian-plugin-dev/ObsidianCustomFrames`
- **현재**: `/d/custom/obsvault/ObsidianCustomFrames` (워크스페이스 내)
- **장점**: IDE에서 직접 파일 수정 가능

### 🔍 현재 상태 확인 방법
```bash
# 프로젝트 디렉토리로 이동
cd /d/custom/obsvault/ObsidianCustomFrames

# Git 상태 확인
git status
git remote -v

# Node.js 환경 확인
node --version  # v22.17.0
npm --version   # v10.9.2

# 빌드 테스트
npm run build

# 개발용 플러그인 파일 확인
ls -la /d/custom/obsvault/.obsidian/plugins/obsidian-custom-frames-dev/
```

## 🚀 다음 단계 (해야 할 일)

### 1. 즉시 해야 할 작업
1. **Obsidian에서 개발 플러그인 활성화**
   - Obsidian 재시작
   - Settings > Community plugins에서 "Custom Frames (Dev)" 활성화
2. **기본 동작 테스트**
3. **원하는 기능 정의 및 개발 시작**

### 2. 개발 워크플로우 설정
```bash
# 현재 위치: /d/custom/obsvault/ObsidianCustomFrames

# 개발 모드 실행 (파일 변경 감지)
npm run dev

# 또는 수동으로 빌드 후 복사:
npm run build
cp main.js manifest.json styles.css "/d/custom/obsvault/.obsidian/plugins/obsidian-custom-frames-dev/"
```

### 3. 기능 개발 준비
- 원하는 기능 정의
- 해당 기능에 맞는 파일 수정:
  - `src/main.ts`: 메인 플러그인 로직
  - `src/frame.ts`: iframe/webview 관리
  - `src/view.ts`: Obsidian 뷰 인터페이스
  - `src/settings.ts`: 설정 데이터
  - `src/settings-tab.ts`: 설정 UI

## 📁 프로젝트 구조

```
ObsidianCustomFrames/
├── src/
│   ├── main.ts          # 메인 플러그인 클래스
│   ├── frame.ts         # CustomFrame 클래스 (iframe/webview 관리)
│   ├── view.ts          # CustomFrameView 클래스 (Obsidian 뷰)
│   ├── settings.ts      # 설정 데이터 구조
│   └── settings-tab.ts  # 설정 UI
├── main.js              # 빌드된 메인 파일
├── manifest.json        # 플러그인 메타데이터
├── styles.css           # 스타일시트
└── package.json         # npm 설정
```

## 🛠️ 개발 명령어

```bash
# 개발 모드 (파일 변경 시 자동 재빌드)
npm run dev

# 프로덕션 빌드
npm run build

# 타입 체크만
npx tsc --noEmit
```

## 🔄 Git 워크플로우

```bash
# 새 기능 브랜치 생성
git checkout -b feature/기능이름

# 변경사항 커밋
git add .
git commit -m "Add: 기능 설명"

# fork에 푸시
git push origin feature/기능이름

# 원본 저장소 동기화 (필요시)
git fetch upstream
git merge upstream/master
```

## 🐛 디버깅 팁

1. **콘솔 로그**: `console.log()`를 사용하여 개발자 도구(F12)에서 확인
2. **플러그인 재로드**: 설정에서 플러그인 비활성화 후 재활성화
3. **Obsidian 재시작**: 큰 변경사항 후에는 Obsidian 완전 재시작

## 📝 현재 환경 정보

- **OS**: Windows (Git Bash)
- **Node.js**: v22.17.0
- **npm**: v10.9.2
- **GitHub CLI**: v2.74.2
- **개발 디렉토리**: `/d/custom/obsvault/ObsidianCustomFrames`
- **Vault 경로**: `/d/custom/obsvault`

## 🎯 다음 대화에서 할 일

1. 개발 플러그인 활성화 확인
2. 추가하고 싶은 기능 논의
3. 구체적인 구현 계획 수립
4. 코드 수정 및 테스트

## ⚠️ 알려진 문제 및 해결방법

### Git Bash 편집기 문제
- **증상**: 명령어에서 `[200~` 문자 출현
- **해결방법**: **똑같은 명령어를 다시 실행**하면 정상 작동
- **예시**: `sed` 명령어나 긴 명령어에서 자주 발생

### 개발용 플러그인이 보이지 않는 경우
1. Obsidian 완전 재시작
2. 개발자 도구(F12) 열어서 콘솔 오류 확인
3. manifest.json 파일 내용 확인:
   ```bash
   cat /d/custom/obsvault/.obsidian/plugins/obsidian-custom-frames-dev/manifest.json
   ```

### 빌드 오류 발생시
1. node_modules 재설치:
   ```bash
   rm -rf node_modules package-lock.json
   npm install
   ```
2. TypeScript 타입 체크:
   ```bash
   npx tsc --noEmit
   ```

## 🆘 다른 LLM을 위한 체크리스트

다른 LLM이 이 프로젝트를 이어받을 때 확인해야 할 사항:

- [ ] 현재 디렉토리가 `/d/custom/obsvault/ObsidianCustomFrames`인지 확인
- [ ] `git remote -v`로 origin과 upstream 설정 확인
- [ ] `npm run build` 명령어가 정상 작동하는지 확인
- [ ] 개발용 플러그인 디렉토리에 파일들이 있는지 확인
- [ ] Git Bash에서 `[200~` 오류 발생시 명령어 재실행
- [ ] 사용자의 구체적인 기능 요구사항 파악

---

**작성일**: 2024-07-30  
**작성자**: Uwaang (fork)  
**원본**: Ellpeck/ObsidianCustomFrames  
**상태**: 개발 환경 설정 완료, 기능 개발 준비 완료
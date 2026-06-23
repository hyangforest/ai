---
inclusion: auto
---

# 작업 규칙

## 확인 후 실행 원칙
- 파일 이동, 폴더 구조 변경, 대규모 리팩토링 시에는 반드시 계획을 먼저 보여주고 사용자 확인을 받은 후 실행할 것
- 단순 버그 수정이나 명시적으로 요청받은 작업은 바로 실행 가능

## 파일 인코딩 규칙 (절대 위반 금지)
- PowerShell의 Set-Content, Out-File, Add-Content 등은 **절대** 사용하지 말 것 (UTF-8 BOM 없이 저장되어 한글이 깨짐)
- PowerShell 스크립트 파일(.ps1)을 만들어서 파일 내용을 수정하는 것도 금지
- 파일 내용 치환이 필요할 때는 반드시 str_replace 도구 또는 fs_write 도구만 사용할 것
- 일괄 치환이 필요하면 여러 번 str_replace를 호출하거나, fs_write로 파일 전체를 다시 작성할 것
- cmd /c powershell로 파일 쓰기 절대 금지
- **모든 C# 파일(.cs)은 UTF-8 with BOM(EF BB BF) 인코딩으로 저장할 것** — 한글 주석/문자열 깨짐 방지


## Git 커밋 메시지 규칙
- 형식: `[스코프] 한국어 설명`
- 1행(제목)은 **스코프 포함 72자 이내** (50자는 설명 부분 기준)
- 본문(body)이 필요하면 한국어로 상세 설명 추가
- 스코프:
  - `[킴스온라인]` — `main/`
  - `[킴스온라인통합API]` — `api/`
  - `[Auth]` — `auth/`  ← 추가
  - `[킴스온라인-프로모션]` — `event/`
  - `[운영작업]` — `jobs/` (conference-update 제외)
  - `[학술센터-해외컨퍼런스]` — `jobs/conference-update/`
  - `[멤버API]` — `member/`
  - `[킴스모바일]` — `mobile/`
  - `[KOL-공통라이브러리]` — `shared/`
  - `[VOD센터]` — `vod/`
- 여러 폴더 변경 시 스코프 병기 (최대 2개, 3개 이상이면 대표 스코프 1개 선택)
- 루트 파일(*.sln, .gitignore) 및 설정(.kiro/, .github/) 수정 시 스코프 생략
- 예시:
  - [VOD센터] 푸터 대표자명 / 정적 리소스 도메인 변경
  - [킴스온라인] 메인 Product Highlights No Data 이미지 경로 오류 수정
  - [운영작업] 작업이력 / SQL / 배치 스크립트 추가
  - [KOL-공통라이브러리] Log 포함된 파일 git 추가

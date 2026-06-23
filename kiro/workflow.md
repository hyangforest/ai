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
- 스코프:
  - `[API]` — `api/` 폴더 내 파일 수정·추가 시
  - `[FRONT]` — `web/` 폴더 내 파일 수정·추가 시
  - 양쪽 모두 변경 시 `[API][FRONT]` 병기
- 1행(제목)은 50자 이내 한국어로 간결하게 작성
- 마침표 없이 끝내기
- 본문(body)이 필요하면 한국어로 상세 설명 추가
- 예시:
  - [API] Ulistin 서울 QnA 등록 API 추가
  - [FRONT] 교통비 영수증 업로드 시 파일 크기 검증 오류 수정
  - [API] AdminCommonController 서비스 레이어 분리
  - [FRONT] 관리자 QnA 목록 페이지 추가
  - [API][FRONT] 관리자 계정 생성 기능 구현

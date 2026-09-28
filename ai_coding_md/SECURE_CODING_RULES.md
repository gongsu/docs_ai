# Secure Coding Rules

KISA 개발보안 가이드 구현단계 49개 보안약점 통합본.
전체 규칙을 매번 검토하지 말 것. **현재 생성·수정하는 코드와 관련된 규칙만 적용.**

핵심 판단 흐름:
**External Input → Validation → Security-Sensitive Operation**
외부 입력이 SQL·명령 실행·HTML 출력·파일·URL 요청·인증·권한·중요데이터에 도달 시 안전한 구현 우선.

## 1. 입력 검증
- 외부 입력(파라미터·Header·Cookie·파일·DB/API 응답) 신뢰 금지
- 허용 목록 우선, 타입·길이·범위·형식 검증
- 서버 측 재검증 필수 (클라이언트 검증은 보안 아님)
- 미검증 입력을 보안 결정에 사용 금지

## 2. Injection 방지 (SQL·Command·Code)
- SQL·LDAP·XPath: Prepared Statement/Parameter Binding, 문자열 연결 금지
- 테이블명·컬럼명·정렬 등 바인딩 불가 값: 허용 목록
- OS 명령: 안전한 API 우선, 명령·인자 분리
- eval/exec 최소화, 역직렬화로 임의 코드 실행 금지

## 3. XSS·출력 인코딩
- 출력 Context(HTML·Attribute·JS·URL)별 인코딩
- Framework Auto Escaping 우선, 사용자 입력 직접 렌더링 금지
- 필요 시 검증된 Sanitizer

## 4. 파일·경로
- Path Traversal(`../`) 차단: 경로 정규화 후 Base Directory 내부 확인
- 업로드: 확장자·MIME·크기 검증, 파일명 서버 생성
- 실행 가능 위치에 업로드 저장 금지

## 5. SSRF·Redirect
- 서버 측 URL 요청: 허용 Host·Protocol·Port 검증
- 내부 IP·Metadata Endpoint 접근 차단
- Redirect: 허용 목록 또는 내부 상대 경로

## 6. 인증·세션
- 인증은 서버 검증, 클라이언트 전달 상태 신뢰 금지
- 세션 ID·토큰: 암호학적 난수
- 인증정보 URL Parameter 노출 금지
- Cookie: Secure·HttpOnly·SameSite
- 로그인·로그아웃·만료·재발급 명확히 처리

## 7. 권한 (인가·IDOR)
- 중요 기능·데이터 접근 전 서버 측 권한 확인
- 요청값(ID)만으로 접근 허용 금지, 객체 소유권 확인
- 관리자 기능 별도 검증, 실패 시 기본 거부

## 8. 비밀정보·암호화
- Password·API Key·Token·암호키 하드코딩 금지 → 환경변수·Secret 관리
- 비밀번호: 검증된 Password Hash (bcrypt/argon2 등)
- 자체 암호 구현·취약 알고리즘 금지
- 보안 목적 난수: CSPRNG
- 암호키는 소스와 분리, TLS·인증서 검증 비활성화 금지
- 비밀정보를 로그·오류·응답에 출력 금지

## 9. 상태 변경 요청
- 생성·수정·삭제: 인증·권한 검증
- Web: CSRF 고려
- 재사용·중복 실행 방지, 동시 처리 시 Race Condition/TOCTOU 고려

## 10. 오류·로그
- Stack Trace·SQL·내부 경로·Framework 정보 응답 노출 금지, 일반화된 메시지
- 예외 무시 금지, Fail Secure
- Password·Token·Session ID·암호키 로그 기록 금지
- 미검증 입력을 로그에 직접 삽입 금지
- 인증·권한 실패는 기록

## 11. 안전한 코드·자원
- Null·미초기화·형변환·경계값(배열·정수) 검증
- 파일·Connection·Stream: 예외 시에도 해제
- 위험·Deprecated API 회피, 검증된 보안 API 우선

## 12. 금지 기본값
다음을 기본값으로 생성 금지:
TLS 검증 비활성화 · CORS 전체 허용 · 인증/권한 생략 · CSRF 비활성화 · Debug 모드 운영 · 예외 전체 허용/검증 우회 · 보안 경고 억제용 임시 코드

# Security Check (작업 완료 시)

전체 규칙·전체 프로젝트 재검토 금지.
변경 코드에 아래 요소 포함 시 관련 위험만 확인, 문제 발견 시 설명보다 코드 수정 우선:

`Input · Query · Command · HTML · File · URL · Auth · Session · Secret · Crypto · State Change · Error · Log · Resource`

판단 불확실 시 편의성보다 안전한 구현 선택.

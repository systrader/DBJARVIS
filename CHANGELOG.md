# Changelog

## v1.3.13 (2026-05-09) — 자동 업데이트 테스트 릴리스

### 버전/배포
- v1.3.12 설치본의 자동 업데이트 확인을 테스트하기 위한 기준 버전 상향
- `AutoMain.exe` 파일/제품 버전을 1.3.13.0으로 갱신
- 배포 ZIP/SHA256 및 설치판 재생성

## v1.3.12 (2026-05-09) — 업데이트 시작 시 전체 프로세스 종료

### 업데이트
- 업데이트 확인 후 사용자가 확인을 누르면 다운로드 전에 `AutoMain.exe`, `run_all.exe`, `dbjarvis.exe`, `web_server.exe`를 모두 종료하도록 수정
- 다운로드 실패, 장중 연기, 적용 실패 시 업데이트 시작 전에 실행 중이던 `run_all.exe`와 `AutoMain.exe`를 복구하도록 보강
- 업데이트 적용 단계와 외부 교체 스크립트까지 기존 AutoMain 실행 상태를 유지해 완료 후 새 AutoMain 재실행이 이어지도록 정리

## v1.3.11 (2026-05-09) — 설치판 무응답/덮어설치 보강

### 설치판
- 설치 프로그램 시작/오류 로그를 `%LOCALAPPDATA%\AutoChart\DBJARVIS\logs\setup.log`에 기록하도록 추가
- 관리자 권한 요청 실패 또는 취소 시 조용히 종료하지 않고 오류 팝업을 표시하도록 수정
- 덮어설치 전 실행 중인 `AutoMain.exe`, `run_all.exe`, `dbjarvis.exe`, `web_server.exe`, `updater.exe`를 종료해 파일 교체 실패를 줄이도록 수정
- 로컬 산출물에도 `DBJARVIS_Setup_v버전.exe` 파일을 생성하도록 빌드 스크립트 수정

## v1.3.10 (2026-05-09) — 다운로드 진행 전 AutoMain 종료

### 업데이트
- 업데이트 확인 후 다운로드 진행창을 띄우기 전에 `AutoMain.exe`를 먼저 종료하도록 수정
- 다운로드 실패, 장중 연기, 적용 실패 시 업데이트 전에 실행 중이던 `AutoMain.exe`를 다시 실행하도록 보강
- 다운로드 전 종료한 AutoMain 상태를 실제 교체/외부 적용 스크립트까지 전달해 업데이트 완료 후 새 AutoMain이 재실행되도록 수정

## v1.3.9 (2026-05-09) — updater 자기 교체/무응답 수정

### 업데이트
- Windows에서 실행 중인 `updater.exe`가 자기 폴더 교체를 막아 업데이트가 조용히 실패하던 문제 수정
- 업데이트 파일을 `bin` 밖에 staging하고, updater 종료 후 외부 적용 스크립트가 `bin`을 교체하도록 변경
- 사용자 데이터/설정 보존 시 이동 대신 복사 방식을 사용해 실패 시 원본이 사라지지 않도록 수정
- 업데이트 적용 실패 시 무응답으로 끝나지 않고 오류 팝업을 표시하도록 수정

## v1.3.8 (2026-05-09) — AutoMain 업데이트/한글 팝업 수정

### AutoMain / 업데이트
- 업데이트 적용 직전 실행 중인 `AutoMain.exe`를 종료해 새 배포판의 AutoMain으로 교체되도록 수정
- 업데이트 전 AutoMain이 실행 중이었다면 업데이트 성공 후 새 `AutoMain.exe`를 자동 재실행
- 한글 팝업이 `????`로 깨지는 문제를 피하기 위해 Windows Unicode `MessageBoxW` 기반 팝업으로 변경

## v1.3.7 (2026-05-09) — 업데이트 테스트 릴리스

### 버전/배포
- 자동 업데이트 테스트를 위해 기준 버전을 1.3.7로 상향
- `AutoMain.dproj` 파일/제품 버전을 1.3.7.0으로 갱신
- GitHub Release 테스트용 ZIP/SHA256 재생성

## v1.3.6 (2026-05-09) — 버전 동기화

### 버전/배포
- `source/VERSION`, `bin/VERSION`, `install/DBJARVIS/VERSION` 기준 버전을 1.3.6으로 동기화
- `AutoMain.dproj` 파일/제품 버전을 1.3.6.0으로 갱신
- 배포 ZIP/SHA256 재생성 기준 버전을 1.3.6으로 갱신

## v1.3.5 (2026-05-09) — AutoMain 시작 업데이트 확인

### AutoMain / 업데이트
- **시작 즉시 업데이트 확인** — `AutoMain.exe` 실행 시 백그라운드에서 `updater.exe --startup-check`를 1회 실행해 최신 GitHub Release를 바로 확인
- **확인/취소 업데이트 팝업** — 새 버전이 있으면 현재/최신 버전, 다운로드 크기, 기능 추가 요약을 보여주고 확인 시 자동 업데이트 진행
- **취소 동작 정리** — AutoMain 실행 1회당 업데이트 체크를 한 번만 실행해 취소 후 같은 실행 세션에서는 재팝업하지 않음
- **AutoMain 캡션 버전 표시** — 창 제목과 상단 제목에 `DB쟈비스 v버전` 표시
- **updater 자체 업데이트 보강** — 새 패키지의 `updater.exe`를 `updater_new.exe`로 보관하고 현재 updater를 새 폴더에 남겨 다음 실행 때 안전하게 자기 교체
- **구버전 updater 복구 경로** — 구버전 updater가 적용한 뒤 `updater_new.exe`만 남은 경우 AutoMain이 `updater.exe`로 자동 복구

### 빌드 자산 정합성
- `source/VERSION` — 1.3.1 → 1.3.5
- `AutoMain.dproj` — 파일/제품 버전 1.3.5.0 반영
- `build_all.bat` — 버전 인자가 없으면 `source/VERSION`을 기본값으로 사용

## v1.3.1 (2026-05-05) — 인스톨러 버전 주입 + AI 4 버튼

### 인스톨러
- **MSI ProductVersion 빌드시 주입** — `modify_ism.py` 가 `--version` 또는 `install/DBJARVIS/VERSION` 으로 ISM 의 ProductVersion 갱신 (이전: 1.0.0 고정)
- **UpgradeCode 신규 추가** — Major Upgrade 체인 활성화. 이전 버전 자동 제거 후 신규 설치
- **ProductCode 매 빌드 신규 GUID** — RemoveExistingProducts 트리거
- **REINSTALLMODE=amus** — 같은 버전 재설치 시 강제 덮어쓰기
- **gen_sed.py / make_installer.py** — 동일하게 VERSION 파일에서 자동 읽기
- **build_all.bat** — `python modify_ism.py --version %VERSION%` 호출

### AutoMain / 인스톨러 화면
- **AI 엔진 4 버튼** — `클로드 설치` / `클로드 인증` / `제미나이 설치` / `제미나이 인증` 분리 (이전: 단일 "설치 / 로그인" 버튼)
- **claude.cmd 다중 경로 폴백** — `%APPDATA%\npm` / `%ProgramFiles%\nodejs` / `%LOCALAPPDATA%\Programs\nodejs` / `npm config get prefix` 순서 검사. 비표준 npm prefix 환경에서 `claude.CMD ... 내부 또는 외부 명령` 오류 해소
- **PATH 보강** — 설치 후 같은 프로세스에서 `%APPDATA%\npm` 즉시 인식
- **Gemini CLI 자동 설치** — `_install_prerequisites` 가 Claude 와 함께 `@google/gemini-cli` 도 설치

### 빌드 자산 정합성
- `install/DBJARVIS_v1.3.0.zip.sha256` — certutil 한글 헤더 mojibake → 64자 hex 정상화
- `source/VERSION` — 1.0.0 → 1.3.1 (빌드 산출물과 동기화)

## v1.3.0 (2026-05-03) — (변경 이력 보충 필요 — 보유 ZIP 만 존재)

## v1.2.6 (2026-05-05) — (변경 이력 보충 필요)

## v1.2.5 (2026-05-04) — (변경 이력 보충 필요)

## v1.2.4 (2026-05-04) — (변경 이력 보충 필요)

## v1.2.3 (2026-05-04) — (변경 이력 보충 필요)

## v1.2.1 (2026-05-02) — (변경 이력 보충 필요)

## v1.2.0 (2026-05-02) — (변경 이력 보충 필요)

## v1.1.4 (2026-05-01) — (변경 이력 보충 필요)

## v1.1.3 (2026-05-01) — (변경 이력 보충 필요)

## v1.1.2 (2026-05-01) — (변경 이력 보충 필요)

## v1.1.1 (2026-05-01) — (변경 이력 보충 필요)

## v1.1.0 (2026-05-01) — 슬롯 시스템

### 핵심 변경
- **L1~L4 4채널 모델 → 슬롯 1개 모델 전환** (deprecated, 1.2.0 삭제 예정)
- **5축 모델**: 모드(5) × 프로필(5) × 매매방향(4) × 스캐닝(4) = 400 조합
- **PositionManager 분리** — 슬롯 종료 시 종목을 PositionManager 로 이관, 매수 당시 룰을 *origin_rules* 로 박제
- **사전 묶음** (한 단어 매핑): 평소 / 회전 / 버티기 / 보수 / 위험회피 / 관망 / AI추천
- **AI 추천 엔진** (결정론적 규칙 트리, LLM 미사용) — 잔고 + 시장 6국면 분석 → 슬롯 카드 3장
- **자연어 라우터 확장** — "오늘 어떻게 할까", "500만 5개", "평소대로 가자", "오늘은 사기만"
- **시퀀스 매매** — "정리하고 다시 잡자" (청산 → 결제 대기 → 매수), 종목 교체, 부분 청산 → 재진입
- **24시간 NXT 운영** — 7개 세션 + 휴장일 캘린더
- **SafetyNet** (항상 작동) — 종목 -10% / 일일 -5% / KOSPI 서킷 자동 청산

### 신규 패키지
- `trader/slot/` — TradingSlot + SlotManager + BasketOrderer + FundDistributor
- `trader/position/` — Position + PositionManager + ExitEngine (4-lane) + PositionMonitor
- `trader/direction/` — DirectionController + SafetyNet + TimeLimitedDirection
- `trader/recommender/` — AccountAnalyzer + MarketRegimeAnalyzer + DecisionTree + UserBiasLearning
- `trader/modes/` + `trader/profiles/` — YAML 외부화된 5 모드 / 5 프로필 / 7 묶음
- `trader/calendar/` — Session enum + SessionPolicy + carry-over + holidays_2026

### 신규 플러그인
- `plugins/slot/` — /슬롯 명령
- `plugins/position/` — /포지션 명령 + 1분 ExitEngine 모니터
- `plugins/direction/` — /방향 명령 + 1분 SafetyNet
- `plugins/ai_recommender/` — /추천 명령
- `plugins/sequence/` — /시퀀스 명령 + 4 패턴

### 신규 NLU 파서 (intent_router/)
- _amount_parser, _time_parser, _bundle_alias
- slot_intent / direction_intent / bundle_intent / recommender_intent / close_intent

### 마이그레이션 스크립트
- `scripts/migrate_l1_l4.py` (dry-run / execute, atomic write + 백업)
- `scripts/rollback_migration.py <timestamp>`
- `scripts/verify_migration.py`

### .env 신규 키
- `SLOT_DEFAULT_MODE=스윙`, `SLOT_DEFAULT_PROFILE=기본`, `SLOT_AUTO_RESTORE=true`
- `SLOT_FORCE_CLOSE_TIME=15:20`
- `SAFETY_DAILY_LOSS_PCT=-5.0`, `SAFETY_EMERGENCY_PCT=-10.0`, `SAFETY_CIRCUIT_PCT=-3.0`

### 알려진 제한
- AutoMain (Delphi 외부 프로그램) UI 패널은 별도 갱신 필요 — 1.1.0 동안 L1~L5 패널 그대로 노출됨
- `webapp/settings.html` 슬롯 패널은 1.1.x 후속 패치에서 추가 예정
- `L1_BUY_START/END`, `L1_BULK_LIQUIDATION_*`, `SCAN_PRIORITY` 키는 1.1.0 부터 무시 (1.2.0 삭제)

### 가이드
- 마이그레이션 가이드: `error/DBJARVIS_SLOT_MIGRATION_GUIDE.md`

## v1.0.0 (2026-04-02)

### 초기 배포
- 4단계 자동매매 전략 엔진 (단타/스윙/포지션/장투)
- NXT 거래소 연동 + 시간대별 자동 라우팅
- 테마/종목 마스터 자동 갱신 (시간 제한 제거)
- 텔레그램 봇 + 웹 대시보드 (포트 8080)
- 리스크 관리 (손절/익절/트레일링/자금격리)
- 뉴스 감시 + 시그널 엔진
- 백테스트 엔진
- GitHub Release 기반 자동 업데이트

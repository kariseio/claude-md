# CHANGELOG

형식: 날짜 / 바뀐 규칙 / 근거가 된 사건. 사건 없는 변경은 넣지 않는다.

## 2026-09-22

### 추가

- 초안 작성. 기반은 Andrej Karpathy 의 LLM 코딩 가이드라인 4원칙(생각 먼저, 단순함 우선, 외과적 변경, 목표 기반 실행)과 `/insights` 리포트가 추천한 CLAUDE.md 항목 5개(Scope Discipline, Before Answering Ambiguous Requests, Evidence Rules, Verification Before Reporting Done, Git & Release), 그리고 재진술 게이트.
- 기존 전역 CLAUDE.md(8줄, 실행 시점 규칙)는 0번 섹션에 영어로 옮겨 보존.
- 상단에 "Reply in the user's language (Korean)" 한 줄 추가. 규칙 파일이 전부 영어가 되면 답변도 영어로 끌릴 수 있어서.

### 근거

- `/insights` 리포트 (2026-08-12 ~ 2026-09-21, 42 세션): misunderstood_request 19, wrong_approach 20, buggy_code 15, excessive_changes 7, incorrect_information 3, recurring_issue 3.
- 재진술 게이트 (1번): 탭 하나 추가 요청에 새 워크북을 만듦. "doc_title_summary 추가", "다 만들어줘"를 임베딩 백필로 오독 (실제는 stage 인덱스 생성). public+private 요청에 private 만 처리. 설계 확인 단계가 있던 세션(RabbitMQ 마이그레이션)은 정상, 없던 세션(엑셀 탭, stage 인덱스, MCP 서버)은 전부 오독.
- 스코프 규율 (4번): MCP 서버 작업에서 "기존 파일 수정 금지" 제약에도 8개 파일 수정, 전체 되돌리기. 요청 안 한 테스트 파일이 커밋에 섞여 amend.
- 근거 규칙 (6번): hotplace_v2.py 에 하드코딩된 Kakao API 키를 없다고 단정하고 라이브 테스트 생략. 실험 리포트 057 의 determinism 컬럼 조작. max_tokens 절단과 클라이언트 타임아웃을 혼동, 실제 원인(6회 재시도 루프)까지 두 번 반박 필요.
- 완료 전 검증 (7번): 다른 파일에서 복사한 xlsx 청킹 주석의 조건 반전이 세션 3개에 걸쳐 반복. RabbitMQ 멱등성 설계에서 DLQ 실패 시 문서가 'I' 상태에 영구 고착.
- Git (8번): main 강제 푸시가 자동화에 막혀 사용자에게 넘어감. stage→real 머지에서 cherry-pick 중복으로 충돌.

### 의도적 선택

- Karpathy 의 "trivial tasks: use judgment" 탈출구는 제외. 오독은 Claude 가 의심을 느끼지 않을 때 생기므로 게이트는 요청의 형태로 판단한다.
- 트리거 단어를 열거하지 않고 원칙 + 예시 형식으로 씀 (insights 리포트의 "Before Answering Ambiguous Requests" 스타일).
- 본문은 영어. 사용자 입력과 대조하는 문구("다 만들어줘", "아니야 있어", "진행해줘" 등)만 한국어 예시로 남김.

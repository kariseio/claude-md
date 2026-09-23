# claude-md

Claude Code 가 편집을 시작하기 전에 자기가 이해한 내용을 먼저 재진술하게 만드는 `CLAUDE.md` 파일 하나.

[Andrej Karpathy 의 4원칙](https://x.com/karpathy/status/2015883857489522876)(생각 먼저, 단순함 우선, 외과적 변경, 목표 기반 실행)을 기반으로, 실행 시점, 재진술 게이트, 근거, 검증, Git 규칙을 얹었다.

## What's inside

| 섹션 | 목적 |
|---|---|
| 0. When to Act | 명시적 실행 신호가 있을 때만 편집을 시작하게 한다. 토론이나 질문에는 분석만 답한다 |
| 1. Restatement Gate | 편집 전에 요청 해석, 적용 범위, 변경 파일, 완료 기준, 확인 필요를 재진술하고 확인을 기다리게 한다. 요청이 여러 갈래면 선택지를 먼저 낸다 |
| 2. Think Before Coding | 가정을 드러내고, 해석이 여럿이면 고르지 않고 제시하게 한다 (Karpathy) |
| 3. Simplicity First | 요청받은 것만 최소한의 코드로 만들게 한다 (Karpathy) |
| 4. Surgical Changes and Scope | 요청 범위 밖의 파일과 코드를 건드리지 않게 한다 (Karpathy) |
| 5. Goal-Driven Execution | 작업을 검증 가능한 완료 기준으로 바꾸게 한다 (Karpathy) |
| 6. Evidence Rules | 없다고 말하기 전에 찾고, 측정과 추정을 구분하고, 원인 후보를 먼저 열거하게 한다 |
| 7. Verification Before Done | 컴파일, 테스트, 로그 출력을 붙인 뒤에만 완료라고 말하게 한다 |
| 8. Git and Release | force-push 와 요청 안 한 파일의 커밋을 막는다 |
| 9. Environment Notes | Windows, PowerShell, 인코딩 |

게이트(1번)가 Karpathy 원본에 없는 부분이다. 요청이 여러 갈래로 읽히면 먼저 선택지를 내고 멈춘다.

```
이 요청은 N가지로 읽힙니다. 하나 골라주세요.

A. <무엇이 바뀌는지 한 줄. 크기>  ← 추천: <이유 한 줄>
B. <무엇이 바뀌는지 한 줄. 크기>

변경 제외: <어느 갈래든 건드리지 않는 것>
```

갈래가 정해지면, 또는 처음부터 명확하면, 편집 전에 고정된 형식으로 재진술하고 멈춘다. 채울 수 없는 줄은 생략한다.

```
요청 해석: <요청을 한 문장으로>
적용 범위: <환경/인덱스/파일 전부 열거>
변경 파일: <파일별 한 줄 이유>
변경 제외: <명시적 제외>
완료 기준: <완료를 무엇으로 증명할지>
확인 필요: <두 가지 이상으로 읽히는 부분과 각 해석. 없으면 이 줄 생략>
```

잘못 읽은 요청을 결과물이 다 나온 뒤가 아니라 이 단계에서 바로잡기 위한 것이다.

## Install

전역 규칙으로. 모든 세션에 로드된다.

```bash
curl -o ~/.claude/CLAUDE.md https://raw.githubusercontent.com/kariseio/claude-md/main/CLAUDE.md
```

또는 프로젝트별로. 기존 `CLAUDE.md` 뒤에 붙인다.

```bash
curl https://raw.githubusercontent.com/kariseio/claude-md/main/CLAUDE.md >> CLAUDE.md
```

## Make it yours

- **언어.** 규칙 본문은 영어다. 0번과 1번 섹션에 인용된 예시는 한국어인데, Claude 가 요청과 대조하는 문구 그대로이기 때문이다. 본인이 실제로 쓰는 축약 표현으로 바꾸면 된다. 맨 위의 "Reply in the user's language (Korean)" 줄은 필요에 맞게 바꾸거나 지운다.
- **0번 섹션**은 Claude 가 편집해도 되는 시점을 정한다. 실행 신호 없이도 바로 움직이게 하고 싶으면 지운다. 1번은 남긴다.
- **7번 섹션**은 Maven 과 Python 테스트를 예로 든다. 본인의 빌드와 테스트 명령으로 바꾼다.
- **9번 섹션**은 Windows 전용이다. macOS 나 Linux 면 지운다.

## Tradeoffs

게이트는 다중 파일 작업마다 왕복 한 번을 더한다. 한 가지로만 읽히는 단일 파일 작업에서는 멈추지 않고, 답변 첫 줄에 해석 한 문장만 붙인다. 작업 대부분이 작고 모호하지 않은 편집이라면 그 비용이 아까울 수 있다.

## Credits

- [4원칙](https://x.com/karpathy/status/2015883857489522876)의 Andrej Karpathy. `CLAUDE.md` 로 묶은 것은 [andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills).

# claude_md

전역 `~/.claude/CLAUDE.md` 의 원본을 관리하는 저장소.

## 구조

```
CLAUDE.md      원본. 상단 Version 줄이 배포된 버전을 식별한다
README.md      이 파일. 목적, 배포 방법, 관리 규율
CHANGELOG.md   날짜 / 바뀐 규칙 / 근거가 된 사건
```

## 배포

저장소가 원본이고 `~/.claude/CLAUDE.md` 는 배포본이다. 심볼릭 링크는 쓰지 않는다 (Windows 파일 심링크는 권한이 필요하고, C: 와 D: 는 다른 볼륨이라 하드링크 불가).

Git Bash:

```bash
cp ~/.claude/CLAUDE.md ~/.claude/CLAUDE.md.bak-$(date +%F) && cp CLAUDE.md ~/.claude/CLAUDE.md
```

PowerShell:

```powershell
Copy-Item "$HOME\.claude\CLAUDE.md" "$HOME\.claude\CLAUDE.md.bak-$(Get-Date -Format yyyy-MM-dd)"; Copy-Item CLAUDE.md "$HOME\.claude\CLAUDE.md"
```

배포본이 원본과 같은지 확인:

```bash
diff CLAUDE.md ~/.claude/CLAUDE.md && echo "in sync"
```

새 세션부터 반영된다. 열려 있는 세션에는 적용되지 않는다.

## 관리 규율

- **사건 없는 규칙은 넣지 않는다.** 규칙을 추가하거나 바꿀 때는 CHANGELOG 와 커밋 메시지에 근거가 된 사건(세션에서 실제로 일어난 오독, 범위 초과, 근거 없는 단정 등)을 인용한다. "좋아 보여서" 넣는 규칙은 금지. CLAUDE.md 의 Evidence Rules 를 파일 자신에게 적용하는 것이다.
- **150줄 상한.** 매 세션 로드되는 파일이라 계속 더하면 주의가 희석된다. 상한을 넘기면 뺄 규칙을 먼저 정한다. 한 번도 마찰을 잡지 못한 규칙이 삭제 후보다.
- **main 직접 커밋.** 1인 설정 저장소라 브랜치와 PR 은 쓰지 않는다. 되돌리기는 `git revert`.
- **효과는 /insights 로 잰다.** 월 1회쯤 Claude Code 에서 `/insights` 를 다시 돌려 마찰 건수를 아래 기준선과 비교한다. 이게 규칙이 효과가 있는지 확인하는 유일한 실측치다.

### 기준선 (2026-08-12 ~ 2026-09-21, 42 세션 분석)

| 마찰 유형 | 건수 |
|---|---|
| misunderstood_request | 19 |
| wrong_approach | 20 |
| buggy_code | 15 |
| excessive_changes | 7 |
| incorrect_information | 3 |
| recurring_issue | 3 |

## 주의

이 폴더에서 Claude Code 세션을 열면 전역 규칙과 프로젝트 규칙으로 같은 파일이 두 번 로드된다. 규칙을 고칠 때만 여는 폴더라 감수한다.

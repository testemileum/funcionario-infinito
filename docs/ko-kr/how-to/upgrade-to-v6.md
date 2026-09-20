---
title: 'v6로 업그레이드하는 방법'
description: Funcionário Infinito v4에서 v6로 마이그레이션합니다
sidebar:
  order: 2
---

Funcionário Infinito 설치 프로그램을 사용해 v4에서 v6로 업그레이드하세요. 레거시 설치 자동 감지와 마이그레이션 지원이 포함되어 있습니다.

## 사용 시점

- Funcionário Infinito v4가 설치되어 있습니다(`.funcionario-method` 폴더)
- 새 v6 아키텍처로 마이그레이션하고 싶습니다
- 보존해야 할 기존 계획 산출물이 있습니다

:::note[필수 조건]

- Node.js 20.12+
- 기존 Funcionário Infinito v4 설치
:::

## 단계

### 1. 설치 프로그램 실행

[설치 프로그램 안내](../start/install-funcionario.md)를 따르세요.

### 2. 레거시 설치 처리

v4가 감지되면 다음 중 선택할 수 있습니다.

- 설치 프로그램이 `.funcionario-method`를 백업하고 제거하게 합니다
- 종료한 뒤 수동으로 정리합니다

Funcionário Infinito 폴더 이름을 다르게 지정했다면 직접 폴더를 제거해야 합니다.

### 3. IDE 스킬 정리

레거시 v4 IDE 명령/스킬을 수동으로 제거하세요. 예를 들어 Claude Code를 사용한다면 funcionario로 시작하는 중첩 폴더를 찾아 제거합니다.

- `.claude/commands/`

새 v6 스킬은 다음 위치에 설치됩니다.

- `.claude/skills/`

### 4. 계획 산출물 마이그레이션

**계획 문서(제품 개요/PRD/UX/아키텍처)가 있다면:**

설명적인 이름으로 `_funcionario-output/planning-artifacts/`에 옮기세요.

- PRD 문서는 파일명에 `PRD`를 포함합니다
- 파일 유형에 맞게 `brief`, `architecture`, `ux-design`을 포함합니다
- 샤딩된 문서는 이름 있는 하위 폴더에 둘 수 있습니다

**계획 도중이라면:** v6 워크플로로 다시 시작하는 것을 고려하세요. 기존 문서를 입력으로 사용할 수 있습니다. 웹 검색과 IDE 계획 모드를 활용해 단계별로 요구사항을 구체화하는 새 워크플로가 더 나은 결과를 냅니다.

### 5. 진행 중인 개발 마이그레이션

이미 생성 또는 구현된 스토리가 있다면:

1. v6 설치를 완료합니다
2. `epics.md` 또는 `epics/epic*.md`를 `_funcionario-output/planning-artifacts/`에 둡니다
3. 개발자의 `funcionario-sprint-planning` 워크플로를 실행합니다
4. 이미 완료된 에픽/스토리를 에이전트에게 알려줍니다

## 얻는 결과

**v6 통합 구조:**

```text
your-project/
├── _funcionario/               # 단일 설치 폴더
│   ├── _config/         # 커스터마이징
│   │   └── agents/      # 에이전트 커스터마이징 파일
│   ├── core/            # 범용 core 프레임워크
│   ├── bmm/             # Funcionário Infinito 모듈
│   ├── bmb/             # Funcionário Infinito 빌더
│   └── cis/             # 창의적 지능 제품군
└── _funcionario-output/        # 출력 폴더(v4의 문서 폴더)
```

## 모듈 마이그레이션

| v4 모듈 | v6 상태 |
| --- | --- |
| `.funcionario-2d-phaser-game-dev` | BMGD 모듈에 통합 |
| `.funcionario-2d-unity-game-dev` | BMGD 모듈에 통합 |
| `.funcionario-godot-game-dev` | BMGD 모듈에 통합 |
| `.funcionario-infrastructure-devops` | 지원 중단 - 새 DevOps 에이전트 예정 |
| `.funcionario-creative-writing` | 아직 적용되지 않음 - 새 v6 모듈 예정 |

## 주요 변경 사항

| 개념 | v4 | v6 |
| --- | --- | --- |
| **코어** | `_funcionario-core`는 실제로 Funcionário Infinito였습니다 | `_funcionario/core/`는 범용 프레임워크입니다 |
| **메서드** | `_funcionario-method` | `_funcionario/bmm/` |
| **설정** | 파일을 직접 수정 | 모듈별 `config.yaml` |
| **문서** | 샤딩 또는 비샤딩 필수 설정 | 완전히 유연하며 자동 스캔 |

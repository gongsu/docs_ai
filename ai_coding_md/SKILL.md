---
name: securecoding-ai-md
description: AI 코딩 도구는 작업 시작 시 COMMON_INSTRUCTIONS.md를 기본 지침으로 적용하고, 코드 생성·수정 내용과 관련된 경우에만 SECURE_CODING_RULES.md의 해당 보안 규칙을 선택적으로 확인합니다. 작업 완료 후에도 전체 규칙을 반복 검토하지 않고 변경 코드와 직접 영향 범위만 확인하여 토큰 사용량을 최소화합니다.
---

# securecoding-ai-md
아래 2개 MD 파일을 AI 코딩 도구의 프로젝트 공통 지침으로 등록하여 활용할 수 있습니다.
공통 보안 원칙과 세부 시큐어코딩 기준을 함께 적용해 개발 단계부터 보안약점을 사전에 줄이기 위한 보조 지침으로 예방에 활용할 수 있습니다.

[구성요소]
skill-md 폴더 내 
COMMON_INSTRUCTIONS.md - 코딩 도구 별 md 전역 적용 가이드 
SECURE_CODING_RULES.md - 실제 시큐어코딩 예방 Skill 요구사항


## When to activate
- AI 코딩 수행 전 공통 지침으로 적용하여 개발 과정에서 보안약점을 사전 예방하고, 별도의 수동 시큐어코딩 검토를 최소화할 때 활용할 수 있습니다.
테스트 결과 50% 이상의 보안약점 예방 효과를 확인했으며, 최종 SAST 검증은 유지하되 낮은 토큰 사용량으로 비용 효율적인 적용이 가능합니다.

## Instructions
- TODO
프로젝트 루트에 COMMON_INSTRUCTIONS.md와 SECURE_CODING_RULES.md를 저장한 후, AI 코딩 도구별 공통 지침 파일에서 두 파일을 우선 참고하도록 연결합니다.

Codex: AGENTS.md
Claude Code: CLAUDE.md
GitHub Copilot: .github/copilot-instructions.md
Cursor: .cursor/rules/common-instructions.mdc
Gemini CLI: GEMINI.md

AI 코딩 도구는 작업 시작 시 COMMON_INSTRUCTIONS.md를 기본 지침으로 적용하고, 코드 생성·수정 내용과 관련된 경우에만 SECURE_CODING_RULES.md의 해당 보안 규칙을 선택적으로 확인합니다.
작업 완료 후에도 전체 규칙을 반복 검토하지 않고 변경 코드와 직접 영향 범위만 확인하여 토큰 사용량을 최소화합니다.


## Notes
- 참고사항)
본 스킬은 기존 시큐어코딩 진단을 대체하는 수단이 아닌, AI 코딩 단계에서 보안약점을 사전에 줄이기 위한 보조 지침입니다.
테스트 결과 약 50% 수준의 시큐어코딩 효과를 확인했으며, 향후 MCP 기반 시큐어코딩 검증을 통해 기존 진단 절차의 대체 가능성을 추가 검토할 예정입니다.
다양한 AI 모델을 대상으로 주기적인 테스트와 개선을 수행할 예정이며, MD 파일은 토큰 사용량과 비용을 최소화하도록 구성했습니다.
프로젝트 환경과 개발 기준에 따라 내용을 자유롭게 수정·보완하여 활용할 수 있습니다.

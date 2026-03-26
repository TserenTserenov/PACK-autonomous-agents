---
id: AS.FM.016
type: failure-mode
title: Tool Misuse and Function Compromise
status: active
source: Galileo AI Agent Failure Modes Guide (2026)
date: 2026-03-25
severity: critical
---

# AS.FM.016: Tool Misuse and Function Compromise

## Описание

Агент превышает авторизованные разрешения, вызывает функции с неверными параметрами или использует capabilities непредусмотренным образом — операционные и security-риски.

## Severity: Критический

«Over-permissioned tools sit high on the security side of failure classifications.»

## Сценарий

Агент имеет `delete_user(user_id)` для spam cleanup → получает prompt injection → интерпретирует «remove all inactive users» как «delete all users with last_login > 30 days» → удаляет 10K платящих клиентов → необратимо.

## Mitigation

- Sandbox testing first: dry-run mode для всех tool calls
- Minimum-necessary privilege: whitelist только необходимых функций per agent role
- Manual approval для sensitive actions: human-in-the-loop для delete/update/payment
- Resource ceilings: rate limits, cost circuit breakers
- Comprehensive logging: audit trail для всех tool invocations

## Связь с IWE

- **AS.M.001 (Trust Stack):** graduated governance, bounded agency
- **WP-132 (scheduler.sh):** tool whitelisting per task
- **AS.FM.017 (Prompt Injection):** часто tool misuse = следствие injection

## Источники

1. Galileo AI: Agent Failure Modes Guide (2026)
   URL: https://galileo.ai/blog/agent-failure-modes-guide

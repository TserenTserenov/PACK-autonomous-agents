---
id: AS.FM.014
type: failure-mode
title: Context and Memory Corruption
status: active
source: Galileo AI Agent Failure Modes Guide (2026)
date: 2026-03-25
severity: severe
---

# AS.FM.014: Context and Memory Corruption

## Описание

Испорченные записи в памяти сохраняются между сессиями. Агент «slowly becomes less reliable as each slightly wrong memory entry influences the next».

## Severity: Серьёзный

Скрытая деградация, остающаяся незамеченной до видимого ухудшения.

## Сценарий

Агент записывает «user prefers email notifications» на основе неверно интерпретированного сигнала → использует в 50+ взаимодействиях → пользователь всё больше раздражён email-ами → риск оттока растёт молча → нет алерта до отписки.

## Mitigation

- Provenance tracking: timestamp + source для каждой записи памяти
- Cryptographic signatures на записи (tamper detection)
- Semantic validators перед persistence: противоречит ли существующей памяти?
- Versioned memory snapshots: откат к known-good state
- Drift detectors: мониторинг slow-motion corruption через embedding distance

## Связь с IWE

- **WP-132 (scheduler.sh):** risk of task state corruption в persistence
- **AS.M.006 (Four-Type Memory):** episodic vs semantic memory integrity
- **DP.SOTA.002 (Context Engineering):** WISC pattern — Isolate контекст для предотвращения corruption

## Источники

1. Galileo AI: Agent Failure Modes Guide (2026)
   URL: https://galileo.ai/blog/agent-failure-modes-guide

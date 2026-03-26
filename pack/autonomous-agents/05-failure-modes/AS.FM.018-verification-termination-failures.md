---
id: AS.FM.018
type: failure-mode
title: Verification and Termination Failures
status: active
source: Galileo AI Agent Failure Modes Guide (2026)
date: 2026-03-25
severity: high
---

# AS.FM.018: Verification and Termination Failures

## Описание

Агент не верифицирует работу, завершается преждевременно до completion, или продолжает выполнение бесконечно без proper stopping conditions.

## Severity: Высокий

«Silent killer category» — неполное выполнение и waste ресурсов.

## Сценарий

Агент задан «generate sales report» → генерирует 80% output → hits token limit → terminates → нет верификации → неполный отчёт отправлен стейкхолдерам → бизнес-решение на partial data.

## Mitigation

- Multi-stage validators: static rules + LLM judges + human sign-off
- Explicit completion criteria: определение «done» per task type
- Comprehensive audit logging: запись причины termination
- Test coverage в CI: симуляция premature termination scenarios
- Timeout + retry с другой стратегией (не endless loop)

## Связь с IWE

- **AS.FM.009 (Loop of Death):** timeout enforcement — противоположная проблема
- **WP-132 (scheduler.sh):** completion verification
- **AS.D.008 (Scout vs Researcher):** termination criteria различаются по типу задачи
- **AS.FM.012 (Specification Failures):** нечёткие требования → невозможность определить «done»

## Источники

1. Galileo AI: Agent Failure Modes Guide (2026)
   URL: https://galileo.ai/blog/agent-failure-modes-guide

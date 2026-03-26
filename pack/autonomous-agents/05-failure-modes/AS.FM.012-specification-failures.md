---
id: AS.FM.012
type: failure-mode
title: Specification and System Design Failures
status: active
source: Galileo AI Agent Failure Modes Guide (2026)
date: 2026-03-25
severity: critical
---

# AS.FM.012: Specification and System Design Failures

## Описание

Нечёткие или недоспецифицированные требования к агенту создают фундаментальные пробелы: неясные цели каскадом портят все последующие решения.

## Severity: Критический

Фундаментальные проблемы влияют на все downstream-решения.

## Сценарий

Агент развёрнут с размытой целью «improve customer satisfaction» → интерпретирует как «respond to all tickets instantly» → игнорирует приоритеты, SLA, правила эскалации → хаос в очереди поддержки.

## Mitigation

- Валидация требований перед деплоем через constraint-based checks
- Adversarial scenario testing
- Конвертация design patterns в executable artifacts (не слайды)
- Документирование edge cases и failure conditions явно

## Связь с IWE

- **WP-132 (scheduler.sh):** требует explicit completion criteria для каждой задачи
- **AS.M.001 (Trust Stack):** bounded agency через constraints
- **AS.FM.018 (Verification Failures):** каскадный эффект — нечёткие требования → невозможность верификации

## Источники

1. Galileo AI: Agent Failure Modes Guide (2026)
   URL: https://galileo.ai/blog/agent-failure-modes-guide

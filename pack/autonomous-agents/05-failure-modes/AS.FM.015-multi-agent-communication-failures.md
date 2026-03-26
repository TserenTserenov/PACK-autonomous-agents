---
id: AS.FM.015
type: failure-mode
title: Multi-Agent Communication Failures
status: active
source: Galileo AI Agent Failure Modes Guide (2026)
date: 2026-03-25
severity: high
---

# AS.FM.015: Multi-Agent Communication Failures

## Описание

Агенты неверно интерпретируют сообщения, теряют информацию при handoff, или работают с несогласованными протоколами — координация разваливается.

## Severity: Высокий

«Coordination complexity grows exponentially, not linearly» с ростом числа агентов.

## Сценарий

Agent A форматирует output как JSON, Agent B ожидает YAML → parsing fails silently → Agent B использует default values → downstream-решение на основе неверных данных → нет ошибки в логах, т.к. «valid YAML».

## Mitigation

- Стандартизированные JSON schemas и role contracts (document, enforce, test)
- Execution traces через границы агентов (distributed tracing)
- Redundant message channels (retry с другой сериализацией)
- Периодический protocol audit: обнаружение drift в стандартах коммуникации
- Contract testing: агенты тестируют интерфейсы друг друга в CI

## Связь с IWE

- **WP-144 (multi-agent systems):** координация Scout, Экстрактор, Стратег
- **AS.D.007 (роли агентов):** чёткие контракты между ролями
- **DP.IPO.001 (IPO-паттерн):** стандартизированные inputs/outputs
- **75% multi-agent систем unmanageable >5 agents** (LangGraph 2026 data)

## Источники

1. Galileo AI: Agent Failure Modes Guide (2026)
   URL: https://galileo.ai/blog/agent-failure-modes-guide

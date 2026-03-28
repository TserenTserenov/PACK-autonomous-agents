---
id: AS.FM.020
type: failure-mode
title: Production Deployment Failure (Organizational Readiness Gap)
status: active
source: "Digital Applied (88% fail), HBR (Why Agentic AI Fails), Use Apify, Gartner"
date: 2026-03-28
severity: critical
---

# AS.FM.020: Production Deployment Failure (Organizational)

## Описание

Failure mode, при котором агентный проект технически валиден (проходит тесты, GEPA validation), но не достигает production или quietly shut down из-за organizational readiness gap: governance gaps, observability limitations, legacy incompatibility, отсутствие accountability frameworks.

**Статистика:** 88% AI agent projects never reach production (Digital Applied). Gartner: 40% agentic AI projects будут отменены к концу 2027.

## Severity: Критический

Не технический провал — организационный. Самый частый failure mode по статистике.

## Различение: Technical FM (012-018) ≠ Organizational FM (020)

| Аспект | Technical FM (012-018) | Organizational FM (020) |
|--------|------------------------|------------------------|
| Причина | Agent behavior (reasoning, memory, tools) | Enterprise readiness (governance, infra, observability) |
| Детектируется | Unit/integration tests, GEPA | Pre-deployment audit, governance checklist |
| Severity point | Runtime (production errors) | Pre-production (never deployed) |
| Owner | AI Engineer, Agent Developer | CTO, Program Manager, Compliance |
| Mitigation | Code fixes, prompt tuning | Governance frameworks, organizational change management |

## Сценарий

1. Team разрабатывает multi-agent систему для automation workflow
2. Agents проходят все technical validations: GEPA tests (quality >0.8), unit tests, integration tests
3. Deployment blocked из-за:
   - **Governance gap:** нет accountability framework (кто одобряет решения агента? кто эскалирует?)
   - **Observability gap:** monitoring stack не поддерживает agent tracing
   - **Legacy integration:** API edge cases, rate limiting, async coordination issues
   - **Risk aversion:** Leadership не уверена в governance → pilot freezes
4. Результат: project quietly shut down через 6-12 месяцев

## Mitigation

- **Pre-deployment governance checklist:**
  - Accountability matrix (decision authority, escalation paths, HITL triggers)
  - Observability plan (tracing stack, behavior monitoring, drift detection)
  - Legacy compatibility assessment (API contracts, auth flows, rate limits)
  - Risk tolerance definition (уровень автономии, rollback triggers)
- **Organizational readiness audit:** отдельный gate после GEPA (проводит CTO/PM, не AI Engineer)
- **Staged rollout governance:** начать с low-risk workflows (internal tools, не customer-facing)
- **Graduated Governance (AS.M.004):** tiered autonomy model (L0-L3) для de-risk deployment

## Связь с IWE

- **AS.M.004** (Graduated Governance) — mitigation framework
- **AS.SOTA.003** (WEF/Singapore Governance) — external governance standards
- **WP-179** (GEPA Test Framework) — добавить organizational readiness gate
- **AS.FM.012-018** — technical failure modes (дополняет, не заменяет)
- **AS.SOTA.001** — 98% не в масштабе из-за этого FM

## Источники

1. Digital Applied: Why 88% of AI Agents Fail Production
   URL: https://www.digitalapplied.com/blog/88-percent-ai-agents-never-reach-production-failure-framework
2. HBR: Why Agentic AI Projects Fail
   URL: https://hbr.org/2025/10/why-agentic-ai-projects-fail-and-how-to-set-yours-up-for-success
3. Use Apify: Agentic AI in Production
   URL: https://use-apify.com/blog/agentic-ai-enterprise-adoption-2026

---
id: AS.FM.013
type: failure-mode
title: Reasoning Loops and Hallucination Cascades
status: active
source: Galileo AI Agent Failure Modes Guide (2026)
date: 2026-03-25
severity: extreme
---

# AS.FM.013: Reasoning Loops and Hallucination Cascades

## Описание

Агент генерирует ложную информацию, затем использует фабрикации для последующих решений — «dangerous chain reaction of errors that amplify across systems».

## Severity: Экстремальный

Одна галлюцинация отравляет множество downstream-систем экспоненциально.

## Сценарий

Phantom SKU hallucinated на шаге 6 → портит pricing logic → triggers inventory checks на шаге 9 → генерирует shipping labels на шаге 12 → отправляет подтверждения клиенту на шаге 15. К моменту обнаружения отравлены 4 системы, стоимость инцидента x10.

## Mitigation

- Ensemble verification: консенсус моделей перед действием
- Uncertainty estimation: измерение confidence, пауза ниже порога
- LLM-as-a-Judge pipelines в CI/CD
- Counterfactual stress testing: симуляция галлюцинаций при тестировании
- Source-of-truth anchoring: верификация против внешнего ground truth

## Связь с IWE

- **AS.FM.010 (Self-Consistency Trap):** majority vote недостаточен, нужен external validation
- **DP.SOTA.002 (Context Engineering):** grounding в factual knowledge через RAG
- **AS.FM.009 (Loop of Death):** reasoning loops = частный случай

## Источники

1. Galileo AI: Agent Failure Modes Guide (2026)
   URL: https://galileo.ai/blog/agent-failure-modes-guide

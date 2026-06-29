---
title: Project Facts
type: note
project: project-alpha
updated: 2026-06-15
tags: [facts, context, invariants]
---

# Project Facts

> Постоянные факты о проекте — стек, интеграции, договорённости команды.
> В отличие от decisions.md, факты не требуют обоснования — это просто реальность.

## Project Identity

- [fact] Project name: <название проекта> #project
- [fact] Platform: iOS + Android (React Native + Expo) #platform
- [fact] Language: TypeScript strict #stack
- [fact] Target: <опиши целевую аудиторию> #product

## Technical Constraints

- [fact] Min iOS version: <версия> #ios
- [fact] Min Android API: <уровень API> #android
- [fact] Node version: <версия> #env
- [fact] Expo SDK: <версия> #expo

## Team & Process

- [fact] Sprint length: <длина спринта> #process
- [fact] PM tool: Jira Structure #process
- [fact] Methodology: Agile / SDD-first #process
- [fact] Specs format: Markdown + BDD (Given/When/Then) #process

## Integrations & APIs

<!--
- [fact] Auth: <провайдер> #integration #auth
- [fact] Analytics: <инструмент> #integration
- [fact] Backend: <тип/технология> #integration
-->

## Key Paths

<!--
- [fact] Entry point: app/(tabs)/index.tsx #structure
- [fact] Shared UI: shared/ui/ #structure
- [fact] Feature modules: features/<name>/ #structure
-->

## Relations

- context_for [[decisions]]
- context_for [[last-session]]
- constrained_by [[constraints]]

---

> **Инструкция для агента**: Факты не обсуждаются — они обновляются
> при изменении реальности. При обновлении ставить дату изменения в комментарий.

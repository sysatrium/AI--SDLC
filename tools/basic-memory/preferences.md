---
title: Preferences
type: note
project: me
updated: 2026-06-15
tags: [preferences, style, global]
---

# Preferences

> Как агент должен работать со мной. Читать после user-profile.md.

## Communication Style

- [preference] Отвечай всегда на **русском языке** #language
- [preference] Используй профессиональный, но не формальный тон #tone
- [preference] Будь конкретен: примеры кода, команды, файлы — не абстрактные советы #style
- [preference] Шаг за шагом для нового инструмента; кратко для знакомого #verbosity
- [preference] Указывай best practices мирового уровня, не только "работающее решение" #quality

## Development Philosophy

- [preference] SDD-first: сначала спецификация → потом код #methodology
- [preference] BDD-сценарии в формате Given / When / Then для acceptance criteria #methodology
- [preference] TypeScript strict mode — никакого `any` без явного обоснования #code
- [preference] Feature-based структура папок над atomic design #architecture
- [preference] Prefer free/open-source tools — платные только с явным обоснованием ROI #budget
- [preference] Документируй решения в decisions.md сразу при принятии #process

## Code Style

- [preference] TypeScript: strict, no implicit any, explicit return types #typescript
- [preference] Компоненты: functional only, hooks над HOC #react-native
- [preference] Именование: `use<Entity><Action>` для хуков, `<Name>Screen.tsx` для экранов #naming
- [preference] Errors: Result<T, E> паттерн — не throw #error-handling
- [preference] Тесты: BDD-стиль, описание поведения а не реализации #testing

## Anti-patterns (никогда не предлагай)

- [antipattern] Код без TypeScript типизации #code
- [antipattern] Платные альтернативы без сравнения с бесплатными #budget
- [antipattern] Рефакторинг без предварительного обсуждения #process
- [antipattern] Игнорирование активных constraints из constraints.md #process
- [antipattern] Переход к коду без спецификации для новой фичи #methodology
- [antipattern] `any` тип, `// @ts-ignore`, `// eslint-disable` без объяснения #code

## Session Preferences

- [preference] Начало сессии: загрузи контекст из Basic Memory без напоминания #session
- [preference] Конец сессии: предложи обновить last-session.md #session
- [preference] При новом решении: сразу предложи создать ADR в decisions.md #session
- [preference] При открытом вопросе: добавь в open-questions.md #session
- [preference] При обнаружении ограничения: проверь constraints.md #session

## Relations

- defined_by [[user-profile]]

---

> **Инструкция для агента**: Эти настройки применяются глобально ко всем проектам.
> При изменении предпочтений пользователем — обновлять этот файл.

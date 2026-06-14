# Настройка Basic Memory 0.22 для OpenAI Codex

## Архитектура памяти

```
~/My project/
  me/                              ← проект Basic Memory "me" (глобальная память)
  │   user-profile.md
  │   preferences.md
  │
  project-alpha/                   ← git-репозиторий
  │   AGENTS.md                    ← системный промпт для Codex
  │   memory/                      ← папка памяти проекта
  │       decisions.md
  │       facts.md
  │       last-session.md
  │   .gitignore
  │
  project-beta/
      AGENTS.md
      memory/
          decisions.md
          facts.md
          last-session.md
```

> **Ключевой принцип**: Basic Memory следит за папкой проекта автоматически через
> file watcher — отдельная команда sync не нужна. Файлы подхватываются сразу после
> сохранения.

---

## Шаг 1: Установка

### macOS (рекомендуется)

```bash
brew tap basicmachines-co/basic-memory
brew trust basicmachines-co/basic-memory
brew install basic-memory

# Проверить версию
basic-memory --version
# Basic Memory version: 0.22.x
```

### Через uv (все платформы, Python 3.13+)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
uv tool install basic-memory
basic-memory --version
```

---

## Шаг 2: Создание структуры папок

```bash
# Глобальная память
mkdir -p ~/My\ project/me

# Память для каждого проекта
mkdir -p ~/My\ project/project-alpha/memory
mkdir -p ~/My\ project/project-beta/memory
```

---

## Шаг 3: Регистрация проектов

Реальные команды `basic-memory project` в версии 0.22:

```bash
# Зарегистрировать проекты
basic-memory project add "me"            ~/My\ project/me
basic-memory project add "project-alpha" ~/My\ project/project-alpha/memory
basic-memory project add "project-beta"  ~/My\ project/project-beta/memory

# Установить "me" как дефолтный
basic-memory project default "me"

# Проверить список
basic-memory project list
```

### Все доступные подкоманды `project`:

| Команда                              | Что делает                            |
|--------------------------------------|---------------------------------------|
| `project list`                       | Список всех проектов                  |
| `project add <name> <path>`          | Добавить проект                       |
| `project remove <name>`              | Удалить проект из конфига             |
| `project default <name>`             | Установить дефолтный проект           |
| `project move <name> <new-path>`     | Переместить проект                    |
| `project info <name>`                | Подробная информация о проекте        |
| `project ls --name <name>`           | Список файлов в проекте               |
| `project set-cloud <name>`           | Подключить проект к облаку            |
| `project set-local <name>`           | Вернуть проект в локальный режим      |

---

## Шаг 4: Копирование стартовых файлов памяти

```bash
cp user-profile.md ~/My\ project/me/user-profile.md
cp preferences.md  ~/My\ project/me/preferences.md

# Проверить что файлы подхвачены
basic-memory status
```

> Sync происходит автоматически — сохранил файл → Basic Memory его подхватил.

---

## Шаг 5: Подключение к Codex CLI

```bash
# Глобальная память (проект me)
codex mcp add bm-me bash -c "uvx basic-memory mcp --project me"

# Проектная память (добавляй по мере появления проектов)
codex mcp add bm-alpha bash -c "uvx basic-memory mcp --project project-alpha"
codex mcp add bm-beta  bash -c "uvx basic-memory mcp --project project-beta"

# Проверить
codex mcp list
```

---

## Шаг 6: Подключение к Codex App

Codex App не поддерживает subprocess — нужен HTTP-сервер:

```bash
# Запустить MCP HTTP-сервер (держать терминал открытым)
basic-memory mcp --transport streamable-http --port 8000
```

В Codex App → **Settings → Connectors → Custom MCP**:
- **Name**: `Basic Memory`
- **Server URL**: `http://localhost:8000/mcp`

**Альтернатива**: Basic Memory Cloud (без постоянного процесса):
- Зарегистрироваться на basicmemory.com → получить API-ключ
- **Server URL**: `https://cloud.basicmemory.com/mcp` → OAuth
- Подключить проекты к облаку: `basic-memory project set-cloud "me"`

---

## Шаг 7: AGENTS.md — системный промпт для Codex

Создай `AGENTS.md` в корне каждого git-репозитория.
Замени `project-alpha` / `bm-alpha` на реальные имена:

```markdown
## Memory Protocol

Project: project-alpha
Memory: bm-me (user profile) + bm-alpha (project context)

### Session START — выполнять всегда
1. read_note("memory://me/user-profile")             — кто пользователь
2. read_note("memory://me/preferences")              — стиль и предпочтения  
3. search_notes("decisions facts")                   — контекст проекта
4. read_note("memory://project-alpha/last-session")  — где остановились

### During session
- Принято архитектурное решение → добавить в memory/decisions.md
- Обнаружен факт о проекте      → добавить в memory/facts.md
- Изменились предпочтения       → обновить memory://me/preferences

### Session END — обязательно перед завершением
Обновить memory/last-session.md:
  - Что сделали
  - Что в процессе (незавершённое)
  - Следующие шаги
  - Открытые вопросы
```

---

## Шаг 8: Шаблоны файлов памяти проекта

Создай три файла при старте каждого нового проекта:

### `memory/decisions.md`

```markdown
---
title: Architecture Decisions
project: project-alpha
type: decisions
---

# Architecture Decisions

## [ADR-001] Название решения
- **Дата**: YYYY-MM-DD
- **Статус**: Принято
- **Контекст**: Почему встала задача
- **Решение**: Что выбрали и почему
- **Альтернативы**: Что рассматривали и отклонили
- **Последствия**: Плюсы и минусы
```

### `memory/facts.md`

```markdown
---
title: Project Facts
project: project-alpha
type: facts
---

# Project Facts

## Технический стек
- Runtime: ...
- Основные зависимости: ...
- Ключевые версии пакетов: ...

## Среда и деплой
- ...

## Ограничения и договорённости команды
- ...

## Внешние интеграции
- ...
```

### `memory/last-session.md`

```markdown
---
title: Last Session
project: project-alpha
type: session-log
---

# Last Session

## Дата: YYYY-MM-DD

## Что сделали
- ...

## Что в процессе (незавершённое)
- ...

## Следующие шаги
- ...

## Открытые вопросы
- ...
```

---

## Шаг 9: Адресация заметок (memory:// URLs)

```
memory://me/user-profile
memory://me/preferences
memory://project-alpha/decisions
memory://project-alpha/facts
memory://project-alpha/last-session
```

---

## Шаг 10: Переключение между проектами

Сказать агенту в Codex:
```
Switch to the "project-alpha" project.
```

Или вручную установить дефолтный:
```bash
basic-memory project default "project-alpha"
```

---

## .gitignore (опционально)

Если не хочешь коммитить память в git:
```bash
echo "memory/" >> ~/My\ project/project-alpha/.gitignore
```

Если хочешь делиться контекстом с командой — не добавляй в `.gitignore`.
Тогда `decisions.md` становится частью документации репозитория.

---

## Полезные команды v0.22

```bash
basic-memory status                         # статус файлов и БД
basic-memory doctor                         # диагностика при проблемах
basic-memory reindex                        # перестроить индексы вручную
basic-memory project list                   # список всех проектов
basic-memory project info "me"              # детали конкретного проекта
basic-memory project default "me"           # сменить дефолтный проект
basic-memory project ls --name "me"         # файлы в проекте
basic-memory project add "name" /path       # добавить проект
basic-memory project remove "name"          # удалить проект из конфига
```

---

## Правила безопасности

- Никогда не храни API-ключи, токены, пароли в файлах Basic Memory
- Секреты — только в `.env`, который добавлен в `.gitignore`



# Changelog

Все значимые изменения в **Legal Agent Kit** будут фиксироваться в этом файле.

Формат основан на подходе [Keep a Changelog](https://keepachangelog.com/), а версии рекомендуется вести по смыслу изменений.

> Проект содержит методические материалы, шаблоны, чек-листы, примеры и промпты для подготовки черновиков правовых документов. Материалы не являются юридической консультацией и требуют проверки юристом перед использованием в реальных проектах.

---

## [0.1.0] — 2026-06-01

### Added

- Добавлена базовая структура репозитория **Legal Agent Kit**.
- Добавлен `README.md` с описанием назначения, структуры и сценариев использования репозитория.
- Добавлен `AGENTS.md` с инструкциями для AI-агентов и Codex.
- Добавлен `LEGAL_AGENT_GUIDE.md` с методикой подготовки правовых документов.
- Добавлен `LEGAL_PROJECT_QUESTIONNAIRE.md` с анкетой проекта.
- Добавлен `CONTRIBUTING.md` с правилами участия в проекте.
- Добавлен `LICENSE`.

### Docs

- Добавлены методические документы в `docs/`:
  - `how-to-use-with-codex.md`;
  - `how-to-use-with-chatgpt.md`;
  - `document-matrix.md`;
  - `interface-checklist.md`;
  - `consent-storage.md`;
  - `legal-disclaimer.md`.

### Prompts

- Добавлены готовые промпты для Codex в `prompts/`:
  - `codex-create-legal-docs.md`;
  - `codex-integrate-legal-pages.md`;
  - `codex-audit-existing-legal-docs.md`;
  - `codex-update-legal-docs.md`.

### Templates

- Добавлены шаблоны правовых документов на русском языке в `templates/ru/`:
  - `terms.template.md`;
  - `privacy.template.md`;
  - `personal-data-consent.template.md`;
  - `offer.template.md`;
  - `payment-and-refund.template.md`;
  - `cookie-policy.template.md`;
  - `support-rules.template.md`;
  - `data-processing.template.md`;
  - `subscription-rules.template.md`;
  - `marketing-consent.template.md`;
  - `bank_data_processing.md`;
  - `api_terms.md`;
  - `bot_terms.md`.

### Checklists

- Добавлены чек-листы на русском языке в `checklists/ru/`:
  - `launch-checklist.md`;
  - `registration-form-checklist.md`;
  - `payment-page-checklist.md`;
  - `subscription-checklist.md`;
  - `personal-data-checklist.md`;
  - `cookies-and-analytics-checklist.md`;
  - `api-tokens-checklist.md`.

### Examples

- Добавлены демонстрационные примеры в `examples/ru/`:
  - `saas-subscription` — пример для SaaS с подпиской;
  - `telegram-max-bot` — пример для Telegram/MAX-бота;
  - `simple-landing` — пример для простого лендинга.

### Notes

- Все шаблоны содержат плейсхолдеры для неизвестных данных.
- Все материалы требуют адаптации под конкретный проект.
- Перед публикацией документов необходима юридическая проверка.

---

## [Unreleased]

### Planned

- Добавить англоязычную структуру `templates/en/`, если появится потребность.
- Добавить дополнительные примеры для маркетплейс-интеграций.
- Добавить дополнительные примеры для сервисов с банковскими данными.
- Добавить checklist для AI-аудита документов перед релизом.
- Добавить workflow проверки Markdown-файлов.
- Добавить шаблоны Issue и Pull Request для GitHub.
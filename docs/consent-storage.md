

# Хранение фактов согласия пользователей

## Назначение

Этот документ описывает рекомендуемый подход к хранению фактов принятия пользователем правовых документов и согласий.

Файл предназначен для AI-агентов, разработчиков и продуктовых команд, которые внедряют в проект:

- регистрацию пользователей;
- личный кабинет;
- онлайн-оплату;
- подписку;
- подключение внешних интеграций;
- обработку персональных данных;
- рекламные или информационные рассылки;
- работу через Telegram/MAX-бота;
- API-доступ.

Хранение согласий помогает восстановить, какие условия пользователь принял, когда он это сделал и через какой интерфейс.

---

## 1. Когда нужно хранить согласия

Фиксация согласий рекомендуется, если в проекте есть хотя бы одно из условий:

| Условие | Что фиксировать |
|---|---|
| Регистрация пользователя | Принятие пользовательского соглашения, политики конфиденциальности, согласия на обработку персональных данных |
| Личный кабинет | Принятие актуальных редакций документов |
| Онлайн-оплата | Принятие публичной оферты и правил оплаты/возврата |
| Подписка | Принятие правил подписки и условий продления |
| Пробный период | Принятие условий пробного доступа |
| Автопродление | Подтверждение условий повторных списаний |
| Форма заявки | Согласие на обработку персональных данных |
| Рассылка | Согласие на информационные и рекламные сообщения |
| API-доступ | Принятие условий использования API |
| Передача API-токенов | Согласие с правилами обработки токенов и данных интеграций |
| Подключение банка | Согласие с правилами обработки банковских данных |
| Telegram/MAX-бот | Принятие условий использования бота и обработки идентификаторов мессенджера |

---

## 2. Какие события согласий хранить

Рекомендуемые типы событий:

```text
accepted
revoked
updated
renewed
expired
```

Расшифровка:

| Событие | Значение |
|---|---|
| `accepted` | Пользователь принял документ или дал согласие |
| `revoked` | Пользователь отозвал согласие, если отзыв предусмотрен |
| `updated` | Документ обновлен, требуется новая фиксация согласия |
| `renewed` | Пользователь принял новую редакцию документа |
| `expired` | Согласие или документ перестали действовать по сроку или условию |

В большинстве проектов достаточно хранить только `accepted` и `revoked`, но для SaaS и подписок полезно учитывать `renewed`.

---

## 3. Типы документов

Рекомендуемые значения `document_type`:

```text
terms
privacy
personal_data_consent
offer
payment_and_refund
subscription_rules
support_rules
cookie_policy
marketing_consent
data_processing
bank_data_processing
api_terms
bot_terms
```

Описание:

| Тип | Документ |
|---|---|
| `terms` | Пользовательское соглашение |
| `privacy` | Политика конфиденциальности |
| `personal_data_consent` | Согласие на обработку персональных данных |
| `offer` | Публичная оферта |
| `payment_and_refund` | Правила оплаты и возврата |
| `subscription_rules` | Правила подписки |
| `support_rules` | Правила поддержки |
| `cookie_policy` | Политика cookies |
| `marketing_consent` | Согласие на информационные и рекламные сообщения |
| `data_processing` | Правила обработки API-токенов и данных интеграций |
| `bank_data_processing` | Правила обработки банковских данных |
| `api_terms` | Условия использования API |
| `bot_terms` | Условия использования бота |

---

## 4. Источники согласий

Рекомендуемые значения `source`:

```text
registration
payment
profile
settings
landing_form
feedback_form
subscription_form
bot
api
oauth_connection
bank_connection
marketplace_connection
admin_panel
manual
```

Описание:

| Источник | Когда используется |
|---|---|
| `registration` | Форма регистрации |
| `payment` | Страница оплаты |
| `profile` | Профиль или личный кабинет |
| `settings` | Настройки пользователя или организации |
| `landing_form` | Форма заявки на лендинге |
| `feedback_form` | Форма обратной связи |
| `subscription_form` | Форма подписки на рассылку |
| `bot` | Telegram/MAX-бот |
| `api` | Принятие условий через API |
| `oauth_connection` | Подключение внешнего сервиса по OAuth |
| `bank_connection` | Подключение банка |
| `marketplace_connection` | Подключение маркетплейса |
| `admin_panel` | Действие в административной панели |
| `manual` | Ручная фиксация администратором |

---

## 5. Рекомендуемая структура хранения

### 5.1. Минимальный набор полей

| Поле | Тип | Описание |
|---|---|---|
| `id` | integer / uuid | ID записи |
| `user_id` | integer / uuid / nullable | ID пользователя, если есть регистрация |
| `document_type` | string | Тип документа |
| `document_version` | string | Версия документа |
| `accepted_at` | datetime | Дата и время принятия |
| `source` | string | Источник согласия |

### 5.2. Расширенный набор полей

| Поле | Тип | Описание |
|---|---|---|
| `id` | integer / uuid | ID записи |
| `user_id` | integer / uuid / nullable | ID пользователя |
| `account_id` | integer / uuid / nullable | ID аккаунта, компании или tenant |
| `organization_id` | integer / uuid / nullable | ID организации, если используется B2B-модель |
| `document_type` | string | Тип документа |
| `document_title` | string | Название документа на момент согласия |
| `document_version` | string | Версия документа |
| `document_date` | date | Дата редакции документа |
| `document_url` | string | URL документа |
| `checkbox_text` | text | Текст чекбокса или подтверждения |
| `event_type` | string | `accepted`, `revoked`, `renewed` и т.д. |
| `accepted_at` | datetime / nullable | Дата принятия |
| `revoked_at` | datetime / nullable | Дата отзыва |
| `ip_address` | string / nullable | IP-адрес пользователя |
| `user_agent` | text / nullable | User-agent браузера или клиента |
| `source` | string | Источник согласия |
| `source_url` | string / nullable | URL страницы, где получено согласие |
| `locale` | string / nullable | Язык документа или интерфейса |
| `meta_json` | json / nullable | Дополнительные данные |
| `created_at` | datetime | Дата создания записи |

---

## 6. Пример SQL-таблицы

Ниже приведен универсальный пример. Его нужно адаптировать под конкретный стек, стиль проекта и используемую СУБД.

```sql
CREATE TABLE user_consents (
    id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NULL,
    account_id BIGINT UNSIGNED NULL,
    organization_id BIGINT UNSIGNED NULL,

    document_type VARCHAR(64) NOT NULL,
    document_title VARCHAR(255) NOT NULL,
    document_version VARCHAR(32) NOT NULL,
    document_date DATE NULL,
    document_url VARCHAR(500) NULL,

    checkbox_text TEXT NULL,
    event_type VARCHAR(32) NOT NULL DEFAULT 'accepted',

    accepted_at DATETIME NULL,
    revoked_at DATETIME NULL,

    ip_address VARCHAR(64) NULL,
    user_agent TEXT NULL,
    source VARCHAR(64) NOT NULL,
    source_url VARCHAR(500) NULL,
    locale VARCHAR(16) NULL,

    meta_json JSON NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,

    PRIMARY KEY (id),
    INDEX idx_user_consents_user_id (user_id),
    INDEX idx_user_consents_account_id (account_id),
    INDEX idx_user_consents_document_type (document_type),
    INDEX idx_user_consents_document_version (document_version),
    INDEX idx_user_consents_event_type (event_type),
    INDEX idx_user_consents_accepted_at (accepted_at)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

---

## 7. Пример JSON-записи

```json
{
  "user_id": 123,
  "account_id": 45,
  "document_type": "terms",
  "document_title": "Пользовательское соглашение",
  "document_version": "1.0",
  "document_date": "2026-05-25",
  "document_url": "https://example.com/legal/terms",
  "checkbox_text": "Я принимаю Пользовательское соглашение",
  "event_type": "accepted",
  "accepted_at": "2026-05-25T12:30:00+03:00",
  "ip_address": "203.0.113.10",
  "user_agent": "Mozilla/5.0 ...",
  "source": "registration",
  "source_url": "https://example.com/register",
  "locale": "ru",
  "meta_json": {
    "form": "registration",
    "button_text": "Зарегистрироваться"
  }
}
```

---

## 8. Что хранить по основным сценариям

### 8.1. Регистрация

При регистрации рекомендуется фиксировать:

```text
terms
privacy
personal_data_consent
```

Для каждого документа:

- версию;
- дату редакции;
- URL;
- текст чекбокса;
- дату и время принятия;
- IP-адрес;
- user-agent;
- источник `registration`.

### 8.2. Оплата

Перед оплатой рекомендуется фиксировать:

```text
offer
payment_and_refund
subscription_rules
```

`subscription_rules` нужны, если доступ предоставляется на период, есть тарифы, пробный период, льготный период или автопродление.

Источник: `payment`.

### 8.3. Рассылка

Для информационных и рекламных сообщений рекомендуется отдельное согласие:

```text
marketing_consent
```

Важно хранить:

- текст согласия;
- дату согласия;
- источник;
- способ отписки;
- дату отзыва, если пользователь отписался.

### 8.4. Подключение маркетплейса или внешнего API

При передаче API-токена рекомендуется фиксировать:

```text
data_processing
api_terms
```

Источник:

```text
marketplace_connection
oauth_connection
settings
```

Рекомендуется сохранить в `meta_json`:

```json
{
  "integration": "marketplace",
  "provider": "ozon",
  "access_scope": "orders, products, stocks"
}
```

### 8.5. Подключение банка

При подключении банка рекомендуется фиксировать:

```text
bank_data_processing
privacy
```

Источник:

```text
bank_connection
oauth_connection
```

Рекомендуется сохранить в `meta_json`:

```json
{
  "provider": "bank_name",
  "access_type": "read_only",
  "data_scope": "accounts, balances, transactions, statements"
}
```

### 8.6. Бот Telegram / MAX

При первом запуске или перед использованием функций бота рекомендуется фиксировать:

```text
terms
privacy
personal_data_consent
bot_terms
```

Источник:

```text
bot
```

В `meta_json` можно сохранить:

```json
{
  "messenger": "telegram",
  "chat_id_hash": "...",
  "command": "/start"
}
```

Если хранение реального `chat_id` не требуется для юридической фиксации, в журнале согласий можно хранить хеш или ссылку на пользователя в основной таблице.

---

## 9. Отзыв согласия

Если пользователь может отозвать согласие, рекомендуется не удалять исходную запись, а создать новое событие `revoked` или заполнить `revoked_at`.

Пример:

```text
Пользователь дал согласие на рекламные сообщения 01.06.2026.
Пользователь отозвал согласие 10.06.2026.
```

В журнале можно хранить:

- исходное событие `accepted`;
- новое событие `revoked`;
- источник отзыва: `profile`, `unsubscribe_link`, `bot`, `support`.

Для обязательных документов, без которых сервис не может предоставляться, отзыв согласия может повлечь ограничение доступа или удаление аккаунта. Это должно быть описано в документах проекта.

---

## 10. Повторное согласие

Повторное согласие может потребоваться, если:

- изменился состав обрабатываемых данных;
- изменились цели обработки данных;
- изменились условия оплаты;
- изменились правила подписки;
- появилось автопродление;
- появились новые внешние интеграции;
- сервис начал получать банковские данные;
- изменились условия использования API;
- изменились существенные условия пользовательского соглашения или оферты.

Рекомендуемый порядок:

1. Создать новую версию документа.
2. Обновить дату редакции.
3. Сохранить старую редакцию.
4. Уведомить пользователя о новой редакции.
5. Запросить повторное согласие, если изменения существенные.
6. Сохранить новое событие `renewed` или `accepted` с новой версией документа.

---

## 11. Версионирование документов

Рекомендуемый формат версии:

```text
1.0
1.1
2.0
```

Пример логики:

| Изменение | Версия |
|---|---|
| Исправление опечаток без изменения смысла | 1.0 → 1.0.1 или без изменения версии |
| Уточнение формулировок | 1.0 → 1.1 |
| Существенное изменение условий | 1.0 → 2.0 |
| Добавление нового вида данных | 1.0 → 2.0 |
| Добавление автопродления | 1.0 → 2.0 |

---

## 12. Что агент должен предложить разработчику

Если агент анализирует проект, он должен подготовить рекомендации:

- где в интерфейсе получать согласия;
- какие документы фиксировать на регистрации;
- какие документы фиксировать на оплате;
- какие документы фиксировать при подключении интеграций;
- какие поля добавить в базу данных;
- как хранить версию документа;
- как хранить текст чекбокса;
- как обрабатывать отзыв согласия;
- как запрашивать повторное согласие после обновления документов.

---

## 13. Минимальный вариант для MVP

Если проект находится на стадии MVP, можно начать с минимального журнала:

```sql
CREATE TABLE user_consents (
    id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NULL,
    document_type VARCHAR(64) NOT NULL,
    document_version VARCHAR(32) NOT NULL,
    checkbox_text TEXT NULL,
    accepted_at DATETIME NOT NULL,
    ip_address VARCHAR(64) NULL,
    user_agent TEXT NULL,
    source VARCHAR(64) NOT NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    INDEX idx_user_consents_user_id (user_id),
    INDEX idx_user_consents_document_type (document_type)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

Для B2B/SaaS-проекта лучше сразу добавить `account_id` или `organization_id`.

---

## 14. Финальная проверка

Перед запуском проекта нужно проверить:

- фиксируются ли обязательные согласия при регистрации;
- фиксируется ли принятие оферты перед оплатой;
- фиксируются ли правила подписки при покупке подписки;
- фиксируется ли отдельное согласие на рекламные сообщения;
- фиксируется ли согласие при подключении API-токенов;
- фиксируется ли согласие при подключении банка;
- сохраняются ли версия и дата редакции документа;
- сохраняется ли текст чекбокса;
- сохраняется ли источник согласия;
- сохраняются ли дата, IP и user-agent;
- есть ли механизм отзыва необязательных согласий;
- есть ли механизм повторного согласия при существенных изменениях документов.

---

## 15. Итоговый вывод агента

После анализа проекта агент должен выдать краткий вывод:

```text
Для проекта рекомендуется хранить факты согласия пользователей.

Обязательные события:
- регистрация: terms, privacy, personal_data_consent;
- оплата: offer, payment_and_refund;
- подписка: subscription_rules;
- интеграции: data_processing;
- банк: bank_data_processing;
- рассылки: marketing_consent.

Рекомендуется добавить таблицу user_consents и фиксировать document_type, document_version, accepted_at, source, checkbox_text, ip_address и user_agent.

Реализация требует проверки с учетом фактической модели проекта и требований юриста.
```
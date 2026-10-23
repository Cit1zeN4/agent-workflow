# Этап 02 — Codex Runtime Integration

Десять самостоятельных заданий на реализацию без программного кода. Подготовлено 2026-10-22 по приложенным исходным документам. Исходные файлы не изменены.

## Порядок работы

Нумерация задаёт основной порядок реализации. Черновики контрактов 02.05 и ошибок 02.09 нужно согласовать после 02.01 до написания транспорта; затем уточнять их на соответствующих подэтапах. Это не требует двух реализаций одного модуля.

| Подэтап | Файл |
|---|---|
| 02.01 | [Protocol Research & Compatibility](02.01-protocol-research-and-compatibility.md) |
| 02.02 | [Runtime Process Lifecycle](02.02-runtime-process-lifecycle.md) |
| 02.03 | [JSON-RPC Transport](02.03-json-rpc-transport.md) |
| 02.04 | [Protocol Initialization](02.04-protocol-initialization.md) |
| 02.05 | [Runtime Adapter Contracts](02.05-runtime-adapter-contracts.md) |
| 02.06 | [Thread Management](02.06-thread-management.md) |
| 02.07 | [Turn Execution & Streaming](02.07-turn-execution-and-streaming.md) |
| 02.08 | [Interruption & Cancellation](02.08-interruption-and-cancellation.md) |
| 02.09 | [Error Handling & Diagnostics](02.09-error-handling-and-diagnostics.md) |
| 02.10 | [Integration & Compatibility Tests](02.10-integration-and-compatibility-tests.md) |

## Реестр ADR

| ADR | Решение | Где зафиксировано |
|---|---|---|
| ADR-02-01 | Codex App Server через stdio | [02.01](02.01-protocol-research-and-compatibility.md) |
| ADR-02-02 | Контракты из целевой установки | [02.01](02.01-protocol-research-and-compatibility.md) |
| ADR-02-03 | Один процесс с явным владельцем | [02.02](02.02-runtime-process-lifecycle.md) |
| ADR-02-04 | Узкий транспорт под wire-профиль Codex | [02.03](02.03-json-rpc-transport.md) |
| ADR-02-05 | Готовность соединения отделена от доступности inference | [02.04](02.04-protocol-initialization.md) |
| ADR-02-06 | Доменный адаптер с обратным каналом | [02.05](02.05-runtime-adapter-contracts.md) |
| ADR-02-07 | Thread — контекст runtime, а не workflow run | [02.06](02.06-thread-management.md) |
| ADR-02-08 | ACK не завершает execution | [02.07](02.07-turn-execution-and-streaming.md) |
| ADR-02-09 | Прерывание требует наблюдаемого подтверждения | [02.08](02.08-interruption-and-cancellation.md) |
| ADR-02-10 | Ошибка отдельно от определённости результата | [02.09](02.09-error-handling-and-diagnostics.md) |
| ADR-02-11 | Два уровня доказательств | [02.10](02.10-integration-and-compatibility-tests.md) |

Все ADR имеют статус «предлагается к реализации»: они задают план, но не подтверждают совместимость. При принятии обновить статус с датой и основанием; при опровержении оставить историю и добавить superseding ADR.

## Что подтверждено и что предстоит проверить

- Подтверждены содержание приложенных требований и наличие описаний App Server в официальной документации.
- В этой среде исполняемый Codex CLI не найден; схемы 0.163.0 не экспортировались, Windows и AI-запросы не тестировались.
- Целевая конфигурация из проекта: Codex 0.163.0, Node.js 24.21.0, Git for Windows 2.55.0. Эти номера не являются результатом проверки текущей работы.
- Перед реализацией сверить справку и schemas именно целевой установки. Современная документация и примеры не доказывают поддержку в 0.163.0.
- В 02.10 обязательный blocked/not-run не считается успешной приёмкой. Проверка реальных Matt Pocock Skills остаётся этапам 05/08.

## Границы общего этапа

| Этап | Передаваемый механизм / остающаяся ответственность |
|---|---|
| 03 | Нормализованные события / хранение, replay и SSE |
| 04 | Create/resume thread / политика сессий и mapping workflow |
| 05 | Server requests и ответы / политика HITL, хранение и UI |
| 06 | Итог execution / переходы workflow и бизнес-статусы |
| 07 | Явный cwd / выбор и создание безопасного workspace |
| 08 | Вход turn и stream / запуск конкретных скиллов и проверка артефактов |
| 11 | OutcomeUnknown, generation и IDs / персистентная сверка и ручное восстановление |

## Общие правила реализации

Один процесс App Server и один активный turn на адаптер в MVP; несколько threads используются последовательно. Handshake, авторизация и доступ к модели различаются. ACK не равен завершению. Interrupt не равен stop и local cancel. Неизвестный исход не даёт разрешения повторить действие. Точные поля и методы задаёт профиль схем, а не предположение по названию capability.

## Источники

- [Codex App Server](https://learn.chatgpt.com/docs/app-server) — протокол и жизненный цикл.
- [Codex as a platform](https://developers.openai.com/blog/codex-as-a-platform) — выбор интерфейса.
- [Windows sandbox](https://learn.chatgpt.com/docs/windows/windows-sandbox) — особенности целевой среды.
- [Sign in with ChatGPT: App Server](https://developers.openai.com/siwc/token-sharing-open-source/codex-app-server) — отдельный сценарий авторизации; не обязательная замена локального входа.

Дата обращения: 2026-10-22. Собственные рекомендации плана отделены от фактов протокола; внешняя документация изменяется.

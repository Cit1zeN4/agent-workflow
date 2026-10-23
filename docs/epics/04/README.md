# Этап 04 — Session Management

Четыре задания на политику сессий поверх [runtime adapter](../02/README.md) и [хранения](../03/README.md). Статус: план реализации; продолжение реального Codex thread здесь ещё не проверено. Основание: [требования](../../project.md) и [общий эпик](04-session-management.md).

| Подэтап | Задание |
|---|---|
| 04.01 | [Идентификаторы и жизненный цикл](04.01-session-identity-and-lifecycle.md) |
| 04.02 | [Политика общих и отдельных сессий](04.02-session-allocation-policy.md) |
| 04.03 | [Контекст и история выполнений](04.03-context-and-execution-history.md) |
| 04.04 | [Продолжение и потеря thread](04.04-resume-and-lost-thread.md) |

Session Manager выбирает session и ведёт её историю; Runtime Adapter создаёт и продолжает Codex thread. Workflow Engine решает, когда запускается этап, а исполнитель tickets — когда запускается ticket. Сверка неопределённого результата после сбоя принадлежит 11. Успешный `thread/resume` подтверждает контекст thread, но сам по себе не означает завершение старого execution.


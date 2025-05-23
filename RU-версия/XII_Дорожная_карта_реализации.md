## XII. Дорожная карта реализации

| Этап             | Срок     | Цель                                             | Готовность / Done                                  | Зависит от      |
|------------------|----------|--------------------------------------------------|----------------------------------------------------|------------------|
| Проектирование   | 3 дня    | Архитектура, документация, карта сигналов       | Архитектура ARU-AGI, файл `bootstrap`, `.md` ТЗ    | —                |
| MVP ядра         | 7 дней   | SignalEngine, QMemory, FanthomEngine             | CLI-агент запускается, мысли → память → отклик     | Проектирование   |
| WebCLI           | 2 дня    | Веб-интерфейс через Fiber (React, Tailwind)      | Ввод текста = сигнал, отклик из ядра               | MVP ядра         |
| Telegram-бот     | 1 день   | Локальный агент через Telegram                   | Ответы ARA в чате, запуск фантомов                 | MVP ядра         |
| LLM-интеграция   | 5 дней   | Модуль подключения GPT по API-ключу              | Возможен fallback или прямой вызов GPT в цепочке   | MVP ядра         |
| ExpansionEngine  | 5 дней   | Обобщение, предложения, пассивное мышление       | ARA формирует идеи без команды                     | LLM, Memory      |
| HumanNodes       | 5 дней   | Интерфейс оценки, ревью мыслей                   | Метрика качества, UX для оценщиков                 | ExpansionEngine  |
| EnterpriseSync   | 5 дней   | HeadAgent, p2p-координация целей                 | Обмен QBits, фантомов, миссий                      | MVP ядра         |
| Финализация      | 7 дней   | UI, GitHub Pages, документация, демо             | Сайт проекта, публичная сборка MVP                 | Всё выше         |

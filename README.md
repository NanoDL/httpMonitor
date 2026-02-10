

# Centralized Metrics Server for Windows (C# / .NET 8)

**Цель проекта:** Разработка серверного приложения для централизованного сбора системных метрик с удалённых Windows-хостов с использованием агента Prometheus Windows Exporter.

**Архитектура (PULL-модель):** Сервер периодически опрашивает (HTTP GET) конечные точки (`/metrics`) агентов, парсит данные в формате Prometheus TextFormat, хранит их и предоставляет REST API для доступа.

**Декомпозиция на модули (соответствие курсу):**
1.  **Configuration** – Загрузка `appsettings.json` (Работа с ФС, конфигурация).
2.  **Scheduler** – `BackgroundService` для периодического опроса (Управление потоками, тайминги).
3.  **Fetcher** – `HttpClient` с таймаутами и Polly (Сеть, ввод-вывод, устойчивость).
4.  **Parser** – Парсинг Prometheus TextFormat (Обработка данных).
5.  **Storage** – `ConcurrentDictionary` для метрик (Управление памятью, конкурентность).
6.  **API** – Контроллеры ASP.NET Core (Сетевой сервис, REST).
7.  **Monitoring** – Serilog, health checks (Наблюдаемость, диагностика).

**Технологический стек:** C#, .NET 8, ASP.NET Core, Polly, Serilog, xUnit, Docker.

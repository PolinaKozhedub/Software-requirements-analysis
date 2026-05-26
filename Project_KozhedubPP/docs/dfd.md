# Диаграмма потоков данных (Уровень 1)

```mermaid
flowchart TB
    %% Внешние сущности
    Dispatcher[Диспетчер цеха]
    HR[Сотрудник ОК]
    Lab[Лаборант]
    Director[Руководитель]

    %% Накопители данных (Хранилища)
    DB_Staff[(База кадров: сотрудники, бригады, ИТР)]
    DB_Products[(База изделий: номенклатура, маршруты)]
    DB_Tests[(База испытаний: протоколы, стенды)]

    %% Процессы
    P1((1. Учет кадров и структур))
    P2((2. Регистрация изделий))
    P3((3. Учет движения по участкам))
    P4((4. Фиксация испытаний))
    P5((5. Сводная аналитика))

    %% Потоки процесса 1: Кадры
    HR --> P1
    P1 --> DB_Staff
    DB_Staff --> P1

    %% Потоки процесса 2: Регистрация изделий
    Dispatcher --> P2
    P2 --> DB_Products

    %% Потоки процесса 3: Движение по участкам
    Dispatcher --> P3
    DB_Staff --> P3
    P3 --> DB_Products
    DB_Products --> P3

    %% Потоки процесса 4: Испытания
    Lab --> P4
    DB_Products --> P4
    P4 --> DB_Tests

    %% Потоки процесса 5: Аналитика и отчеты
    Director --> P5
    DB_Staff --> P5
    DB_Products --> P5
    DB_Tests --> P5
    P5 --> Director

    %% Стилизация под пример
    style P1 fill:#f0f4f8,stroke:#2b6cb0,stroke-width:1.5px;
    style P2 fill:#f0f4f8,stroke:#2b6cb0,stroke-width:1.5px;
    style P3 fill:#f0f4f8,stroke:#2b6cb0,stroke-width:1.5px;
    style P4 fill:#f0f4f8,stroke:#2b6cb0,stroke-width:1.5px;
    style P5 fill:#f0f4f8,stroke:#2b6cb0,stroke-width:1.5px;
    style DB_Staff fill:#edf2f7,stroke:#4a5568,stroke-width:2px;
    style DB_Products fill:#edf2f7,stroke:#4a5568,stroke-width:2px;
    style DB_Tests fill:#edf2f7,stroke:#4a5568,stroke-width:2px;

**ДЗ-4 по предмету Базы данных**

**ФИО:** Асриян Александр Арамович, группа М05-307a

**Версия:** СУБД Jatoba v4.5.1-1000

- 1. **История развития Jatoba**

Jatoba СУБД - это отечественная СУБД разработанная на базе PostreSQL крупным в РФ интегратором и разработчиком ПО – ООО Газинформсервис, и впервые было представлено в 2020 году. Основной целью Jatoba СУБД являлось импортозамещение аналогичного ПО от Oracle (Oracle Database), и в то же время удовлетворение нужд enterprise-клиентов Газинформсервис (open-source версия PostrgreSQL для этого не годится по ряду причин). СУБД Jatoba фактически является версией PostgreSQL, которую дорабатывает компания, и идет параллельно с open-source версией, опционально развивая/изменяя свой вариант (исходя из нужд), соответственно open-source версии. Последней версией СУБД является «СУБД Jatoba v4.5.1-1000», и использует ядро PostrgreSQL 15. ПО получило аккредитацию ФСТЭК России по 4 уровню доверия в 2023 году. Начиная с 2020 года (с момента релиза), СУБД Jatoba активно интегрируется с отечественным ПО и программно-аппаратными комплексами (серверы и тд.). Последний процесс стал набирать обороты в 2023 году, в связи с актуализацией проблемы импортозамещения (более 14-и интеграций, с платформами типа 1С:Предприятие и тд). Развитие платформы продолжается, тренд импортозамещения в РФ набирает обороты.

- 1. **Инструменты для взаимодействия с Jatoba**

СУБД Jatoba адаптирована для использования с различными российскими программными продуктами и операционными системами, что делает её подходящей для импортозамещения иностранных СУБД, таких как Oracle или Microsoft SQL Server.

Для взаимодействия с СУБД Jatoba можно использовать стандартные инструменты PostgreSQL, поскольку она совместима с этой платформой (типа GUI pgAdmin, psql, Postico и тд). У СУБД также есть свой проприетарный графический интерфейс для работы с СУБД, который позволяет управлять функциями и оптимизацией СУБД Jatoba без командной строки. Также возможно взаимодействие через различные отечественные платформы и системы, с которыми интегрирована СУБД Jatoba, например, через ОС "РОСА КОБАЛЬТ" и работа с "1С:Предприятие".

Помимо стандартного программного обеспечения для взаимодействия, СУБД Jatoba поддерживает множество отечественных разработок, предоставляя полную техническую поддержку и консультации по вопросам миграции данных и бизнес-логики из других систем (как уже отмечалось, очень это продвигается очень активно в последние годы в связи с импортозамещением). Это делает Jatoba удобной и адаптированной под нужды российских пользователей и организаций.

- 1. **Какой database engine используется в Jatoba?**

СУБД Jatoba основана на PostgreSQL, который в свою очередь использует database engine, также называемый PostgreSQL. Этот движок является объектно-реляционной системой управления базами данных (СУБД), отличающейся своей надёжностью, расширяемостью и соответствием стандартам SQL. PostgreSQL database engine поддерживает широкий спектр функций, включая сложные запросы, внешние ключи, триггеры, представления и хранимые процедуры, что делает его адаптивным для различных вычислительных сред и сложных задач управления данными.

- 1. **Как устроен язык запросов в Jatoba? Разверните БД с данными и выполните ряд запросов.**

Поскольку СУБД Jatoba базируется на PostgreSQL, язык запросов, который она использует, также является SQL. Это стандартный язык для управления данными в базах данных. В PostgreSQL SQL используется для выполнения множества задач, таких как (приведем для справки):

**SELECT**: Используется для извлечения данных из базы данных.

**INSERT**: Добавляет новые данные в таблицу базы данных.

**UPDATE**: Изменяет существующие данные в таблице.

**DELETE**: Удаляет данные из таблицы.

**CREATE DATABASE/TABLE**: Создает новые базы данных и таблицы.

**ALTER TABLE**: Изменяет структуру существующей таблицы.

**DROP TABLE/DATABASE**: Удаляет таблицы и базы данных.

Кроме того, PostgreSQL поддерживает продвинутые возможности SQL, такие как:

**Joins**: Соединение данных из нескольких таблиц.

**Subqueries**: Запросы, вложенные в другой запрос.

**Window Functions**: Выполнение вычислений по наборам строк, связанных с текущей строкой запроса.

**CTEs, Common Table Expressions**: Временный набор результатов, который можно использовать в другом SQL-запросе, включая \`SELECT\`, \`INSERT\`, \`UPDATE\` или \`DELETE\`.

**Хранимые процедуры и функции**: Использование PL/pgSQL или других языков для написания сложных процедур, которые можно использовать повторно.

Произведем несколько простых запросов:

postgres=# create table dummy_table(name varchar(20),address text,age int);

CREATE TABLE

\-- создание таблицы с помощью CREATE

postgres=# insert into dummy_table values('XYZ','location-A',25);

INSERT 0 1

postgres=# insert into dummy_table values('ABC','location-B',35);

INSERT 0 1

postgres=# insert into dummy_table values('DEF','location-C',40);

INSERT 0 1

postgres=# insert into dummy_table values('PQR','location-D',54);

INSERT 0 1

\-- вставка информации в таблицу через команду INSERT

postgres=# select \* from dummy_table;

name | address | age

\---------+--------------+ -----

XYZ | location-A | 25

ABC | location-B | 35

DEF | location-C | 40

PQR | location-D | 54

(4 rows)

\-- команда SELECT

postgres=# update dummy_table set age=50 where name='PQR';

UPDATE 1

postgres=# select \* from dummy_table;

name | address | age

\--------+--------------+-------

XYZ | location-A | 25

ABC | location-B | 35

DEF | location-C | 40

PQR | location-D | 50

(4 rows)

\-- команда UPDATE, меняем значение возраста и имени

- 1. **Распределение файлов БД по разным носителям?**

Для Jatoba, так же как и в PostgreSQL, распределение файлов по разным носителям (или дисковым устройствам) может быть реализовано с использованием различных методов и инструментов. Ниже приведены некоторые из них:

**Tablespaces (Таблицы пространств**): PostgreSQL поддерживает концепцию таблиц пространств, которые позволяют администраторам баз данных определять различные местоположения на диске для хранения различных объектов базы данных, таких как таблиц, индексы и т. д. Путем создания таблиц пространств и ассоциирования с ними конкретных объектов данных можно распределить их по разным носителям.

**RAID (Массив из независимых дисков)**: PostgreSQL может быть настроен для использования RAID-массивов, что позволяет объединить несколько физических дисков в единый логический том с целью повышения производительности и отказоустойчивости. Различные уровни RAID предлагают разные способы организации данных по дискам.

**Файловые системы с поддержкой разделения данных (Data Partitioning)**: Некоторые файловые системы предоставляют функциональность разделения данных, позволяя размещать части файлов на разных физических дисках. Это может быть использовано для распределения данных PostgreSQL по разным носителям.

**Репликация и шардинг (Replication and Sharding)**: В случае больших баз данных можно использовать репликацию для создания копий данных на разных серверах, а также шардинг для распределения данных между разными узлами системы.

Выбор конкретного метода зависит от требований к производительности, отказоустойчивости и доступности данных, а также от инфраструктуры и возможностей, доступных для администрирования базы данных PostgreSQL.

- 1. **На каком языке/ах программирования написана СУБД?**

Jatoba СУБД – это версия PostgreSQL, которая была написана на языке программирования C. Это фундамент, на котором построена сама система управления базами данных PostgreSQL, и он используется для разработки многих внутренних компонентов системы, включая серверную часть и основной интерфейс API (libpq) для взаимодействия с клиентскими приложениями​.

- 1. **Какие типы индексов поддерживаются в БД? Приведите пример создания индексов.**

В PostgreSQL (i.e. Jatoba) поддерживаются несколько типов индексов:

**B-tree** – подходит для большинства ситуаций, особенно для индексации порядка и точных совпадений.

**Hash** – оптимизирован для поиска точных совпадений.

**GiST (Generalized Search Tree)** – для индексации комплексных структур данных, таких как геометрические фигуры или текст для полнотекстового поиска.

**GIN (Generalized Inverted Index)** – используется для индексирования элементов, которые содержат множество значений в одном ключе индекса, например, массивы.

**BRIN (Block Range Indexes)** – подходит для больших таблиц с упорядоченными данными.

**SP-GiST (Space-Partitioned Generalized Search Tree)** – для индексирования данных, которые могут быть разделены на неперекрывающиеся регионы, например квадродеревья.

Пример создания индекса **B-tree**:

CREATE INDEX idx_name ON table_name (column_name);

\-- создание индекса B-tree для column_name в table_name.

- 1. **Как строится процесс выполнения запросов в вашей СУБД?**

Процесс выполнения запросов в Jatoba, аналогично PostgreSQL, в общих чертах выглядит следующим образом:

- **Парсинг**: Разбор и анализ SQL-запроса для проверки синтаксиса и преобразования во внутреннее представление.
- **Планирование**: Определение наиболее эффективного пути выполнения запроса (план запроса), включая выбор индексов и способов соединения таблиц.
- **Оптимизация**: Выбор оптимального плана из возможных вариантов, на основе статистики и стоимости операций.
- **Выполнение**: Реализация плана запроса с доступом к данным и их обработкой.
- **Возврат результатов**: Отправка обработанных данных обратно клиенту.

PostgreSQL использует сложные алгоритмы для оптимизации и может автоматически адаптироваться к различным рабочим нагрузкам, благодаря чему обеспечивает высокую производительность.

- 1. **Есть ли для Jatoba понятие «план запросов»? Если да, объясните, как работает данный этап.**

Да, в Jatoba, аналогично PostgreSQL есть понятие «план запросов». Этот этап называется планированием (или оптимизацией) запросов и является ключевым в процессе выполнения запроса. План запроса определяет, как база данных будет выполнять запрос, выбирая наиболее эффективный способ обращения к данным. PostgreSQL использует статистику о таблицах и индексах для создания нескольких потенциальных планов выполнения запроса, из которых затем выбирается оптимальный. Этот процесс включает оценку стоимости различных операций, таких как доступ к дискам, использование индексов и объединение таблиц.

- 1. **Поддерживаются ли транзакции в вашей СУБД? Если да, то расскажите о нем. Если нет, то существует ли альтернатива?**

Да, Jatoba (да, да - как PostgreSQL) поддерживает транзакции. Транзакции в Jatoba обеспечивают принципы ACID (атомарность, согласованность, изолированность, долговечность), что является фундаментальным для надежной работы с данными. В рамках транзакции можно выполнять множество операций, и все они либо полностью выполнятся, либо не будут выполнены вообще. Это позволяет обеспечить целостность данных даже в случае возникновения ошибок или сбоев системы. Jatoba также поддерживает различные уровни изоляции транзакций, что позволяет настраивать баланс между строгой изоляцией и производительностью.

- 1. **Какие методы восстановления поддерживаются в Jatoba. Расскажите о них.**

В Jatoba, как и в PostgreSQL существует несколько методов восстановления данных:

- **Point-In-Time Recovery (PITR)**: Этот метод позволяет восстановить состояние базы данных на определённый момент в прошлом. Он основан на использовании журналов транзакций, которые записывают все изменения в базе данных. Это может быть необходимо для отмены ошибочных операций или восстановления после сбоев.
- **Репликация**: В PostgreSQL можно настроить репликацию данных, которая позволяет создавать одну или несколько копий базы данных на отдельных серверах. Эти копии могут использоваться для восстановления данных в случае сбоя основного сервера.
- **Физическое восстановление**: С помощью таких инструментов, как pg_basebackup, можно создать полную копию (бэкап) всех данных базы данных. Этот бэкап может быть использован для восстановления базы данных в первоначальное состояние.
- **Логическое восстановление**: Включает экспорт данных в формате SQL (SQL dump), который затем может быть импортирован для восстановления базы данных или отдельных таблиц.
- **Непрерывное архивирование (Continuous Archiving)**: PostgreSQL может постоянно архивировать WAL-журналы, что обеспечивает возможность восстановления до любой точки во времени, пока данные архивируются.
    1. **Расскажите про шардинг в вашей конкретной СУБД. Какие типы используются? Принцип работы.**

В PostgreSQL шардинг реализуется через разбиение больших таблиц на меньшие части, которые называются "шардами". Шарды распределяют данные горизонтально по нескольким узлам, составляющим кластер баз данных. Основная идея шардинга заключается в том, чтобы распределить данные таким образом, чтобы запросы к базе данных выполнялись параллельно на всех узлах, что увеличивает производительность и масштабируемость.

Существуют разные стратегии шардинга в PostgreSQL:

**Горизонтальный шардинг (Horizontal Sharding):** При этом подходе данные распределяются по различным шардам на основе значений определенного столбца, называемого ключом шардинга. Например, если у вас есть таблица с данными пользователей, вы можете распределить строки на основе географического признака, так что данные всех пользователей из определенного региона будут находиться на одном шарде.

**Вертикальный шардинг (Vertical Sharding):** Здесь данные разделяются на столбцовом уровне. Разные столбцы (или группы столбцов) хранятся в разных базах данных или таблицах. Этот подход может быть использован, если разные столбцы таблицы используются разными приложениями, которые могут работать эффективнее с меньшим объемом данных.

**Функциональный шардинг (Functional Sharding):** Данные распределяются по шардам на основе функциональности или бизнес-логики, которую они поддерживают. Например, все операции связанные с заказами могут быть в одном шарде, а операции связанные с учетом пользователей — в другом.

- 1. **Возможно ли применить термины Data Mining, Data Warehousing и OLAP в вашей СУБД?**

Да, термины Data Mining, Data Warehousing и OLAP (Online Analytical Processing) могут быть применены в контексте PostgreSQL (i.e. Jatoba в нашем случае), так как PostgreSQL обладает необходимыми характеристиками и возможностями для работы в этих областях:

**Data Warehousing:** PostgreSQL может использоваться как система управления базами данных для хранилища данных (Data Warehouse) благодаря своей масштабируемости, производительности и поддержке сложных запросов. PostgreSQL поддерживает большие объемы данных, расширенные индексы и оптимизированные запросы, что является важным для хранилищ данных.

**OLAP:** PostgreSQL может использоваться для OLAP-систем благодаря своим возможностям по работе с сложными запросами, агрегации данных и поддержке многомерных запросов. Также есть дополнительные инструменты и расширения, такие как PostGIS для геопространственных аналитических запросов, которые расширяют OLAP-возможности PostgreSQL.

**Data Mining:** Хотя PostgreSQL сам по себе не предоставляет специализированных инструментов для Data Mining, его можно интегрировать с внешними инструментами аналитики и обработки данных, такими как R, Python, Apache MADlib. Это позволяет использовать PostgreSQL в качестве основы для систем Data Mining, где база данных служит хранилищем данных для последующего извлечения знаний.

- 1. Какие методы защиты поддерживаются вашей СУБД? Шифрование трафика, модели авторизации и т.п.

В СУБД Jatoba, в т.ч. есть ряд кастомных решений, которые не доступны в PostgreSQL «из коробки»:

**Модуль SecurityProfile**: Улучшенные парольные политики в Jatoba позволяют настраивать требования к паролям в соответствии с предустановленными профилями безопасности, такими как стандарты ФСТЭК, требования CIS и корпоративные требования. Это усиливает защиту аккаунтов и данных.

**Механизм скрытия текстов процедур и функций**: Jatoba защищает код хранимых процедур и функций, делая их текст невидимым для пользователей, что предотвращает несанкционированное изменение кода и повышает безопасность исполняемых процедур.

**Модуль JCS**: Система контроля доступа и шифрования файлов данных на уровне операционной системы, обеспечивает дополнительный уровень безопасности за счёт шифрования файлов данных.

**JDV**: Инструмент для ограничения доступа даже для пользователей с высокими привилегиями (например, Super User), чтобы защитить данные в таблицах от несанкционированного доступа.

**DataSafe**: Инструмент для контроля баз данных на серверной инфраструктуре, включая управление пользователями, ролями и привилегиями.

**Jadog**: Утилита для обеспечения высокой доступности и отказоустойчивости, автоматически переключающая систему на резервный узел в случае сбоя основного сервера и поддерживающая различные технологии резервирования, включая shared disk cluster.

**Japooler**: Средство распределения нагрузки в кластере, обеспечивающее маршрутизацию запросов и балансировку чтения, а также корректную обработку вложенных команд.

- 1. **Какие сообщества развивают данную СУБД? Кто в проекте имеет права на коммит и создание дистрибутива версий? Расскажите об этих людей и/или компаниях.**

Jatoba развивается/разрабатывается только ООО Газинформсервис, это проприетарный софт компании, а точнее слегка кастомизированная private версия PostgreSQL для энтерпрайза (подробнее в пункте **(а)** ). Кампания Газинформсервис (15 млрд руб выручки в 2023 году) это один из крупнейших в России системных интеграторов в области безопасности и разработчиков средств защиты информации. Компания работает с 2004 года, реализует весь комплекс услуг, необходимых для создания систем информационной безопасности и комплексов инженерно-технических средств охраны любого масштаба.

- 1. **Создайте свои собственные данные для демонстрации работы СУБД.**

![Alternate image text](https://i.imgur.com/PBROPlM.png)

jatoba – база данных, в которой находятся сгенерированные данные

![Alternate image text](https://i.imgur.com/rKhLnUW.png)

Производим поиск по jatoba, ищем всех «customer»-ов

![Alternate image text](https://i.imgur.com/DQSHV5V.png)


Этот вывод перечисляет таблицы в схеме "public" базы данных "jatoba" вместе с построенными на них индексами. Каждая строка представляет собой таблицу и связанный с ней индекс. Например, таблица "customer" имеет индекс с названием "idx_customer_email". Аналогично, другие таблицы, такие как "rental", "payment", "film" и "address", также имеют на них построенные индексы.

- 1. **Как продолжить самостоятельное изучение языка запросов с помощью демобазы. Если демобазы нет, то создайте ее.**

Для продолжения самостоятельного изучения языка запросов PostgreSQL с помощью демобазы данных, нужно начать с освоения структуры базы данных и основных запросов SELECT, INSERT, UPDATE и DELETE. Затем можно изучить использование JOIN для объединения данных из разных таблиц, агрегатные функции и группировку данных, подзапросы и управление индексами для оптимизации производительности запросов.

- 1. **Где найти документацию и пройти обучение**

Если речь идет про PostgreSQL – ответ очевиден: <https://www.postgresql.org/docs/> , также есть качественные YT туториалы (пример: <https://www.youtube.com/watch?v=qw--VYLpxG4>). Если речь именно про Jatoba, и с тонкостями работы с ней, то здесь все основывается на взаимодействии с ООО Газинформсервис, [сайт](https://www.gaz-is.ru/produkty/inform-sistemy/subd-jatoba#morenews). Документация и полная версия доступна при условии энтерпрайз использования, и покупки соотв. ПО у компании. Даже demo-версия высылается по индивидуальному запросу (ничего открытого нет).

- 1. **Как быть в курсе происходящего**

Следить за новостями на сайте ([сайт](https://www.gaz-is.ru/produkty/inform-sistemy/subd-jatoba#morenews)). Open-source/ссылок на гитхаб нет, единственное место с агрегированными новостями, кроме офиц сайта, про данную СУБД: [Тadviser](https://www.tadviser.ru/index.php/%D0%9F%D1%80%D0%BE%D0%B4%D1%83%D0%BA%D1%82:%D0%93%D0%B0%D0%B7%D0%B8%D0%BD%D1%84%D0%BE%D1%80%D0%BC%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81:_Jatoba_%D0%A1%D0%A3%D0%91%D0%94)
# Содержание
[1. Понятие БД. Предметная область. Архитектура СУБД](#T1) <br>
[2. Хранение данных: базы данных. Отличия от файловых систем.](#T2) <br>
[3. Классификация баз данных](#T3) <br>
[4. Системный каталог, метаданные. Интегрируемость и разделяемость данных.](#T4) <br>
[5. Интерфейсы СУБД. Основные функции СУБД (по Кодду)](#T5) <br>
[6. Функции СУБД: буферизация данных, журнализация изменений БД](#T6) <br>
[7. Уровни моделей БД. Инфологическое, даталогическое, физическое проектирование](#T7) <br>
[8. Возможности CASE-средств для автоматизированного проектирования БД.](#T8) <br>

<br>
<a name="T1"></a>

# 1. Понятие БД. Предметная область. Архитектура СУБД

**База данных (БД)** - это поименованная совокупность структурированных данных.

**Система управления базами данных (СУБД)** - программные средства и языки, позволяющие работать с базами данных.

Уровни

1. **Внутренний** - данные на физическом носителе. (сторона железа)
2. **Концептуальный** - логическое представление БД.
3. **Внешний** - интерфейс.

<br><a name="T2"></a>

# 2. Хранение данных: базы данных. Отличия от файловых систем.

**Хранилище данных**: совокупность информационно-технологических и программно-технических средств и методов, обеспечивающих единую среду хранения данных, оптимизированных для выполнения аналитических операций. 

>База данных отличается от файловой системы структурированностью, организованностью данных, позволяет удобно работать с большим объемом данных

<br><a name="T3"></a>


# 3. Классификация баз данных

> По типу хранимой информации:
- **Документальные** - различные документы: рефераты, библеографические, плнотекстовые. Часто в критерии поиска в качестве признака включается «дата принятия документа», «кем принят» и другие «выходные данные» документов.
- **Фактографические** - информация некой предметнй области в виде фактов. (например, библиографические данные о сотрудниках, данные о выпуске продукции производителя и т.п.). Результат запроса: данные в виде фактов или сообщение об их отсутствии.
- **Лексиграфические** - словари (классификаторы, многоязычные словари, словари основ слов и т.п.)


> По способу хранения данных:
- **Локальные**
 Данные находятся на одном устройстве (диск компьютера или сетевой диск, сервер). В локальных базах, данных применяется метод **блокировки файлов** - пока данные используются одним пользователем, для другого пользователя они заблокированы.

- **Удалённые**
Одновременный доступ к информации нескольким пользователям. При этом для обеспечения доступа к данным вместо механизма блокировки файлов используется механизм транзакции.

**Транзакция** – это некоторая последовательность действий, которая должна быть обязательно выполнена над данными перед тем, как они будут переданы. В случае обнаружения ошибки во время выполнения любого из действий, вся последовательность действий, составляющая транзакцию, повторяется снова. Таким образом, механизм транзакции обеспечивает защиту от аппаратных сбоев. Он также обеспечивает возможность многопользовательского доступа к данным.

>По структуре:
- Неструктурированные
- Частично структурированные
- Структурированные

>Структурированные по типу модели:
- **Иерархические** - древовидная структура со связями из объектов разных уровней
- **Сетевые** - сеть из данных, объединенных между собою ссылками друг на друга
- **Реляционные** - БД, состоящие из соединенных между собой таблиц, хранящих в себе столбцы определенных типов данных.

<br><a name="T4"></a>


# 4. Системный каталог, метаданные. Интегрируемость и разделяемость данных.

**Системный каталог** - это набор таблиц, в которых содержится информация, необходимая для правильного функционирования СУБД: о поддержиfваемых базах данных и их базовых таблицах, представлениях, курсорах, индексах, пользователях и их правах доступа к информации, правилах модификации данных и т.д. В разных СУБД, поддерживающих SQL, существует от десятка до нескольких десятков системных таблиц, структура которых ничем не отличается от уже знакомой нам структуры пользовательских таблиц.

**Метаданные** - то, из чего состоит системный каталог.

**Интегрируемость данных** - Возможность представить БД как объединение отдельных файлов с данными, полностью или частично исключая избыточность хранения данных.

**Разделяемость данных** - Возможность использования несколькими различными пользователями одних и тех же данных в БД

<br><a name="T5"></a>


# 5. Интерфейсы СУБД. Основные функции СУБД (по Кодду).

>Виды интерфейсов:
- **форма и ее генератор** - структурированное и гибкое отображение необходимых данных

- **командный интерфейс** - больше возможностей, но необходимы знания ЯМД

>Требования к реляционным СУБД (по Кодду)

> На уровне языка

5. **Полнота подмножества языка (Comprehensive Data Sublanguage Rule)**. Система управления реляционными базами данных должна поддерживать единственный язык запросов, который позволяет выполнять все операции работы к данным:
операции определения данных, операции манипулирования данными, управление доступом к данным, управление транзакциями.

12. **Согласование языковых уровней (Non-Subversion Rule)**. Не должно быть иного средства доступа к данным, отличного от стандартного языка работы с данными. Если используется низкоуровневый язык доступа к данным, он не должен игнорировать правила безопасности и целостности, которые поддерживаются языком более высокого уровня.

10. **Независимость контроля целостности (Integrity Independence)**. Вся информация, необходимая для поддержания целостности, должна находиться в словаре данных. СУБД должна выполнять проверку заданных ограничений целостности и автоматически поддерживать целостность данных.

4. **Доступ к словарю данных в терминах реляционной модели (Dynamic On-Line Catalog Based on the Relational Model)**. Словарь данных должен сохраняться в форме реляционных таблиц, и СУБД должна поддерживать доступ к нему при помощи стандартных языковых средств.

>На уровне бд

6. **Поддержка обновляемых представлений (View Updating Rule)**. Обновляемое представление должно поддерживать все операции манипулирования данными, которые поддерживают реляционные таблицы: операции выборки, вставки, модификации и удаления данных.

7. **Наличие высокоуровневых операций управления данными (High-Level Insert, Update, and Delete)**. Операции вставки, модификации и удаления данных должны поддерживаться не только по отношению к одной строке реляционной таблицы, но по отношению к любому множеству строк.

11. **Независимость от распределенности (Distribution Independence)**. База данных может быть распределенной, может находиться на нескольких компьютерах, и это не должно оказывать влияние на приложения.

> На уровне ячеек таблицы

1. **Явное представление данных (The Information Rule)**. Информация должна быть представлена в виде данных, хранящихся в ячейках. Данные, хранящиеся в ячейках, должны быть атомарны. Порядок строк в реляционной таблице не должен влиять на смысл данных.

2. **Гарантированный доступ к данным (Guaranteed Access Rule)**. К каждому элементу данных должен быть гарантирован доступ с помощью комбинации имени таблицы, первичного ключа строки и имени столбца.

3. **Полная обработка неизвестных значений (Systematic Treatment of Null Values)**. Неизвестные значения (NULL), отличные от любого известного значения, должны поддерживаться для всех типов данных при выполнении любых операций.

>На уровне приложений

9. **Логическая независимость данных (Logical Data Independence)**. Представление данных в приложении не должно зависеть от структуры реляционных таблиц.

8. **Физическая независимость данных (Physical Data Independence)**. Приложения не должны зависеть от используемых способов хранения данных на носителях, от аппаратного обеспечения компьютеров, на которых находится реляционная база данных.

<br>

# 6. Функции СУБД: буферизация данных, журнализация изменений БД.

**Журнализация** - запись сеанса взаимодействия пользователя с бд для возможности дальнейшего восстановления в случае сбоя системы

**Буферизация** служит для ускорения работы системы с БД и заключается в записи данных из журнала не сразу на диск, а предварительно в оперативную память.

**Протокол WAL - Write Ahead Log** - записи в журнале об изменении объекта некой бд выталкиваются во внешнюю память раньше самих изменений

<br>

# 7. Уровни моделей БД. Инфологическое, даталогическое, физическое проектирование.

> Уровни моделей БД
- **Физический** - все данные БД, которые содержатся в таблицах/файлах/на внешних носителях

- **Концептуальный** - предмет устройства, архитектуры, соединений БД.

- **Внешний** - отдельные единицы данных, необходимые для конкретного пользователя/приложения. (Остальные ненужные данные игнорируются)

**Логическая независимость** – Независимость друг от друга приложений, взаимодействующих с одной и той же БД (это возможность изменения одного приложения без корректировки других приложений, работающих с этой же БД. )

**Физическая независимость** – это возможность переноса хранимой информации с одних носителей на другие при сохранении работоспособности всех приложений.

**Инфологическое концептуальное проектирование** - построение обобщенной, не имеющей конкретики, модели базы данных с описанием ее объектов и связей между ними;

**Даталогическое логическое проектирование** - создание схемы базы данных с учетом специфики конкретной модели данных; (связи между таблицами)

**Физическое проектирование** - построение схемы базы данных под конкретную СУБД. При таком проектировании учитываются ограничения на именование объектов базы данных, ограничения на определенные типы данных, физические условия хранения данных в БД (разделение по файлам и устройствам), возможность доступа к БД.

<br>

# 8. Возможности CASE-средств для автоматизированного проектирования БД.

CASE-средства позволяют существенно сократить время на разработку БД и уменьшить количество ошибок в них.

>Виды Case-средств

**S-Designor(SDP)** - графический case-инструмент, позволяет проектировать как концептуальную, так и физическую модель БД, имея возможность перехода от одного этапа к другому.

**Database Designer(ORACLE)** - инструмент, позволяет после анализирования предметной области программировать и проектировать БД, проводить настройку, оценку и тестирование.

**Erwin(Logic Works)** - инструмент для создания концептуальных и логических схем данных, позволяет редактировать различные наборы данных в виде таблиц, разрабатывать структуры, скрипты, настраивать шаблоны, выводить информацию в виде отчетов, строить диаграммы

<br>

# 9. Проектирование предметной области. Моделирование с помощью нотаций.

Предметная область характеризуетя объектами и процессами.

При проектировании, предметная область рассматривается в виде трех представлений:

1. Предметная область без изменений, такая, какая она есть
2. Предметная область как ее вопринимает проектировщик БД
3. Предметная область описанная в виде символов

Этапы:

1. **Построение концептуальной модели** (сущность - связь) - анализ и изучение предметной области, сбор данных для пострения модели; выявление фрагментов, построение связей между ними; создание концпетуальной модели.

2. **Логическое проектирование** - построение моделей со структурами, ориентированными на СУБД и спецификации прикладных программ и их сравнительный анализ.

3. **Физическое проектирование** - определение особенностей хранения данных, методов доступа и т.д.

Моделирование в нотации eEPC представляет собой описание описание последовательности шагов бизнес-процесса, выполняемых сотрудниками(отделами, департаментами), которые позволяют осуществить связь между организационной и функциональными моделями.

<br>

# 10. Семантика БД: обратимость утверждений, генерализация и специализация объектов. Примеры. 

Модель ER обладает способностью представлять сущности БД в виде иерархической модели. Выше по иерархии располагаются более обобщенные представления о сущностях, тогда как ниже по иерархии сущности рассмотриваются более детально.

Подъем по иерархии (сущности объединяются, более обобщенное представление) - **генерализация**, спуск - **специализация**

Пример: 
- генерализация: Иванов Иван -> ученик 8А -> школьник -> человек
- специализация: человек -> школьник -> ученик 8А -> Иванов Иван

<br>

# 11. Семантика БД: агрегирование и группировка объектов. Примеры.

**Агрегирование** - объединение нескольких элементов в единое целое (MIN, MAX, AVG)
```SQL
SELECT MAX(price) FROM book;
```

**Группировка данных** - это процедура объединения в логическом порядке строк с. определенными значениями. 

```SQL
SELECT age, SUM(salary) FROM people
GROUP BY age;
```

<br>

# 12. ER – модель. Сущности, связи, атрибуты, домены. Пример.

**Entity-relational** - концептуальная модель высокого уровня, представляет собой модель из сущностей и отношений между ними

**Сущность** - объект, событие или явление, то, что хранит данные в БД, имеет атрибуты, представляющие эту сущность. **Пример**: человек - работник, студент, пациент.

**Отношения** - объединение двух или более сущностей: Том работает в химическом отделе

**Атрибут** - свойство сущности или типа связи. **Пример**: лекция может иметь атрибуты время, дата, продолжительность, место...

Виды
- простой атрибут - не могут быть разделены дальше: номер студента

- композитный - можно разбить на составные атрибуты: полное имя можно разбить на имя и фамилию

- производный: не хранится в БД напрямую, получается из других атрибутов, хранящихся в БД: возраст человека вычисляется по дате его рождения

- многозначный - несколько значений: несколько номеров телефонов, несколько электронных почт

**Домен** - множество допустимых значений для определенного типа. Пример: имя состоит из русских букв, не содержит цифры, длиной от 5 до 20 символов.

<br>

# 13. Кардинальность и степень связи. Унарная, бинарная, n – арная связь.

**Кардинальность** – количество возможных связей для каждой из сущностей-участниц (One-To-One, One-To-Many, Many-To-Many). Количество связей для сущности

**Степень связи** – количество типов отношений, которые охвачены данной связью

Для связи «один к одному» кардинальности будут равны  1 и 1, для связей «один ко многим» - 1 и N (часто вместо N используется знак ∞ - «бесконечность» или просто символ «звездочка» ′*′), для связи «многие к одному » - N и 1, для связи «многие ко многим» - N и N. 

-унарная связь – связь, которая определена на одной сущности. Самый простой пример – иерархическая структура.
−  бинарные связи (между двумя отношениями или между отношением и ем же самим - рекурсивная связь),
−  и в общем случае - n-арные связи.


<br>

# 14. Сущность: степень участия. Супертип и подтип. Примеры.

**Степень участия** – определяет, зависит ли существование некой сущности от участия в связи некой другой сущности.

Пример. Сущность Автомобиль можно разбить на следующие подтипы: автомобили с приводом на два колеса, автомобили с приводом на четыре колеса, автомобили с переключаемым приводом.

<br>

# 15. Иерархическая модель данных. Структурное представление данных, навигация. 

В иерархии главный элемент - корень, древовидная структура с потомками.

**Структура данных** — это коллекция, который хранит данные в определенном макете.

**Линейные**, элементы образуют последовательность или линейный список, обход узлов линеен. Примеры: Массивы. Связанный список, стеки и очереди.

**Нелинейные**, если обход узлов нелинейный, а данные не последовательны. Пример: граф и деревья.

<br>

# 16. Обработка данных в иерархической БД. Поддержка целостности данных. 

Проход ИБД слева-направо сверху-вниз. .Все  операции по изменению данных (выборка, удаление, обновление и т.п.) осуществляются по одной записи единовременно.

Поиск в ИБД осуществляется либо с помощью указателей, которые отслеживают, какая запись обрабатывалась последней, либо извлечением/вставкой записи, удовлетворяющей заданным условиям.

**Поддержка ограничений целостности**: 
- дочерняя запись не может существовать независимо от родителя (т.е. обеспечивается целостность связи между владельцем и участниками группового отношения); 
- если родительская запись удаляется, то все подчиненные (дочерние) автоматически будут удалены; 
- при внесении в родительскую запись каких-либо изменений они будут унаследованы всеми дочерними записями. Каскадные удаления или обновления могут приводить к потере данных.

<br>

# 17. Сетевая модель данных. Типы записей. Правила манипулирования данными. 

Сетевые - сеть из данных, объединенных между собою ссылками друг на друга

Плюсы: минимум избыточности данных, потомки могут иметь любое число предков

Минусы: сложности в навигации

Типы записей: предки и потомки (1 к многим)

**Операции с данными**: удалить/сохранить/обновить запись, переключить связь на другого владельца, ликвидировать связь, извлечь запись по критериям.

# 18. Достоинства и недостатки ранних моделей БД (ИБД и СБД).
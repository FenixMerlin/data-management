# Data Management

Мои решения задач из раздела [SQL на HackerRank](https://www.hackerrank.com/domains/sql), разложенные по неделям курса. Все запросы написаны на диалекте MySQL.

В каждом файле сначала идёт запрос (блок `Code`), а за ним результат, который вернул HackerRank (блок `OUTPUT` или `Result`).

## Неделя 1: основы SELECT

| Задача | Что нужно сделать | Приёмы |
| --- | --- | --- |
| [Select All](src/week%201/Select%20all) | Вывести все строки и столбцы таблицы `CITY` | `SELECT *` |
| [Select By ID](src/week%201/Select%20by%20ID) | Найти город с `ID = 1661` | `WHERE` |
| [Japanese Cities' Attributes](src/week%201/Attributes%20of%20Japanese%20cities) | Вывести все поля японских городов | `WHERE` по строке |
| [Japanese Cities' Names](src/week%201/The%20names%20of%20Japanese%20cities) | Вывести только названия японских городов | `WHERE` по строке |
| [Weather Observation Station 1](src/week%201/Weather%20observation%20station%201) | Вывести город и штат каждой станции | выбор столбцов |
| [Weather Observation Station 3](src/week%201/Weather%20observation%20station%203) | Города с чётным `ID` без повторов | `DISTINCT`, `%` |
| [Weather Observation Station 5](src/week%201/Weather%20Observation%20Station%205) | Самое короткое и самое длинное название города | `LENGTH`, `ORDER BY`, `LIMIT`, `UNION ALL` |
| [Weather Observation Station 7](src/week%201/Weather%20Observation%20Station%207) | Города, название которых оканчивается на гласную | `REGEXP` |
| [Higher Than 75 Marks](src/week%201/More%20than%2075%20Points) | Студенты с баллом выше 75, отсортированные по трём последним буквам имени | `RIGHT`, сортировка по нескольким ключам |
| [Employee Names](src/week%201/employee%20names) | Имена сотрудников в алфавитном порядке | `ORDER BY` |

## Неделя 2: шаблоны, агрегаты и соединения

| Задача | Сложность | Что нужно сделать | Приёмы |
| --- | --- | --- | --- |
| [Weather Observation Station 8](src/week%202/Weather%20observation%20station%208%20%28Easy%29) | Easy | Города, которые начинаются и заканчиваются на гласную | `REGEXP` с якорями `^` и `$` |
| [Weather Observation Station 9](src/week%202/Weather%20observation%20station%209%20%28Easy%29) | Easy | Города, которые не начинаются на гласную | `NOT REGEXP` |
| [Weather Observation Station 18](src/week%202/Weather%20observation%20station%2018%20%28Normal%29) | Medium | Манхэттенское расстояние между крайними точками координат | `MIN`, `MAX`, `ROUND` |
| [Interviews](src/week%202/Interviews%20%28Hard%29) | Hard | Сводная статистика отправок и просмотров по каждому конкурсу | `JOIN`, `LEFT JOIN` на подзапросы, `GROUP BY`, `HAVING`, `COALESCE` |

### Разбор задачи Interviews

Это самая сложная задача в репозитории. Если сразу соединить `Submission_Stats` и `View_Stats` с таблицей заданий, строки размножатся, и суммы окажутся завышены. Поэтому каждая таблица статистики сначала агрегируется в подзапросе по `challenge_id`, и только потом к ней делается `LEFT JOIN`. `COALESCE` превращает отсутствующие значения в нули, а `HAVING` отбрасывает конкурсы, у которых все четыре суммы нулевые.

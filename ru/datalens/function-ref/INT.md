---
editable: false
sourcePath: ru/_api-ref/datalens/function-ref/INT.md
---

# INT



#### Синтаксис {#syntax}


```
INT( expression )
```

#### Описание {#description}
Переводит выражение `expression` в формат целого числа по следующим правилам:

| Тип                                   | Значение                                                                                                                                                                                                                                        |
|:--------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Целое число`                         | Исходное значение.                                                                                                                                                                                                                              |
| `Дробное число`                       | Целая часть числа (округление вниз).                                                                                                                                                                                                            |
| <code>Дата &#124; Дата и время</code> | [Unix-время](https://ru.wikipedia.org/wiki/Unix-время) соответствующее дате и времени. Если значение содержит в себе информацию о временной зоне, то она учитывается при вычислении. Если же временная зона неизвестна, то время считается UTC. |
| `Строка`                              | Число из строки в десятичной записи.                                                                                                                                                                                                            |
| `Логический`                          | `TRUE` — `1`, `FALSE` — `0`.                                                                                                                                                                                                                    |

**Типы аргументов:**
- `expression` — `Логический | Дата | Дата и время | Дробное число | Целое число | Строка`


**Возвращаемый тип**: `Целое число`

#### Примеры {#examples}

```
INT(7.7) = 7
```

```
INT("365") = 365
```

```
INT(TRUE) = 1
```


#### Поддержка источников данных {#data-source-support}

`ClickHouse 21.8`, `Файлы`, `Google Sheets`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.7`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`, `Яндекс Документы`, `YDB`.

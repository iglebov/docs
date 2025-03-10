# Не удается удалить кластер {{ mpg-name }} в состоянии `DEAD`, если на нем включена защита от удаления


## Описание проблемы {#issue-description} 

* Не удается удалить кластер, находящийся в состоянии `DEAD`, поскольку на нем включена защита от удаления;
* Кластер {{ mpg-name }} перешел в состояние `UNKNOWN` сразу же после создания, и его не получается удалить из [Консоли управления]({{ link-console-main }}).

## Решение {#issue-resolution}

Если кластер находится в состоянии `DEAD` или `UNKNOWN`, вы можете снять защиту от удаления средствами YC CLI командой:
```
yc managed-postgresql cluster update --deletion-protection=false <CLUSTER_ID>
```

По завершении этой операции вы можете запустить удаление этого кластера:
```
yc managed-postgresql cluster delete <CLUSTER_ID>
```

## Если проблема осталась {#if-issue-still-persists}

Если вышеописанные действия не помогли решить проблему, [создайте запрос в техническую поддержку]({{ link-console-support }}). При создании запроса укажите идентификатор проблемного кластера и кратко опишите проблему.

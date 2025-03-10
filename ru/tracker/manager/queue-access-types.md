# Права доступа в очереди

{% note warning %}

При настройке прав доступа в очереди будьте осторожны, чтобы случайно не заблокировать доступ для себя. Это может произойти, например, если настроить запрещающий доступ для группы, в которой состоите, или удалить настройки доступа, которые позволяли управлять доступом. Если все же случилось что-то из перечисленного, обратитесь к [администраторам организации](queue-access.md#implicit-access).

{% endnote %}

Ограничить доступ можно в настройках очереди. Чтобы открыть настройки:

1. На панели слева нажмите **Очереди** и выберите из списка нужную очередь.

1. Нажмите **{{ ui-key.startrek.ui_Queues_pages_PageQueue_header.settings }}** → **{{ ui-key.startrek.ui_Queues_pages_page-queue-admin_QueueAdminPageContent.menu-item-permissions }}**. Если вы не видите кнопку **{{ ui-key.startrek.ui_Queues_pages_PageQueue_header.settings }}**, значит у вас нет прав для настройки очереди. Если права вам необходимы, обратитесь к владельцу очереди.

Доступы в очереди настраиваются с помощью следующих прав:

* `Настройки очереди` — просмотр и редактирование настроек очереди. Право не включает в себя права доступа к задачам очереди и, соответственно, не пересекается с остальными правами.
* `Редактирование задач` — просмотр всех задач в очереди, возможность оставлять комментарии, редактировать описание и любые поля задачи.
* `Создание задач` — создание задач в очереди. При создании задачи пользователь получает роль автора в этой задаче и, соответственно, права на просмотр и редактирование созданной задачи.
* `Просмотр задач` — просмотр задач очереди и возможность оставлять в них комментарии.

Набор прав меняется в зависимости от [инструмента настройки прав доступа](#set-access).

{% note info %}

Если пользователь был призван в комментарии к задаче, он появляется в поле **Доступ**. После первого оставленного комментария пользователь автоматически появляется в списке **Наблюдателей**.

{% endnote %}

## Как настраивать права доступа к очереди {#set-access}

Доступы в очереди можно ограничивать с помощью 4 инструментов:

* [Основные участники](#main) — используйте для назначения доступов конкретным пользователям, группам пользователей или роботам. Итоговый доступ формируется из всех источников: если у пользователя есть персональные права и права в рамках каждой группы, в которой он присутствует, то итоговый доступ соберется по максимальному доступу.
* [Роли в задачах](#task-role) — действует в дополнение к первому инструменту и позволяет изменять доступы пользователя в зависимости от того, какую роль он получает в конкретной задаче: автор, исполнитель, наблюдатель или добавлен в поле **Доступ**. Это хорошо работает, когда доступа к очереди нет, но при добавлении пользователя в задачу доступ у него появляется.
* [Задачи с компонентом](#access-component) — позволяет полностью переопределить доступ к тем задачам, в которых он проставлен.
* [Запрещающий доступ](#prohibit) — запретить любой доступ к задачам очереди для пользователя или группы пользователей.

Эти инструменты можно комбинировать и сочетать.

{% note info %}

Изменения настроек прав доступа в очереди применяются не мгновенно и синхронизируются в течение часа.

{% endnote %}

### Основные участники очереди {#main}

В разделе **Основные участники** можно выбрать пользователей, которые должны иметь определенные доступы в очереди. Действуют все 4 доступа. Данная функция хорошо работает, когда доступа к очереди нет, но при добавлении пользователя в задачу он появляется.

Чтобы выбрать участников очереди:

1. Нажмите **Добавить** и с помощью поиска найдите пользователя или группу пользователей.

1. Выберите доступы, которые готовы предоставить пользователю и группе пользователей. Если пользователь уже имеет права в рамках группы, в этом же окне вы увидите, в каких группах он состоит.

1. Нажмите **Добавить**.

### Роли в задачах {#task-role}

В разделе **Роли в задачах** можно изменить права участников задачи. Эти права будут выданы в дополнение к тем, что настроены в разделе **Основные участники**. Для участников задачи действуют 2 доступа: `Просмотр задач` и `Редактирование задач`.

Чтобы изменить доступы для роли в задаче:

1. Выберите из списка роль, доступ для которой необходимо скорректировать.

1. Нажмите **Изменить доступ**.

1. В окне редактирования доступа вы можете выбрать подходящий доступ из списка или отменить расширенный доступ для этой роли. В этом случае для участника задачи с этой ролью будут действовать только права из раздела **Основные участники**.

1. Нажмите **Сохранить**.

{% note info %}

При предоставлении доступа с правом `Редактирование задач` необязательно отмечать галочкой право `Просмотр задач`, потому что `Редактирование задач` включает в себя `Просмотр задач`.

{% endnote %}

### Задачи с компонентом {#access-component}

Вы можете настраивать доступ к различным [компонентам](components.md) очереди. Это позволит задавать разные настройки для задач очереди без компонентов и для задач с компонентами.

{% note warning %}

Правила доступа к компоненту имеют приоритет над правилами доступа к очереди, но не переопределяют [запрещающий доступ](#prohibit).
Если права в компоненте не настроены, то в поле Доступ этого компонента отображается `Не влияет на доступ`.

{% endnote %}

Действуют 3 доступа: `Редактирование задач`, `Создание задач`, `Просмотр задач`. Компоненты не позволяют переопределять возможность редактирования настроек очереди.

Чтобы настроить доступ к компоненту:

1. В разделе **Задачи с компонентом** вы увидите список всех компонентов очереди. Если компонентов в очереди еще нет, нажмите **Создать** и [заполните форму создания компонента](components.md#create-component).

1. Нажмите стрелку в строке с компонентом.

1. В открывшемся окне вы можете переопределить доступы:

  * **Закрыть доступ** — выберите из списка пользователя, группу пользователей или роль пользователя в задаче, чтобы запретить им доступ к задачам с этим компонентом;
  * **Основные участники** — сформируйте список пользователей, которые получат выбранный доступ к задачам очереди с компонентом;
  * **Роли в задачах** — переопределите доступы участников задачи.

{% note info %}

Доступ к компоненту заменяет доступы к задаче. Если задача относится к нескольким компонентам, то их права объединятся и доступ к задаче имеют все пользователи, которым разрешен доступ хотя бы к одному компоненту.

{% endnote %}

### Запрещающий доступ {#prohibit}

Чтобы запретить любой доступ к задачам очереди, в разделе **Доступ запрещен** нажмите **Добавить** и с помощью поиска найдите пользователя или группу пользователей. Нажмите **Запретить доступ**.

Запрещающий доступ можно настроить и для владельца очереди.

{% note warning %}

Запрещающий доступ не переопределяется другими типами доступов. То есть если пользователю запрещен доступ к очереди, а для [Ролей в задачах](#task-role) настроено, что наблюдатель может редактировать задачу, то даже если мы сделаем пользователя наблюдателем, он даже посмотреть задачу не сможет. Переопределение работает только для [Основных участников очереди](#main), [Ролей в задачах](#task-role) и [Задачах с компонентом](#access-component).

{% endnote %}



## Массовое редактирование доступов в группах

В группах [Основные участники](#main), [Роли в задачах](#task-role), [Задачи с компонентом](#access-component), [Доступ запрещен](#prohibit) вы можете использовать массовое редактирование. Причем в каждом из блоков они работают по-разному. 

### Основные участники

1. Отметьте один или несколько элементов в группе.
   
1. В появившемся снизу блоке измените или отзовите [доступ](#acces-types).

    * Если вы выбрали пункт **Изменить доступ**, то в открывшемся окне **Доступ к очереди** настройте соответствующие доступы к задачам. 
     
    * Если вы выбрали пункт **Отозвать доступ**, то в открывшемся окне **Отозвать доступ к очереди** убедитесь, что вы сделали правильный выбор. 

2. Нажмите **Сохранить**.

### Роли в задачах

1. Отметьте один или несколько элементов в группе.

1. В появившемся снизу блоке измените доступ.

1. Нажмите **Изменить доступ**. 

1. В открывшемся окне **Доступ к очереди** включите **Расширить доступ** — при получении роли в задаче пользователь получит больше прав. Вы сможете добавить такие права, как **Просмотр задач** и **Редактирование задач**. 

1. Нажмите **Сохранить**.

### Задачи с компонентом

1. Отметьте один или несколько элементов в группе.

1. В появившемся снизу блоке нажмите **Выдать доступ к компонентам**.

1. В открывшемся окне **Добавить участников в компоненты** введите в окне поиска имя, фамилию или почту пользователя, название или идентификатор группы.

1. Нажмите **Добавить**.

### Доступ запрещен

1. Отметьте один или несколько элементов в группе.

1. В появившемся снизу блоке нажмите **Снять ограничения**.

---
title: Примеры использования триггеров в {{ tracker-full-name }}
description: Из статьи вы узнаете, как можно использовать триггеры в {{ tracker-name }}.
---

# Примеры использования триггеров в {{ tracker-name }}

Рассмотрим несколько примеров использования триггеров в {{ tracker-name }}:

- Как [автоматически назначать исполнителя задачи](#assign_ticket) в зависимости от статуса или компонента.

- Как [автоматически призывать исполнителя задачи](#summon_ticket) в зависимости от статуса и значения поля.

- Как [автоматически изменять статус задачи](#new-link), если к ней была добавлена связь определенного типа. 

- Как [автоматически отправлять пользователю уведомление](#notify_mail) после создания задачи из обращения в службу поддержки по почте.

- Как [автоматически отправлять пользователю уведомление](#notify_form) после создания задачи из обращения в службу поддержки через {{ forms-full-name }}.

- Как [автоматически добавлять форму](#insert_form) в комментарии задачи.

- Как [автоматически добавлять задачи на доску](#board).

- Как [настроить уведомления в мессенджеры](#section_vsn_mb2_d3b) через HTTP-запросы.

- Как [автоматически посчитать разницу дат](#tracker_data) в {{ tracker-name }}.


- Как [создать подзадачу и записать в нее значения полей из родительской задачи](#create-ticket-with-params).


## Автоматически назначать исполнителя задачи {#assign_ticket}

Часто за выполнение разных этапов работы отвечают определенные сотрудники. Когда сотрудник выполняет свою часть работы, он передает задачу следующему исполнителю. Если команда ведет работу в {{ tracker-name }}, то каждому этапу работы соответствует статус задачи. Когда задача переходит в определенный статус, с помощью триггера можно автоматически назначать исполнителя, который отвечает за выполнение этого этапа работы.

Другой вариант организации работы — когда выделенные сотрудники отвечают за разные направления. Например, каждый сотрудник службы поддержки работает с обращениями по своему продукту. В этом случае в очереди можно [настроить компоненты](components.md), которые соответствуют продуктам компании. Когда в задачу добавляется определенный компонент, с помощью триггера можно автоматически назначать исполнителя, который отвечает за работу с этим продуктом.

Настроим триггер для автоматического назначения исполнителя задачи:


1. Убедитесь, что у всех сотрудников, которые могут быть назначены исполнителями задач, есть [полный доступ к {{ tracker-name }}](../access.md).


1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера. 

1. Задайте условия, чтобы триггер срабатывал при изменении параметров задачи «Статус» или «Компоненты»:

    1. Выберите опцию **Будут выполнены условия** → **Все**.

    1. Добавьте условие **Событие** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.eventType.update }}**.

    1. Чтобы назначать исполнителя задачи при изменении статуса, добавьте условие **{{ ui-key.startrek-backend.fields.issue.fields.system }}** → **Статус** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldBecameEqual }}** и укажите статус. Доступные статусы зависят от [воркфлоу](workflow.md), который настроен для очереди. 

        ![](../../_assets/tracker/trigger-example-status.png)

        Чтобы назначать исполнителя задачи при изменении компонентов, добавьте условие **{{ ui-key.startrek-backend.fields.issue.fields.system }}** → **Компоненты** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldBecameEqual }}** и укажите компоненты.

        ![](../../_assets/tracker/trigger-example-components.png)

        {% note info %}

        Триггер с таким условием сработает, только если в задаче указан один компонент.

        {% endnote %}

1. Задайте действие триггера: 

    1. Добавьте действие **Изменить значения в полях**.

    1. Выберите поле **{{ ui-key.startrek-backend.fields.issue.fields.system }}** → **{{ ui-key.startrek-backend.fields.issue.assignee-key-value }}** → **Установить значение** и укажите сотрудника, который должен быть назначен исполнителем при срабатывании триггера. 

        ![](../../_assets/tracker/trigger-example-assignee.png)

1. Сохраните триггер. 
   Чтобы проверить работу триггера, измените статус или компоненты у любой задачи из очереди, в которой вы настроили триггер.

## Автоматически призывать исполнителя задачи {#summon_ticket}

Выполнив задачу, сотрудник может забыть указать важную информацию, например, затраченное время. В этом случае можно настроить триггер, который будет автоматически призывать исполнителя, если задача закрыта и не указано затраченное время:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера.

1. Задайте условия, чтобы триггер срабатывал при закрытии задачи в случае, если поле «Затраченное время» не заполнено:

    1. Выберите опцию **Будут выполнены условия** → **Все**.

    1. Добавьте условие **{{ ui-key.startrek-backend.fields.issue.fields.system }}** → **Статус** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldBecameEqual }}** → **{{ ui-key.startrek-backend.applinks.samsara.status.closed }}**. Доступные статусы зависят от [воркфлоу](workflow.md), который настроен для очереди. 

    1. Добавьте условие **{{ ui-key.startrek-backend.fields.issue.fields.timetracking }}** → **{{ ui-key.startrek-backend.fields.issue.spent-key-value }}** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldIsEmpty }}**.

1. Задайте действия триггера:

    1. Добавьте действие **Добавить комментарий**.

    1. Нажмите ![](../../_assets/tracker/summon.png) и в строке **Призвать пользователей из поля** введите «Исполнитель».

    1. Введите текст комментария, который должен увидеть исполнитель, и выберите опцию **Отправлять от имени робота**.

1. Сохраните триггер, нажав кнопку **Создать**.

    ![](../../_assets/tracker/trigger-example-summon.png)

При закрытии любой задачи, где не указано затраченное время, робот будет создавать комментарий и призывать исполнителя.

## Изменять статус задачи после создания связи {#new-link}

Во многих проектах задачи зависят друг от друга, даже когда над ними работают разные люди. Если задача влияет на выполнение одной или нескольких других, важно оповестить коллег о возникших проблемах. Например, связать такие задачи между собой и установить [тип связи](../user/links.md) **{{ ui-key.startrek-backend.fields.issue.links.relationship.is.dependent.by }}**.

Настроим триггер, который будет изменять статус задачи и добавлять комментарий для автора, если появилась связь **{{ ui-key.startrek-backend.fields.issue.links.relationship.is.dependent.by }}**:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера.

1. Задайте условия, чтобы триггер срабатывал при появлении связи **{{ ui-key.startrek-backend.fields.issue.links.relationship.is.dependent.by }}**:

    1. Выберите опцию **Будут выполнены условия** → **Все**.

    1. Добавьте условие **Действие со связью** → **{{ ui-key.startrek-backend.fields.trigger.condition.type.links.created }}** → **{{ ui-key.startrek-backend.fields.issue.links.relationship.is.dependent.by }}**.

    ![](../../_assets/tracker/blocker-conditions.png)

1. Задайте действия триггера:

    1. Добавьте действие **Изменить статус задачи**.

    1. В поле **Новый статус задачи** выберите статус, который будет установлен у задачи после выполнения условия. Например, **{{ ui-key.startrek-backend.applinks.samsara.status.need.info }}**. Доступные статусы зависят от [воркфлоу](workflow.md), который настроен для очереди. 

    1. Добавьте действие **Добавить комментарий**.

    1. Нажмите ![](../../_assets/tracker/summon.png) и в строке **Призвать пользователей из поля** введите «Автор».

    1. Введите текст комментария, который должен увидеть автор задачи, и выберите опцию **Отправлять от имени робота**. Иначе комментарий будет отправлен от имени пользователя, который запустил действие триггера — добавил связь. 

    ![](../../_assets/tracker/blocker-actions.png)

1. Сохраните триггер, нажав кнопку **Создать**.

## Отправлять уведомление о создании задачи из письма {#notify_mail}

Предположим, что сотрудники службы поддержки регистрируют обращения в {{ tracker-name }}. Пользователи пишут в службу поддержки по почте, и на основе их писем создаются задачи в {{ tracker-name }}.

Настроим триггер, который после создания задачи будет оправлять пользователю письмо о том, что его обращение зарегистрировано:

#### Шаг 1. Настроить интеграцию с почтой

Чтобы отправлять письма из {{ tracker-name }} и создавать задачи из входящих писем, настройте интеграцию с почтой:

1. [Настройте почтовый адрес для очереди](queue-mail.md#section_gwv_hqb_hgb), в которой будут создаваться задачи по обращениям пользователей.

   
   Если добавление адреса очереди недоступно, значит у вашей организации нет домена. Домен нужен для создания почтовых ящиков и рассылок, в том числе чтобы создать адрес очереди. Домен можно бесплатно [подключить в сервисе {{ ya-360 }}]({{ support-business-domain }}).


1. [Настройте псевдонимы и подписи](queue-mail.md#send_outside), если нужно.


1. Если пользователи не являются сотрудниками организации:

    1. [Разрешите принимать письма с внешних ящиков](queue-mail.md#mail_tasks).

    1. [Разрешите отправку писем из задач на внешние адреса](queue-mail.md#send_outside).


#### Шаг 2. Настроить триггер для отправки писем

Настройте триггер, который при создании новой задачи из письма будет отправлять пользователю уведомление по почте:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера.

1. Задайте условия, чтобы триггер срабатывал при создании новой задачи из входящего письма:

    1. Выберите опцию **Будут выполнены условия** → **Все**.

    1. Добавьте условие **Событие** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.eventType.create }}**.

    1. Добавьте условие **{{ ui-key.startrek-backend.fields.issue.fields.email }}** → **{{ ui-key.startrek-backend.fields.issue.emailCreatedBy }}** → **{{ ui-key.startrek-backend.fields.trigger.condition.type.text.field.equals.string }}** и введите почтовый адрес очереди.

    1. Включите опцию **{{ ui-key.startrek-backend.fields.trigger.condition.property.ignoreCase }}** на случай, если пользователь введет адрес очереди с заглавной буквы.

    ![](../../_assets/tracker/trigger-example-mail-condition.png)

1. В качестве действия триггера задайте отправку письма:

    1. Выберите действие **Добавить комментарий**.

    1. Включите опцию **{{ ui-key.startrek-backend.messages.sla.send.mail.threshold.excess.function.type }}**.

    1. В поле **{{ ui-key.startrek-backend.fields.issue.emailTo }}** добавьте переменную с адресом пользователя, от которого пришло обращение. Для этого выберите поле **{{ ui-key.startrek-backend.fields.issue.emailTo }}**, нажмите кнопку **Добавить переменную** и выберите **{{ ui-key.startrek-backend.fields.issue.fields.email }}** → **{{ ui-key.startrek-backend.fields.issue.emailFrom }}**.

    1. Напишите текст письма. Вы можете добавить в письмо [параметры задачи](../user/vars.md) с помощью кнопки **Добавить переменную**.

    ![](../../_assets/tracker/trigger-example-mail-action.png)

1. Сохраните триггер. 

    Чтобы проверить работу триггера, отправьте письмо на почтовый адрес очереди.

## Отправлять уведомление о создании задачи через форму {#notify_form}

Предположим, что сотрудники службы поддержки регистрируют обращения в {{ tracker-name }}. Пользователи обращаются в службу поддержки через форму обратной связи, которая создана в сервисе [{{ forms-full-name }}]({{ link-forms }}). На основе заполненной формы создаются задачи в {{ tracker-name }}.

Настроим триггер, который после создания задачи будет оправлять пользователю письмо о том, что его обращение зарегистрировано:

#### Шаг 1. Настроить интеграцию с почтой

Чтобы отправлять письма из {{ tracker-name }}, настройте интеграцию с почтой:

1. [Настройте почтовый адрес для очереди](queue-mail.md#section_gwv_hqb_hgb), в которой будут создаваться задачи по обращениям пользователей.

   
   Если добавление адреса очереди недоступно, значит у вашей организации нет домена. Домен нужен для создания почтовых ящиков и рассылок, в том числе чтобы создать адрес очереди. Домен можно бесплатно [подключить в сервисе {{ ya-360 }}]({{ support-business-domain }}).


1. [Настройте псевдонимы и подписи](queue-mail.md#send_outside), если нужно.

1. Если пользователи не являются сотрудниками организации, [разрешите отправку писем из задач на внешние адреса](queue-mail.md#send_outside).
   
#### Шаг 2. Настроить форму для регистрации обращений

Чтобы создавать задачи из обращений через форму:

1. Перейдите в сервис [{{ forms-full-name }}]({{ link-forms }}) и создайте новую форму.

1. Добавьте на форму вопросы, чтобы пользователь мог сообщить информацию, которая нужна для регистрации обращения.

    Чтобы узнать почтовый адрес пользователя, добавьте вопрос **Почта** и сделайте его обязательным.

    ![](../../_assets/tracker/trigger-example-form-constructor.png)

1. Настройте для формы [интеграцию с {{ tracker-name }}](../../forms/create-task.md):

    1. Укажите очередь и другие параметры задачи.

    1. В поле **Описание задачи** добавьте ответы на вопросы формы.

    1. Чтобы сохранить в параметрах задачи почтовый адрес пользователя, добавьте поле **{{ ui-key.startrek-backend.fields.issue.emailFrom }}** и выберите **Переменные** → **Ответ на вопрос** → **Почта**.
        
    1. Сохраните параметры интеграции.

    ![image](../../_assets/tracker/trigger-example-form-integration.png)

1. [Опубликуйте](../../forms/publish.md#section_link) форму.

#### Шаг 3. Настроить триггер для отправки писем

Настройте триггер, который при создании новой задачи через форму будет отправлять пользователю уведомление по почте:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера.

1. Задайте условия, чтобы триггер срабатывал при создании новой задачи из входящего письма:

    1. Выберите опцию **Будут выполнены условия** → **Все**.

    1. Добавьте условие **Событие** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.eventType.create }}**.

    1. Добавьте условие **{{ ui-key.startrek-backend.fields.issue.fields.email }}** → **{{ ui-key.startrek-backend.fields.issue.emailFrom }}** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldBecameNotEmpty }}**

    ![](../../_assets/tracker/trigger-example-form-condition.png)

1. В качестве действия триггера задайте отправку письма:

    1. Выберите действие **Добавить комментарий**.

    1. Включите опцию **{{ ui-key.startrek-backend.messages.sla.send.mail.threshold.excess.function.type }}**.

    1. В поле **{{ ui-key.startrek-backend.fields.issue.emailTo }}** добавьте переменную с адресом пользователя, от которого пришло обращение. Для этого выберите поле **{{ ui-key.startrek-backend.fields.issue.emailTo }}**, нажмите кнопку **Добавить переменную** и выберите **{{ ui-key.startrek-backend.fields.issue.fields.email }}** → **{{ ui-key.startrek-backend.fields.issue.emailFrom }}**.

    1. Напишите текст письма. Вы можете добавить в письмо [параметры задачи](../user/vars.md) с помощью кнопки **Добавить переменную**.

    ![](../../_assets/tracker/trigger-example-mail-action.png)

1. Сохраните триггер. 

    Чтобы проверить работу триггера, заполните форму, в которой вы настроили интеграцию с {{ tracker-name }}.

## Автоматически добавлять форму в комментарии задачи {#insert_form}

С помощью триггера в комментарии задачи можно добавлять форму с автоматическим предзаполнением полей. Для этого в текст комментария нужно добавить специальный код со ссылкой на форму. Значения в поля формы можно передавать через [GET-параметры](../../forms/get-params.md). Например, передавать параметры задачи с помощью [переменных](../user/vars.md), которые доступны в триггере.

Настроим триггер, который после закрытия задачи будет добавлять форму обратной связи в комментарии и призывать исполнителя:

#### Шаг 1. Создать форму обратной связи

1. Перейдите в сервис [{{ forms-full-name }}]({{ link-forms }}) и создайте форму. 

1. Добавьте на форму вопросы, чтобы исполнитель мог сообщить необходимую информацию.

#### Шаг 2. Создать триггер для добавления формы

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Задайте условия, чтобы триггер срабатывал при закрытии задачи:

    1. Выберите опцию **Будут выполнены условия** → **Все**.

    1. Добавьте условие **Статус** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldBecameEqual }}** → **{{ ui-key.startrek-backend.applinks.samsara.status.closed }}**.

    ![](../../_assets/tracker/trigger-example-add-form-1.png)

1. Добавьте действие **Добавить комментарий**.

1. В текст комментария вставьте код:

   
    ```
   {{=<% %>=}}/iframe/(src="https://forms.yandex.ru/surveys/<идентификатор_формы>/?iframe=1&<идентификатор_вопроса>=<значение>" frameborder=0 width=500)
    ```


    Где:
    - `<идентификатор_формы>` — ID формы, которую необходимо добавить;

    - `<идентификатор_вопроса>` — [идентификатор вопроса](../../forms/question-id.md#sec_question);

    - `<значение>` — значение, которое нужно подставить в поле формы.

      Чтобы передать в форму параметры задачи, в качестве значений используйте [переменные](../user/vars.md): внизу окна нажмите кнопку **Добавить переменную** и выберите параметр задачи, затем вокруг имени переменной замените символы `not_var{{ }}` на `<% %>`.

      Например, чтобы передать ключ задачи, используйте значение `<%issue.key%>`. Чтобы передать логин исполнителя задачи, используйте значение `<%issue.assignee.login%>`.

    Пример кода, в котором в поле формы передается ключ задачи:

    
    ```
    {{=<% %>=}}/iframe/(src="https://forms.yandex.ru/surveys/68***/?iframe=1&answer_short_text_584943=<%issue.key%>" frameborder=0 width=100% height=660px scrolling=no)
    ```
   


1. Нажмите ![](../../_assets/tracker/summon.png) и в строке **Призвать пользователей из поля** введите «Исполнитель».

1. Включите опцию **Отправлять от имени робота**.


1. Сохраните триггер, нажав кнопку **Создать**.

#### Шаг 3. Добавить в очередь yndx-forms-cnt-robot@

Для корректной вставки формы дайте доступ к очереди роботу yndx-forms-cnt-robot@. Подробнее о настройке доступа читайте в разделе [Настроить доступ к очереди](queue-access.md).


После закрытия задачи робот будет создавать комментарий с формой и призывать исполнителя.

## Автоматически добавлять задачи на доску {#board}

На [новой версии доски задач](agile-new.md) можно настроить автоматическое добавление задач по фильтру или [триггеру](trigger-examples.md#board).

Вместо триггера также можно [настроить автодействие](../user/create-autoaction.md) с аналогичными условием и действием. При использовании автодействия задачи, подходящие под условие, будут добавляться на доску не сразу, а с заданной периодичностью. 

{% note warning %}

Триггеры и автодействия работают только для задач той очереди, в которой они настроены.

{% endnote %}


Рассмотрим пример триггера, который добавляет задачу на доску при назначении исполнителем определенного пользователя:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера.

1. Задайте условие: **{{ ui-key.startrek-backend.fields.issue.assignee-key-value }}** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.fieldBecameEqual }}** → `<имя_пользователя>`.

   {% note info %}

   Триггер с таким условием сработает также в том случае, если будет создана новая задача с указанным исполнителем. 

   {% endnote %}

1. Задайте действие:

    1. Выберите действие **Изменить значения в полях**.

    1. Выберите поле **{{ ui-key.startrek-backend.fields.issue.boards }}**.

    1. Выберите действие **Добавить к списку** и укажите доску, на которую нужно добавлять задачу.

    ![](../../_assets/tracker/trigger-example-board.png)

1. Сохраните триггер.

## Отправлять уведомления в мессенджеры {#section_vsn_mb2_d3b}

Для быстрого оповещения сотрудников о важных событиях удобно использовать мессенджеры. Если у мессенджера есть API, в {{ tracker-name }} можно настроить триггер, который отправляет в API мессенджера HTTP-запросы при наступлении определенных событий. Например, если в очереди создается ошибка с критическим приоритетом. Что такое [REST API](../../glossary/rest-api.md).

Примеры настройки триггеров для отправки уведомлений в Slack и Telegram приведены в разделе [{#T}](../messenger.md).

## Автоматически посчитать разницу дат {#tracker_data}

Настроим триггер для автоматического вычисления разницы между датами в {{ tracker-name }}:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Введите название триггера.

1. Выберите опцию **Будут выполнены условия** → **Все**.

1. Добавьте условие **Событие** → **{{ ui-key.startrek-backend.messages.trigger.condition.type.calculate.formula.watch }}**.

    ![](../../_assets/tracker/create_trigger.png)

1. Задайте действия триггера:

    1. Добавьте значение **Вычислить значение**.

    1. Чтобы получить значение разницы дат, выраженное в днях, в поле **Формула для вычисления значения** укажите:

        ```
        (not_var{{issue.end.unixEpoch}}-not_var{{issue.start.unixEpoch}})/86400000
        ```

    1. Выберите **Вычисляемое поле** из [списка]({{ link-admin-fields}}).

        Вы можете выбрать поле из стандартных или [создать новое](../user/create-param.md), например, **Длительность**:

        ![](../../_assets/tracker/create_trigger_two.png)

1. Сохраните триггер, нажав кнопку **Создать**.

Чтобы проверить работу триггера, измените значение полей **{{ ui-key.startrek-backend.fields.issue.start-key-value }}** и **{{ ui-key.startrek-backend.fields.issue.end-key-value }}**.

 

## Создать подзадачу и записать в нее значения полей из родительской задачи {#create-ticket-with-params}

Рассмотрим пример триггера, который создает подзадачу и заполняет поля значениями из исходной задачи. С помощью триггера и [{{ api-name }}](../about-api.md) вы можете настроить автоматическое создание такой задачи:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Выберите [условия срабатывания триггера](../user/set-condition.md).

1. В качестве целевого действия выберите [**HTTP-запрос**](../user/set-action.md#create-http).

1. Укажите параметры запроса. В поле **Тело запроса** укажите параметры создаваемой подзадачи. Для подстановки значений из исходной задачи используйте [переменные](../user/vars.md):

    #|
    || **Поле** | **Содержание** ||
    || Метод | POST ||
    || Адрес | `{{ host }}/{{ ver }}/issues` ||
    || Способ авторизации | OAuth 2.0 ||
    || Токен | [Руководство по получению токена](../concepts/access.md#section_about_OAuth) ||
    || Заголовок авторизации | Authorization ||
    || Тип токена | OAuth ||
    || Тип содержимого | application/json ||
    || Тело запроса |

    >Пример: создать подзадачу и передать в нее поля из исходной: описание, исполнитель, наблюдатели и теги.
    >
    >```
    >{
    >    "summary": "<название_задачи>",
    >    "queue": "<ключ_очереди>",
    >    "description": not_var{{issue.description.json}},
    >    "links": [
    >        {
    >            "relationship": "is subtask for",
    >            "issue": "not_var{{issue.key}}"
    >        }
    >    ],
    >    "assignee": "not_var{{issue.assignee.login}}",
    >    "tags": not_var{{issue.tags.json}},
    >    "followers": not_var{{issue.followers.uid.json}}
    >}
    >```
    Подробнее о запросе: [{#T}](../concepts/issues/create-issue.md), [{#T}](../concepts/issues/link-issue.md). ||
    || Заголовки | Заголовок: `X-Org-ID` или `X-Cloud-Org-ID`.
    Значение: Идентификатор организации. Если у вас только организация {{ org-full-name }}, используйте заголовок `X-Cloud-Org-ID`, если только {{ ya-360 }} или оба типа организаций — `X-Org-ID`. Идентификатор указан в поле **ID организации для API** на странице [настроек {{ tracker-name }}]({{ link-settings }}). ||
    |#

    {% note info %}

    Параметры, которые вы передаете в теле запроса при помощи переменных, должны быть заполнены в исходной задаче. Иначе триггер не сработает.

    {% endnote %}

1. Нажмите кнопку **Создать**.

## Обновить статус, приоритет и добавить комментарий в связанных задачах {#update-related-tasks}

Рассмотрим пример триггера, который обновляет статус, приоритет и добавляет комментарий в связанных задачах. С помощью триггера и [{{ api-name }}](../about-api.md) вы можете настроить автоматическое обновление связанных задач:

1. Перейдите в настройки очереди и в разделе **Триггеры** нажмите кнопку [**Создать триггер**](../user/create-trigger.md).

1. Выберите [условия срабатывания триггера](../user/set-condition.md).

   {% note warning %}

   При создании условия срабатывания триггера обратите внимание на возможность каскадного вызова в связанных задачах.
   
   {% endnote %}

1. В качестве целевого действия выберите [**HTTP-запрос**](../user/set-action.md#create-http).

1. Укажите параметры запроса. В поле **Тело запроса** укажите параметры обновления в связанных задачах. Для подстановки значений из исходной задачи используйте [переменные](../user/vars.md):

    #|
    || **Поле** | **Содержание** ||
    || Метод | POST ||
    || Адрес | `{{ host }}/{{ ver }}/bulkchange/_transition` ||
    || Способ авторизации | OAuth 2.0 ||
    || Токен | [Руководство по получению токена](../concepts/access.md#section_about_OAuth) ||
    || Заголовок авторизации | Authorization ||
    || Тип токена | OAuth ||
    || Тип содержимого | application/json ||
    || Тело запроса |

    >Пример: изменить статус, приоритет и добавить комментарий в связанных задачах.
    >
    >```
    >{
    >    "transition": "need_info", 
    >    "issues": "Relates: not_var{{issue.key}}", 
    >    "values": { 
    >        "comment": "<Комментарий для связанных задач>", 
    >        "priority": { 
    >            "key": "critical" 
    >        } 
    >    } 
    >} 
    >```
    Подробнее о запросе: [{#T}](../concepts/bulkchange/bulk-transition.md). ||
    || Заголовки | Заголовок: `X-Org-ID` или `X-Cloud-Org-ID`.
    Значение: Идентификатор организации. Если у вас только организация {{ org-full-name }}, используйте заголовок `X-Cloud-Org-ID`, если только {{ ya-360 }} или оба типа организаций — `X-Org-ID`. Идентификатор указан в поле **ID организации для API** на странице [настроек {{ tracker-name }}]({{ link-settings }}). ||
    |#

    {% note info %}

    Если требуется изменить в связанных задачах только значения полей без изменения статуса, используйте запрос: [{#T}](../concepts/bulkchange/bulk-update-issues.md).
       
    Параметры, которые вы передаете в теле запроса при помощи переменных, должны быть заполнены в исходной задаче. Иначе триггер не сработает.

    {% endnote %}

1. Нажмите кнопку **Создать**.

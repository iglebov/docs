---
title: Как настроить правила
description: Следуя данной инструкции, вы сможете настроить правила.
---

# Настроить правила

{% note warning %}

По умолчанию настраивать очередь может [только ее владелец](queue-access.md).

{% endnote %}

## Создать правило {#create-rule}

Правило будет применено ко всем новым задачам в очереди. Таймер SLA не появится в задачах, созданных раньше, чем правило.

Чтобы создать новое правило SLA:

1. {% include [go to settings](../../_includes/tracker/transition-page.md) %} 

1. В правом верхнем углу нажмите ![](../../_assets/tracker/svg/queue-settings.svg) **{{ ui-key.startrek.ui_Queues_pages_PageQueue_header.settings }}**. 

1. Перейдите на вкладку **Правила SLA**.

1. Нажмите кнопку **Создать правило**.

1. По умолчанию правило называется `Новое правило SLA`. Чтобы скорректировать название, нажмите на него и введите новое название.

1. Выберите из списка [график работы](schedule.md). График работы устанавливает время, когда правило активно. В нерабочие часы отсчет времени идти не будет.

1. При необходимости настройте **Группы задач, попадающих под правило, и время для ответа**. Группы задач отбираются с помощью фильтров. Для каждой группы задач можно установить срок выполнения и время предупреждения. По умолчанию включен фильтр «Все задачи очереди».

   * По умолчанию группа задач называется `Новая группа задач`. Чтобы скорректировать название, нажмите на него и введите новое название.
   
   * Чтобы добавить фильтр, под названием группы задач нажмите **+** и выберите из списка поле для фильтрации. Поле добавится в строку группы задач. Нажмите на поле для фильтрации и выберите для него значение. Если для фильтрации используется несколько полей, снова нажмите **+** и повторите описанные действия.

   * Укажите **Время до предупреждения** (необязательный параметр) в формате `00h 00m` — по истечении этого срока {{ tracker-name }} отправит предупреждение, что время обработки задачи на исходе.
   
   * Укажите **Время на выполнение** в формате `00h 00m` — предельное время на обработку задачи. По истечении этого времени {{ tracker-name }} отправит уведомление о срыве срока.

   * Для одного правила SLA можно задать несколько групп задач. Чтобы создать новую группу задач, нажмите **+ Добавить группу задач**.

   * Чтобы удалить группу задач, в конце её строки нажмите ![](../../_assets/console-icons/trash-bin.svg).

1. В блоке **Оповещения о превышении времени** укажите, как и кому отправлять предупреждения и оповещать о срыве сроков.

1. В блоке **Настройки таймера SLA** задайте условия, при которых таймер будет запускаться, приостанавливаться или останавливаться:

    * **Старт** — таймер запустится, если выполнено любое из перечисленных условий. Если таймер стоял на паузе, отсчет времени будет возобновлен.

    * **Пауза** — таймер приостановится, если выполнено любое из перечисленных условий. Таймер запустится, когда будет выполнено условие из списка **Старт**.

        {% note alert %}

        Если в качестве условия для паузы выбрано "{{ ui-key.startrek-backend.messages.sla.issue.on.status.timer.trigger.condition.type }}", таймер запустится, как только задача будет переведена в любой другой статус.

        {% endnote %}

    * **Остановка** — таймер остановится, если выполнено любое из перечисленных условий.

    Возможные условия:
    Условие | Режим таймера | Описание
    ----- | ----- | -----
    {{ ui-key.startrek-backend.messages.sla.assignee.deleted.timer.trigger.condition.type }} | **Старт**, **Остановка** | Условие считается выполненным, когда в задаче удаляют исполнителя.
    {{ ui-key.startrek-backend.messages.sla.assignee.set.timer.trigger.condition.type }} | **Старт**, **Остановка** | Условие считается выполненным, когда задаче назначают нового исполнителя.
    {{ ui-key.startrek-backend.messages.sla.client.commented.timer.trigger.condition.type }} | **Старт**, **Остановка** | Условие считается выполненным, когда задачу прокомментировал пользователь, не входящий в [команду очереди](queue-team.md).
    {{ ui-key.startrek-backend.messages.sla.issue.created.timer.trigger.condition.type }} | **Старт** | Таймер запустится сразу после создания задачи.
    {{ ui-key.startrek-backend.messages.sla.status.changed.timer.trigger.condition.type }} | **Старт**, **Остановка** | Условие считается выполненным, когда задачу переводят в один из указанных в нем статусов.
    {{ ui-key.startrek-backend.messages.sla.resolution.deleted.timer.trigger.condition.type }} | **Старт** | Условие считается выполненным, когда из задачи удаляют проставленную ранее резолюцию.
    {{ ui-key.startrek-backend.messages.sla.issue.on.status.timer.trigger.condition.type }} | **Пауза** | Таймер будет приостановлен, пока задача находится в одном из указанных статусов. После изменения статуса таймер автоматически запустится.
    {{ ui-key.startrek-backend.messages.sla.resolution.set.timer.trigger.condition.type }} | **Остановка** | Условие считается выполненным, когда в задаче проставляют одну из указанных в нем резолюций.
    {{ ui-key.startrek-backend.messages.sla.team.commented.timer.trigger.condition.type }} | **Остановка** | Условие считается выполненным, когда задачу прокомментировал пользователь, входящий в [команду очереди](queue-team.md).
    {{ ui-key.startrek-backend.messages.sla.issue.has.assignee.condition.type }} | **Пауза** | Таймер будет приостановлен, пока в задаче указан исполнитель. После удаления исполнителя таймер автоматически запустится.
    {{ ui-key.startrek-backend.messages.sla.issue.has.no.assignee.condition.type }} | **Пауза** | Таймер будет приостановлен, пока в задаче не указан исполнитель. После назначения исполнителя таймер автоматически запустится.

1. Вы можете настроить обновление таймера при выполнении условий старта. Для этого в блоке **Настройки таймера SLA** включите опцию **Перезапускаемый таймер**. В этом случае после паузы он не продолжит отсчет, а запустится заново.

1. Нажмите кнопку **Создать правило**.

### Пример {#example}

Создадим правило для контроля времени реакции на новые задачи. Таймер правила запустится, как только задаче будет назначен исполнитель, и остановится, когда исполнитель возьмет задачу в работу. Если за 15 минут исполнитель не отреагирует на задачу, вы получите оповещение по почте.

Чтобы создать правило:

1. В блоке **Группы задач, попадающих под правило, и время для ответа**:

   * Поскольку правило должно распространяться на все задачи очереди, не добавляйте новые группы задач, а в группе задач, созданной по умолчанию, не настраивайте фильтры.

   * Поле **Время до предупреждения** оставьте пустым.

   * В поле **Время на выполнение** введите время реакции, например, `15m`.

1. В блоке **Оповещения о превышении времени** настройте оповещение о срыве срока:

   * В блоке **Предупреждения** оставьте **Без оповещений**. 

   * В блоке **Срыв срока** выберите опцию **Отправить письмо** и укажите ваш логин в {{ tracker-name }}.

1. В блоке **Настройки таймера SLA** настройте таймер:

   * **Старт** — **Назначен исполнитель**.

   * Блок **Пауза** оставьте пустым.

   * **Остановка** — выберите условие **Задача переведена в статус**, под ним нажмите **+** и выберите статус **В работе**.

## Просмотреть правила {#section_nbs_r2g_vdb}

Чтобы просмотреть список правил SLA, действующих в очереди:

1. {% include [go to settings](../../_includes/tracker/transition-page.md) %}

1. В правом верхнем углу нажмите ![](../../_assets/tracker/svg/queue-settings.svg) **{{ ui-key.startrek.ui_Queues_pages_PageQueue_header.settings }}**. 

1. Перейдите на вкладку **Правила SLA**.

Чтобы просмотреть параметры правила, в блоке с ним нажмите на ![](../../_assets/console-icons/chevron-down.svg):

* **График работы**

    График работы — это время, когда правило активно. В нерабочие часы отсчет времени идти не будет.

* **Группы задач, попадающих под правило, и время для ответа**

    Правило может применяться не только ко всем задачам очереди, но и к отдельным группам задач, которые формируются с помощью фильтров. Для каждой группы можно установить свои сроки выполнения:

    * **Время до предупреждения** (необязательный параметр) — по истечении этого срока {{ tracker-name }} отправит предупреждение, что время обработки задачи на исходе.

    * **Время на выполнение** — предельное время на обработку задачи. По истечении этого времени {{ tracker-name }} отправит уведомление о срыве срока.

* **Оповещения о превышении времени**

    Как и кому {{ tracker-name }} отправляет предупреждения и сообщает о нарушении сроков.

* **Настройки таймера SLA**

    События, при которых таймер будет запускаться, приостанавливаться или останавливаться:

    * **Старт** — таймер запустится, если выполнено любое из перечисленных условий. Если таймер стоял на паузе, отсчет времени будет возобновлен.

    * **Пауза** — таймер приостановится, если выполнено любое из перечисленных условий. Таймер запустится, когда будет выполнено условие из списка **Старт**.

        {% note info %}

        Если в качестве условия для паузы выбрано «{{ ui-key.startrek-backend.messages.sla.issue.on.status.timer.trigger.condition.type }}», таймер запустится, как только задача будет переведена в любой другой статус.

        {% endnote %}

    * **Остановка** — таймер остановится, если выполнено любое из перечисленных условий.

## Изменить правило {#edit-rule}

Чтобы изменить правило SLA:

1. {% include [go to settings](../../_includes/tracker/transition-page.md) %}

1. В правом верхнем углу нажмите ![](../../_assets/tracker/svg/queue-settings.svg) **{{ ui-key.startrek.ui_Queues_pages_PageQueue_header.settings }}**. 

1. Перейдите на вкладку **Правила SLA**.

1. Выберите правило и в блоке с ним нажмите на ![](../../_assets/console-icons/chevron-down.svg).

1. Внесите изменения и нажмите кнопку **Сохранить**.

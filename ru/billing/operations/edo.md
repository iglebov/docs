---
title: Подключиться к электронному документообороту
description: Следуя данной инструкции, вы сможете подключиться к электронному документообороту.
---

# Подключиться к электронному документообороту


Юридические лица и индивидуальные предприниматели, которые являются резидентами РФ, могут воспользоваться услугой Электронного документооборота (ЭДО) в {{ yandex-cloud }}. 
С помощью ЭДО можно получать [закрывающие отчетные документы](../concepts/edo.md#document). 

{% note warning %}

При подключении к ЭДО, отправка электронных версий закрывающих документов на e-mail адрес и оригиналов закрывающих документов на почтовый адрес прекращается.
Но скачивание закрывающих документов будет доступно в сервисе {{ billing-name }}. См. [инструкцию](download-reporting-docs.md).

{% endnote %}

## Подключитесь к ЭДО {#connect}

Чтобы начать сотрудничество по ЭДО с {{ yandex-cloud }}:

1. Подключитесь к [оператору](../concepts/edo.md#operator) ЭДО — [Диадок (СКБ Контур)](https://promo.diadoc.ru/yandexfd?p=z05983&utm_abtest=order-lightbox) или [СБИС (Тензор)](https://sbis.ru/edo/telecoms/yandex). Инструкцию по подключению можно найти на сайте оператора. {{ yandex-cloud }} не работает с другими операторами и не поддерживает роуминг.

1. Подпишите соглашение от {{ yandex-cloud }}. Перейдите в ваш личный кабинет [Диадок (СКБ Контур)](https://promo.diadoc.ru/yandexfd?p=z05983&utm_abtest=order-lightbox) или [СБИС (Тензор)](https://sbis.ru/edo/telecoms/yandex) и подпишите соглашение от ООО «Яндекс.Облако».

    {{ yandex-cloud }} автоматически направляет соглашения в одностороннем порядке двум операторам ЭДО, если:
    * регистрируется новый плательщик;
    * выставляется счет;
    * заключается договор.

После подписания соглашения вы начнете получать документы от {{ yandex-cloud }}. Это документы, сформированные не ранее даты доставки подписанного соглашения во внутренний ИТ-сервис ЭДО. Они будут автоматически отправляться через ЭДО в сроки, которые указаны в договоре на оказание услуг.

Оригиналы документов, сформированных до подписания соглашения, отправляются только Почтой России на физический адрес.

Информацию о подписантах соглашения с принимающей стороны можно найти в личном кабинете оператора. Если информацию найти не удается, обратитесь в техническую поддержку оператора.

{{ yandex-cloud }} не обрабатывает вопросы из личного кабинета оператора. Если у вас есть вопрос, обратитесь в [техническую поддержку]({{ link-console-support }}).

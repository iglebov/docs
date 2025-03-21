# Как удалить пользователя из {{ tracker-name }}


## Описание сценария {#case-description}

Необходимо удалить пользователя из {{ tracker-name }}.

## Решение {#case-resolution}

{% note info %}

Удалить аккаунт может пользователь с ролью `{{ roles-organization-admin }}` или `{{ roles-organization-owner }}`.

{% endnote %}

Чтобы удалить аккаунт пользователя из {{ tracker-name }}, исключите сотрудника из организации, в которой он состоит. Для этого необходимо:

1. Войти в аккаунт администратора или владельца организации.
1. Перейти в сервис [{{ org-name }}]({{  link-org-main }}).
1. На левой панели выбрать раздел **{{ ui-key.yacloud_org.pages.users }}**..
1. Выбрать сотрудника из списка или воспользоваться строкой поиска вверху страницы.
1. В строке сотрудника нажать ![***](../../../_assets/options.svg) и выбрать **{{ ui-key.yacloud.common.delete }}**.

{% note info %}

Если сотрудник состоит в организации {{ yandex-360 }}, из нее сотрудника нужно отдельно исключить [здесь](https://admin.yandex.ru/users).

{% endnote %}

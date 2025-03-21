---
title: История изменений в {{ at-full-name }}
description: В разделе представлена история изменений сервиса {{ at-name }}.
---

# История изменений в {{ at-full-name }}

## IV квартал 2024 {#q4-2024}

* Добавлены новые события для сервисов:

  {% cut "{{ org-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `AttachRegion` | Подключение региона

  {% endcut %}

  {% cut "{{ ml-platform-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `ActivateDataset` | Активация датасета
  `ActivateDocker` | Применение Docker-образа для проекта
  `CreateDataset` | Создание датасета
  `CreateDocker` | Создание Docker-образа
  `DeactivateDataset` | Деактивация датасета
  `DeleteDataset` | Удаление датасета
  `DeleteDocker` | Удаление Docker-образа

  {% endcut %}

  {% cut "{{ mos-short-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `DeleteBackup` | Удаление резервной копии

  {% endcut %}

  {% cut "{{ objstorage-name }} " %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `PresignURLCreate` | Создание подписанной ссылки

  {% endcut %}


## III квартал 2024 {#q3-2024}

* Добавлена возможность фильтрации по типам событий. Подробнее см. в разделе [Настройки трейла](./concepts/trail.md#trail-settings).
* Добавлены новые события для сервисов:

  {% cut "{{ certificate-manager-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Имя события | Описание
  --- | ---
  `GetCertificateContent` | Получение содержимого SSL-сертификата

  {% endcut %}

  {% cut "{{ org-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `DeleteFederatedUserAccounts` | Удаление пользователя из федерации

  {% endcut %}

  {% cut "{{ ml-platform-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CloseProject` | Закрытие проекта
  `CreateNode` | Создание ноды
  `DeleteNode` | Удаление ноды
  `OpenProject` | Открытие проекта
  `ResumeNode` | Возобновление работы ноды
  `SuspendNode` | Приостановка работы ноды
  `UpdateNode` | Изменение ноды

  {% endcut %}

  {% cut "{{ iam-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `workload.CreateFederatedCredential` | Создание [привязки](../iam/concepts/workload-identity.md#federated-credentials) в федерации сервисных аккаунтов
  `workload.DeleteFederatedCredential` | Удаление привязки из федерации сервисных аккаунтов
  `workload.oidc.CreateFederation` | Создание [федерации сервисных аккаунтов](../iam/concepts/workload-identity.md)
  `workload.oidc.DeleteFederation` | Удаление федерации сервисных аккаунтов
  `workload.oidc.UpdateFederation` | Изменение федерации сервисных аккаунтов

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `RevokeIamToken` | Отзыв IAM-токена

  {% endcut %}

  {% cut "{{ load-testing-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateRegressionDashboard` | Создание дашборда регрессий
  `DeleteRegressionDashboard` | Удаление дашборда регрессий
  `UpdateRegressionDashboard` | Изменение дашборда регрессий

  {% endcut %}

  {% cut "{{ maf-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Имя события | Описание
  --- | ---
  `CreateCluster` | Создание кластера
  `DeleteCluster` | Удаление кластера
  `StartCluster` | Запуск кластера
  `StopCluster` | Остановка кластера
  `UpdateCluster` | Изменение кластера

  {% endcut %}

  {% cut "{{ mch-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `AddClusterShard` | Добавление шарда в кластер
  `DeleteClusterShard` | Удаление шарда из кластера

  {% endcut %}

  {% cut "{{ mgp-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Имя события | Описание
  --- | ---
  `MoveCluster` | Перемещение кластера

  {% endcut %}

  {% cut "{{ managed-k8s-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Имя события | Описание
  --- | ---
  `ApiServerAuditEvent` | Событие аудита кластера {{ managed-k8s-name }}

  {% endcut %}

  {% cut "{{ mmy-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Имя события | Описание
  --- | ---
  `DatabaseUserSQLRequest` | SQL-запрос пользователя к базе данных

  {% endcut %}

  {% cut "{{ sd-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Имя события | Описание
  --- | ---
  `ComputeNodeAccess` | Подключение [модуля](../security-deck/concepts/access-transparency.md) {{ atr-name }} к [подкластеру](../data-proc/concepts/index.md#resources) {{ dataproc-name }}
  `MDBClusterAccess` | Подключение модуля {{ atr-name }} к кластеру базы данных

  {% endcut %}

  {% cut "{{ sws-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateArlProfile` | Создание профиля ARL
  `CreateSecurityProfile` | Создание профиля безопасности
  `CreateWafProfile` | Создание профиля WAF
  `DeleteArlProfile` | Удаление профиля ARL
  `DeleteSecurityProfile` | Удаление профиля безопасности
  `DeleteWafProfile` | Удаление профиля WAF
  `UpdateArlProfile` | Изменение профиля ARL
  `UpdateSecurityProfile` | Изменение профиля безопасности
  `UpdateWafProfile` | Изменение профиля WAF

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `ArlMatchedRequest` | Запрос по правилам ARL
  `WafMatchedExclusionRule` | Примененное правило исключения WAF
  `WafMatchedRule` | Примененное правило WAF

  {% endcut %}

  {% cut "{{ postbox-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Имя события | Описание
  --- | ---
  `CreateConfigurationSet` | Создание [конфигурации](../postbox/concepts/glossary.md#configuration)
  `CreateIdentity` | Создание адреса
  `DeleteConfigurationSet` | Удаление конфигурации
  `DeleteIdentity` | Удаление адреса
  `UpdateConfigurationSet` | Изменение конфигурации
  `UpdateIdentity` | Изменение адреса

  {% endcut %}

## II квартал 2024 {#q2-2024}

* Добавлены новые события для сервисов:

  {% cut "{{ api-gw-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `SetApiGatewayAccessBindings` | Назначение привязок прав доступа к API-шлюзу
  `UpdateApiGatewayAccessBindings` | Изменение привязок прав доступа к API-шлюзу

  {% endcut %}

  {% cut "{{ backup-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `InitResource` | Инициализация подключения ВМ к сервису {{ backup-name }}
  `UpdateResource`| Обновление статуса подключения ВМ к сервису {{ backup-name }}

  {% endcut %}

  {% cut "{{ certificate-manager-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `SetCertificateAccessBindings` | Назначение привязок прав доступа для сертификата
  `SetDomainPrimaryCertificate` | Назначение домену основного сертификата

  {% endcut %}

  {% cut "{{ compute-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `AttachInstanceNetworkInterface` | Подключение сетевого интерфейса
  `DetachInstanceNetworkInterface` | Отключение сетевого интерфейса

  {% endcut %}

  {% cut "{{ ml-platform-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CloneJob` | Клонирование задания
  `UpdateJobDataTtl` | Изменение времени жизни данных задания

  {% endcut %}

  {% cut "{{ sf-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `mdbproxy.SetProxyAccessBindings` | Назначение привязок прав доступа к управляемой базе данных
  `mdbproxy.UpdateProxyAccessBindings` | Изменение привязок прав доступа к управляемой базе данных
  `triggers.PauseTrigger` | Остановка триггера
  `triggers.ResumeTrigger` | Запуск триггера

  {% endcut %}

  {% cut "{{ iam-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `SetServiceAccountAccessBindings` | Назначение привязок прав доступа для сервисного аккаунта

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `CreateIamToken` | Создание IAM-токена
  `oslogin.CheckSshPolicy` | Проверка прав на подключение по SSH при доступе по {{ oslogin }}
  `oslogin.GenerateSshCertificate` | Генерация SSH-сертификата для доступа по {{ oslogin }}

  {% endcut %}

  {% cut "{{ mch-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `DeleteBackup` | Удаление резервной копии

  {% endcut %}

  {% cut "{{ mgl-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `FinishMigration` | Завершение процесса миграции инстанса в другую зону доступности
  `PrepareBackupUpload` | Подготовка к восстановлению из резервной копии
  `RollbackMigration` | Отмена процесса миграции инстанса в другую зону доступности
  `StartMigration` | Запуск процесса миграции инстанса в другую зону доступности

  {% endcut %}

  {% cut "{{ mpg-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `DatabaseUserSQLRequest`| SQL-запрос пользователя к базе данных

  {% endcut %}

  {% cut "{{ mrd-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `EnableClusterSharding` | Включение шардирования кластера

  {% endcut %}

  {% cut "{{ marketplace-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `ActivateSubscriptionAutoRenewal` | Активация автоматического продления подписки
  `CancelSubscriptionAutoRenewal` | Отмена автоматического продления подписки

  {% endcut %}

  {% cut "{{ speechsense-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateProject` | Создание проекта
  `CreateSpace` | Создание пространства
  `DeleteProject` | Удаление проекта
  `DeleteSpace` | Удаление пространства
  `SetProjectAccessBindings` | Назначение привязок прав доступа к проекту
  `SetSpaceAccessBindings` | Назначение привязок прав доступа к пространству
  `UpdateProject` | Изменение проекта
  `UpdateProjectAccessBindings` | Изменение привязок прав доступа к проекту
  `UpdateSpace` | Изменение пространства
  `UpdateSpaceAccessBindings` | Изменение привязок прав доступа к пространству

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `CreateTalksReport` | Создание отчета о диалоге
  `GetTalk` | Получение диалога
  `GetTalkAudio` | Получение аудиозаписи диалога
  `SearchTalks` | Поиск диалога
  `UploadTalkToConnection` | Загрузка диалога в подключение

  {% endcut %}

  {% cut "{{ websql-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateSavedQuery` | Сохранение запроса
  `DeleteExecutedQuery` | Удаление выполненного запроса
  `DeleteSavedQuery` | Удаление сохраненного запроса
  `EditSavedQuery` | Редактирование сохраненного запроса
  `PublishExecutedQuery` | Публикация выполненного запроса
  `PublishSavedQuery` | Публикация сохраненного запроса

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `Execute` | Выполнение запроса
  `GenerateSql` | Генерация запроса
  `GetDatabaseStructure` | Получение структуры базы данных

  {% endcut %}

  {% cut "{{ wiki-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `AccessRequestCreate` | Создание запроса доступа к странице
  `AccessRequestProcess` | Обработка запроса доступа к странице
  `AttachmentCreate` | Загрузка файла на страницу
  `AttachmentDelete` | Удаление файла со страницы
  `AuthorRoleRequestCreate` | Создание запроса на добавление в авторы страницы
  `AuthorRoleRequestProcess` | Обработка запроса на добавление в авторы страницы
  `BookmarkCreate` | Добавление в избранное
  `BookmarkDelete` | Удаление из избранного
  `BookmarkTagsCreate` | Создание тегов для избранного
  `BookmarkTagsDelete` | Удаление тегов для избранного
  `BookmarkUpdate` | Обновление тегов для страницы в избранном
  `ClusterMove` | Перемещение кластера страниц
  `CommentCreate` | Создание комментария
  `CommentDelete` | Удаление комментария
  `CommentUpdate` | Обновление комментария
  `GridAddColumns` | Добавление столбцов в динамическую таблицу
  `GridAddRows` | Добавление строк в динамическую таблицу
  `GridClone` | Создание копии динамической таблицы
  `GridCreate` | Создание новой динамической таблицы
  `GridDelete` | Удаление динамической таблицы
  `GridImport` | Импорт динамической таблицы из файла
  `GridMoveColumns` | Перемещение столбца динамической таблицы
  `GridMoveRows` | Перемещение строки динамической таблицы
  `GridRemoveColumns` | Удаление столбцов динамической таблицы
  `GridRemoveRows` | Удаление строк в динамической таблице
  `GridRollback` | Отмена изменений в динамической таблице
  `GridUpdate` | Обновление динамической таблицы
  `GridUpdateCells` | Обновление ячеек в динамической таблице
  `GridUpdateColumn` | Обновление столбца в динамической таблице
  `GridUpdateRow` | Обновление строки в динамической таблице
  `PageChangeOrder` | Изменение порядка страницы
  `PageChangeToYFM` | Конвертирование страницы в новый редактор
  `PageClone` | Создание копии страницы
  `PageCreate` | Создание страницы
  `PageDelete` | Удаление страницы
  `PageImport` | Импорт страницы из файла
  `PageRecover` | Восстановление удаленной страницы
  `PageUpdate`| Обновление страницы
  `RecoveryTokenDelete` | Удаление токена для восстановления страницы
  `SubscriberDelete` | Удаление подписчика
  `SubscribersAdd` | Добавление подписчиков
  `SubscriptionAdd` | Добавление подписки
  `SubscriptionDelete` | Удаление подписки

  {% endcut %}

* Поле `impersonator_info` в блоке `authentication` было заменено на поле `token_info`.

## I квартал 2024 {#q1-2024}

* Добавлены новые события для сервисов:

  {% cut "{{ certificate-manager-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `UpdateDomainAccessBindings` | Изменение прав доступа для домена

  {% endcut %}

  {% cut "{{ cloud-apps-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateCloudApplication` | Создание приложения
  `DeleteCloudApplication` | Удаление приложения
  `UpdateCloudApplication` | Изменение приложения

  {% endcut %}

  {% cut "{{ dns-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `UpdatePrivateNetworks` | Изменение приватных сетей

  {% endcut %}

  {% cut "{{ cloud-logging-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `ChangeLogGroupAccessBindings` | Изменение прав доступа для лог-группы
  `CreateExport` | Создание выгрузки логов
  `CreateLogGroup` | Создание лог-группы
  `CreateSink` | Создание приемника логов
  `UpdateLogGroup` | Изменение лог-группы
  `DeleteExport` | Удаление выгрузки логов
  `DeleteLogGroup` | Удаление лог-группы
  `DeleteSink` | Удаление приемника логов
  `SetExportAccessBindings` | Назначение прав доступа для выгрузки логов
  `SetLogGroupAccessBindings` | Назначение прав доступа для лог-группы
  `SetSinkAccessBindings` | Назначение прав доступа для приемника логов
  `UpdateExport` | Изменение выгрузки логов
  `UpdateExportAccessBindings` | Изменение прав доступа для выгрузки логов
  `UpdateLogGroupAccessBindings` | Изменение прав доступа для лог-группы
  `UpdateSink` | Изменение приемника логов
  `UpdateSinkAccessBindings` | Изменение прав доступа для приемника логов

  {% endcut %}

  {% cut "{{ org-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateOsLoginProfile` | Создание профиля {{ oslogin }}
  `CreateUserSshKey` | Создание SSH-ключа пользователя
  `UpdateOsLoginProfile` | Изменение профиля {{ oslogin }}
  `UpdateOsLoginSettings` | Изменение настроек {{ oslogin }}
  `UpdateUserSshKey` | Изменение SSH-ключа пользователя
  `SetDefaultProfile` | Назначение профиля по умолчанию
  `DeleteOsLoginProfile` | Удаление профиля {{ oslogin }}
  `DeleteUserSshKey` | Удаление SSH-ключа пользователя

  {% endcut %}

  {% cut "{{ compute-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateHostGroup` | Создание группы выделенных хостов
  `DeleteHostGroup` | Удаление группы выделенных хостов
  `UpdateHostGroup` | Изменение группы выделенных хостов
  `serialssh.ConnectSerialPort` | Подключение к серийному порту инстанса

  {% endcut %}

  {% cut "{{ kms-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `asymmetricencryption.CancelAsymmetricEncryptionKeyDeletion` | Отмена удаления асимметричной ключевой пары шифрования
  `asymmetricsignature.CancelAsymmetricSignatureKeyDeletion` | Отмена удаления ключевой пары электронной подписи

  {% endcut %}

  {% cut "{{ load-testing-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateAgent` | Создание агента
  `CreateConfig` | Создание конфигурации
  `CreateMigration` | Создание миграции
  `CreateTest` | Создание теста
  `DeleteAgent` | Удаление агента
  `DeleteConfig` | Удаление конфигурации
  `DeleteTest` | Удаление теста
  `RestartAgent` | Перезапуск агента
  `StartAgent` | Запуск агента
  `StopAgent` | Остановка агента
  `StopTest` | Остановка теста
  `UpdateAgent` | Изменение агента
  `UpdateTest` | Изменение теста
  `UpgradeImageAgent` | Обновление образа агента

  {% endcut %}

  {% cut "{{ mgl-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateInstanceBackup` | Создание резервной копии инстанса
  `ReconfigureGitlab` | Изменение конфигурации GitLab
  `RescheduleMaintenance` | Перенос запланированного технического обслуживания
  `ScheduleUpgrade` | Назначение времени обновления инстанса

  {% endcut %}

  {% cut "{{ mch-short-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `UpdateClusterExternalDictionary` | Изменение внешнего словаря

  {% endcut %}


  {% cut "{{ mgp-short-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `CreateHBARule` | Создание правила аутентификации пользователей
  `CreatePXFDatasource` | Создание подключения к внешней таблице
  `DeleteBackup` | Удаление резервной копии
  `DeleteHBARule` | Удаление правила аутентификации пользователей
  `DeletePXFDatasource` | Удаление подключения к внешней таблице
  `UpdateHBARule` | Изменение правила аутентификации пользователей
  `UpdatePXFDatasource` | Изменение подключения к внешней таблице

  {% endcut %}

  {% cut "{{ mmg-short-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `DeleteBackup` | Удаление резервной копии

  {% endcut %}

  {% cut "{{ mmy-short-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `DatabaseUserLogin` | Подключение пользователя к базе данных
  `DatabaseUserLogout` | Отключение пользователя от базы данных

  {% endcut %}

  {% cut "{{ mos-short-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `MoveCluster` | Перемещение кластера
  `UpdateDashboardsNodeGroup` | Изменение группы хостов типа `Dashboards`

  {% endcut %}

  {% cut "{{ mpg-short-name }}" %}

  [События уровня сервисов](./concepts/format-data-plane.md):

  Событие | Описание
  --- | ---
  `DatabaseUserLogin` | Подключение пользователя к базе данных
  `DatabaseUserLogout` | Отключение пользователя от базы данных
  `StartClusterFailover` | Запуск переключения мастера для кластера

  {% endcut %}

  {% cut "{{ vpc-name }}" %}

  [События уровня конфигурации](./concepts/format.md):

  Событие | Описание
  --- | ---
  `RelocateSubnet` | Перемещение облачной подсети в другую зону доступности

  {% endcut %}
* Исправлена ошибка, из-за которой события поставлялись с задержкой, когда трейл находился в статусе `Error`.

* Изменен механизм доставки событий управления базами данных и пользователями внутри баз данных от сервисов {{ mpg-full-name }}, {{ mmy-full-name }} и {{ mmg-full-name }}. Теперь они относятся к [событиям уровня сервисов](./concepts/format-data-plane.md).
---
title: Как удалить публичную зону DNS в {{ dns-full-name }}
description: Следуя данной инструкции, вы сможете удалить публичную зону DNS.
---

# Удалить зону

Чтобы удалить [зону DNS](../concepts/dns-zone.md):

{% list tabs group=instructions %}

- Консоль управления {#console}

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, где требуется удалить зону DNS.
  1. Выберите сервис **{{ ui-key.yacloud.iam.folder.dashboard.label_dns }}**.
  1. Нажмите значок ![image](../../_assets/console-icons/ellipsis.svg) в строке зоны, которую требуется удалить.
  1. В открывшемся меню нажмите кнопку **{{ ui-key.yacloud.common.delete }}**.
  1. В открывшемся окне нажмите кнопку **{{ ui-key.yacloud.common.delete }}**.

- CLI {#cli}

  {% include [include](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  1. Посмотрите описание команды CLI для удаления зоны:

      ```
      yc dns zone delete --help
      ```
  1. Получите список всех зон в каталоге по умолчанию:

      ```
      yc dns zone list
      ```
  1. Выберите идентификатор (`ID`) или имя (`NAME`) нужной зоны.
  1. Удалите зону из каталога по умолчанию:

      ```
      yc dns zone delete <имя_или_идентификатор_зоны>
      ```

- {{ TF }} {#tf}

  {% include [terraform-install](../../_includes/terraform-install.md) %}

  Чтобы удалить зону DNS, созданную с помощью {{ TF }}:

  1. Откройте файл конфигурации {{ TF }} и удалите фрагмент с описанием зоны DNS.

     {% cut "Пример описания зоны DNS в конфигурации {{ TF }}" %}

     ```hcl
     resource "yandex_vpc_network" "foo" {}
     
     resource "yandex_dns_zone" "zone1" {
       name        = "my-public-zone"
       description = "Test public zone"
     
       labels = {
         label1 = "test-public"
       }
     
       zone    = "test.example-public2.com."
     }
     ```

     {% endcut %}

  1. В командной строке перейдите в папку, где расположен конфигурационный файл {{ TF }}.

  1. Проверьте конфигурацию командой:
     ```
     terraform validate
     ```
     
     Если конфигурация является корректной, появится сообщение:
     
     ```
     Success! The configuration is valid.
     ```

  1. Выполните команду:
     ```
     terraform plan
     ```
  
     В терминале будет выведен список ресурсов с параметрами. На этом этапе изменения не будут внесены. Если в конфигурации есть ошибки, {{ TF }} на них укажет.

  1. Примените изменения конфигурации:
     ```
     terraform apply
     ```
     
  1. Подтвердите изменения: введите в терминал слово `yes` и нажмите **Enter**.

     Проверить удаление зоны DNS можно в [консоли управления]({{ link-console-main }}) или с помощью команды [CLI](../../cli/quickstart.md):

     ```
     yc dns zone list
     ```

- API {#api}

  Чтобы удалить зону DNS, воспользуйтесь методом REST API [delete](../api-ref/DnsZone/delete.md) для ресурса [DnsZone](../api-ref/DnsZone/index.md) или вызовом gRPC API [DnsZoneService/Delete](../api-ref/grpc/DnsZone/delete.md).

{% endlist %}

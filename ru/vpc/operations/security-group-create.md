---
title: Как создать группу безопасности
description: Следуя данной инструкции, вы сможете создать группу безопасности.
---

# Создать группу безопасности

{% include [sg-rules](../../_includes/vpc/sg-rules.md) %}

Чтобы создать новую [группу безопасности](../concepts/security-groups.md):

{% list tabs group=instructions %}

- Консоль управления {#console}

  1. В [консоли управления]({{ link-console-main }}) перейдите в каталог, где требуется создать группу безопасности.
  1. В списке сервисов выберите **{{ ui-key.yacloud.iam.folder.dashboard.label_vpc }}**.
  1. На панели слева выберите ![image](../../_assets/console-icons/shield.svg) **{{ ui-key.yacloud.vpc.label_security-groups }}**. 
  1. Нажмите кнопку **{{ ui-key.yacloud.vpc.network.security-groups.button_create }}**.
  1. Введите имя группы безопасности.
  1. В поле **{{ ui-key.yacloud.vpc.network.security-groups.forms.field_sg-network }}** выберите сеть, которой будет назначена группа безопасности.
  1. В блоке **{{ ui-key.yacloud.vpc.network.security-groups.forms.label_section-rules }}** создайте правила для управления трафиком: 
     1. Выберите вкладку **{{ ui-key.yacloud.vpc.network.security-groups.label_egress }}** или **{{ ui-key.yacloud.vpc.network.security-groups.label_ingress }}**.
     1. Нажмите кнопку **{{ ui-key.yacloud.vpc.network.security-groups.button_add-rule }}**.
     1. В открывшемся окне в поле **{{ ui-key.yacloud.vpc.network.security-groups.forms.field_sg-rule-port-range }}** укажите один порт или диапазон портов, куда или откуда будет поступать трафик.
     1. В поле **{{ ui-key.yacloud.vpc.network.security-groups.forms.field_sg-rule-protocol }}** укажите нужный протокол или оставьте `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_any }}`, чтобы разрешить передачу трафика по всем протоколам.
     1. В поле **{{ ui-key.yacloud.vpc.network.security-groups.forms.field_sg-rule-destination }}** или **{{ ui-key.yacloud.vpc.network.security-groups.forms.field_sg-rule-source }}** выберите назначение правила:
        1. `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_sg-rule-destination-cidr }}` — правило будет применено к диапазону IP-адресов. В поле **{{ ui-key.yacloud.vpc.network.security-groups.forms.field_sg-rule-cidr-blocks }}** укажите CIDR и маски подсетей, в которые или из которых будет поступать трафик. Чтобы добавить несколько CIDR, нажимайте кнопку **{{ ui-key.yacloud.vpc.subnetworks.create.button_add-cidr }}**.
        1. `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_sg-rule-destination-sg }}` — альтернатива полю `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_sg-rule-destination-cidr }}`. Выберите:
           * `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_sg-rule-sg-type-self }}` — чтобы разрешить сетевое взаимодействие между ресурсами, на которые применена текущая группа безопасности.
           * `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_sg-rule-sg-type-list }}` — чтобы разрешить сетевое взаимодействие с ресурсами, на которые применена выбранная группа.
        1. `{{ ui-key.yacloud.vpc.network.security-groups.forms.value_sg-rule-sg-type-balancer }}`.
  1. Нажмите кнопку **{{ ui-key.yacloud.common.save }}**. Если требуется, добавьте другие правила.
  1. Нажмите кнопку **{{ ui-key.yacloud.common.save }}**.

- CLI {#cli}
  
  Чтобы создать группу с правилом для IPv4 CIDR, выполните команду:

  ```bash
  yc vpc security-group create \
    --name test-sg-cli \
    --rule "direction=ingress,port=443,protocol=tcp,v4-cidrs=[10.0.0.0/24]" \
    --network-id c645mh47vscb********
  ```

  Где:

  * `name` — имя группы безопасности.
  * `rule` — описание правила:
    * `direction` — направление трафика. `ingress` — входящий трафик, `egress` — исходящий.
    * `port` — порт для получения или передачи трафика. Также можно указать диапазон портов с помощью параметров `from-port` и `to-port`.
    * `protocol` — протокол передачи данных. Возможные значения: `tcp`, `udp`, `icmp`, `esp`, `ah`, `any`.
    * `v4-cidrs` — список CIDR IPv4 и масок подсетей, откуда или куда будет поступать трафик.
    * `network-id` — идентификатор сети, к которой будет подключена группа безопасности.

  Чтобы создать группу с правилом разрешающим трафик от всех ресурсов другой группы безопасности, выполните команду:

  ```bash
  yc vpc security-group create \
    --name allow-connection-from-app \
    --rule "direction=ingress,port=5642,protocol=tcp,security-group-id=enp099cqehlfvabec36d" \
    --network-name infra2
  ```

  Где:

  * `name` — имя группы безопасности.
  * `rule` — описание правила:
    * `direction` — направление трафика. `ingress` — входящий трафик, `egress` — исходящий.
    * `port` — порт для получения или передачи трафика. Также можно указать диапазон портов с помощью параметров `from-port` и `to-port`.
    * `protocol` — протокол передачи данных. Возможные значения: `tcp`, `udp`, `icmp`, `esp`, `ah`, `any`.
    * `security-group-id` — идентификатор группы безопасности, для которой разрешен трафик в сторону создаваемой группы безопасности по порту 443.
  * `network-name` — имя сети, к которой будет подключена группа безопасности.

- {{ TF }} {#tf}

  {% include [terraform-install](../../_includes/terraform-install.md) %}

  Чтобы создать группу безопасности с несколькими правилами: 
    
  1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:

     * `name` – имя группы безопасности.
     * `description` – опциональное описание группы безопасности.
     * `network_id` – идентификатор сети, которой будет назначена группа безопасности.
     * `ingress` и `egress` – параметры правил для входящего и исходящего трафика:
       * `protocol` – протокол передачи трафика. Возможные значения: `tcp`, `udp`, `icmp`, `esp`, `ah`, `any`.
       * `description` – опциональное описание правила.
       * `v4_cidr_blocks` — список CIDR и масок подсетей, откуда или куда будет поступать трафик.
       * `port` – порт для трафика.
       * `from-port` — первый порт из диапазона портов для трафика. 
       * `to-port` — последний порт из диапазона портов для трафика.

     Пример структуры конфигурационного файла:

     ```
     provider "yandex" {
       token     = "<OAuth_или_статический_ключ_сервисного_аккаунта>"
       folder_id = "<идентификатор_каталога>"
       zone      = "{{ region-id }}-a"
     }

     resource "yandex_vpc_security_group" "test-sg" {
       name        = "Test security group"
       description = "Description for security group"
       network_id  = "<идентификатор_сети>"

       ingress {
         protocol       = "TCP"
         description    = "Rule description 1"
         v4_cidr_blocks = ["10.0.1.0/24", "10.0.2.0/24"]
         port           = 8080
       }
     
       ingress {
         protocol          = "ANY"
         description       = "Разрешает взаимодействие между ресурсами текущей группы безопасности"
         predefined_target = "self_security_group"
         from_port         = 0
         to_port           = 65535
       }

       ingress {
         protocol           = "TCP"
         description        = "Разрешает подключение по порту 27017 со стороны ресурсов с группой безопасности sg-frontend"
         security_group_id  = yandex_vpc_security_group.sg-frontend.id
         port               = 27017
       }

       egress {
         protocol       = "ANY"
         description    = "Rule description 2"
         v4_cidr_blocks = ["10.0.1.0/24", "10.0.2.0/24"]
         from_port      = 8090
         to_port        = 8099
       }
     }
     ```

     Более подробную информацию о ресурсах, которые вы можете создать с помощью {{ TF }}, см. в [документации провайдера]({{ tf-provider-link }}/).
     
  2. Проверьте корректность конфигурационных файлов.
     
     1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
     2. Выполните проверку с помощью команды:
        ```
        terraform plan
        ```
     Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, {{ TF }} на них укажет. 
        
  3. Разверните облачные ресурсы.

     1. Если в конфигурации нет ошибок, выполните команду:
        ```
        terraform apply
        ```
     2. Подтвердите создание ресурсов.
     
     После этого в указанном каталоге будут созданы все требуемые ресурсы. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-main }}).

- API {#api}

  Воспользуйтесь методом REST API [create](../api-ref/SecurityGroup/create.md) для ресурса [SecurityGroup](../api-ref/SecurityGroup/index.md) или вызовом gRPC API [SecurityGroupService/Create](../api-ref/grpc/SecurityGroup/create.md) и передайте в запросе:

  * Идентификатор каталога, в котором будет размещена группа безопасности, в параметре `folderId`.
  * Идентификатор сети, в которой будет размещена группа безопасности, в параметре `networkId`.
  * Настройки правил группы безопасности в массиве `ruleSpecs[]`:

    * Направление трафика, для которого задается правило, в параметре `ruleSpecs[].direction`. Возможные значения:

      * `ingress` — входящий трафик;
      * `egress` — исходящий трафик.

    * Имя протокола передачи трафика в параметре `ruleSpecs[].protocolName`. Возможные значения: `tcp`, `udp`, `icmp`, `esp`, `ah`, `any`.
    * Список CIDR и масок подсетей, откуда или куда будет поступать трафик, в параметре `ruleSpecs[].cidrBlocks.v4CidrBlocks[]`. Если правило задается для передачи трафика в группу безопасности, то вместо этого передайте идентификатор группы безопасности в параметре `ruleSpecs[].securityGroupId`.
    * Первый порт из диапазона портов для трафика в параметре `ruleSpecs[].ports.fromPort`. Возможные значения: от `0` до `65535`.
    * Последний порт из диапазона портов для трафика в параметре `ruleSpecs[].ports.toPort`. Возможные значения: от `0` до `65535`.

{% endlist %}

# Сделать публичный IP-адрес виртуальной машины статическим

_Статический IP-адрес_ — постоянный IP-адрес, который не изменяется при остановке виртуальной машины.

### Использование статических IP-адресов {#use-of-static-IP-addresses}

Публичные статические IP-адреса тарифицируются по отдельному тарифу. Подробнее читайте в разделе [{#T}](../../../vpc/pricing.md#prices-public-ip) документации сервиса {{ vpc-name }}.

Чтобы сделать статическим публичный IP-адрес, привязанный к [сетевому интерфейсу](../../concepts/network.md) виртуальной машины:

{% list tabs group=instructions %}

- Консоль управления {#console}

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, которому принадлежит ВМ.
  1. Выберите сервис **{{ ui-key.yacloud.iam.folder.dashboard.label_compute }}**.
  1. Выберите виртуальную машину.
  1. Определите публичный IP-адрес виртуальной машины: он указан в поле **{{ ui-key.yacloud.compute.instance.overview.label_public-ipv4 }}** блока сетевого интерфейса в секции **{{ ui-key.yacloud.compute.instance.overview.section_network }}** на странице виртуальной машины.
  1. Сделайте публичный IP-адрес статическим. Подробнее читайте в разделе [{#T}](../../../vpc/operations/set-static-ip.md) документации сервиса {{ vpc-name }}.

{% endlist %}
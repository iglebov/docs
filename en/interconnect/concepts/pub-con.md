# Public connection

A public connection provides access to {{ yandex-cloud }} [services](#svc-list). A public connection is set up within a [trunk](./trunk.md) and has its own unique **VLAN-ID**. A single trunk can host multiple public connections enabling access to various combinations of [services](#svc-list).

The maximum IP MTU for a public connection is **1,500 bytes**. {{ yandex-cloud }} equipment does not support changing the IP MTU.


## List of services {#svc-list}

Each {{ yandex-cloud }} service has its own entry point: `API Endpoint`. You can view the list of entry points for services [here](https://{{ api-host }}/endpoints). Each entry point has its own ID and address that consists of `FQDN API Endpoint` and the number of the port to which this service gets requests.

Below, you can see the list of {{ yandex-cloud }} services you can access through a public connection:

{% include [svc-list](../../_includes/interconnect/svc-list.md) %}

Technically, a public connection ensures connectivity between your infrastructure and the IP address to which the respective service's `FQDN API Endpoint` is converted. FQDN is converted to an IP address through DNS.

For example, if you want to get access from your infrastructure to [{{ objstorage-name }}](../../storage/) through a service connection, the {{ yandex-cloud }} equipment will announce the `{{ cic-pbc-svc1-ip }}` prefix to your router over BGP. This prefix maps to the `{{ s3-storage-host }}` API Endpoint FQDN for [{{ objstorage-name }}](../../storage/).

You need to set up traffic routing in your infrastructure so that traffic to {{ yandex-cloud }} [services](#svc-list) goes through the devices handling [NAT functions](#pub-nat) for the public connection.


## Point-to-point subnet {#pub-address}

You can set up a point-to-point subnet for public connection using the following methods:

1. Using IPv4 addresses from the {{ yandex-cloud }} [address pool](../../vpc/concepts/ips.md). With this method, {{ yandex-cloud }} assigns a `/31` **point-to-point subnet** to the customer. The customer must use a private BGP ASN to set up BGP peering.
1. Using private (RFC-1918) or custom public IPv4 addresses. This method is used if the customer plans to announce their custom public IP prefixes via the point-to-point subnet. In this case, the customer must follow the [recommendations](#pub-bgp) for setting up BGP peering listed below.


{% note alert %}

[Services](#svc-list) accessible through a public connection are hosted in [our own data centers](../../overview/concepts/geo-scope.md). Traffic within a public connection between your infrastructure and the [services](#svc-list) stays within {{ yandex-cloud }}.

{% endnote %}

{% include [bgp](../../_includes/interconnect/bgp.md) %}


## Setting up BGP peering when announcing custom IP prefixes {#pub-bgp}

If you need to announce your own public IP prefixes for setting up BGP peering for a public connection, follow these rules:

1. Your public IP prefixes must be properly registered. This involves creating the [Route Object](https://docs.db.ripe.net/entire-documentation-HTML.html#creating-route-objects) and [Route Origin Authorization](https://www.ripe.net/manage-ips-and-asns/resource-management/rpki/resource-certification-roa-management/) objects with the regional registrar.
1. A public BGP ASN can only be used for setting up BGP peering between your equipment and {{ yandex-cloud }} equipment. Using private BGP ASNs for such communication is not allowed.
1. Your IP prefixes must be longer than or equal to `/24`. {{ yandex-cloud }} equipment will discard any more specific prefixes, i.e., `/25` to `/32`.

## NAT functions {#pub-nat}

When setting up a public connection (type 1 point-to-point subnet) with IPv4 addresses provided by {{ yandex-cloud }}, you need to implement [NAT](https://en.wikipedia.org/wiki/Network_address_translation) on your equipment to route your traffic correctly across {{ yandex-cloud }} services. You can implement NAT in the following ways:

* Running a NAT function on your equipment (router) which establishes the public connection. All public connection traffic originates from the IPv4 address of the router interface in the [point-to-point subnet](#pub-address). In this case, your router handling the public connection must announce the point-to-point subnet prefix to the {{ yandex-cloud }} equipment over BGP.

* Running a NAT function on your equipment that is not used for the public connection, e.g., on a server or firewall. In this case, {{ yandex-cloud }} additionally allocates an auxiliary IPv4 address (`/32` prefix), and your router handling the public connection will announce this prefix over BGP to the {{ yandex-cloud }} equipment.

When using custom IPv4 addresses (type 2 point-to-point subnet), NAT functions must utilize those IP addresses.


## Use cases {#examples}

* [{#T}](../tutorials/trunk-pub-add.md)
* [{#T}](../tutorials/pub-add.md)
* [{#T}](../tutorials/pub-del.md)
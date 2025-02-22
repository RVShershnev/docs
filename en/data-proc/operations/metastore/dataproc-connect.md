---
noIndex: true
---

# Connecting {{ dataproc-name }} to {{ metastore-name }}

{% note info %}

To use the {{ metastore-name }} server, a {{ dataproc-name }} cluster must have the following components:

* `SPARK`
* `YARN`
* `HIVE`

{% endnote %}

{% list tabs %}

- Management console

   1. [Create a {{ metastore-name }} server](./cluster-create.md).
   1. When [creating](../cluster-create.md) or [updating](../cluster-update.md) a {{ dataproc-name }} cluster, specify the following [property](../../concepts/settings-list.md):

      ```text
      spark:spark.hive.metastore.uris=thrift://<{{ metastore-name }} IP address>:{{ port-metastore }}
      ```

      To find out the {{ metastore-name }} IP address, go to the {{ metastore-name }} page in the management console. You will see the IP address in the **{{ ui-key.yacloud.common.section-base }}** section.

   1. If the {{ metastore-name }} server and the {{ dataproc-name }} cluster are hosted in different cloud networks, set up routing between these cloud networks so that the {{ metastore-name }} subnet is accessible from the {{ dataproc-name }} subnet.

      There are [multiple ways](../../../tutorials/routing/index.md) to configure routing. For example, you can [create an IPsec tunnel](../../../tutorials/routing/ipsec-vpn.md).

   1. If the cloud network uses [security groups](../../../vpc/concepts/security-groups.md), [set up the security group](../../../vpc/operations/security-group-add-rule.md) of the {{ dataproc-name }} cluster to work with {{ metastore-name }}. To do this, add the following rule for outgoing traffic:

      * Port range: `{{ port-metastore }}`.
      * Protocol: `Any`.
      * Source: `CIDR`.
      * CIDR blocks: `0.0.0.0/0`.

{% endlist %}

For an example of using {{ dataproc-name }} with enabled {{ metastore-name }}, see the [{#T}](../../tutorials/dataproc-to-dataproc.md) tutorial.

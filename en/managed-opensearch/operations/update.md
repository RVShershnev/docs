---
title: "Changing {{ OS }} cluster settings"
description: "After creating an {{ OS }} cluster, you can edit its service settings."
keywords:
  - OpenSearch settings
  - OpenSearch cluster settings
  - OpenSearch
---

# Changing {{ OS }} cluster settings

After creating a cluster, you can edit its service settings. To update the configuration of individual host groups, follow the instructions in [Managing host groups](host-groups.md#update-host-group).

## Updating service settings {#change-service-settings}

{% list tabs %}

- Management console

   1. In the [management console]({{ link-console-main }}), go to the folder page and select **{{ mos-name }}**.
   1. Select a cluster and click ![pencil](../../_assets/pencil.svg) **Edit cluster** on the top panel.
   1. Under **Service settings**:

      1. Change the `admin` user password.
      1. If required, change additional cluster settings:

         {% include [extra-settings](../../_includes/mdb/mos/extra-settings.md) %}

   1. Click **Save**.

- API

   To change service settings, use the [update](../api-ref/Cluster/update.md) REST API method for the [Cluster](../api-ref/Cluster/index.md) resource or the [ClusterService/Update](../api-ref/grpc/cluster_service.md#Update) gRPC API call and provide the following in the request:

   * Cluster ID in the `clusterId` parameter.

      {% include [get-cluster-id](../../_includes/managed-opensearch/get-cluster-id.md) %}

   * New `admin` user password in the `configSpec.adminPassword` parameter.
   * List of plugins in the `configSpec.opensearchSpec.plugins` parameter. The plugins that are not included in the list will be disabled.
   * Settings for access from other services in the `configSpec.access` parameter.

   
   * ID of the [service account](../../iam/concepts/users/service-accounts.md) used for cluster operations in the `serviceAccountId` parameter.


   * Cluster deletion protection settings in the `deletionProtection` parameter.

      {% include [deletion-protection-limits-db](../../_includes/mdb/deletion-protection-limits-db.md) %}

   * Settings for the [maintenance window](../concepts/maintenance.md) (including those for disabled clusters) in the `maintenanceWindow` parameter.

   {% include [Note API updateMask](../../_includes/note-api-updatemask.md) %}

{% endlist %}

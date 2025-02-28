---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Start an instance group

When an instance group is started, all its stopped instances are started. You can start an individual instance, for example, for diagnostics, but to enable [automatic recovery](../../concepts/instance-groups/autohealing.md) and [scaling](../../concepts/instance-groups/scale.md), you must start the entire instance group.

{% note warning %}

If an instance group is stopped by {{ yandex-cloud }} because it was blocked for failure to pay, the instance group can be started again only after the block is removed.

{% endnote %}

{% list tabs %}

- Management console
  1. Open the folder page in the management console.
  1. Select **{{ compute-full-name }}**.
  1. On the **Virtual machines** page, go to the **Instance groups** tab.
  1. Select the instance group and click ![image](../../../_assets/horizontal-ellipsis.svg), and select **Start**.

- CLI

  {% include [cli-install.md](../../../_includes/cli-install.md) %}

  {% include [default-catalogue.md](../../../_includes/default-catalogue.md) %}

  1. View a description of the start instance group command in the CLI:

     ```
     $ {{ yc-compute-ig }} start --help
     ```

  1. Get a list of instance groups in the default folder:

      {% include [instance-group-list.md](../../../_includes/instance-groups/instance-group-list.md) %}

  1. Select the group `ID` or `NAME` (for example, `first-instance-group`).

  1. Start an instance group in the default folder:

      ```
      $ {{ yc-compute-ig }} start first-instance-group
      ```

     {{ ig-name }} begins to start instances in the group. When all instances are started, the group status switches to `ACTIVE`.

- API

  You can start an instance group using the API method [start](../../api-ref/InstanceGroup/start.md).

  To request a list of available groups, use the method [listInstances](../../api-ref/InstanceGroup/listInstances.md).

{% endlist %}


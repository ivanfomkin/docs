---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Удалить реестр

{% note info %}

Удалить можно только пустой реестр. Не забудьте [удалить Docker-образы из реестра](../docker-image/docker-image-delete.md) перед началом операции.

{% endnote %}

Для обращения к [реестру](../../concepts/registry.md) используйте его идентификатор или имя. Как узнать идентификатор или имя реестра,
читайте в разделе [Получить информацию об имеющихся реестрах](registry-list.md).

{% list tabs %}

- Консоль управления
  
  Чтобы удалить [реестр](../../concepts/registry.md):
  1. Откройте раздел **Container Registry** в каталоге, где требуется удалить реестр.
  1. Нажмите значок ![image](../../../_assets/vertical-ellipsis.svg) в строке реестра, который требуется удалить.
  1. В открывшемся меню нажмите кнопку **Удалить**.
  1. В открывшемся окне нажмите кнопку **Удалить**.
  
  
- CLI
  
  {% include [cli-install](../../../_includes/cli-install.md) %}
  
  1. Удалите реестр:
  
      ```
      $ yc container registry delete new-reg
      ..done
      ```
  
  1. Проверьте, что реестр действительно удален:
  
      ```
      $ yc container registry list
      +----+------+-----------+
      | ID | NAME | FOLDER ID |
      +----+------+-----------+
      +----+------+-----------+
      ```
  
- API
  
  Чтобы удалить реестр, воспользуйтесь методом [delete](../../api-ref/Registry/delete.md) для ресурса [Registry](../../api-ref/Registry/).
  
  
{% endlist %}

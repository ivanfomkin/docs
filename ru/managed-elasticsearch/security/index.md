---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Управление доступом к {{ mes-name }}


В этом разделе вы узнаете:

* [на какие ресурсы можно назначить роль](#resources);
* [какие роли действуют в сервисе](#roles-list);
* [какие роли необходимы](#required-roles) для того или иного действия.

{% include [about-access-management](../../_includes/iam/about-access-management.md) %}

## На какие ресурсы можно назначить роль {#resources}

{% include [basic-resources](../../_includes/iam/basic-resources-for-access-control.md) %}

Чтобы разрешить доступ к ресурсам сервиса {{ mes-name }} (кластеры и хосты, резервные копии кластеров, учетные записи), назначьте пользователю нужные роли на каталог или облако, в котором содержатся эти ресурсы.

## Какие роли действуют в сервисе {#roles-list}

На диаграмме показано, какие роли есть в сервисе и как они наследуют разрешения друг друга. Например, в `editor` входят все разрешения `viewer`. После диаграммы дано описание каждой роли.

![image](../../_assets/security/service-roles-hierarchy.svg)

Роли, действующие в сервисе:

* Сервисные роли:
    * {% include [resource-manager.clouds.owner](../../_includes/iam/roles/short-descriptions/resource-manager.clouds.owner.md) %}
    * {% include [resource-manager.clouds.member](../../_includes/iam/roles/short-descriptions/resource-manager.clouds.member.md) %}
* Примитивные роли:
    * {% include [viewer](../../_includes/iam/roles/short-descriptions/viewer.md) %}
    * {% include [editor](../../_includes/iam/roles/short-descriptions/editor.md) %}
    * {% include [admin](../../_includes/iam/roles/short-descriptions/admin.md) %}

## Какие роли мне необходимы {#required-roles}

В таблице ниже перечислены возможные действия с ресурсами кластера и роли, которые нужны для их выполнения.

Действие | Методы | Необходимые роли
----- | ----- | -----
**Просмотр информации** | |
Просмотр информации о кластере и связанных ресурсах | `get`, `list` | `viewer`, `editor` или `admin` на каталог с кластером
**Управление ресурсами** | |
Создание кластеров в каталоге | `create` | `editor` или `admin` на каталог с кластером
Изменение, удаление кластеров и связанных ресурсов | `update`, `delete` | `editor` или `admin` на каталог с кластером
**Управление доступом к ресурсам** | |
[Создание](../operations/cluster-users.md#adduser), [изменение](../operations/cluster-users.md#updateuser), [удаление](../operations/cluster-users.md#removeuser) учетных записей в кластере | `create`, `update`, `delete` | `editor` или `admin` на каталог с кластером
[Назначение роли](../../iam/operations/roles/grant.md), [отзыв роли](../../iam/operations/roles/revoke.md) и просмотр назначенных ролей на каталог или облако | `setAccessBindings`, `updateAccessBindings`, `listAccessBindings` | `admin` на каталог с кластером или облако

## Что дальше {#whats-next}

* [Как назначить роль](../../iam/operations/roles/grant.md).
* [Как отозвать роль](../../iam/operations/roles/revoke.md).
* [Подробнее об управлении доступом в {{ yandex-cloud }}](../../iam/concepts/access-control/index.md).
* [Подробнее о наследовании ролей](../../resource-manager/concepts/resources-hierarchy.md#access-rights-inheritance).

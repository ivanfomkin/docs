---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Создание кластера {{ MS }}

Кластер {{ MS }} — это один или несколько хостов базы данных, между которыми можно настроить репликацию. Репликация работает по умолчанию в любом кластере из более чем 1 хоста: хост-мастер принимает запросы на запись, синхронно дублирует изменения в основной реплике и асинхронно — во всех остальных.

{% note info %}

Если хранилище баз данных заполнится на 95%, кластер перейдет в режим только чтения. Рассчитывайте и увеличивайте необходимый размер хранилища заранее.

{% endnote %}


Количество хостов, которые можно создать вместе с {{ MS }}-кластером, зависит от выбранного [типа хранилища](../concepts/storage.md):

* При использовании **локального хранилища** вы можете создать кластер из трех или более хостов (минимум три хоста необходимо, чтобы обеспечить отказоустойчивость).
* При использовании сетевого хранилища:
    * Если выбрано **стандартное** или **быстрое сетевое хранилище**, вы можете добавить любое количество хостов в пределах [текущей квоты](../concepts/limits.md).
    * Если выбрано **нереплицируемое сетевое хранилище**, вы можете создать кластер из трех или более хостов (минимум три хоста необходимо, чтобы обеспечить отказоустойчивость).
      
После создания кластера в него можно добавить дополнительные хосты, если для этого достаточно [ресурсов каталога](../concepts/limits.md).

## Как создать кластер {{ MS }} {#create-cluster}

{% list tabs %}

- Консоль управления

  1. В консоли управления выберите каталог, в котором нужно создать кластер баз данных.
  1. Выберите сервис **{{ mms-name }}**.
  1. Нажмите кнопку **Создать кластер**.
  1. Введите имя кластера в поле **Имя кластера**. Имя кластера должно быть уникальным в рамках каталога.
  1. Выберите окружение, в котором нужно создать кластер (после создания кластера окружение изменить невозможно):
      - `PRODUCTION` — для стабильных версий ваших приложений.
      - `PRESTABLE` — для тестирования, в том числе самого сервиса {{ mms-short-name }}. В Prestable-окружении раньше появляются новая функциональность, улучшения и исправления ошибок. При этом не все обновления обеспечивают обратную совместимость.
  1. Выберите версию СУБД. На текущий момент поддерживается версия `2016 ServicePack 2` следующих редакций:
     * Standard Edition.
     * Enterprise Edition.

     Подробнее см. в разделе [{#T}](../concepts/index.md).

  1. Выберите класс хостов — он определяет технические характеристики виртуальных машин, на которых будут развернуты хосты баз данных. Все доступные варианты перечислены в разделе [{#T}](../concepts/instance-types.md). При изменении класса хостов для кластера меняются характеристики всех уже созданных хостов.
  1. В блоке **Размер хранилища**:

           
      - Выберите [тип хранилища](../concepts/storage.md) — более гибкое сетевое (`network-hdd`, `network-ssd` или `network-ssd-nonreplicated`) или более быстрое локальное хранилище (`local-ssd`). 

        При выборе типа хранилища обратите внимание, что:
        - Размер локального хранилища можно менять только с шагом 100 ГБ.
        - Размер нереплицируемого сетевого хранилища можно менять только с шагом 93 ГБ.

      - Выберите объем, который будет использоваться для данных и резервных копий. Подробнее о том, как занимают пространство резервные копии, см. раздел [{#T}](../concepts/backup.md).
  1. В блоке **База данных** укажите атрибуты базы данных:

      - Имя базы данных. Это имя должно быть уникальным в рамках каталога и содержать только латинские буквы, цифры и подчеркивания.
      - Имя пользователя — владельца базы данных. Это имя должно содержать только латинские буквы, цифры и подчеркивания. По умолчанию новому пользователю выделяется 50 подключений к каждому хосту кластера.
      - Пароль пользователя, от 8 до 128 символов.

  1. В блоке **Хосты** выберите параметры хостов баз данных, создаваемых вместе с кластером. Вы можете добавить либо один, либо три и более хостов. По умолчанию каждый хост создается в отдельной подсети. Чтобы выбрать конкретную подсеть для хоста, нажмите значок ![image](../../_assets/pencil.svg) в строке этого хоста и выберите необходимые зону доступности и подсеть.

     {% note warning %}

     * Если вы выбрали редакцию **Standard Edition**, то вы можете создать кластер только из одного хоста. Такой кластер не обеспечивает отказоустойчивости. Подробнее см. в разделе [{#T}](../concepts/index.md).
     * На текущий момент вы можете создать кластер редакции **Enterprise Edition** либо из одного, либо из трех хостов. Обратите внимание, что если в блоке **Хранилище** выбран `local-ssd` или `network-ssd-nonreplicated`, то необходимо добавить не менее трех хостов в кластер.

     {% endnote %}

  1. При необходимости задайте [настройки СУБД](../concepts/settings-list.md).
  1. Нажмите кнопку **Создать кластер**.

- Terraform

    {% include [terraform-definition](../../_includes/solutions/terraform-definition.md) %}

    Если у вас еще нет {{ TF }}, [установите его и настройте провайдер](../../solutions/infrastructure-management/terraform-quickstart.md#install-terraform).

    Чтобы создать кластер:

    1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:

        - Кластер базы данных — описание кластера и его хостов. При необходимости здесь же можно задать [настройки СУБД](../concepts/settings-list.md).
        - Сеть — описание [облачной сети](../../vpc/concepts/network.md#network), в которой будет расположен кластер. Если подходящая сеть у вас уже есть, описывать ее повторно не нужно.
        - Подсети — описание [подсетей](../../vpc/concepts/network.md#network), к которым будут подключены хосты кластера. Если подходящие подсети у вас уже есть, описывать их повторно не нужно.

        Пример структуры конфигурационного файла:

        ```hcl
        resource "yandex_mdb_sqlserver_cluster" "<имя кластера>" {
          name               = "<имя кластера>"
          environment        = "<окружение: PRESTABLE или PRODUCTION>"
          network_id         = "<идентификатор сети>"
          version            = "<версия: 2016sp2std или 2016sp2ent>"
          security_groups_id = ["<список идентификаторов групп безопасности>"]

          resources {
            resource_preset_id = "<класс хоста>"
            disk_type_id       = "<тип хранилища>"
            disk_size          = <размер хранилища в гигабайтах>
          }

          host {
            zone      = "<зона доступности>"
            subnet_id = "<идентификатор подсети>"
          }

          database = {
            name = "<имя базы>"
          }

          user {
            name     = "<имя пользователя>"
            password = "<пароль>"

            permission {
              database_name = "<имя базы>"
              roles         = ["<список ролей>"]
            }
          }

          backup_window_start {
            hours   = <Час начала резервного копирования>
            minutes = <Минута начала резервного копирования>
          }
        }

        resource "yandex_vpc_network" "<имя сети>" { name = "<имя сети>" }

        resource "yandex_vpc_subnet" "<имя подсети>" {
          name           = "<имя подсети>"
          zone           = "<зона доступности>"
          network_id     = "<идентификатор сети>"
          v4_cidr_blocks = ["<диапазон>"]
        }
        ```

       Более подробную информацию о ресурсах, которые вы можете создать с помощью {{ TF }}, см. в [документации провайдера]({{ tf-provider-mms }}).

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Создайте кластер.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

        После этого в указанном каталоге будут созданы все требуемые ресурсы, а в терминале отобразятся IP-адреса виртуальных машин. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-main }}).

- API

  Чтобы создать кластер, воспользуйтесь методом API [create](../api-ref/Cluster/create.md) и передайте в запросе:
  - Идентификатор каталога, в котором должен быть размещен кластер, в параметре `folderId`.
  - Имя кластера в параметре `name`.
  - Конфигурацию кластера в параметре `configSpec`.
  - Конфигурацию хостов кластера в одном или нескольких параметрах `hostSpecs`.
  - Конфигурацию баз данных кластера в одном или нескольких параметрах `databaseSpecs`.
  - Конфигурацию учетных записей баз данных кластера в одном или нескольких параметрах `userSpecs`.
  - Идентификатор сети в параметре `networkId`.

{% endlist %}

## Примеры {#examples}

### Создание кластера с одним хостом

{% list tabs %}

- Terraform

    Допустим, нужно создать {{ MS }}-кластер и сеть для него со следующими характеристиками:

    - С именем `mssql-1`.
    - В окружении `PRODUCTION`.
    - С версией {{ MS }} `2016 ServicePack 2` и редакцией `Standard Edition`.
    - В облаке с идентификатором `{{ tf-cloud-id }}`.
    - В каталоге с идентификатором `{{ tf-folder-id }}`.
    - В новой сети `mynet`.
    - В новой группе безопасности `ms-sql-sg`, разрешающей подключение к кластеру из интернета через порт `{{ port-mms }}`.
    - С одним хостом класса `s2.small` в новой подсети `mysubnet`, в зоне доступности `{{ zone-id }}`. Подсеть `mysubnet` будет иметь диапазон `10.5.0.0/24`.
    - С быстрым сетевым хранилищем объемом 32 Гб.
    - С базой данных `db1`.
    - С пользователем `user1` и паролем `user1user1`. Этот пользователь будет владельцем базы `db1` ([предопределенная роль `DB_OWNER`](./grant.md#predefined-db-roles)).

    Конфигурационный файл для такого кластера выглядит так:

    ```hcl
    terraform {
      required_providers {
        yandex = {
          source = "yandex-cloud/yandex"
        }
      }
    }

    provider "yandex" {
      token     = "<OAuth или статический ключ сервисного аккаунта>"
      cloud_id  = "{{ tf-cloud-id }}"
      folder_id = "{{ tf-folder-id }}"
      zone      = "{{ zone-id }}"
    }

    resource "yandex_mdb_sqlserver_cluster" "mssql-1" {
      name               = "mssql-1"
      environment        = "PRODUCTION"
      version            = "2016sp2std"
      network_id         = yandex_vpc_network.mynet.id
      security_group_ids = [yandex_vpc_security_group.ms-sql-sg.id]

      resources {
        resource_preset_id = "s2.small"
        disk_type_id       = "network-ssd"
        disk_size          = 32
      }

      host {
        zone             = "{{ zone-id }}"
        subnet_id        = yandex_vpc_subnet.mysubnet.id
        assign_public_ip = true
      }

      database {
        name = "db1"
      }

      user {
        name     = "user1"
        password = "user1user1"
        permission {
          database_name = "db1"
          roles         = ["OWNER"]
        }
      }
    }

    resource "yandex_vpc_network" "mynet" { name = "mynet" }

    resource "yandex_vpc_subnet" "mysubnet" {
      name           = "mysubnet"
      zone           = "{{ zone-id }}"
      network_id     = yandex_vpc_network.mynet.id
      v4_cidr_blocks = ["10.5.0.0/24"]
    }

    resource "yandex_vpc_security_group" "ms-sql-sg" {
      name       = "ms-sql-sg"
      network_id = yandex_vpc_network.mynet.id

      ingress {
        description    = "Public access to SQL Server"
        port           = {{ port-mms }}
        protocol       = "TCP"
        v4_cidr_blocks = ["0.0.0.0/0"]
      }
    }
    ```

{% endlist %}

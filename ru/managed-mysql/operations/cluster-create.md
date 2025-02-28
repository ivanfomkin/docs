---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Создание {{ MY }}-кластера

{{ MY }}-кластер — это один или несколько хостов базы данных, между которыми можно настроить репликацию. Репликация работает по умолчанию в любом кластере из более чем 1 хоста: хост-мастер принимает запросы на запись, синхронно дублирует изменения в основной реплике и асинхронно — во всех остальных.


Количество хостов, которые можно создать вместе с {{ MY }}-кластером, зависит от выбранного [типа хранилища](../concepts/storage.md):

* При использовании **локального хранилища** вы можете создать кластер из трех или более хостов (минимум три хоста необходимо, чтобы обеспечить отказоустойчивость).
* При использовании сетевого хранилища:
    * Если выбрано **стандартное** или **быстрое сетевое хранилище**, вы можете добавить любое количество хостов в пределах [текущей квоты](../concepts/limits.md).
    * Если выбрано **нереплицируемое сетевое хранилище**, вы можете создать кластер из трех или более хостов (минимум три хоста необходимо, чтобы обеспечить отказоустойчивость).
    
После создания кластера в него можно добавить дополнительные хосты, если для этого достаточно [ресурсов каталога](../concepts/limits.md).

{% note info %}

Если хранилище баз данных заполнится на 95%, кластер перейдет в режим только чтения. Увеличивайте размер хранилища заранее.

{% endnote %}

## Как создать кластер {{ MY }} {#create-cluster}

{% list tabs %}

- Консоль управления

  1. В консоли управления выберите каталог, в котором нужно создать кластер БД.
  1. Выберите сервис **{{ mmy-name }}**.
  1. Нажмите кнопку **Создать кластер**.
  1. Введите имя кластера в поле **Имя кластера**. Имя кластера должно быть уникальным в рамках каталога.
  1. Выберите окружение, в котором нужно создать кластер (после создания кластера окружение изменить невозможно):
      - `PRODUCTION` — для стабильных версий ваших приложений.
      - `PRESTABLE` — для тестирования, в том числе самого сервиса {{ mmy-short-name }}. В Prestable-окружении раньше появляются новая функциональность, улучшения и исправления ошибок. При этом не все обновления обеспечивают обратную совместимость.
  1. Выберите версию СУБД.
  1. Выберите класс хостов — он определяет технические характеристики виртуальных машин, на которых будут развернуты хосты БД. Все доступные варианты перечислены в разделе [{#T}](../concepts/instance-types.md). При изменении класса хостов для кластера меняются характеристики всех уже созданных хостов.
  1. В блоке **Размер хранилища**:
      - Выберите [тип хранилища](../concepts/storage.md) — более гибкое сетевое (`network-hdd`, `network-ssd` или `network-ssd-nonreplicated`) или более быстрое локальное хранилище (`local-ssd`).
        
        При выборе типа хранилища обратите внимание, что:
        - Размер локального хранилища можно менять только с шагом 100 ГБ.
        - Размер нереплицируемого сетевого хранилища можно менять только с шагом 93 ГБ.

      - Выберите объем, который будет использоваться для данных и резервных копий. Подробнее о том, как занимают пространство резервные копии, см. раздел [{#T}](../concepts/backup.md).
  1. В блоке **База данных** укажите атрибуты БД:

      - Имя базы данных. Имя БД должно быть уникальным в рамках каталога и содержать только латинские буквы, цифры и подчеркивания.
      - Имя пользователя — владельца БД. Имя пользователя должно содержать только латинские буквы, цифры и подчеркивания.
      - Пароль пользователя, от 8 до 128 символов.

  1. В блоке **Сетевые настройки** выберите облачную сеть для размещения кластера и группы безопасности для сетевого трафика кластера. Может потребоваться дополнительная [настройка групп безопасности](connect.md#configuring-security-group) для того, чтобы можно было подключаться к кластеру.

  1. В блоке **Хосты** выберите параметры хостов БД, создаваемых вместе с кластером. Открыв блок **Расширенные настройки**, вы можете выбрать конкретные подсети для каждого хоста — по умолчанию каждый хост создается в отдельной подсети.

     При настройке параметров хостов обратите внимание, что если в блоке **Хранилище** выбран `local-ssd` или `network-ssd-nonreplicated`, то необходимо добавить не менее трех хостов в кластер.

  1. При необходимости задайте дополнительные настройки кластера:

      {% include [mmy-extra-settings](../../_includes/mdb/mmy-extra-settings-web-console.md) %}

  1. При необходимости задайте [настройки СУБД уровня кластера](../concepts/settings-list.md#dbms-settings).

      {% include [mmy-settings-dependence](../../_includes/mdb/mmy/note-info-settings-dependence.md) %}

  1. Нажмите кнопку **Создать кластер**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы создать кластер:

  1. Проверьте, есть ли в каталоге подсети для хостов кластера:

     ```
     $ yc vpc subnet list
     ```

     Если ни одной подсети в каталоге нет, [создайте нужные подсети](../../vpc/operations/subnet-create.md) в сервисе {{ vpc-short-name }}.

  1. Посмотрите описание команды CLI для создания кластера:

      ```
      $ {{ yc-mdb-my }} cluster create --help
      ```

  1. Укажите параметры кластера в команде создания:

     ```
     $ {{ yc-mdb-my }} cluster create \
        --name=<имя кластера> \
        --environment <окружение, prestable или production> \
        --network-name <имя сети> \
        --host zone-id=<зона доступности>,subnet-id=<идентификатор подсети> \
        --mysql-version <версия MySQL> \
        --resource-preset <класс хоста> \
        --user name=<имя пользователя>,password=<пароль пользователя> \
        --database name=<имя базы данных> \
        --disk-size <размер хранилища в гигабайтах> \
        --disk-type  <network-hdd | network-ssd | local-ssd | network-ssd-nonreplicated> \
        --security-group-ids <список идентификаторов групп безопасности>
     ```

      Идентификатор подсети `subnet-id` необходимо указывать, если в выбранной зоне доступности создано 2 и больше подсетей.

      При необходимости задайте [настройки СУБД](../concepts/settings-list.md#dbms-settings).

- Terraform

  {% include [terraform-definition](../../_includes/solutions/terraform-definition.md) %}

  Если у вас еще нет Terraform, [установите его и настройте провайдер](../../solutions/infrastructure-management/terraform-quickstart.md#install-terraform).

  Чтобы создать кластер:

  1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:

     {% include [terraform-create-cluster-step-1](../../_includes/mdb/terraform-create-cluster-step-1.md) %}

     Пример структуры конфигурационного файла:

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
       cloud_id  = "<идентификатор облака>"
       folder_id = "<идентификатор каталога>"
       zone      = "<зона доступности>"
     }

     resource "yandex_mdb_mysql_cluster" "<имя кластера>" {
       name               = "<имя кластера>"
       environment        = "<окружение, PRESTABLE или PRODUCTION>"
       network_id         = "<идентификатор сети>"
       version            = "<версия MySQL: 5.7 или 8.0>"
       security_group_ids = [ "<список групп безопасности>" ]

       resources {
         resource_preset_id = "<класс хоста>"
         disk_type_id       = "<тип хранилища>"
         disk_size          = "<размер хранилища в гигабайтах>"
       }

       database {
         name = "<имя базы данных>"
       }

       user {
         name     = "<имя пользователя>"
         password = "<пароль пользователя>"
         permission {
           database_name = "<имя базы данных>"
           roles         = ["ALL"]
         }
       }

       host {
         zone      = "<зона доступности>"
         subnet_id = "<идентификатор подсети>"
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

     Более подробную информацию о ресурсах, которые вы можете создать с помощью Terraform, см. в [документации провайдера](https://www.terraform.io/docs/providers/yandex/r/mdb_mysql_cluster.html).

  1. Проверьте корректность конфигурационных файлов.

     {% include [terraform-create-cluster-step-2](../../_includes/mdb/terraform-create-cluster-step-2.md) %}

  1. Создайте кластер.

     {% include [terraform-create-cluster-step-3](../../_includes/mdb/terraform-create-cluster-step-3.md) %}

{% endlist %}

{% note warning %}

Если вы указали идентификаторы групп безопасности при создании кластера, то для подключения к нему может потребоваться дополнительная [настройка групп безопасности](connect.md#configuring-security-groups).

{% endnote %}

## Примеры {#examples}

### Создание кластера с одним хостом {#creating-a-single-host-cluster}

{% list tabs %}

- CLI

  Чтобы создать кластер с одним хостом, передайте один параметр `--host`.

  Допустим, нужно создать {{ MY }}-кластер со следующими характеристиками:

    
    - С именем `my-mysql`.
    - Версии `8.0`.
    - В окружении `production`.
    - В сети `default`.
    - В группе безопасности с идентификатором `{{ security-group }}`.
    - С одним хостом класса `{{ host-class }}` в подсети `{{ subnet-id }}`, в зоне доступности `{{ zone-id }}`.
    - С быстрым сетевым хранилищем (`{{ disk-type-example }}`) объемом 20 Гб.
    - С одним пользователем (`user1`), с паролем `user1user1`.
    - С одной базой данных `db1`, в которой пользователь `user1` имеет полные права (эквивалент `GRANT ALL PRIVILEGES on db1.*`).

  1. Запустите команду создания кластера:

      
      ```bash
      {{ yc-mdb-my }} cluster create \
         --name="my-mysql" \
         --mysql-version 8.0 \
         --environment=production \
         --network-name=default \
         --security-group-ids {{ security-group }} \
         --host zone-id={{ host-net-example }} \
         --resource-preset {{ host-class }} \
         --disk-type {{ disk-type-example }} \
         --disk-size 20 \
         --user name=user1,password="user1user1" \
         --database name=db1
      ```

  1. Запустите команду изменения привилегий пользователя `user1`.

      ```bash
      {{ yc-mdb-my }} user grant-permission user1 \
         --cluster-name="my-mysql" \
         --database=db1 \
         --permissions ALL
      ```

- Terraform

  Допустим, нужно создать {{ MY }}-кластер и сеть для него со следующими характеристиками:

    - С именем `my-mysql`.
    - Версии `8.0`.
    - В окружении `PRESTABLE`.
    - В облаке с идентификатором `{{ tf-cloud-id }}`.
    - В каталоге с идентификатором `{{ tf-folder-id }}`.
    - В новой сети `mynet`.
    - С одним хостом класса `{{ host-class }}` в новой подсети `mysubnet`, в зоне доступности `{{ zone-id }}`. Подсеть `mysubnet` будет иметь диапазон `10.5.0.0/24`.
    - В новой группе безопасности `mysql-sg`, разрешающей подключение к кластеру из интернета через порт `{{ port-mmy }}`.
    - С быстрым сетевым хранилищем (`{{ disk-type-example }}`) объемом 20 ГБ.
    - С одним пользователем (`user1`), с паролем `user1user1`.
    - С одной базой данных `db1`, в которой пользователь `user1` имеет полные права (эквивалент `GRANT ALL PRIVILEGES on db1.*`).

  Конфигурационный файл для такого кластера выглядит так:

  ```go
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

  resource "yandex_mdb_mysql_cluster" "my-mysql" {
    name               = "my-mysql"
    environment        = "PRESTABLE"
    network_id         = yandex_vpc_network.mynet.id
    version            = "8.0"
    security_group_ids = [ yandex_vpc_security_group.mysql-sg.id ]

    resources {
      resource_preset_id = "{{ host-class }}"
      disk_type_id       = "{{ disk-type-example }}"
      disk_size          = 20
    }

    database {
      name = "db1"
    }

    user {
      name     = "user1"
      password = "user1user1"
      permission {
        database_name = "db1"
        roles         = ["ALL"]
      }
    }

    host {
      zone      = "{{ zone-id }}"
      subnet_id = yandex_vpc_subnet.mysubnet.id
    }
  }

  resource "yandex_vpc_network" "mynet" {
    name = "mynet"
  }

  resource "yandex_vpc_security_group" "mysql-sg" {
    name       = "mysql-sg"
    network_id = yandex_vpc_network.mynet.id

    ingress {
      description    = "MySQL"
      port           = {{ port-mmy }}
      protocol       = "TCP"
      v4_cidr_blocks = [ "0.0.0.0/0" ]
    }
  }

  resource "yandex_vpc_subnet" "mysubnet" {
    name           = "mysubnet"
    zone           = "{{ zone-id }}"
    network_id     = yandex_vpc_network.mynet.id
    v4_cidr_blocks = ["10.5.0.0/24"]
  }
  ```

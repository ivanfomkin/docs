---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Создание группы виртуальных машин

Cоздайте группу виртуальных машин с помощью компонента [Instance Groups](../concepts/instance-groups/index.md) в консоли управления {{ yandex-cloud }}.

## Перед началом работы {#before-you-begin}

1. Войдите в [консоль управления](https://console.cloud.yandex.ru) или зарегистрируйтесь. Если вы еще не зарегистрированы, перейдите в консоль управления и следуйте инструкциям.
1. [На странице биллинга](https://console.cloud.yandex.ru/billing) убедитесь, что у вас подключен [платежный аккаунт](../../billing/concepts/billing-account.md), и он находится в статусе `ACTIVE` или `TRIAL_ACTIVE`. Если платежного аккаунта нет, [создайте его](../../billing/quickstart/index.md#create_billing_account).
1. Если у вас еще нет каталога, [создайте его](../../resource-manager/operations/folder/create.md).

## Создайте группу виртуальных машин {#create-ig}

Вы можете создать автоматически масштабируемую группу или группу с фиксированным количеством ВМ. Подробнее читайте в разделе [{#T}](../concepts/instance-groups/scale.md).

{% include [warning.md](../../_includes/instance-groups/warning.md) %}

Чтобы создать группу виртуальных машин:
1. В [консоли управления](https://console.cloud.yandex.ru) выберите каталог, в котором будет создана группа виртуальных машин.
1. В списке сервисов выберите **{{ compute-name }}**.
1. Перейдите на вкладку **Группы виртуальных машин**.
1. Нажмите кнопку **Создать группу**.
1. В блоке **Базовые параметры**:
    - Введите имя и описание группы ВМ. Требования к имени:

        {% include [name-format](../../_includes/name-format.md) %}

        {% include [name-fqdn](../../_includes/compute/name-fqdn.md) %}

    - Выберите [сервисный аккаунт](../../iam/concepts/users/service-accounts.md) из списка или создайте новый. Чтобы иметь возможность создавать, обновлять и удалять виртуальные машины в группе, назначьте сервисному аккаунту роль `editor`. По умолчанию все операции в {{ ig-name }} выполняются от имени сервисного аккаунта.

1. В блоке **Распределение** выберите нужные зоны доступности. Виртуальные машины группы могут находиться в разных зонах и регионах доступности. [Подробнее о географии {{ yandex-cloud }}](../../overview/concepts/geo-scope.md).
1. В блоке **Шаблон виртуальной машины** нажмите кнопку **Задать**, чтобы задать конфигурацию базовой виртуальной машины:
    - В блоке **Базовые параметры**:
        - Введите описание базовой ВМ.
        - Выберите [сервисный аккаунт](../../iam/concepts/users/service-accounts.md) из списка или создайте новый.
    - Выберите публичный [образ](../../compute/operations/images-with-pre-installed-software/get-list.md).
    - В блоке **Диски**:
        - Выберите [тип диска](../../compute/concepts/disk.md#disks_types).
        - Укажите размер диска.
        - (опционально) Нажмите кнопку **Добавить диск**, чтобы добавить дополнительные диски.
    - В блоке **Вычислительные ресурсы**:
        - Выберите [платформу](../../compute/concepts/vm-platforms.md).
        - Укажите [гарантированную долю](../../compute/concepts/performance-levels.md) и необходимое количество vCPU, а также объем RAM.
        - (опционально) Укажите, что виртуальная машина должна быть [прерываемой](../../compute/concepts/preemptible-vm.md).
    - В блоке **Сетевые настройки**:
        - Выберите [облачную сеть](../../compute/concepts/vm.md#network) и подсеть. Если сети нет, создайте ее:
            - Нажмите кнопку **Создать новую сеть**.
            - Укажите имя новой сети и выберите, к какой сети необходимо подключить группу ВМ.
            - Выберите или создайте новую подсеть. У каждой сети должна быть как минимум одна подсеть.
            - Нажмите кнопку **Создать**.
        - В поле **Публичный адрес** выберите способ назначения адреса:
            - **Автоматически** — чтобы назначить случайный IP-адрес из пула адресов {{ yandex-cloud }}.
            - **Без адреса** — чтобы не назначать публичный IP-адрес.
    - В блоке **Доступ**:
        - Если вы выбрали публичный образ на базе Linux:
            - В поле **Логин** введите имя пользователя.
            - В поле **SSH-ключ** вставьте содержимое файла открытого ключа. Пару ключей для подключения по SSH необходимо [создать](../../compute/operations/vm-connect/ssh.md#creating-ssh-keys) самостоятельно.
        - Если вы выбрали публичный образ на базе Windows:
            - В поле **Пароль** задайте пароль пользователя `Administrator`. Пользователь с именем `Administrator` создается автоматически.
        - Нажмите кнопку **Добавить**.
1. В блоке **В процессе создания и обновления разрешено** укажите:
    - На какое количество виртуальных машин можно превышать размер группы.
    - На какое количество виртуальных машин можно уменьшать размер группы.
    - Сколько виртуальных машин можно одновременно создавать.
    - Сколько виртуальных машин можно одновременно удалять.

        Подробнее читайте в разделе [{#T}](../concepts/instance-groups/policies/deploy-policy.md).
1. В блоке **Масштабирование**:
    - Выберите [тип масштабирования](../../compute/concepts/instance-groups/scale.md).
    - Если вы выбрали **Фиксированный**, укажите размер группы.
    - Если вы выбрали **Автоматический**, укажите:
        - Минимальное количество ВМ в одной зоне доступности.
        - Максимальный размер группы.
        - Промежуток измерения нагрузки — период, за который следует усреднять замеры нагрузки для каждой ВМ в группе.
        - Время на разогрев ВМ, в течение которого созданная ВМ не учитывается при замере средней нагрузки на группу.
        - Период стабилизации, в течение которого требуемое количество ВМ в группе не может быть снижено.
        - Начальный размер группы — количество ВМ, которые создаются вместе с группой.
        - Целевой уровень загрузки CPU. Задается в процентах.
1. В блоке **Интеграция с Load Balancer**:
    - (опционально) Нажмите переключатель **Создать целевую группу**. [Целевые группы](../../network-load-balancer/concepts/target-resources.md) нужны для распределения нагрузки [сетевым балансировщиком](../../network-load-balancer/concepts/index.md).
        - Введите имя и описание целевой группы.
1. В блоке **Проверка состояний**:
    - (опционально) Нажмите переключатель **Активировать**.
       - Выберите тип проверки: **HTTP** или **TCP**.
       - Укажите порт из диапазона 1-32767.
       - Если вы выбрали проверку через HTTP, укажите URL, по которому будут выполняться проверки.
       - Укажите время ожидания ответа в секундах.
       - Укажите интервал отправки проверок состояния в секундах.
       - Укажите порог работоспособности — количество успешных проверок, после которого ВМ будет считаться готовой к приему трафика.
       - Укажите порог неработоспособности — количество проваленных проверок, после которого на ВМ перестанет подаваться трафик.
1. Нажмите кнопку **Создать**.
Группа виртуальных машин появится в списке.

## Что дальше {#what-is-next}

- Посмотрите [сценарии создания веб-сервисов в {{ yandex-cloud }}](../../solutions/web/index.md).
- Узнайте, [как работать с группами виртуальных машин](../operations/index.md).
- Прочитайте [ответы на часто задаваемые вопросы](../qa/general.md).
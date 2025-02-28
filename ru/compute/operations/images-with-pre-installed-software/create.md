---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Создать виртуальную машину из публичного образа

Чтобы создать виртуальную машину:

1. Откройте каталог, в котором будет создана виртуальная машина.
1. Нажмите кнопку **Создать ресурс**.
1. Выберите **Виртуальная машина**.
1. В поле **Имя** введите имя виртуальной машины.

    {% include [name-format](../../../_includes/name-format.md) %}

1. Выберите [зону доступности](../../../overview/concepts/geo-scope.md), в которой будет находиться виртуальная машина.
1. Выберите публичный образ c программным обеспечением, которое хотите использовать.
1. В блоке **Вычислительные ресурсы**:
    - Выберите [платформу](../../concepts/vm-platforms.md).
    - Укажите необходимое количество vCPU и объем RAM.

    {% note info %}

    Для создания виртуальной машины из образа **GitLab** требуется не меньше 4 виртуальных ядер (100% vCPU) и 4 ГБ оперативной памяти.

    {% endnote %}

1. В блоке **Сетевые настройки** нажмите кнопку **Добавить сеть**.
1. В открывшемся окне выберите, к какой подсети необходимо подключить виртуальную машину при создании.
1. В поле **Публичный адрес** выберите:
    - **Автоматически** — чтобы назначить публичный IP-адрес автоматически. Адрес выделяется из пула адресов {{ yandex-cloud }}.
    - **Список** — чтобы выбрать публичный IP-адрес из списка статических адресов. Подробнее читайте в разделе [{#T}](../../../vpc/operations/set-static-ip.md) документации сервиса {{ vpc-name }}.
    - **Без адреса** — чтобы не назначать публичный IP-адрес.
1. Выберите [подходящие группы безопасности](../../../vpc/concepts/security-groups.md) (если соответствующего поля нет, для виртуальной машины будет разрешен любой входящий и исходящий трафик).    
1. Укажите данные для доступа на виртуальную машину.
1. Нажмите кнопку **Создать ВМ**.

Создание виртуальной машины занимает несколько минут. Когда виртуальная машина перейдет в статус `RUNNING`, переходите к [настройке программного обеспечения](setup.md). Следить за статусами машин можно в списке виртуальных машин каталога.

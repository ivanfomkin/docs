---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Зарезервировать статический публичный IP-адрес

Вы можете зарезервировать публичный статический IP-адрес, чтобы потом использовать его для доступа к облачным ресурсам.

{% note info %}

Обратите внимание на [правила тарификации](../pricing.md#prices-public-ip) неактивных статических публичных адресов.

{% endnote %}

{% list tabs %}

* Консоль управления
  
   Чтобы зарезервировать статический публичный IP-адрес:
   1. Перейдите на страницу каталога, в котором нужно зарезервировать адрес, и выберите сервис **Virtual Private Cloud**.
   1. Выберите вкладку **IP-адреса**.
   1. Нажмите кнопку **Зарезервировать адрес**.
   1. В открывшемся окне выберите зону доступности, в которой нужно зарезервировать адрес.
   1. Нажмите кнопку **Зарезервировать**.
  
* CLI

   {% include [include](../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../_includes/default-catalogue.md) %}

   Чтобы зарезервировать статический публичный IP-адрес:

   1. Просмотрите описание команды CLI для резервирования адреса:

      ```bash
      yc vpc address create --help
      ```

   1. Зарезервируйте адрес, указав зону доступности:

      ```bash
      yc vpc address create --external-ipv4 zone=ru-central1-a
      ```

      Результат выполнения:

      ```bash
      id: e9b6un9gkso6stdh6b3p
      folder_id: b1g7gvsi89m34pipa3ke
      created_at: "2021-01-19T17:52:42Z"
      external_ipv4_address:
        address: 178.154.253.52
        zone_id: ru-central1-a
        requirements: {}
      reserved: true
      ```

      Статический публичный IP-адрес зарезервирован.

{% endlist %}

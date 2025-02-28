---
title: Разработка на Node.js в Yandex Cloud Functions. Обзор
description: 'С помощью сервиса Cloud Functions вы можете запускать приложения, написанные на Node.js. Сервис предоставляет несколько сред выполнения с различными версиями операционной системы.'

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---


# Обзор

С помощью сервиса {{ sf-name }} вы можете запускать приложения, написанные на [Node.js](https://nodejs.org/en/docs/). Сервис предоставляет несколько [сред выполнения](../../concepts/runtime/index.md) с различными версиями:

| Название | Версия Node.js | Версия SDK <br>{{ yandex-cloud }} | Операционная <br>система |
|----|----|----|----|
| nodejs10 | 10.16.3 | 1.1.1 | Ubuntu 18.04 LTS |
| nodejs12 | 12.11.1 | 1.1.1 | Ubuntu 18.04 LTS |
| nodejs14 | 14.11.0 | 1.1.1 | Ubuntu 18.04 LTS |

В среду выполнения по умолчанию установлена SDK-библиотека для работы с API {{ yandex-cloud }}. Подробнее о способах использования SDK читайте в разделе [Использование SDK](sdk.md).

В процессе создания новой [версии функции](../../concepts/function.md#version) {{ sf-name }} автоматически установит все объявленные зависимости, необходимые для работы функции. Ознакомьтесь подробнее с требованиями и ограничениями в разделе [{#T}](dependencies.md).

Среда выполнения автоматически загружает ваш код и вызывает указанный вами [обработчик запросов](handler.md). В качестве аргументов он получает входящий запрос и [контекст вызова](context.md), который содержит дополнительную информацию о параметрах функции.

Сервис {{ sf-name }} автоматически захватывает потоки стандартного вывода приложения и отправляет их в централизованную систему журналирования, доступную в {{ yandex-cloud }}. Туда же сохраняются служебные записи о начале и окончании выполнения функции и обо всех ошибках, которые произошли во время выполнения. Подробнее о формате журналов читайте в разделе [{#T}](logging.md).

Если вы хотите больше узнать о том, как писать на языке программирования JavaScript или как работают те или иные конструкции, ознакомьтесь с [Современным учебником JavaScript](https://learn.javascript.ru/).

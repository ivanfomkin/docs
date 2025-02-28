---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Вопросы и ответы про {{ container-registry-short-name }}

#### Почему тег latest отсутствует или установлен не на последнем загруженном Docker-образе? {#latest}

Потому что вы указали другой тег при загрузке Docker-образа.

Docker-клиент подставляет тег `latest` автоматически, если Docker-образ создается и загружается без тега. Также можно указать тег `latest` явно. 

{% include [latest-info](../../_includes/container-registry/info-about-latest.md) %}

#### Как сделать реестр публичным? {#public-registry}

Можно выдать роль [container-registry.images.puller](../security/index.md) на ваш реестр для системной группы [allUsers](../../iam/concepts/access-control/system-group.md).

{% note alert %}

При этом все образы из этого реестра станут доступны без аутентификации. 

Не назначайте системной группе роли `container-registry.images.pusher`, `editor` и `admin` на реестр. Это позволит любому, кто узнает идентификатор вашего реестра, пользоваться им за ваш счет.

{% endnote %} 

#### У меня возникла ошибка. Что делать? {#error}

Ознакомьтесь с информацией в разделе [{#T}](../error/index.md), там перечислены часто встречающиеся ошибки и способы их решения.

{% include [qa-logs.md](../../_includes/qa-logs.md) %}

#### Что означает ошибка "Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock"? {#permission-denied}

Вы запускаете команды не от пользователя `root`.

Можете использовать `sudo` или настроить [non-root доступ](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

#### Как можно диагностировать работу Credential helper? {#cred-helper}

- Проверьте, от какого пользователя операционной системы и на каком хосте запускаются команды CLI. Это должен быть пользователь, для которого сконфигурирован Credential helper и от имени которого была запущена команда `yc container registry configure-docker`. Соответствующая запись при этом появляется в файле `/home/<user>/.docker/config.json`. Если вы выполняете действия на ВМ, то на ней тоже должен быть настроен Credential helper.
- Проверьте, есть ли Credential helper в `PATH` при вызове команд. Когда происходит аутентификация в {{ container-registry-short-name }} при помощи Credential helper, Docker обращается к бинарному файлу `docker-credential-yc`. Необходимо, чтобы этот бинарный файл был в `PATH` для пользователя, который работает c Docker. Например, если Docker используется с `sudo`, то и `configure-docker` должен вызываться с `sudo`. Проверить можно командой `echo cr.yandex | docker-credential-yc get` или `echo cr.yandex | sudo docker-credential-yc get`, если команды вызываются из-под `sudo`. Если все работает, то вывод будет вида `{"Username":"iam","Secret":"***<iam-token>***"}`.
- Если команды работают в интерактивном режиме, но не работают в неинтерактивном, проверьте файл `.bashrc`. Программы `yc` и `docker-credential-yc` устанавливаются в директорию, которая обычно не доступна в дефолтном `PATH`. В файл `.bashrc` при этом прописываются следующие строки: 
  
  ```
  # The next line updates PATH for Yandex Cloud CLI
  if [ -f '/home/<user>/yandex-cloud/path.bash.inc' ]; then source '/home/<user>/yandex-cloud/path.bash.inc'; fi
  ```
 
  В начале файла `.bashrc` есть условие, что команды, прописанные в нем, не выполняются в неинтерактивном режиме. Из-за этого команды могут работать при заходе на ВМ вручную, но не работать по SSH.


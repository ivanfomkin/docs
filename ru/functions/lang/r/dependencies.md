---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Сборка и управление зависимостями

## Предустановленные пакеты {#pre-inst-pack}

Среда выполнения имеет следующий набор предустановленных пакетов, доступных для использования из кода функции:
`httr`,  `logging`, `data.table`, `dplyr`, `paws`, `rjson`, `stringr`, `BiocManager`, `ggplot2`, `plotly`, `devtools`, `Rcpp`, `tidyr`, `lubridate`, `e1071`, `caret`, `mongolite`, `Rsamtools`.

## Установка дополнительных пакетов {#inst-addit-pack}

Во время создания новой [версии функции](../../operations/function/version-manage.md#func-version-create) сервис {{ sf-name }} позволяет установить зависимости, необходимые для работы функции. Для этого требуется загрузить в корень проекта файл `packages.R` с описанием процесса установки пакетов.

Также возможна ручная поставка зависимостей вместе с исходным кодом.

## packages.R {#pack-r}

Данный скрипт исполняется однократно при создании версии функции.

Пример установки пакета через  `packages.R`:

```R
install.packages("purrr", repo="http://cran.r-project.org")
```

## Ручная поставка зависимостей {#man-del-of-dep}

Для того, чтобы настроить зависимости вручную, положите скомпилированные пакеты в подкаталог `usr/library/` архива с проектом.

Процесс установки зависимостей имеет ограничения по ресурсам и времени исполнения. Подробнее об этом читайте в разделе [{#T}](../../concepts/limits.md). Ознакомиться с журналом установки зависимостей можно по ссылке, которая отображается в списке операций.

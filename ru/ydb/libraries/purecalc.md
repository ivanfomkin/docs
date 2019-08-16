# library/purecalc

* **Описание:** выполнение YQL запросов локально в памяти использующего библиотеку процесса. В роли входных и выходных таблиц выступают итераторы по произвольным плоским protobuf сообщениям. На старте запрос компилируется, подгружаются UDF и граф вычислений сверяется по типам с дескрипторами указанных protobuf сообщений (рекурсия и вложенность не поддерживаются). На сам граф вычислений тоже есть ограничения, например запрещен JOIN, но при наличии спроса поддержку недостающего можно добавлять. Данная библиотека может быть полезна для задач, где нужно делать в памяти ровно те же вычисления что и в YT, но в каком-либо другом окружении, например для избежания задержек связанных с запуском MapReduce операций.
* Языки: [C++](https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/purecalc).
* [Примеры использования](https://cs.yandex-team.ru/#!yql%2Flibrary%2Fpurecalc,ya.make,,arcadia).
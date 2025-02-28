{% list tabs %}

- CLI

	{% include [cli-install](../cli-install.md) %}
    
    {% include [default-catalogue](../default-catalogue.md) %}

	Чтобы добавить записи в лог-группу, выполните команду:

	```
	yc logging write \
	  --group-name=default \
	  --message="My message" \
	  --timestamp="2021-06-08T19:10:40.000Z" \
	  --level=INFO \
	  --json-payload='{"request_id": "1234"}'
	```

	* `--group-name` — имя лог-группы, в которую вы хотите добавить записи. Необязательный параметр. Если параметр не указан, записи добавляются в [лог-группу по умолчанию](../../logging/concepts/log-group.md) текущего каталога.
	* `--message` — сообщение.
	* `--timestamp` — время отправки записи.
	* `--level` — уровень логирования.
	* `--json-payload` — дополнительная иннформация в формате JSON.

- API

	Добавить записи в лог-группу можно с помощью метода API [write](../../logging/api-ref/LogIngestion/write.md).

{% endlist %}
---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Logging

{{ sf-name }} automatically captures standard application output streams and sends them to the centralized logging system available in {{ yandex-cloud }}. In addition to the application run history, the system logs request execution events.

Additional messages are logged using standard language constructs:

1. `print`: Outputs a message to the standard output stream, `stdout`.
1. `print_r`: Outputs information about a variable in a readable form to the standard output stream, `stdout`.

{% include [multiline warning](../../../_includes/functions/multiline.md) %}

{% include [router-logging](../../../_includes/functions/router-logging.md) %}


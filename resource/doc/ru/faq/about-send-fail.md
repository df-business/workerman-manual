# Причины send_fail в статусе

**Явление:**

При выполнении команды status видим ситуацию send_fail. В чем причина?

**Ответ:**

Обычно send_fail не является серьезной проблемой и обычно возникает из-за того, что клиентский сокет был закрыт или клиент не может принимать данные, что приводит к сбою отправки данных.

send_fail имеет две причины:

1. Если вызван интерфейс send для отправки данных клиенту, но обнаружено, что клиент уже отключился, тогда счетчик send_fail увеличивается. Поскольку это происходит из-за активного разъединения клиента, это является нормальным явлением и обычно можно игнорировать.

2. Скорость отправки данных с сервера превышает скорость приема клиентом, что приводит к постоянной накоплению данных в буфере сервера (для каждого клиента workerman создает буфер отправки). Если размер буфера превышает установленное значение (по умолчанию TcpConnection::$maxSendBufferSize - 1 МБ), данные будут отброшены, инициируется событие onError (если есть), и счетчик send_fail увеличивается.

Например, когда браузер минимизируется, JavaScript может приостановиться, что приведет к приостановке приема данных сервером, которые долго накапливаются в буфере и, превысив ограничение, каждый вызов send приведет к увеличению счетчика send_fail.

**Вывод:**

Не нужно беспокоиться о send_fail, вызванном разрывом соединения клиента.

Если send_fail вызван тем, что клиент прекратил принимать данные, следует проверить работу клиента.

Если скорость приема данных клиентом **постоянно** ниже скорости отправки с сервера, следует рассмотреть оптимизацию бизнес-процессов или улучшение производительности клиента. Если проблема вызвана недостаточной пропускной способностью, можно рассмотреть увеличение пропускной способности сервера.
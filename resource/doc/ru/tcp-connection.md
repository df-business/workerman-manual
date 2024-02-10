# Интерфейсы класса Connection

В WorkerMan есть два важных класса - Worker и Connection.

Каждое клиентское подключение соответствует объекту Connection, который может быть настроен с помощью обратных вызовов onMessage, onClose и т. д. Также предоставляется интерфейс send для отправки данных клиенту и интерфейс close для закрытия соединения, а также другие необходимые интерфейсы.

Можно сказать, что Worker является контейнером для прослушивания, отвечающим за принятие клиентских подключений и предоставление этих подключений в виде объектов connection для работы разработчика.
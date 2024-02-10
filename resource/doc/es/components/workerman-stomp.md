# workerman/stomp

STOMP es un protocolo de comunicación. Es compatible con la mayoría de las colas de mensajes como RabbitMQ, Apollo, etc.

## Dirección del proyecto:
https://github.com/walkor/stomp

## Instalación:
```php
composer require workerman/stomp
```

## Ejemplo:
```php
<?php
use Workerman\Worker;
use Workerman\Timer;
use Workerman\Stomp\Client;
use Workerman\RedisQueue\Client;
require_once __DIR__ . '/vendor/autoload.php';

$worker = new Worker();
$worker->onWorkerStart = function(){
    $client = new Workerman\Stomp\Client('stomp://127.0.0.1:61613');
    $client->onConnect = function(Client $client) {
       // Suscribirse
        $client->subscribe('/topic/foo', function(Client $client, $data) {
            var_export($data);
        });
    };
    $client->onError = function ($e) {
        echo $e;
    };
    Timer::add(1, function () use ($client) {
        // Publicar
        $client->send('/topic/foo', 'Hola desde Workerman STOMP');
    });
    $client->connect();
};
Worker::runAll();
```
通信プロトコルの役割

TCPはストリームに基づいており、クライアントからのリクエストデータは水のようにサーバーに流れ込んできます。サーバーはデータが到着すると、そのデータが完全かどうかを確認する必要があります。なぜなら、サーバーに到着するのはリクエストの一部だけかもしれず、複数のリクエストが連続して到着することもあります。リクエストが完全に到着したか、または複数の連続したリクエストからリクエストを分離するには、通信プロトコルを規定する必要があります。

## WorkerManでプロトコルを定義する理由

従来のPHP開発は基本的にWebに基づいており、ほとんどがHTTPプロトコルを使用しています。HTTPプロトコルの解析処理はWebサーバーが独自に処理しているため、開発者はプロトコルに関することを気にする必要はありませんでした。しかし、非HTTPプロトコルに基づいた開発が必要になると、開発者はプロトコルについて考える必要があります。

## WorkerManで既にサポートされているプロトコル

WorkerManは現在、HTTP、websocket、textプロトコル（付録を参照）、frameプロトコル（付録を参照）、wsプロトコル（付録を参照）をサポートしています。これらのプロトコルを使用する際には、初期化するWorkerでプロトコルを指定することができます。例：

```php
use Workerman\Worker;
use Workerman\Connection\TcpConnection;
require_once __DIR__ . '/vendor/autoload.php';

// websocket://0.0.0.0:2345 はwebsocketプロトコルでポート2345をリッスンすることを示します
$websocket_worker = new Worker('websocket://0.0.0.0:2345');

// textプロトコル
$text_worker = new Worker('text://0.0.0.0:2346');

// frameプロトコル
$frame_worker = new Worker('frame://0.0.0.0:2347');

// tcp Worker、直接的なsocket転送であり、アプリケーション層のプロトコルは使用しない
$tcp_worker = new Worker('tcp://0.0.0.0:2348');

// udp Worker、アプリケーション層のプロトコルは使用しない
$udp_worker = new Worker('udp://0.0.0.0:2349');

// unix domain Worker、アプリケーション層のプロトコルは使用しない
$unix_worker = new Worker('unix:///tmp/wm.sock');
```

## カスタム通信プロトコルの使用

WorkerManのデフォルトの通信プロトコルが開発要件を満たさない場合、開発者は独自の通信プロトコルを定義することができます。定義方法については、次のセクションを参照してください。

**注意：**

Workermanにはtextプロトコルが組み込まれており、プロトコルの形式はテキストと改行です。textプロトコルは開発とデバッグが非常に簡単なため、ほとんどのカスタムプロトコルのシーンに使用できます。また、telnetデバッグもサポートしています。開発者が独自のアプリケーションプロトコルを開発する場合は、textプロトコルを直接使用でき、別途開発する必要はありません。

textプロトコルの説明は「付録 テキストプロトコル」を参照してください。
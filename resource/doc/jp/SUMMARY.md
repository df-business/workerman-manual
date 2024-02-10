* [序論](README.md)
* [原理](principle.md)
* [開発者必読](must-read.md)
* ガイド
    * [特徴](getting-started/feature.md)
    * [シンプルな開発例](getting-started/simple-example.md)
* インストール
    * [システム要件](install/requirement.md)
    * [ダウンロードとインストール](install/install.md)
    * [起動と停止](install/start-and-stop.md)
* 開発フロー
    * [開発前の注意事項](development/before-development.md)
    * [ディレクトリ構造](development/directory-structure.md)
    * [開発規約](development/standard.md)
    * [基本フロー](development/process.md)
* 通信プロトコル
    * [通信プロトコルの役割](protocols/why-protocols.md)
    * [カスタム通信プロトコル](protocols/how-protocols.md)
    * [いくつかの例](protocols/example.md)
* [Workerクラス](worker.md)
    * [コンストラクタ](worker/construct.md)
    * プロパティ
        * [id](worker/workerid.md)
        * [count](worker/count.md)
        * [name](worker/name.md)
        * [protocol](worker/protocol.md)
        * [transport](worker/transport.md)
        * [reusePort](worker/reuse-port.md)
        * [connections](worker/connections.md)
        * [stdoutFile](worker/stdout-file.md)
        * [pidFile](worker/pid-file.md)
        * [logFile](worker/log-file.md)
        * [user](worker/user.md)
        * [reloadable](worker/reloadable.md)
        * [daemonize](worker/daemonize.md)
        * [globalEvent](worker/global-event.md)
    * コールバックプロパティ
        * [onWorkerStart](worker/on-worker-start.md)
        * [onWorkerReload](worker/on-worker-reload.md)
        * [onConnect](worker/on-connect.md)
        * [onMessage](worker/on-message.md)
        * [onClose](worker/on-close.md)
        * [onBufferFull](worker/on-buffer-full.md)
        * [onBufferDrain](worker/on-buffer-drain.md)
        * [onError](worker/on-error.md)
    * インタフェース
        * [runAll](worker/run-all.md)
        * [stopAll](worker/stop-all.md)
        * [listen](worker/listen.md)
* [TcpConnectionクラス](tcp-connection.md)
    * プロパティ
        * [id](tcp-connection/id.md)
        * [protocol](tcp-connection/protocol.md)
        * [worker](tcp-connection/worker.md)
        * [maxSendBufferSize](tcp-connection/max-send-buffer-size.md)
        * [defaultMaxSendBufferSize](tcp-connection/default-max-send-buffer-size.md)
        * [defaultMaxPackageSize](tcp-connection/default-max-package-size.md)
    * コールバックプロパティ
        * [onMessage](tcp-connection/on-message.md)
        * [onClose](tcp-connection/on-close.md)
        * [onBufferFull](tcp-connection/on-buffer-full.md)
        * [onBufferDrain](tcp-connection/on-buffer-drain.md)
        * [onError](tcp-connection/on-error.md)
    * インタフェース
        * [send](tcp-connection/send.md)
        * [getRemoteIp](tcp-connection/get-remote-ip.md)
        * [getRemotePort](tcp-connection/get-remote-port.md)
        * [close](tcp-connection/close.md)
        * [destroy](tcp-connection/destroy.md)
        * [pauseRecv](tcp-connection/pause-recv.md)
        * [resumeRecv](tcp-connection/resume-recv.md)
        * [pipe](tcp-connection/pipe.md)
* [AsyncTcpConnectionクラス](async-tcp-connection.md)
    * [__construct](async-tcp-connection/construct.md)
    * [connect](async-tcp-connection/connect.md)
    * [reconnect](async-tcp-connection/reconnect.md)
    * [transport](async-tcp-connection/transport.md)
* [AsyncUdpConnectionクラス](async-udp-connection.md)
    * [__construct](async-udp-connection/construct.md)
    * [connect](async-udp-connection/connect.md)
    * [send](async-udp-connection/send.md)
    * [close](async-udp-connection/close.md)
* タイマークラス
    * [add](timer/add.md)
    * [del](timer/del.md)
    * [タイマーの注意事項](timer/notice.md)
    * [crontab](timer/crontab.md)
* HTTPサービス
    * [リクエスト](http/request.md)
    * [レスポンス](http/response.md)
    * [セッション](http/session.md)
    * [セッション管理](http/session-control.md)
    * [SSE](http/SSE.md)
* デバッグ
    * [基本的なデバッグ](debug/base.md)
    * [ステータスコマンドを使用した実行状態の確認](debug/status.md)
    * [ビジーなプロセスのデバッグ](debug/busy-process.md)
    * [ネットワークパケットキャプチャ](debug/tcpdump.md)
    * [システムコールのトレース](debug/strace.md)
* 一般的なコンポーネント
    * [GlobalDataデータ共有コンポーネント](components/global-data.md)
        * [GlobalDataServer](components/global-data-server.md)
        * [GlobalDataClient](components/global-data-client.md)
            * [add](components/global-data-client-add.md)
            * [cas](components/global-data-client-cas.md)
            * [increment](components/global-data-client-increment.md)
    * [Channel分散通信コンポーネント](components/channel.md)
        * [ChannelServer](components/channel-server.md)
        * [channelClient](components/channel-client.md)
            * [connect](components/channel-client-connect.md)
            * [on](components/channel-client-on.md)
            * [publish](components/channel-client-publish.md)
            * [unsubsribe](components/channel-client-unsubsribe.md)
        * [例-クラスタープッシュ](components/channel-examples.md)
        * [例-グループ送信](components/channel-examples2.md)
    * [FileMonitorファイル監視コンポーネント](components/file-monitor.md)
    * [MySQLコンポーネント](components/mysql.md)
        * [workerman/mysql](components/workerman-mysql.md)
        * [他のデータベースクラス](components/other-mysql-class.md)
    * [Redisコンポーネント](components/redis.md)
        * [workerman/redis](components/workerman-redis.md)
    * [非同期HTTPコンポーネント](components/async-http.md)
        * [workerman/http-client](components/workerman-http-client.md)
    * [非同期メッセージキューコンポーネント](components/async-message-queue.md)
        * [workemran/mqtt](components/workerman-mqtt.md)
        * [workerman/redis-queue](components/workerman-redis-queue.md)
        * [workerman/stomp](components/workerman-stomp.md)
        * [workerman/rabbitmq](components/workerman-rabbitmq.md)
    * [Crontabスケジュールタスク](components/crontab.md)
    * [Memcache](components/memcache.md)
* よくある質問
    * [ハートビート](faq/heartbeat.md)
    * [自動読み込み](faq/autoload.md)
    * [クライアント接続の失敗原因](faq/client-connect-fail.md)
    * [マルチスレッドサポートの有無](faq/about-multi-thread.md)
    * [他のフレームワークとの連携](faq/work-with-other-framework.md)
    * [複数のworkermanの実行](faq/running-concurent.md)
    * [サポートされているプロトコル](faq/protocols.md)
    * [プロセス数の設定方法](faq/processes-count.md)
    * [クライアント接続数の確認方法](faq/connection-status.md)
    * [オブジェクトとリソースの永続化](faq/persistent-data-and-resources.md)
    * [デモが動作しない場合](faq/demo-not-work.md)
    * [起動に失敗](faq/workerman-start-fail.md)
    * [停止に失敗](faq/stop-fail.md)
    * [同時接続数のサポート数](faq/how-many-connections.md)
    * [変更したコードの反映方法](faq/change-code-not-work.md)
    * [特定のクライアントにデータを送信する方法](faq/send-data-to-client.md)
    * [アクティブにメッセージをプッシュする方法](faq/active-push.md)
    * [他のプロジェクトにプッシュする方法](faq/push-in-other-project.md)
    * [非同期タスクの実装方法](faq/async-task.md)
    * [statusコマンドでのsend_failの原因](faq/about-send-fail.md)
    * [Windowsでの開発とLinuxでの展開](faq/windows-to-linux.md)
    * [socket.ioのサポート有無](faq/socketio-support.md)
    * [SSHの終了とworkermanの停止について](faq/ssh-close-and-workerman-stop.md)
    * [ApacheやNginxとの関係](faq/relationship-with-apache-nginx.md)
    * [無効化関数のチェック](faq/disable-function-check.md)
    * [スムーズな再起動原理](faq/reload-principle.md)
    * [Flash用の843ポートの作成方法](faq/flash-843.md)
    * [データのブロードキャスト方法](faq/how-to-broadcast.md)
    * [UDPサービスの作成方法](faq/how-to-create-udp-service.md)
    * [IPv6のリスニング](faq/ipv6.md)
    * [認証されていない接続のクローズ方法](faq/close-unauthed-connections.md)
    * [トランスポートエンクリプト-ssl/tls](faq/ssl-support.md)
    * [WSSサービスの作成方法](faq/secure-websocket-server.md)
    * [HTTPSサービスの作成方法](faq/secure-http-server.md)
    * [workermanをクライアントとして使用する方法](faq/use-workerman-as-client-side.md)
    * [WS/WSSクライアントとして使用する方法](faq/as-wss-client.md)
    * [微信小程序](faq/weixin-app.md)
    * [PHPのコールバックメソッドの種類](faq/callback_methods.md)
    * [プロキシからクライアントの実際のIPを取得する方法](faq/get-real-ip-from-proxy.md)
    * [起動時の自動実行](faq/start-with-system.md)
    * [16進数データの受信と送信](faq/send-recv-hexadecimal-data.md)
    * [特定のリクエスト後の再起動](faq/max-requests.md)
    * [Windowsでの複数のworkerの初期化](faq/multi-woker-for-windows.md)
    * [特定のプロセスでのリクエストの集中](faq/requests-concentrated-in-certain-processes.md)
* 付録
    * [Linuxカーネルの最適化](appendices/kernel-optimization.md)
    * [ストレステスト](appendices/stress-test.md)
    * [拡張機能のインストール](appendices/install-extension.md)
    * [WebSocketプロトコルについて](appendices/about-websocket.md)
    * [WSプロトコルについて](appendices/about-ws.md)
    * [textプロトコルについて](appendices/about-text.md)
    * [frameプロトコルについて](appendices/about-frame.md)
    * [使用できない関数/機能](appendices/unavailable-functions.md)
* [著作権情報](license.md)
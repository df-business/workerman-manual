# Connectionクラスの提供するインターフェース

WorkerManには、WorkerとConnectionという2つの重要なクラスがあります。

各クライアント接続には、Connectionオブジェクトが対応しており、オブジェクトのonMessageやonCloseなどのコールバックを設定できます。さらに、クライアントにデータを送信するsendインターフェースや接続を閉じるcloseインターフェースなどが提供されており、その他にも必要なインターフェースがいくつかあります。

Workerは実質的にはクライアント接続を受け入れ、接続をConnectionオブジェクトとして開発者が操作できるようにするリスニングコンテナーと言えます。
* [Foreword](README.md)
* [Principle](principle.md)
* [Must Read for Development](must-read.md)
* Getting Started Guide
    * [Features](getting-started/feature.md)
    * [Simple Development Example](getting-started/simple-example.md)
* Installation
    * [System Requirements](install/requirement.md)
    * [Download and Installation](install/install.md)
    * [Start and Stop](install/start-and-stop.md)
* Development Process
    * [Pre-development Must Read](development/before-development.md)
    * [Directory Structure](development/directory-structure.md)
    * [Development Standards](development/standard.md)
    * [Basic Process](development/process.md)
* Communication Protocols
    * [Role of Communication Protocols](protocols/why-protocols.md)
    * [Customizing Communication Protocols](protocols/how-protocols.md)
    * [Some Examples](protocols/example.md)
* [Worker Class](worker.md)
    * [Constructor](worker/construct.md)
    * Attributes
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
    * Callback Attributes
        * [onWorkerStart](worker/on-worker-start.md)
        * [onWorkerReload](worker/on-worker-reload.md)
        * [onConnect](worker/on-connect.md)
        * [onMessage](worker/on-message.md)
        * [onClose](worker/on-close.md)
        * [onBufferFull](worker/on-buffer-full.md)
        * [onBufferDrain](worker/on-buffer-drain.md)
        * [onError](worker/on-error.md)
    * Interface
        * [runAll](worker/run-all.md)
        * [stopAll](worker/stop-all.md)
        * [listen](worker/listen.md)
* [TcpConnection Class](tcp-connection.md)
    * Attributes
        * [id](tcp-connection/id.md)
        * [protocol](tcp-connection/protocol.md)
        * [worker](tcp-connection/worker.md)
        * [maxSendBufferSize](tcp-connection/max-send-buffer-size.md)
        * [defaultMaxSendBufferSize](tcp-connection/default-max-send-buffer-size.md)
        * [defaultMaxPackageSize](tcp-connection/default-max-package-size.md)
    * Callback Attributes
        * [onMessage](tcp-connection/on-message.md)
        * [onClose](tcp-connection/on-close.md)
        * [onBufferFull](tcp-connection/on-buffer-full.md)
        * [onBufferDrain](tcp-connection/on-buffer-drain.md)
        * [onError](tcp-connection/on-error.md)
    * Interface
        * [send](tcp-connection/send.md)
        * [getRemoteIp](tcp-connection/get-remote-ip.md)
        * [getRemotePort](tcp-connection/get-remote-port.md)
        * [close](tcp-connection/close.md)
        * [destroy](tcp-connection/destroy.md)
        * [pauseRecv](tcp-connection/pause-recv.md)
        * [resumeRecv](tcp-connection/resume-recv.md)
        * [pipe](tcp-connection/pipe.md)
* [AsyncTcpConnection Class](async-tcp-connection.md)
    * [__construct](async-tcp-connection/construct.md)
    * [connect](async-tcp-connection/connect.md)
    * [reconnect](async-tcp-connection/reconnect.md)
    * [transport](async-tcp-connection/transport.md)
* [AsyncUdpConnection Class](async-udp-connection.md)
    * [__construct](async-udp-connection/construct.md)
    * [connect](async-udp-connection/connect.md)
    * [send](async-udp-connection/send.md)
    * [close](async-udp-connection/close.md)
* Timer Class
    * [add](timer/add.md)
    * [del](timer/del.md)
    * [Notes on Timers](timer/notice.md)
    * [crontab](timer/crontab.md)
* Http Service
    * [Request](http/request.md)
    * [Response](http/response.md)
    * [Session](http/session.md)
    * [Session Management](http/session-control.md)
    * [SSE](http/SSE.md)
* Debugging
    * [Basic Debugging](debug/base.md)
    * [Viewing Runtime Status with `status` command](debug/status.md)
    * [Debugging Busy Processes](debug/busy-process.md)
    * [Network Packet Capture](debug/tcpdump.md)
    * [Tracing System Calls](debug/strace.md)
* Commonly Used Components
    * [GlobalData Data Sharing Component](components/global-data.md)
        * [GlobalDataServer](components/global-data-server.md)
        * [GlobalDataClient](components/global-data-client.md)
            * [add](components/global-data-client-add.md)
            * [cas](components/global-data-client-cas.md)
            * [increment](components/global-data-client-increment.md)
    * [Channel Distributed Communication Component](components/channel.md)
        * [ChannelServer](components/channel-server.md)
        * [channelClient](components/channel-client.md)
            * [connect](components/channel-client-connect.md)
            * [on](components/channel-client-on.md)
            * [publish](components/channel-client-publish.md)
            * [unsubscribe](components/channel-client-unsubscribe.md)
        * [Example-Cluster Push](components/channel-examples.md)
        * [Example-Group Send](components/channel-examples2.md)
    * [FileMonitor File Monitoring Component](components/file-monitor.md)
    * [MySQL Component](components/mysql.md)
        * [workerman/mysql](components/workerman-mysql.md)
        * [Other Database Classes](components/other-mysql-class.md)
    * [Redis Component](components/redis.md)
        * [workerman/redis](components/workerman-redis.md)
    * [Asynchronous HTTP Component](components/async-http.md)
        * [workerman/http-client](components/workerman-http-client.md)
    * [Asynchronous Message Queue Component](components/async-message-queue.md)
        * [workerman/mqtt](components/workerman-mqtt.md)
        * [workerman/redis-queue](components/workerman-redis-queue.md)
        * [workerman/stomp](components/workerman-stomp.md)
        * [workerman/rabbitmq](components/workerman-rabbitmq.md)
    * [Crontab Scheduled Tasks](components/crontab.md)
    * [Memcache](components/memcache.md)
* Frequently Asked Questions
    * [Heartbeat](faq/heartbeat.md)
    * [Autoloading](faq/autoload.md)
    * [Reasons for Client Connection Failures](faq/client-connect-fail.md)
    * [Support for Multithreading](faq/about-multi-thread.md)
    * [Integrating with Other Frameworks](faq/work-with-other-framework.md)
    * [Running Multiple Workermans](faq/running-concurrent.md)
    * [Supported Protocols](faq/protocols.md)
    * [Setting the Number of Processes](faq/processes-count.md)
    * [Viewing Client Connection Count](faq/connection-status.md)
    * [Persistence of Objects and Resources](faq/persistent-data-and-resources.md)
    * [Troubleshooting Non-functional Examples](faq/demo-not-work.md)
    * [Startup Failure](faq/workerman-start-fail.md)
    * [Stop Failure](faq/stop-fail.md)
    * [Supporting Concurrent Connections](faq/how-many-connections.md)
    * [Changes in Code Not Taking Effect](faq/change-code-not-work.md)
    * [Sending Data to Specific Clients](faq/send-data-to-client.md)
    * [Implementing Active Message Push](faq/active-push.md)
    * [Pushing Messages in Other Projects](faq/push-in-other-project.md)
    * [Implementing Asynchronous Tasks](faq/async-task.md)
    * [Reasons for `send_fail` in `status`](faq/about-send-fail.md)
    * [Developing on Windows and Deploying on Linux](faq/windows-to-linux.md)
    * [Support for socket.io](faq/socketio-support.md)
    * [Closing SSH and Stopping Workerman](faq/ssh-close-and-workerman-stop.md)
    * [Relationship with Nginx and Apache](faq/relationship-with-apache-nginx.md)
    * [Disabling Function Checks](faq/disable-function-check.md)
    * [Principles of Smooth Reload](faq/reload-principle.md)
    * [Opening Port 843 for Flash](faq/flash-843.md)
    * [Broadcasting Data](faq/how-to-broadcast.md)
    * [Creating UDP Services](faq/how-to-create-udp-service.md)
    * [Listening for IPv6](faq/ipv6.md)
    * [Closing Unauthenticated Connections](faq/close-unauthed-connections.md)
    * [Transport Encryption - SSL/TLS](faq/ssl-support.md)
    * [Creating WSS Services](faq/secure-websocket-server.md)
    * [Creating HTTPS Services](faq/secure-http-server.md)
    * [Using Workerman as a Client](faq/use-workerman-as-client-side.md)
    * [Using as WS/WSS Client](faq/as-wss-client.md)
    * [WeChat Mini Program](faq/weixin-app.md)
    * [Several Callback Writing Methods in PHP](faq/callback_methods.md)
    * [Obtaining Client's Real IP through Proxy](faq/get-real-ip-from-proxy.md)
    * [Boot on Startup](faq/start-with-system.md)
    * [Receiving and Sending Hexadecimal Data](faq/send-recv-hexadecimal-data.md)
    * [Restarting After Receiving a Certain Number of Requests](faq/max-requests.md)
    * [Initializing Multiple Workers on Windows](faq/multi-woker-for-windows.md)
    * [Concentrating Requests in Certain Processes](faq/requests-concentrated-in-certain-processes.md)
* Appendices
    * [Linux Kernel Optimization](appendices/kernel-optimization.md)
    * [Stress Testing](appendices/stress-test.md)
    * [Installing Extensions](appendices/install-extension.md)
    * [WebSocket Protocol](appendices/about-websocket.md)
    * [WS Protocol](appendices/about-ws.md)
    * [Text Protocol](appendices/about-text.md)
    * [Frame Protocol](appendices/about-frame.md)
    * [Unavailable Functions/Features](appendices/unavailable-functions.md)
* [Copyright Information](license.md)
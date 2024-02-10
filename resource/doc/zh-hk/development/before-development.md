# 開發前必讀

使用 WorkerMan 開發應用，你需要了解以下內容：

## 一、WorkerMan 開發與普通PHP開發的不同之處

除了與HTTP協議相關的變量函數無法直接使用外，WorkerMan 開發與普通PHP開發並沒有很大不同。

### 1、應用層協議不同
* 普通PHP開發一般是基於HTTP應用層協議，WebServer已經幫開發者完成了協議的解析
* WorkerMan支持各種協議，目前內置了HTTP、WebSocket等協議。WorkerMan推薦開發者使用更簡單的自定義協議通訊
*  HTTP協議開發請參考[Http服務部分](../http/request.md)

### 2、請求周期差異
* PHP在Web應用中一次請求過後會釋放所有的變量與資源
* WorkerMan開發的應用程式在第一次載入解析後便常駐內存，使得類的定義、全局對象、類的靜態成員不會釋放，便於後續重複利用

### 3、注意避免類和常量的重複定義
* 由於WorkerMan會緩存編譯後的PHP文件，所以要避免多次require/include相同的類或者常量的定義文件。建議使用require_once/include_once加載文件。

### 4、注意單例模式的連接資源的釋放
* 由於WorkerMan不會在每次請求後釋放全局對象及類的靜態成員，在數據庫等單例模式中，往往會將數據庫實例（內部包含了一個數據庫socket連接）保存在數據庫靜態成員中，使得WorkerMan在進程生命週期內都復用這個數據庫socket連接。需要注意的是當數據庫伺服器發現某個連接在一定時間內沒有活動後可能會主動關閉socket連接，這時再次使用這個數據庫實例時會報錯，（錯誤信息類似mysql gone away）。WorkerMan提供了[數據庫類](../components/workerman-mysql.md)，有斷開重連的功能，開發者可以直接使用。

### 5、注意不要使用exit、die出語句
* WorkerMan運行在PHP命令行模式下，當調用exit、die退出語句時，會導致當前進程退出。雖然子進程退出後會立刻重新創建一個的相同的子進程繼續服務，但是還是可能對業務產生影響。

### 6、改完程式碼需要重啟服務才能生效
由於WorkerMan是常駐內存的，php類即函數的定義加載一次後便常駐內存，不會再次讀取磁盤加載，所以每次修改完業務程式碼需要重啟才能生效。

## 二、需要了解的基本概念

### 1、TCP傳輸層協議
TCP是一種面向連接的、可靠的、基於IP的傳輸層協議。TCP傳輸層協議一個重要特點是TCP是基於數據流的，客戶端的請求會源源不斷的發送給服務端，服務端收到的數據可能不是一個完整的請求，也有可能是多個請求連在一起。這就需要我們在這源源不斷的數據流中區分每個請求的邊界。而應用層協議主要是為請求邊界定義一套規則，避免請求數據混亂。

### 2、應用層協議
應用層協議(application layer protocol)定義了運行在不同端系統上（客戶端、服務端）的應用程式進程如何相互傳遞報文，例如HTTP、WebSocket都屬於應用層協議。例如一個簡單的應用層次協議可以如下```{"module":"user","action":"getInfo","uid":456}\n"```。此協議是以```"\n"```（注意這裡```"\n"```代表的是回車）標記請求結束，消息體是字符串。

### 3、短連接
短連接是指通訊雙方有數據交互時，就建立一個連接，數據發送完成後，則斷開此連接，即每次連接只完成一項業務的發送。像WEB網站的HTTP服務一般都用短連接。

*短連接應用程式開發可以參考基本開發流程一章*

### 4、長連接
長連接，指在一個連接上可以連續發送多個數據包。

注意：長連接應用必須加[心跳](../faq/heartbeat.md)，否則連接可能由於長時間不活躍而被路由節點防火牆斷開。

長連接多用於操作頻繁，點對點的通訊的情況。每個TCP連接都需要三步握手，這需要時間，如果每個操作都是先連接，再操作的話那麼處理速度會降低很多。所以長連接在每個操作完後都不斷開，下次處理時直接發送數據包就OK了，不用建立TCP連接。例如：數據庫的連接用長連接，如果用短連接頻繁的通訊會造成socket錯誤，而且頻繁的socket創建也是對資源的浪費。

*當需要主動向客戶端推送數據時，例如聊天類、即時遊戲類、手機推送等應用需要長連接。*
*長連接應用程式開發可以參考Gateway/Worker開發流程*

### 5、平滑重啟
一般的重啟的過程是把所有進程全部停止後，再開始創建全新的服務進程。在這個過程中會有一個短暫的時間內是沒有進程對外提供服務的，這就會導致服務暫時不可用，在高併發時勢必會導致請求失敗。

而平滑重啟則不是一次性的停止所有進程，而是一個進程一個進程的停止，每停止一個進程後馬上重新創建一個新的進程頂替，直到所有舊的進程都被替換為止。

平滑重啟WorkerMan可以使用 ```php your_file.php reload```命令，能夠做到在不影響服務質量的情況下更新應用程式。

**注意：只有在on{...}回撥中載入的文件平滑重啟後才會自動更新，啟動腳本中直接載入的文件或者寫死的程式碼運行reload不會自動更新。**

## 三、區分主進程和子進程
有必要注意下程式碼是運行在主進程還是子進程，一般來說在```Worker::runAll();```調用前運行的程式碼都是在主進程運行的，onXXX回撥運行的程式碼都屬於子進程。注意寫在```Worker::runAll();```後面的程式碼永遠不會被執行。

例如下面的程式碼
```php
use Workerman\Worker;
use Workerman\Connection\TcpConnection;
require_once __DIR__ . '/vendor/autoload.php';

// 運行在主進程
$tcp_worker = new Worker("tcp://0.0.0.0:2347");
// 賦值過程運行在主進程
$tcp_worker->onMessage = function(TcpConnection $connection, $data)
{
    // 這部分運行在子進程
    $connection->send('hello ' . $data);
};

Worker::runAll();
```

**注意：** 不要在主進程中初始化數據庫、memcache、redis等連接資源，因為主進程初始化的連接可能會被子進程自動繼承（尤其是使用單例的時候），所有進程都持有同一個連接，服務端通過這個連接返回的數據在多個進程上都可讀，會導致數據錯亂。同樣的，如果任何一個進程關閉連接(例如daemon模式運行時主進程會退出導致連接關閉)，都導致所有子進程的連接都被一起關閉，並發生不可預知的錯誤，例如mysql gone away 錯誤。推薦在onWorkerStart裡面初始化連接資源。
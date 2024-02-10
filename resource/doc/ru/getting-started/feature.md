# Возможности WorkerMan

### 1. Чистая разработка на PHP
Приложения, разработанные с использованием WorkerMan, могут быть запущены независимо от контейнеров, таких как php-fpm, apache, nginx. Это делает разработку, развертывание и отладку приложений на PHP очень удобными для разработчиков.

### 2. Поддержка многопроцессорной обработки в PHP
Для полного использования мощности многоядерных серверов WorkerMan по умолчанию поддерживает многопроцессорную обработку. WorkerMan открывает основной процесс и несколько дочерних процессов для обслуживания запросов. Основной процесс отвечает за мониторинг дочерних процессов, а дочерние процессы независимо слушают сетевые подключения, обрабатывают и отправляют данные. Благодаря простой модели процесса WorkerMan становится более стабильным и эффективным.

### 3. Поддержка TCP и UDP
WorkerMan поддерживает два транспортных уровня протокола - TCP и UDP. Изменение протокола достаточно изменить одно свойство, без изменения бизнес-логики.

### 4. Поддержка долгосрочного соединения
Во многих случаях PHP-приложения должны поддерживать долгосрочное соединение с клиентами, такие как чаты, игры и т. д. Традиционные PHP-контейнеры (apache, nginx, php-fpm) имеют трудности с этим. С использованием WorkerMan, при условии, что серверный бизнес не вызывает явное закрытие соединения, можно использовать долгосрочное соединение. Один процесс WorkerMan может поддерживать до десятков тысяч одновременных соединений, а несколько процессов поддерживают до сотен тысяч или даже миллионов одновременных соединений.

### 5. Поддержка различных протоколов прикладного уровня
Интерфейс WorkerMan поддерживает различные протоколы прикладного уровня, включая пользовательские протоколы. В WorkerMan замена протокола также очень проста - это всего лишь изменение одного поля в настройках, без изменения бизнес-логики. Даже можно запустить несколько портов с разными протоколами, чтобы удовлетворить разные потребности клиентов.

### 6. Поддержка высокой пропускной способности
WorkerMan поддерживает библиотеку событийного цикла Libevent (требуется установка расширения event). При высоких нагрузках на долгосрочные соединения производительность событийного цикла Event весьма впечатляющая. Если отсутствует расширение Event, то используется встроенный в PHP вызов системы Select, который также обладает высокой производительностью.

### 7. Поддержка плавного перезапуска служб
При необходимости перезапуска службы (например, при выпуске новой версии), мы не хотим, чтобы процессы, обрабатывающие запросы пользователей, были немедленно прерваны, и тем более не хотим, чтобы в момент перезапуска клиентские соединения потерпели неудачу. WorkerMan поддерживает возможность плавного перезапуска, обеспечивая плавное обновление службы без влияния на клиентов.

### 8. Поддержка обнаружения обновлений файлов и автоматической загрузки
В процессе разработки мы хотим, чтобы изменения в коде сразу вступали в силу для просмотра результатов. WorkerMan предоставляет [компонент мониторинга файлов FileMonitor](../components/file-monitor.md): при обновлении файла WorkerMan автоматически перезагружается для загрузки нового файла и его активации.

### 9. Поддержка запуска дочерних процессов от указанного пользователя
Поскольку дочерние процессы фактически обрабатывают запросы пользователей, в целях безопасности они не должны иметь слишком высоких привилегий. Поэтому WorkerMan поддерживает настройку пользователя, от имени которого должны запускаться дочерние процессы, что делает ваш сервер более безопасным.

### 10. Поддержка постоянного хранения объектов или ресурсов
В WorkerMan при работе происходит однократная загрузка и разбор PHP-файла с последующим постоянным пребыванием в памяти. Это позволяет избежать повторного создания и уничтожения объявлений классов и функций, окружения выполнения PHP, таблицы символов и т. д., что совершенно не похоже на механизм PHP в веб-контейнерах. В WorkerMan в пределах жизненного цикла процесса статические члены класса или глобальные переменные сохраняются на постоянной основе без явного удаления, что значит, что объекты или ресурсы, помещенные в глобальные переменные или статические члены класса, могут быть повторно использованы для всех запросов этого процесса. Например, достаточно инициализировать соединение с базой данных только один раз в одном процессе, и после этого все запросы этого процесса могут повторно использовать это соединение с базой данных, избегая частого процесса установки соединения с базой данных, TCP-рукопожатия и авторизации в базе данных, что значительно повышает эффективность приложения.

### 11. Высокая производительность
Поскольку файл PHP считывается с диска, а затем постоянно находится в памяти, при следующем использовании непосредственно используется операционный код в памяти, что существенно уменьшает ввод-вывод на диск и множество затратных процессов инициализации, создания среды выполнения, лексического анализа, синтаксического анализа, компиляции операционного кода, закрытия запроса и т. д. Более того, WorkerMan не зависит от контейнеров типа nginx, apache, что устраняет некоторые издержки связи PHP с nginx и другими контейнерами. И, самое главное, ресурсы могут сохраняться на постоянной основе, не требуя инициализации подключения к базе данных и другие процессы каждый раз, что делает разработку приложений на WorkerMan очень производительной.

### 12. Поддержка HHVM
Поддерживается запуск на виртуальной машине HHVM, что значительно повышает производительность PHP. Особенно на CPU-интенсивных бизнес-процессах производительность очень хорошая. По результатам стыковочного тестирования, при отсутствии нагрузочного бизнеса WorkerMan под HHVM демонстрирует увеличение пропускной способности сети на 30-80% по сравнению с Zend PHP5.6.

### 13. Поддержка распределенного развертывания

### 14. Поддержка демонизации

### 15. Поддержка прослушивания нескольких портов

### 16. Поддержка перенаправления стандартных ввода-вывода
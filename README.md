## Ansibe Roles ##

В какой-то момент я осознал, что синхронизировать роли между несколькими компьютерами с помощью rsync неудобно. Потребовалось единое внешнее хранилище, доступное отовсюду. Так и появился этот репозиторий. Можете пользоваться =).
Я не претендую на уникальность. Возможно кто-то написал и выложил код получше, но я просто не в курсе.


## Краткая документация по имеющимся ролям ##

### Elaticsearch ###

Пустая роль. Ставит Elasticsearch и все. Пока никакой кастомизации не добавлено.

### MongoDB ###

Пустая роль. Ставит MongoDB и все. Пока никакой кастомизации не добавлено.

### GrayLog ###

Пустая роль. Ставит GrayLog и все. Пока никакой кастомизации не добавлено.
Т.к. GrayLog зависит от MongoDB и ElasticSearch, то установил эту зависимость принудительно.

### Docker ###

Устанавливаем Docker-ce.

Есть параметры для настройки.
- Переменная **logserv**. Если существует и содержит ip-адрес, то в daemon.json добавляется настройка логгера gelf. Логи шлем на ip из переменной на порт 12201

### Sudo ###

Установка sudo

А дальше идет настройка. Но у меня пока реализованы правила для безпарольных одиночных правил.
Для этого нужно создать структуру по примеру из defaults. 

### Fail2Ban ###

Устанавливает fail2ban и базовая настройка. Плюс к этому реализована преднастройка модулей ssh, asterisk, postfix.

### Zabbix ###

Тут я собрал кумулятивную роль. Т.е. в зависимости от выставленных переменных через нее же ставится и серверная часть и агент и веб-интерфейс. Можно пачкой, а можно по отдельности.

Пока стабильно работает только агент. Чтобы установить агента надо задать следующие переменные (я делаю это для группы all)

- **zabbix_server_ip**
- **zabbix_version**
- **zabbix_agent: true**

Также для zabbix-агента есть 3 скрипта под шаблоны. Для широкой публики пригодится только один - iostat. Подключается он переменной - **zabbix_agent_script_iostat: true** 

### Ejabberd ###

Установка и настройка Ejabberd. Для моих целей хватает, но для универсальности еще нужно доработать.

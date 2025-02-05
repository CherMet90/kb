##### Отключение авто-обновления:  
```
config system central-management
    set allow-push-configuration disable        # запрещает изменять конфигурацию из облака (необходимость СПОРНА)
    set allow-push-firmware disable             # запрещает автоматически отправалять обновление прошивки на устройства
    set allow-remote-firmware-upgrade disable   # запрещает инициировать обновление прошивки удаленно
end

config system fortiguard
    set auto-firmware-upgrade disable   # не разрешает запрашивать обновление со стороны самого устройства
end
```  
<br>

##### Сохранение вручную  
###### Включить режим  
```
config system global
set cfg-save manual
end
```  
###### Команда сохранения  
```
exec cfg save
```

##### Управление таймаутом сессий
```
config system session-ttl
    set default 3600    # глобальное значение
    config port         # port-specific настройки
        edit 7700       # id елемента (не обязан быть равен порту)
            set protocol 6          # протокол, TCP=6, обязательный параметр
            set timeout 9000        # значение таймаута
            set start-port 7700     # задаем порты, на которые распространяется настройка
            set end-port 7700
        next
    end
```
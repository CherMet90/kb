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
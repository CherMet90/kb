Сохранить все *states* хоста в файл:  
```
pfctl -vvss | grep <IP_хоста> > states.txt
```
Завершить все *states* хоста:  
```
pfctl -k <IP_хоста>
```
<br>

##### Балансировка нагрузки
Посмотреть настройки:  
```
netstat -Q
```
Найти строки текущей конфигурации:  
```
sysctl -a | grep rss
```
```
sysctl -a | grep isr
```
###### Рекомендуется
1. Включить RSS (распределяет потоки по ядрам)  
```
hw.ix.enable_rss: 1
```
2. Закрепить поток за ядром *(не проверено)*:  
```
net.isr.bindthreads: 1
```
3. Снять ограничение на число потоков *(не проверено)*:  
```
net.isr.maxthreads: -1
```
4. Включить режим постоянного распределения потока по очередям ядер:  
```
net.isr.dispatch: deferred
```
Есть режим `hybrid` по документации должен начинать раскидывать поток по ядрам только если основное ядро потока занято *(не проверено)*
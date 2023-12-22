1. Устанавливаем `strongswan`  
```
sudo apt update
sudo apt install strongswan
```
2. `/etc/ipsec.conf`:  
```
config setup
    charondebug="ike 2, knl 2, cfg 2, net 2, esp 2, dmn 2,  mgr 2"

conn %default
    keyexchange=ikev1
    authby=secret
    ike=aes128-sha256-modp2048
    esp=aes128-sha256-modp2048
    dpdaction=clear
    keyingtries=%forever

conn cisco-to-ubuntu
    left=%defaultroute
    leftid=<локальный_внешний_ip>
    right=<удаленный_внешний_ip>
    rightid=<удаленный_внешний_ip>
    type=tunnel
    auto=start
```
Если не указывать `leftsubnet` и `rightsubnet`, то сервер поднимет тунель, но принимать или отправлять трафик в него не будет  

3. `/etc/ipsec.secrets`:  
```
<локальный_внешний_ip> <удаленный_внешний_ip> : PSK "p@ssw0rd"
```
4. Перезапускаем службу, поднимаем тунель:  
```
sudo ipsec restart
sudo ipsec up cisco-to-ubuntu
```
5. Для автоматического запуска после загрузки включаем в `systemctl`:
```
sudo systemctl enable strongswan
```
Конфигурация *telnet* без использования *aaa new-model* (логина):  
```
!
line vty 0 4
 login
 password cisco
 transport input telnet
!
```
<br>

Конфигурация `ipsec`:  
```
!
crypto isakmp policy 1
 encr aes
 hash sha256
 authentication pre-share
 group 14
crypto isakmp key <ключ> address <удаленный_внешний_ip>
crypto isakmp keepalive 10 periodic
!
!
crypto ipsec transform-set AES-SHA esp-aes esp-sha256-hmac 
 mode tunnel
!
crypto ipsec profile VTI
 set transform-set AES-SHA 
 set pfs group14
!
interface Tunnel2
 ip address <локальный_ip_тунеля> 255.255.255.252
 tunnel source Dialer1
 tunnel mode ipsec ipv4
 tunnel destination <удаленный_внешний_ip>
 tunnel protection ipsec profile VTI
!
```
<br>

Чтобы в логах было локальное время:  
`service timestamps log datetime localtime show-timezone`

Мониторинг утилизации ресурсов (CPU, память и т.д.):  
`sh processes`
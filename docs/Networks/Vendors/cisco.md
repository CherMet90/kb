Конфигурация *telnet* без использования *aaa new-model*:  
```
!
line vty 0 4
 login
 password cisco
 transport input telnet
!
```
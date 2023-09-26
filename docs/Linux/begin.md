##### sudo WinSCP 
1. Разрешаем пользователю запуск sftp с рут-правами без запроса пароля:
```
chermet ALL=NOPASSWD: /usr/lib/openssh/sftp-server
```
2. Добавить параметры запуска для соединения в самой программе WinSCP:
```
sudo /usr/lib/openssh/sftp-server
```
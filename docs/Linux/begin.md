##### sudo WinSCP 
1. В файле `/etc/sudoers` разрешаем пользователю запуск sftp с рут-правами без запроса пароля:
```
chermet ALL=NOPASSWD: /usr/lib/openssh/sftp-server
```
2. Добавляем параметры запуска для соединения в самой программе WinSCP:
```
sudo /usr/lib/openssh/sftp-server
```
<br>

##### После первого запуска
```
sudo apt update
sudo apt upgrade
```
<br>

##### Настройка авторизации SSH
1. Создаём пользака и помещаем его в группу `sudo`:
```
sudo adduser <username>
sudo usermod -aG sudo <username>
```
* Перелогиниваемся, тестируем
2. Выключаем доступ для `root` в файле `/etc/ssh/sshd_config`:
```
PermitRootLogin no
```
* Тестируем
3. Копируем папку с ключами `~/.ssh` со старого сервера на новый
4. Правим права скопированных файлов:
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
5. В `sshd_config` включаем авторизацию по ключам:
```
PubkeyAuthentication yes
```
6. Тестируем, выключаем авторизацию по паролю:
```
PasswordAuthentication no
```
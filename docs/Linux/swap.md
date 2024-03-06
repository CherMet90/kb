1. Проверить размер и наличие swap:
```
swapon --show
```
2. Если swap есть, но нужно увеличить размер:
```
sudo swapoff /swapfile
```
3. Создаём файл заново:
```
sudo fallocate -l 3G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
swapon --show
```
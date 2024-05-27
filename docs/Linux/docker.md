##### Остановить все docker-контейнеры, удалить всю неиспользуемую инфу
**Step 1: Stop All Running Containers**  
First, stop all the currently running Docker containers:
```
docker stop $(docker ps -q)
```
**Step 2: Remove All Containers**  
Then, remove all Docker containers:
```
docker rm $(docker ps -a -q)
```
**Step 3: Prune Docker System**  
Next, clean up (prune) your Docker system, which will remove all stopped containers, unused networks, images, and cached layers:
```
docker system prune -a
```
**Step 4: Confirm the Cleanup**  
You can confirm the cleanup by listing any remaining containers and images (both should show nothing):
```
docker ps -a
docker images
```
**Combined Commands**  
For convenience, you can combine these commands into a single command sequence:
```
docker stop $(docker ps -q) && docker rm $(docker ps -a -q) && docker system prune -a -f
```
**Notes:**  
* **Volumes**: If you want to also remove all unused volumes, you can use `docker system prune --volumes`, but remember this will also delete any data stored in those volumes permanently.
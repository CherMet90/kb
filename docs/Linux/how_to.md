##### Unzip tar.gz
```
# To uncompress the gz file
gunzip file.tar.gz

# Now you will have a .tar file
# To extract the tar file
tar -xvf file.tar
```
<br>

##### Add a new Virtual Disk to VM established by VMware Workstaion Player
1. Shutdown the VM
2. Add the New Virtual Disk:  
    - Open VMware Workstation Player.
    - Go to "Player" > "Manage" > "Virtual Machine Settings".
    - Click "Add..." to add a new hard disk.
    - Follow the wizard steps:  
        * Type: Select "Hard Disk".
        * Disk Type: Choose a disk type, typically "SCSI" for simplicity.
        * Disk Size: Set the size to 20GB.
        * Options: Choose whether you want to allocate the disk space now or allow it to grow as needed.
3. Start the VM
4. Partition and Format the New Disk:
* Identify the new disk first:  
     ```lsblk```
 You should see the new disk, likely as `/dev/sdb`.
* Partition the new disk:  
     ```sudo fdisk /dev/sdb```
 Follow the prompts to create a new partition. When done, it might create something like `/dev/sdb1`.
* Format the partition:  
     ```sudo mkfs.ext4 /dev/sdb1```
5. Create a Mount Point and Mount the New Disk:
   ```
   sudo mkdir /mnt/newdisk
   sudo mount /dev/sdb1 /mnt/newdisk
   ```
6. Update /etc/fstab to Auto-Mount the New Disk:  
Open /etc/fstab in a text editor:  
   ```sudo nano /etc/fstab```
Add an entry to ensure the new disk mounts at startup:  
   ```/dev/sdb1  /mnt/newdisk  ext4  defaults  0  2```
7. Reboot to Verify:  
   ```sudo reboot```
<br>

##### Переместить данные на другой раздел и создать символьную ссылку на старом (на примере `.vscode-server`)
1. Stop the VSCode server or any processes using `.vscode-server`:  
     ```pkill -f vscode```
2. Move the `.vscode-server` directory:  
     ```sudo mv /home/username/.vscode-server /mnt/newdisk/.vscode-server```
3. Create a symbolic link to the new location:  
     ```sudo ln -s /mnt/newdisk/.vscode-server /home/username/.vscode-server```
4. Ensure the link works and the `.vscode-server` directory is accessible:  
   ```ls -l /home/username/.vscode-server```

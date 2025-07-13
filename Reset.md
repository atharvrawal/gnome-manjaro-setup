### Booting from partition on startup (Windows into a specific folder)
- `sudo blkid` : lists all disks present on system with respective UUID & type
- `sudo nano /etc/fstab`
- Add the below line
	- `UUID=xxxx-xxxx-xxxx-xxxx  /mount/point  file-system  mounting-opt  0  0`
	- file-system : `ntfs-3g`, `ext4`, `exfat` etc..
	- mounting-opt : `defaults`, `rw`, `realtime` etc.. {use defaults as mounting option}
	- dump : 0 or 1 i.e. disable or enable backup dump utility {keep 0, no one cares}
	- file system check : 0 or 1 i.e. disables or enables fsck {keep 0, no one cares} 
	- Hence, final line :
		- `UUID=EAAE69DBAE69A0B5    /mnt/Windows    ntfs-3g    defaults    0    0`
- To and a symbolic link to the home dir
	- `mkdir Windows`
	- `ln -s /mnt/Windows/Users/Atharv /home/atharv/Windows` 
	- `ln -s /mnt/Windows /home/atharv/Windows` 
	```bash
	atharvrawal@fedora:~/Windows$ tree
	.
	├── Atharv -> /mnt/windows/Users/Atharv
	└── windows -> /mnt/windows
	```

### Slow Shutdown Time Solve
1. 
	- `sudo nvim /etc/systemd/system.conf`
	- un-comment the line `DefaultTimeoutStopSec=90s`
	- Then make the default timeout `10s`
2. 
	- `sudo nvim /usr/lib/systemd/user/gnome-session-restart-dbus.service` 
	- Add `Slice=.slice` to the bottom of the file under `[Service]`

###
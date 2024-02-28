# Setting up Bricks on Ovirt Nodes

 ### Step 1: Create directories for Gluster bricks
 - Make a main directory to house all the bricks
```bash
mkdir /gluster_bricks/
```
 - Navigate to the created directory
```bash
cd /gluster_bricks/
```
- Create individual directories for each brick
```bash
mkdir brick1 brick2 brick3
```
### Step 2: Update the file system table to automount the bricks

- Open the file system table in an editor
```bash
vi /etc/fstab
``` 
- Add entries to mount the disks to the respective brick directories on system boot
- The settings indicate that the file system type is xfs, and several mount options are provided
```bash
/dev/sdb1 /gluster_bricks/brick1 xfs rw,inode64,noatime,nouuid  1 2
/dev/sdc1 /gluster_bricks/brick2 xfs rw,inode64,noatime,nouuid  1 2
/dev/sdd1 /gluster_bricks/brick3 xfs rw,inode64,noatime,nouuid  1 2
```

### Step 3: Update multipath configuration

- Open the multipath configuration in an editor
```bash
vi /etc/multipath.conf
```

- Add a blacklist entry to prevent specific devices from being used by multipath tools
```bash
Blacklist
devnode "^(sd)[a-z][0-9]*"
```

- Flush all unused multipath device maps
  
```bash
multipath -F
```

- Restart the multipath service to apply the changes
```bash
systemctl restart multipathd
```

### Step 4: Create a new partition table and partition on the devices

- Start the parted tool
```bash
parted
```

- In the tool, you'd select the device, create a new GPT partition table, and then create a new xfs partition
- The below are commands inside parted
```bash
select device
mklabel gpt
mkpart primary xfs 0% 100% 
```
### Step 5: Format the partitions with xfs file system

- The -f option is used to force the format action
```bash
mkfs.xfs /dev/sda1 -f 
mkfs.xfs /dev/sdc1 -f
mkfs.xfs /dev/sdd1 -f
```

### Step 6: Mount the bricks

- Mount all entries from fstab
```bash
mount -a
```

- Display all currently mounted file systems to verify the bricks have been mounted
```bash
mount
```



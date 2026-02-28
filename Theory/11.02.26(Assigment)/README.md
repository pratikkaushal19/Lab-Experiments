# Assignment (11.02.26): Backup, Share and Remove Docker Volume
---

## Aim
To learn how to:

- Backup a Docker volume  
- Share volume data using backup file  
- Restore volume from backup  
- Remove Docker volumes safely  

---

## Step 1: List Docker Volumes

```bash
docker volume ls
```
![](./images/image1.jpeg)

Example:
local     test
local     myvolume

## Step 2: Backup Docker Volume
Backup volume test into a tar file:
```bash
docker run --rm \
  -v test:/data \
  -v $(pwd):/backup \
  ubuntu \
  tar cvf /backup/test-backup.tar /data
  ```
  ![](./images/image2.jpeg)
Backup file created:

test-backup.tar

Verify:
```bash
ls test-backup.tar
```
## Step 3: Share Volume Backup
The volume is shared by transferring the backup file:

**test-backup.tar**
This file can be uploaded to Google Drive, GitHub, or copied to another system.
![](./images/image3.jpeg)

## Step 4: Restore Backup into New Volume
Create a new volume:

```bash
docker volume create restoredtest
```
Restore backup:
```bash
docker run --rm \
  -v restoredtest:/data \
  -v $(pwd):/backup \
  ubuntu \
  tar xvf /backup/test-backup.tar -C /
  ```
![](./images/image4.jpeg)

## Step 5: Verify Restored Data
List files:

```bash
docker run --rm \
  -v restoredtest:/data \
  ubuntu \
  ls /data
  ```

Check content:
```bash
docker run --rm \
  -v restoredtest:/data \
  ubuntu \
  cat /data/sapid.txt
  ```
Output:
![](./images/image6.jpeg)

## Step 6: Remove Docker Volume
Remove volume (only if not in use):
```bash
docker volume rm test
```
![](./images/image7.jpeg)

## Conclusion
Docker volumes can be backed up as tar files, shared across systems, restored into new volumes, and removed safely. This ensures persistent and portable container data management.
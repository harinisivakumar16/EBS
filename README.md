## WORKING WITH EBS
## NAME: Harini S K
## REG NO: 212225230092
## Aim
To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

## Algorithm / Steps
Create a new Amazon EBS volume with a size of 1 GiB.
Select the same Availability Zone as the EC2 instance.
Attach the EBS volume to the EC2 instance using /dev/sdb.
Connect to the EC2 instance using AWS Systems Manager Session Manager.
Check the available storage using df -h.
Create an ext3 file system on the EBS volume.
Create the /mnt/data-store directory.
Mount the EBS volume to /mnt/data-store.
Configure /etc/fstab for automatic mounting.
Verify that the EBS volume is successfully mounted.
Create file.txt inside the mounted EBS volume.
Verify the contents of the created file.
Create an EBS snapshot named My Snapshot.
Delete file.txt from the original EBS volume.
Create a new EBS volume from the snapshot.
Attach the restored volume to the EC2 instance using /dev/sdc.
Create the /mnt/data-store2 directory.
Mount the restored volume to /mnt/data-store2.
Verify that file.txt has been successfully restored.
## Program
## 1. Check Available Storage
df -h
## 2. Create an ext3 File System
sudo mkfs -t ext3 /dev/sdb
## 3. Create a Mount Directory
sudo mkdir /mnt/data-store
## 4. Mount the EBS Volume
sudo mount /dev/sdb /mnt/data-store
## 5. Configure Automatic Mounting
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
## 6. View the File System Configuration
cat /etc/fstab
## 7. Verify the Mounted Volume
df -h
## 8. Create a File in the EBS Volume
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
## 9. Read the File
cat /mnt/data-store/file.txt
## 10. Delete the File
sudo rm /mnt/data-store/file.txt
## 11. Verify File Deletion
ls /mnt/data-store/
## 12. Create a Mount Directory for the Restored Volume
sudo mkdir /mnt/data-store2
## 13. Mount the Restored EBS Volume
sudo mount /dev/sdc /mnt/data-store2
### 14. Verify Snapshot Restoration
ls /mnt/data-store2/
Expected output:

file.txt
## Outputs
<img width="1920" height="1080" alt="Screenshot (174)" src="https://github.com/user-attachments/assets/e606523b-113c-4c8b-8791-0030630a03a4" />
<img width="1920" height="1080" alt="Screenshot (175)" src="https://github.com/user-attachments/assets/4266eac8-516a-4b55-a65c-55b0affce22a" />
<img width="1920" height="1080" alt="Screenshot (176)" src="https://github.com/user-attachments/assets/a17edcb5-f10e-4d5b-b55a-8ea7f283ddc4" />
<img width="1920" height="1080" alt="Screenshot (177)" src="https://github.com/user-attachments/assets/25ec4d52-c272-41f8-b1cf-e65934aa7f3e" />
<img width="1920" height="1080" alt="Screenshot (178)" src="https://github.com/user-attachments/assets/a573578d-e539-43fd-aed5-83263fec8c91" />
<img width="1920" height="1080" alt="Screenshot (179)" src="https://github.com/user-attachments/assets/ca44cf3f-d82a-4528-a8a0-ae428b3e53dd" />
<img width="1920" height="1080" alt="Screenshot (180)" src="https://github.com/user-attachments/assets/b5fb92b4-3940-488b-a5b4-fd6038c29841" />
<img width="1920" height="1080" alt="Screenshot (182)" src="https://github.com/user-attachments/assets/1037d71e-c8da-4546-9e2a-70edaccc94e1" />
<img width="1920" height="1080" alt="Screenshot (183)" src="https://github.com/user-attachments/assets/2e227a8f-468a-4387-9cbf-5221bf46ad62" />

## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.

***Snapshots:***<br>
An EBS Snapshot is a point-in-time backup of an EBS volume as an image stored in Amazon S3 (managed by AWS)<br>
By using the snapshot we can recreate the EBS volume with the same data<br>
Recover the data which got deleted accidentally <br>
If You want migrate Volume From Source region to Destination Region Snapshots Play’s a vital role while migrating Volumes from source to Destination region.

***Types of Snapshots:***
***1. Manual Snapshot*** <br>
    Manual Snapshot Is the process of creating the snapshot of EBS volume Manually by selecting the EBS volume.
    ```
    How to create : EC2 → Volumes → Select volume → Actions → Create snapshot
    ```
    <img width="1918" height="759" alt="image" src="https://github.com/user-attachments/assets/ca532ded-cdcf-4a9f-82e0-0fade3a08d42" />
    
  ***Snapshot Lock Options:***<br>
  1. Governance Mode: Can't be deleted by users without special permission<br>
  2. Compliance Mode: Can’t be deleted even by root or admins until lock period ends
  ```
  Go to Snapshots , Select snapshot → Click Actions → Manage Snapshot Lock
  Enable lock → Set Retention period (in days/months/years) and Mode
  Click Save
  ```
<img width="1386" height="788" alt="image" src="https://github.com/user-attachments/assets/54353432-a2dc-4dbd-81e9-205356d39dd5" />

***Share EBS Snapshot with Another Account***
    Snapshots must be unencrypted to share. (Encrypted snapshots can’t be shared directly)
    ```Console:
    Go to Snapshots
    Select your unencrypted snapshot
    Click Actions → Modify Permissions
    Choose Add account ID
    Enter target AWS Account ID and click Save
    ```
  The target account can now copy this shared snapshot into their account and region.
  
***2. Automated Snapshot***<br>
Created automatically using policies<br>
Tools: Amazon Data Lifecycle Manager (DLM) and AWS Backup<br>

***Example policy***
Daily snapshot at 2 AM, Keep last 7 days and Delete older ones automatically

***Steps***
***Step 1: Tag Your EC2 or EBS Volume***
```
Go to EC2 →  Volumes
Select your instance / volume
Click Tags → Manage tags
Add: Key: Backup and Value: Daily
```
<img width="1899" height="585" alt="image" src="https://github.com/user-attachments/assets/2989a5a5-e93b-4820-858e-c46552b3a3e2" />

***Step 2: Create Lifecycle Policy (DLM)***
```
Go to EC2 → Lifecycle Manager (DLM)
Click Create lifecycle policy
Policy details: Policy type: EBS snapshot policy
Resource type: Choose Instance (backs up all attached EBS volumes)OR Volume (backs up only specific volumes)
Target with tags:Key: Backup and Value: Daily
```
***Step 3: Schedule the Snapshots***
```
Choose when snapshots should run:
Frequency: Daily Time: e.g., 02:00
Retain: e.g. 7 snapshots
Example:
Take snapshot every day at 2 AM
Keep last 7 snapshots
Delete older ones automatically
```
<img width="1870" height="722" alt="image" src="https://github.com/user-attachments/assets/edba2b04-d460-4ea3-af24-500468b758d1" />

Now Create policy
<img width="1582" height="444" alt="image" src="https://github.com/user-attachments/assets/ce904cd9-8170-40da-ba7f-f8a4a4bf5c80" />

***3. Incremental Snapshot:***
 An incremental snapshot captures only the changes made since the last snapshot. This helps reduce storage costs and improves efficiency.

 ```
  Step 1: Create First Snapshot (Full Snapshot) (snap-1)
  Step 2: Change Data on the Volume
  Step 3: Take Second Snapshot (snap-2)
  Step 4: Verify (Conceptual)
  You won’t see “incremental” written in the console UI, but:
  snap-1 = full baseline
  snap-2 = incremental
  AWS automatically chains snapshots efficiently.
 ```

***Migrate Volume From One to Another Region:***<br>

Migrating an Amazon EBS (Elastic Block Store) volume from one AWS region to another involves a few steps. Here's a general overview of the process:.<br>

***Step 1: Create Snapshot of Source EBS Volume (Source Region)***
```
Go to EC2 → Volumes (in source region, e.g., N.Verginia)
Select the volume
Actions → Create snapshot
Name it: mumbai-vol-backup
Create and Snapshot created in N.Verginia region
```
<img width="1585" height="313" alt="image" src="https://github.com/user-attachments/assets/51ac0335-6bd2-4b0d-bb93-528a2afc601d" />

***Step 2: Copy Snapshot to Target Region***<br>
```
Go to EC2 → Snapshots
Select the snapshot
Actions → Copy snapshot
Choose Destination region (e.g., mumbai region)
Copy :Snapshot now exists in the target region
```
<img width="1647" height="641" alt="image" src="https://github.com/user-attachments/assets/87a72692-a3d2-4db8-9dbf-279740c95008" />

***Step 3: Create New EBS Volume in Target Region***
```
Switch AWS Console region to target region (e.g., N. Virginia)
Go to EC2 → Snapshots
Select the copied snapshot
Actions → Create volume
Choose: AZ (same AZ as target EC2) Volume type (gp3) Size (same or larger)
Create volume : New EBS volume created in target region
```
<img width="1541" height="335" alt="image" src="https://github.com/user-attachments/assets/ee185ede-2abd-4960-98b4-d8c1d47445f6" />

***Step 4: Attach Volume to EC2 in Target Region***
```
EC2 → Volumes
Select new volume
Actions → Attach volume
Choose target EC2 instance
Attach : Then mount inside OS (Linux/Windows) like normal.
```

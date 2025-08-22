📌 AWS EC2 + EBS Volume Management

📖 Overview

This project demonstrates how to:

1. Launch EC2 instances (Linux + Windows).


2. Install and configure a web server on both instances.


3. Create and attach a 5 GB EBS Volume to each EC2 instance.


4. Format and mount the EBS volume for use.


5. Take a snapshot of the EBS volume.


6. Create a new EBS volume from the snapshot and attach it to another EC2 instance.



This task simulates real-world AWS operations like storage provisioning, backup strategy, and disaster recovery.


---

🛠️ Tech Stack

AWS EC2 (Linux & Windows)

AWS EBS (Elastic Block Store)

AWS Snapshots

Web Servers

Apache (Linux)

IIS (Windows)




---

🚀 Step-by-Step Implementation

1. Launch EC2 Instances

Create 1 Linux EC2 (Amazon Linux 2 / Ubuntu) and 1 Windows EC2.

Use a key pair for SSH/RDP login.

Ensure Security Groups allow:

Linux → SSH (22), HTTP (80)

Windows → RDP (3389), HTTP (80)




---

2. Configure Web Servers

Linux (Apache):

sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Hello from Linux EC2</h1>" | sudo tee /var/www/html/index.html

Windows (IIS):

Enable IIS from Server Manager → Add Roles and Features.

Place index.html under C:\inetpub\wwwroot.

Verify via http://<public-ip>.



---

3. Create and Attach EBS Volume

Create a 5 GB EBS volume in the same AZ as your EC2.

Attach it to your Linux EC2 instance (/dev/sdb).


Linux Setup:

lsblk   # verify new disk
sudo mkfs -t ext4 /dev/sdb
sudo mkdir /data
sudo mount /dev/sdb /data
echo "/dev/xvdf /data ext4 defaults,nofail 0 2" | sudo tee -a /etc/fstab

Windows Setup:

Open Disk Management → Initialize disk.

Create New Simple Volume → Assign Drive Letter → Format as NTFS.



---

4. Create Snapshot

In AWS Console → Volumes → Select Volume → Actions → Create Snapshot.

Add tags for easy identification (e.g., Project=EBS-Demo).



---

5. Create New Volume from Snapshot

Navigate to Snapshots → Select → Create Volume.

Attach it to another EC2 instance.

Mount/assign as needed (Linux: mount, Windows: assign drive).



---

✅ Expected Output

Linux EC2 serving "Hello from Linux EC2".

Windows EC2 serving "Hello from Windows EC2".

Additional EBS volume available with snapshot data.



---

📊 Key Learnings

How to provision and attach EBS volumes.

How to persist data beyond instance termination.

How to create snapshots for backup and recovery.

How to restore storage from snapshots.



---

📸 Screenshots to Capture

EC2 instance list (Linux + Windows).

Running web server pages (Apache + IIS).

Attached EBS volumes in lsblk/Disk Management.

Snapshot creation screen.

New volume created from snapshot.

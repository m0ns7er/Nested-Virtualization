# Nested-Virtualization
Nested Virtualization on GCP


Goal is to install windows on google cloud platform in trial period. 

![image](https://github.com/m0ns7er/Nested-Virtualization/assets/13703520/5463b1c8-6ad3-44a6-acd8-600d743354dd)


Create ubuntu instance with N2 machine type (4vCPU, 2 Core, 16 GB memry) and do not boot up. Just stop it after creating instance. 

![image](https://github.com/m0ns7er/Nested-Virtualization/assets/13703520/297c0920-0165-446a-8446-2be3b70763ad)

![image](https://github.com/m0ns7er/Nested-Virtualization/assets/13703520/6e1476e1-a393-4623-9770-e293db7c0a97)


Open gcloud terminal and run below command (Which make image copy of vm with VMX enabled)

```
gcloud compute images create nested-ubuntu-image \
--source-disk=ubuntu --source-disk-zone=us-west4-b \
 --licenses="https://www.googleapis.com/compute/v1/projects/vm-options/global/licenses/enable-vmx"
```

Now delete the vm and create new one with same configuration  

Insted of selecting the os select import and select the exporetd image file.

![image](https://github.com/m0ns7er/Nested-Virtualization/assets/13703520/c6545e96-2a8d-48b4-896f-f59f6de7e8b4)

Run below command to check if VMX is enabled or not 

```
grep -cw vmx /proc/cpuinfo
```

# Ubuntu virtulization, VNCServer, GNOME-CORE packages installation. 

Download the zip
```
curl -o src-cloud.zip https://github.com/m0ns7er/Nested-Virtualization/blob/main/src-cloud.zip
```
Update the default repository and install unzip. 
```
sudo apt update
sudo apt -y install unzip
```

unzip src-cloud and install required packages. 

```
unzip src-cloud.zip
cd src-cloud/
./install.sh
```

Install VNC server and gnome-core packages. 
```
sudo apt-get update
sudo apt-get install tightvncserver
sudo apt-get install gnome-core
```

Start VNCServer
```
vncserver -localhost no
```



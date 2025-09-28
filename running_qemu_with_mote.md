## Setup `qemu` for XM1000 Mote Support (optional)

This document describes how to run `qemu` that can support code uploading to XM1000.

Due to the complicated security and permission setup in our lab PCs, **it is more complicated to run ContikiOS with a mote**. 
We shall use **Virtual Machine Manager** `virt-manager` to control our virtual machine and capture USB devices for our guest OS.

### Step 1: Copy the image to the `/scratch` folder

Unfortunately, `virt-manager` is unable to access your network drive. We need to copy the VM image from your network drive to the local drive.
Use the following command to copy the VM image into the `/scratch` directory which is a local drive:

```bash
cp /vol/teaching/CSEE/EEEM048.qcow2 /scratch/
```

> **Important**
> The image stored in `/stratch` will be kept in the local drive rather than your network drive.
> It is important that you delete the image after the lab session.
> It should only be used to learn how to upload and run your code in a mote. **You should not use it for your coursework development**.

To confirm that the file was copied successfully, do the following:
```bash
ls -l /scratch/EEEM048.qcow2
```
You should see a similar output to the one below (the size and date may vary):

```console
-rwxr--r-- 1 libvirt-qemu kvm 6815416320 Sep 26 15:47 /scratch/EEEM048.qcow2
```

### Step 2: Launch `virt-manager` to start VM creation

Open the **Virtual Machine Manager** (`virt-manager`). You should see the QEMU hypervisor listed.  
To create a new virtual machine, click the **"Create a new virtual machine"** icon in the top-left corner, as shown in the screenshot below:  
<p align="center">
  <img width="456" height="283" alt="Screenshot from 2025-09-26 16-25-12" src="https://github.com/user-attachments/assets/c105bab0-4c6f-4243-9312-288d9a54d850" />
</p>

### Step 3: Select the installation method

In the **New VM** window, choose **"Import existing disk image"** as the installation method.  
This tells `virt-manager` that you already have a prepared image file (the one you copied to `/scratch` in Step 1).  

Then click **Forward** to continue.
<p align="center">
  <img width="456" height="400" alt="image(1)" src="https://github.com/user-attachments/assets/9921df2e-632b-4f82-9db1-4fe080cef5ac" />
</p>

### Step 4: Select the VM image file
In the next window:  
1. Click **Browse…** to locate the VM image.  
2. In the storage browser, click **Browse Local** to search your filesystem.  
3. Navigate to the `/scratch` directory:  
   - Select **+ Other Locations**  
   - Choose **Computer**  
   - Open the **/scratch** folder  
4. Select the `EEEM048.qcow2` file.

<p align="center">
  <img width="456" height="350" alt="image(2)" src="https://github.com/user-attachments/assets/edd0435e-3281-4b90-8221-5866f01111fa" />
  <img width="456" height="350" alt="image(3)" src="https://github.com/user-attachments/assets/d443e5c6-655b-4889-b259-427e8d29dfe8" />
</p>

### Step 5: Confirm the image path and select OS type
Once you have selected the image, the path should now appear in the field as shown below. 
In the **Choose the operating system you are installing** section, make sure to set the OS type to **Generic or unknown OS (Usage is not recommended).**
This is required for the VM to run properly. After setting the OS type, click **Forward** to continue.  

<p align="center">
<img width="456" height="400" alt="image(4)" src="https://github.com/user-attachments/assets/6d0c274f-e090-468e-89a2-665c85e6e8ea" />
</p>  

### Step 6: Configure VM resources and Finish creation

In the **Memory and CPU settings** window:  
1. Set the **Memory (RAM)** to **4096 MB**.  
2. Leave the **Number of CPUs** set to **1** (default).
3. Click **Forward**.
4. You can set a new name for the VM if you want.
5. Click **Finish** to complete the VM creation.  

Your new VM will now appear in the list in `virt-manager`. You may now launch ContikiOS from `virt-manager`.

### Step 7: Capture XM1000

Once you have launched ContikiOS, you can use the file menu to redirect USB device. 
It allows you to capture XM1000 FTDI by redirecting the control from host OS to guest OS (ContikiOS).

<p align="center">
<img width="645" height="570" alt="image" src="https://github.com/user-attachments/assets/17162767-4af3-4bfe-a880-21dddc40786b" />
</p>

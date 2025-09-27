# Launching ContikiOS using `qemu` 

The instruction provides procedure to run ContikiOS for Cooja simulation and XM1000 mote experiment.
You are required to develop your coursework using Cooja. 
Optionally, you may also try to experiment with XM1000 mote for a session to understand the procedure to upload and test your code with a mote.
- [Cooja Simulation Setup](#chapter-1:-cooja-simulation-setup)
- [XM1000 Mote Setup](#xm1000-mote-setup) (Optional)


## Chapter 1: Cooja Simulation Setup

### Step 1: Copy the new image to your Download folder

Since qemu is not compatible with VMware, we have converted the image to qemu image format. 
You need to copy the new image (a single file) to your `Downloads` folder.
Note that you may need to delete the VMwave image to make space for the new image.

Open a terminal (hotkey:[Ctrl]+[Alt]+[T]) and type the following command to copy the new image to your `Downloads` folder. 
It may take a while to download the huge image file.

```bash
cp /vol/teaching/CSEE/EEEM048.qcow2 ~/Downloads/
```

Use the following command to confirm that you have downloaded the image file. It should show the file with a size of 6810828800 bytes.

```bash
ls -l ~/Downloads/EEEM048.qcow2
```

### Step 2: Launch qemu from the terminal

You need to first find the full path to the image file. You can find it by using the following command.

```bash
ls ~/Downloads/EEEM048.qcow2
```

You should see `/user/xxxx/xxxx/Downloads/EEEM048.qcow2` where `xxxx` is your user credential. 
Copy the following command and replace `...` with the full path.

```
qemu-system-x86_64 -cpu host -machine type=q35,accel=kvm -m 5000 \
  -drive if=virtio,format=qcow2,file=/user/...
```

You should now see the ContikiOS Window. You can rescale the window by using `View` menu and select `Zoom In` or `Zoom Out` to adjust the size.

Please make sure that you **shut down** Contiki inside the guest OS before closing the window, otherwise, your work may not be saved properly.

## Chapter 2: XM1000 Mote Setup

### Step 1: Copy the image to the `/scratch` folder

Use the following command to copy the VM image into the `/scratch` directory:

```bash
cp /vol/teaching/CSEE/EEEM048.qcow2 /scratch/
```
Then confirm that the file was copied successfully:
```bash
ls -l /scratch/EEEM048.qcow2
```
You should see a similar output to the one below (the size and date may vary):

``console
-rwxr--r-- 1 libvirt-qemu kvm 6815416320 Sep 26 15:47 /scratch/EEEM048.qcow2
``

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

Your new VM will now appear in the list in `virt-manager`.

## Launch the new VM to allow access to the XM1000 mote
### Step 1:
In virt-manager application you should be able to see the list of VMs that exist. Launch the VM you created, by rick click **RUN**. 
### Step 2: 
You should be able to **Redirect USB device** by clicking the **Virtual Machine** tab and selecting the XM1000 mote. 

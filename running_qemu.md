## Launching ContikiOS using `qemu` 

The instruction provides procedure to run ContikiOS for Cooja simulation. Note that this setup **DOES NOT** support XM1000 connectivity. You will use Cooja simulation environment to test your code.

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

### Backing up your work

Although the virtual machine will store your progress in the guest OS image for your next use, it is always a good practice to do your own backup. The VM image may fail to run if the VM was not shutdown properly.

To **backup** your source code from the guest OS to the host OS, you need to do the following:
- Open a terminal in the guest OS
- Change the directory to the folder that contains the source code
- Check to confirm that the file is in the folder
  - type `ls hello_world.c` to confirm that `hello_world.c` is in the folder
- Use secured copy command to copy it out to the host OS
  - `scp hello_world.c st0013@heron25:~/Downloads`
  - where `st0013` is your username and `heron25` is the hostname of the host PC
- You'll be prompted to enter your password. This is the password of your university account
- Your source code should now appear in your host OS under `Downloads` folder

To **restore** your source code from the host OS to the guest OS, you need to do the following:
- Open a terminal in the guest OS
- Change the directory to the folder that should receive the source code
- Use secured copy command to copy it from the host OS
  - `scp st0013@heron25:~/Downloads/hello_world.c ./`
  - where `st0013` is your username and `heron25` is the hostname of the host PC
- You'll be prompted to enter your password. This is the password of your university account
- Your source code should now appear in your guest OS

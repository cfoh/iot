## Launch ContikiOS using `qemu`

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
Copy the following command and replace `...` with the full path to the image.

```
qemu-system-x86_64 -cpu host -machine type=q35,accel=kvm -m 5000 \
  -drive if=virtio,format=qcow2,file=/user/...
```

You should now see the ContikiOS Window. You can rescale the window by using `View` menu and select `Zoom In` or `Zoom Out` to adjust the size.

Please make sure that you shut down Contiki inside the guest OS before closing the window, otherwise, your work may not be saved properly.

### Step 3: Setup the USB device


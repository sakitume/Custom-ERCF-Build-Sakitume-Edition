# Preparing the FYSETC ERB board
There is a Github repo for this board. It provides instructions on how to build and flash Klipper firmware onto the FYSETC ERB board. 
You can find that repo [here](https://github.com/FYSETC/FYSETC-ERB/tree/main)

I chose the option that lets you build and flash directly from your Klipper host (usually a Raspberry Pi....but not for me as I use other devices for my printers).

Run the following commands (line by line) on your Klipper host (usually a Raspberry Pi).
```
cd  ~/klipper
make clean
make menuconfig
```

Select the options as shown in this screenshot

![image](https://user-images.githubusercontent.com/875866/282971519-8c0c0980-0c48-4155-9825-7c400598ee80.png)

Exit the menu config using the `ESC` key. Then use the following command to actually build the firmware.

```
make
```

After the firmware is built you will want to power up the FYSETC ERB and get into boot mode so you can flash this firmware onto it. Follow these steps to get into boot mode.

1. Connect 24V to the ERB
2. Connect USB-C cable to ERB and your Klipper device (usually Raspberry Pi)
3. Push and hold the `BOOTSEL` button (keep this held down until step 6)
4. Push and hold `RST` button for 0.5 seconds, then release
5. Continue holding the `BOOTSEL` button for another 3 seconds, then release
6. The ERB will have reset into boot mode and you can verify this using `lsusb`

![image](https://user-images.githubusercontent.com/875866/282964661-ffb50e9f-df8c-4786-853a-c6263b9e284c.png)

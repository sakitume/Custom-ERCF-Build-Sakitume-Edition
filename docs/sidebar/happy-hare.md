# Setting up Happy Hare
Happy Hare is the software package that you will use with your new SturdyBunny/ERCF. It replaces the software described in the original ERCF v1.1 manual. 

> Note: Happy Hare isn't just for ERCF, it can work with other MMU systems. But for our purposes we are using it to interface with the SturdyBunny/ERCF we just built

**TODO**

## Just some misc notes while I'm working on this


## Basic install of Happy Hare
Clone Happy Hare v2.2 from the Github repo

```
cd ~
git clone https://github.com/moggieuk/Happy-Hare.git
cd Happy-Hare
```

The docs say there's a way to perform a kind of dry-run of the install without actually modifying your current installation. It will end up creating the files that a normal install would but it will place them into your `/tmp` folder so you can inspect them before doing a real install.
```
./install.sh -i -c /tmp -k /tmp
```

This let me inspect what it would do (look in the `mmu` subfolder it creates and view the files)

Then I decided to actually install it:

```
cd ~/Happy-Hare
./install.sh -i
```

Using the `-i` parameter so that the install script will interactively prompt you for various options. The first question you are asked is what type of MMU are you running. For this build I tried several of the options before determining the best one. The options I chose were "ERCF v1.1. (all variations)", "ERCF v2.0" and "Other (Custom creation, ...)".

I intitially thought that "ERCF v2.0" might be the best option, since I'm using SturdyBunny, Thumper Blocks, Springy and Binky. But the problem is that if you choose "ERCF v2.0" some configuration values will be generated based on Happy Hare thinking you're using the 23.05mm wide Triple Decky filament blocks when we're actually using the 21.0mm Thumper Blocks. This ends up breaking the `MMU_CALIBRATE_SELECTOR` auto-calibration later on.

I tried custom but that wasn't sufficient as well. It turns out that "ERCF v1.1. (all variations)" is actually what you want as it will let you specify each mod you're using. When it ask you if you are using "Triple-Decky" just say no and it will end up using the correct 21.0mm width that Thumper Blocks and original SturdyBunny/ERCF uses.

Here's what the install script looks like when I ran it and chose the correct options for my particular build.

```
donovan@kp:~/Happy-Hare$ ./install.sh -i

Klipper config directory (/home/donovan/printer_data/config) found
Klipper service found
Reading default configuration parameters...

Let me see if I can help you with initial config (you will still have some manual config to perform)

What type of MMU are you running?
1) ERCF v1.1 (all variations)
2) ERCF v2.0
3) Tradrack v1.0
4) Other (Custom creation, ...)
MMU Type? (1-4)? 1
Some popular upgrade options for ERCF v1.1 are supported. Let me ask you about them...
Are you using the 'Springy' sprung servo selector cart (y/n)? y
Are you using the improved 'Binky' encoder (y/n)? y
Are you using the wider 'Triple-Decky' filament blocks (y/n)? n

----------
Let me see if I can help you with initial config (you will still have some manual config to perform)...
Are you using the EASY-BRD or Fysetc Burrows ERB controller? (y/n)? y
Great, I can setup almost everything for you. Let's get started

----------
You seem to have a RP2040-based controller serial port.
Are you using the Fysetc Burrows ERB controller? (y/n)? y
----------
This looks like your ERB controller serial port. Is that correct?
/dev/serial/by-id/usb-Klipper_rp2040_E66888351B82A336-if00 (y/n)? y

Board Type: ERB

----------
Touch selector operation using TMC Stallguard? This allows for additional selector recovery steps but is difficult to tune
Enable selector touch operation (not recommend if you are new to MMU / Happy Hare (y/n)? n

----------
How many gates (selectors) do you have (eg 3, 6, 9, 12)?
Number of gates? 6

----------
Do you have a toolhead sensor you would like to use?
(if reliable this provides the smoothest and most reliable loading and unloading operation)
Enable toolhead sensor (y/n)? n

----------
Which servo are you using?
1) MG-90S
2) Savox SH0255MG
Servo? (1-2)? 1

----------
Clog detection? This uses the MMU encoder movement to detect clogs and can call your filament runout logic
Enable clog detection (y/n)? y
    Would you like MMU to automatically adjust clog detection length (recommended)?
    Automatic (y/n)? y

----------
EndlessSpool? This uses filament runout detection to automate switching to new spool without interruption
Enable EndlessSpool (y/n)? n

----------
Finally, would you like me to include all the MMU config files into your printer.cfg file
Add include? (y/n)? y
    Would you like to include Mini 12864 menu configuration extension for MMU
    Include menu (y/n)? n
    Would you like to include legacy ERCF_ command set compatibility module
    Include legacy ERCF command set (y/n)? y
    Would you like to include the default pause/resume macros supplied with Happy Hare
    Include client_macros.cfg (y/n)? n

mmu_vendor: ERCF
mmu_version: 1.1sb
mmu_num_gates: 6
servo_up_angle: 30
servo_move_angle: 30
servo_down_angle: 140
enable_clog_detection: 2
enable_endless_spool: 0
gate_parking_distance: 23


    vvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvvv

    NOTES:
     What still needs to be done:
     * Tweak motor speeds and current, especially if using non BOM motors
     * Adjust motor direction with '!' on pin if necessary. No way to know here
     * Move you extruder stepper configuration into mmu/base/mmu_hardware.cfg
     * Adjust your config for loading and unloading preferences

    Advanced:
         * Tweak configurations like speed and distance in mmu/base/mmu_parameter.cfg

    Good luck! MMU is complex to setup. Remember Discord is your friend..

    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Copying original printer.cfg file to /home/donovan/printer_data/config/printer-20231114_205612.cfg-old
Copying configuration files into /home/donovan/printer_data/config/mmu directory...
Config directory /home/donovan/printer_data/config/mmu already exists - backing up old config files to /home/donovan/printer_data/config/mmu-20231114_205612
Installing configuration file mmu.cfg
Installing configuration file mmu_hardware.cfg
Installing configuration file mmu_parameters.cfg
Installing configuration file mmu_software.cfg
Skipping copy of mmu_vars.cfg file because already exists
Linking mmu extensions to Klipper...
Linking mmu extension to Moonraker...
Adding update manager to moonraker.conf
[update_manager happy-hare] already exists in moonraker.conf - skipping install
[mmu_server] already exists in moonraker.conf - skipping install
Klipper not restarted automatically because you need to validate and complete config

Done.  Enjoy ERCF (and thank you Ette for a wonderful design)...

(\_/)
( *,*)
(")_(") Happy Hare Ready

donovan@kp:~/Happy-Hare$
```

After this install I restarted the Klipper firmware (using Mainsail) and then i performed the basic hardware config/tests found in the [hardware configuration doc](https://github.com/moggieuk/Happy-Hare/blob/main/doc/hardware_config.md). 

Then I started to perform the calibration steps described in the [MMU Calibration Doc](https://github.com/moggieuk/Happy-Hare/blob/main/doc/calibration.md)

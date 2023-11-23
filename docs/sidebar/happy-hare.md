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

This should complete the basic install. You will want to restart the Klipper firmware (using Mainsail interface) before continuing on with calibration.
After this install I restarted the Klipper firmware (using Mainsail) and then i performed the basic hardware config/tests found in the [hardware configuration doc](https://github.com/moggieuk/Happy-Hare/blob/main/doc/hardware_config.md). 

## Hardware configuration/testing of our ERCF for use with Happy Hare
The basic hardware configuration steps are found in the [hardware configuration doc](https://github.com/moggieuk/Happy-Hare/blob/main/doc/hardware_config.md). 
I will summarize the steps that I followed with some clarification and/or pointers.

TODO elaborate on this section.

* I checked that the endstop was working (use MainSail query endstops, manually trigger the switch, view that it is triggered with Mainsail, etc)
* Use `MMU_MOTORS_OFF` to ensure all motors off, move selector manually to middle, use `MMU_HOME` to test selector moves in the proper direction. Adjust config if needed.
* Check encoder via `MMU_ENCODER`, insert filament and push/pull so it moves the encoder wheel, re-issue `MMU_ENCODER` and value should always increase


## Basic calibration/testing of your ERCF for use with Happy Hare

The calibration steps are described in the [MMU Calibration Doc](https://github.com/moggieuk/Happy-Hare/blob/main/doc/calibration.md).
I will summarize the steps that I followed with some clarification and/or pointers.

### Step 1. Calibrate selector offsets

Line up the selector against the first gate (Gate 0) so that you can pass filament from inlet side to outlet side. Using your fingers, rotate the selector pulley clockwise/counter-clockwise back and forth slightly, you'll see that there is a small range that you can move the selector as the filament is keeping it in place. Use the pulley
to center the selector in the middle of this range. 

> Pro Tip: Look at the belt teeth by the selector edge, using the selector edge as visual marker. This will tell you how much range is available, usually around one tooth. Halve this number of teeth to find the center.

```
MMU_CALIBRATE_SELECTOR GATE=0
```

Repeat this process for gate 1 and changing the macro `GATE` parameter to `1`
```
MMU_CALIBRATE_SELECTOR GATE=1
```

Repeat this for the rest of the gates remembering to change the `GATE` parameter each time.

After you've done this for all of the gates you should now be able to select any gate using the `MMU_SELECT TOOL=XXX` command where `XXX` is replaced with the gate/tool number. For example the following will move the selector to gate 4.

```
MMU_SELECT TOOL=4
```

You can also use `MMU_HOME` command to select a gate/tool but this command will first home the selector before selecting the gate/tool.


> Note: If you execute the either `MMU_HOME` or `MMU_SELECT` command, the selector motor will remain engaged. Do not try to manually move the selector unless you turn off the motor via `MMU_MOTORS_OFF`.

### Step 2. Calibrate your gear stepper
Issue the following in the console to home the selector and the move the selector to a convenient gate (gate 2 in this case)
```
MMU_HOME TOOL=2
```
Have at least 400mm of filament handy. Either a length you've cut to size or on a spool holder that can freely feed this amount to the ERCF.

```
MMU_SERVO POS=down
```

```
MMU_CALIBRATE_ENCODER
```

### Step 3. Calibrate bowden length


## Configuration

### Extruder homing

TODO: Just collecting some notes, for now.


I'm using a Sherpa mini with a reverse bowden tube. The reverse bowden tube will pop out of the Sherpa because it isn't locked onto it with anything, just a friction fit.
I think I will give this Sherpa mod a try:
https://www.printables.com/model/591576-sherpa-mini-with-zero-ecas-and-filament-sensor-mod

I found a simple/faster solution to use. It is a simple bracket that mounts onto the Sherpa mini. This way I don't have to disassemble and reassemble the extruder and be able to instead focus on the ERCF project.
https://www.printables.com/model/462294-sherpa-mini-ptfe-coupler-holder-reverse-bowden-pc4


NOTE: The following is just a copy/paste from the [Happy Hare documentation](https://github.com/moggieuk/Happy-Hare/blob/main/doc/configuration.md)

```yaml
# Extruder homing ---------------------------------------------------------------------------------------------------------
#
# Happy Hare needs a reference "homing point" close to the extruder from which to accurately complete the loading of the toolhead.
# This homing operation takes place after the fast bowden load and it is anticipated that that load operation will leave the
# filament just shy of the homing point. If using a toolhead sensor this initial extruder homing is unecessary (but can be forced)
# because the homing will occur inside the extruder for the optimum in accuracy.
#
# In addition to an entry sensor "mmu_extruder" it is possbile to Happy Hare to "feel" for the extruder gear entry by colliding
# with it. Because this method is not completely deterministic you might find have to find the sweetspot for your setup by adjusting
# the TMC current reduction. Also, touch (stallguard) sensing is possible to configure but unfortunately doesn't work well with
# some external EASY-BRD or ERB mcu's. Note that reduced current during collision detection can also prevent unecessary filament griding.
#
# Possible homing_endtop names:
#   collision      - Detect the collision with the extruder gear by monitoring encoder movement
#   mmu_gear_touch - Use touch (stallguard) detection when the gear stepper hits the extruder
#   mmu_extruder   - If you have a "filament entry" endstop configured
# Note the homing_endstop will be ignored if a toolhead sensor is available unless `extruder_force_homing: 1`
#
extruder_homing_max: 50			# Maximum distance to advance in order to attempt to home the extruder
extruder_homing_endstop: collision	# Filament homing method/endstop name
extruder_homing_current: 40		# % gear_stepper current (10%-100%) to use when homing to extruder homing (100 to disable)
#
# In the absence of a toolhead sensor Happy Hare will automatically default to extruder entrance detection regardless of
# this setting, however if you have a toolhead sensor you can still force the additional (unecessary) step of initially homing to
# extruder entrance then homing to the toolhead sensor
extruder_force_homing: 0
```
`gsx8299` helped me with some questions about this and offered some [advice](https://discord.com/channels/460117602945990666/909743915475816458/1176955206626459669).


# ERCF Filament Cutter
TODO Move following to a new page
```
CUTTER_OPEN
CUTTER_CLOSE
```

```
SET_SERVO SERVO=cut_servo  ANGLE=0
```
```
SET_SERVO SERVO=cut_servo  ANGLE=5
```




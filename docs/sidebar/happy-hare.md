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

I tried custom but that wasn't sufficient as well. It turns out that choosing "ERCF v1.1. (all variations)" worked the best as it will let you specify each mod you're using. When it asks you if you are using "Triple-Decky" just say no and it will end up using the correct 21.0mm width that Thumper Blocks and original SturdyBunny/ERCF uses.

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

Since I had used a spare Nema17 for the gear motor I found that 


## Basic calibration/testing of your ERCF for use with Happy Hare

The calibration steps are described in the [MMU Calibration Doc](https://github.com/moggieuk/Happy-Hare/blob/main/doc/calibration.md).
I will summarize the steps that I followed with some clarification and/or pointers.

### Step 1. Calibrate selector offsets

Line up the selector against the first gate (Gate 0) so that you can pass filament from inlet side to outlet side. Using your fingers, rotate the selector pulley clockwise/counter-clockwise back and forth slightly, you'll see that there is a small range that you can move the selector as the filament is keeping it in place. Use the pulley
to center the selector in the middle of this range. 

> Pro Tip: Look down and see where the side of the selector lines up against a filament block hopefully its just a couple of millimeters away from a filament block edge. Then move back the selector back and forth until you figure out the range that it travels, then slide the selector's edge until it is in the middle of that range. Alternatively  look at the belt teeth by the selector edge, using the selector edge as visual marker. Move the selector back and forth and see how many teeth/valleys it travels within. This will tell you how much range is available, usually around two teeth/valleys. Halve this number to find the center and place the selector's edge at that point.

```
MMU_CALIBRATE_SELECTOR GATE=0
```

Repeat this process for gate 1 and changing the `GATE` parameter to `1`
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


The "end" block (part `Filament_Blocks_End_Nobearing_V2A.stl`) has a built-in bypass hole. It doesn't have an ECAS collet like a real filament block but is usable as a quick and easy bypass. 


Filament End block with bypass hole
![image](https://gist.github.com/assets/875866/5309e270-5f31-4aac-8081-430fc94f0af7)


If you wish to use this then you should also configure HappyHare about its offset now. Its the same procedure. Line up the selector to this bypass hole, feed the filament and center the selectior. Then issue this command so it knows you're setting the position for the bypass.

```
MMU_CALIBRATE_SELECTOR BYPASS=1
```


### Step 2. Calibrate your gear stepper
Issue the following in the console to home the selector and the move the selector to a convenient gate (gate 2 in this case)
```
MMU_HOME TOOL=2
```
> Note: You could also just use `MMU_HOME` (without the specifying `TOOL`) in which case gate 0 will be selected.

Have at least 400mm of filament handy. Either a length you've cut to size or on a spool holder that can freely feed this amount to the ERCF.
Feed this by hand into the gate until the filament exits the ECAS04 collet on the selector and then pull back until it is flush with the collet.

Attempt to move 100mm of filament
```
MMU_TEST_MOVE MOVE=100
```

Measure how much was actually moved and enter the following command with that value. That's it. Happy Hare now knows how to much to move the stepper motor to move a particular amount of filament.
```
MMU_CALIBRATE_GEAR MEASURED=99.5
```

### Step 4. Calibrate encoder
```
MMU_CALIBRATE_ENCODER
```

### Step 3. Calibrate bowden length

The Happy Hardware documentation now wants you to calibrate the bowden length, and another simple macro is used for that. You just need to guesstimate the length of the bowden tube and subtract about 30mm from your guess. Let's say I measure around 350mm. I'd use this command.
```
MMU_CALIBRATE_BOWDEN BOWDEN_LENGTH=350
```

#### But wait!
There are a few things I think you should really test/adjust **before** trying to calibrate your bowden length. This is important because this will be the first calibration step that will use the servo and push down on the tophats. So I really think it is important to ensure the servo arm is properly installed and if you're using the Springy mod, properly tensioned.

[Here is a short writeup on how I setup the servo arm](./align-servo.md)


> Note: By default Happy Hare configures itself to use "collision" method. You can verify this by examining your `mmu_parameters.cfg` file and looking search for `extruder_homing_endstop`. While I eventually switched to using the "touch" (Stallguard) method I'm keeping my notes for when I used the "collision" method.

But wait...there's more! **Another important thing** you must do is check your `mmu_hardware.cfg` and ensure the run current is appropriate for your gear stepper motor.


```yaml
# FILAMENT DRIVE GEAR STEPPER  ---------------------------------------------------------------------------------------------
# Note that 'mmu_toolhead' endstop will automatically be added if a toolhead sensor is defined
#
# The default values are tested with the BOM NEMA14 motor. Please adapt these values to the motor you are using
# Example : for NEMA17 motors, you'll usually use higher current
#
[tmc2209 stepper_mmu_gear]
uart_pin: mmu:MMU_GEAR_UART
uart_address: 0 			# Comment out for ERB board
interpolate: True
run_current: 0.5			# NEMA14 motor
hold_current: 0.1			# Recommend this is minimal to reduce power consumption (unless issues with TMC stallguard)
sense_resistor: 0.110			# 0.15 for BTT TMC2226
stealthchop_threshold: 0		# Spreadcycle has more torque and better at speed
#
# Uncomment two lines below if you have TMC and want the ability to use filament "touch" homing with gear stepper
#diag_pin: ^mmu:MMU_GEAR_DIAG		# Set to MCU pin connected to TMC DIAG pin for gear stepper
#driver_SGTHRS: 60			# 255 is most sensitive value, 0 is least sensitive
```

The `run_current` parameter is what you want to verify and possibly adjust. I'm using a Nema17 pancake motor, the default value you see here of `0.5` wasn't sufficient for my case. I initially had issues trying to calibrate my Bowden tube length because of this!!! It took me a bit of head scratching and inspecting the Happy Hare logs and Happy Hare source code to figure out that the process it was using to check for when the filament hit the extruder ("collision") wasn't working because the run current was too low. 
I decided to use `0.650` and that worked for my particular setup.

### What `MMU_CALIBRATE_BOWDEN` actually does

Okay, if you've addressed those pre-requisites we're almost ready to run the `MMU_CALIBRATE_BOWDEN` command that I mentioned. But let me describe how it works. 
In this example we'll say the bowden tube is about 530mm and we'll execute the following command.

```
MMU_CALIBRATE_BOWDEN BOWDEN_LENGTH=500 
```

Happy Hare will spin the gear motor until 500mm of filament have been extended into the bowden tube. Then it will repeatedly push out 3mm of filament, after each push it will see if the filament has moved or if it has collided with the extruder gears. When it detects no movement has occured after a push it concludes that it has collided with the extruder gears and stops trying to push any more filament. It does this three times.

> Note: During those 3mm steps that it performs, it **reduces the run current** of the stepper motor. This way when the filament collides with the extruder gears the gear stepper motor can skip steps or the BMG gears slip. I don't know exactly which of these two it is designed to do but I'm hoping the stepper motor skips rather than the BMG gears grinding the filament. 

Okay. Run that command with a guess of how long your filament is. When you do this watch the filament end through your reverse Bowden tube. Hopefully you'll see it push the filament through tube and stop before it hits the extruder and then it performs those incremental 3mm steps until it hits. If it doesn't stop before the extruder and just rams into it reduce the `BOWDEN_LENGTH` value. If it stops too soon and then performs those 3mm incremental steps but never reaches the extruder than increase the value of the `BOWDEN_LENGTH` parameter (or add the `HOMING_MAX=100` parameter as the default is 50 and 100 or more can be specified).

Okay...if all goes well Happy Hare will perform 3 full tests (that you'll see being logged into the console) and then it will compute and save the actual length it detected and this part of your calibration is now done!

**One last thing** 

You might want to consider tuning the reduced run current I mentioned earlier. The HappyHare docs say you can adjust the current when using "collision" method by adjusting the `extruder_homing_current` parameter in your `mmu_parameters.cfg` file. Here's what that section looks like:

```
extruder_homing_current: 40		# % gear_stepper current (10%-100%) to use when homing to extruder homing (100 to disable)
```


### The `mmu.log` can help you diagnose things
Remember about that `run_current` setting? The reason I know about it is because I initially did this bowden calibration wrong by trying to work around a weird issue, not recognizing it for what it really was. Here's the story...

The main issue I had trying to calibrate the bowden tube length was that Happy Hare was never pushing the filament to the extruder gears unless I overshot *by a large amount* the guesstimated distance from the ERCF to the extruder. So to make it "work" I simply gave it a large value until it hit the extruders and then it was able to detect that the filament had stopped and definitely "collided" with the extruder gears. I did not know how HappyHare was supposed to work and thought I just needed to do that. But I recognized later that this just didn't seem right. 


I re-read the Happy Hare documentation and it is supposed to advance up to `extruder_homing_max` (which is set to `50`) as it tries to collide with the extruder. This definitely wasn't happening for me. It would simply say "sorry...not working" (not really...but something short and simple was displayed...can't remember what exactly).
I then examined the source code and traced it down to the code that performs this advancement. The code will *log* how many steps it will take and the outcome of each step.
Ah...so the logfile should have clues! It is found at `~/printer_data/logs/mmu.log`. Sure enough, here is the relevant info it logged

```log
11:28:57 Calibrating bowden length from reference Gate #0
11:28:57 - DEBUG: Selecting tool T0 on gate #0...
11:28:57 Tool T0 enabled
11:28:57 - - TRACE: Setting MMU gear motor rotation distance ratio to 1.000000
11:28:57 - - TRACE: Processing idle_timeout 'printing' event
11:28:58 - DEBUG: Setting servo to down (filament drive) position at angle: 135
11:29:00 - - TRACE: Initial load into encoder. Stepper: 'gear' moved 70.0mm, encoder measured 45.7mm (delta 24.3mm). Pos: @70.0, (45.7mm)
11:29:00 - DEBUG: Loading bowden tube
11:29:02 - - TRACE: Course loading move #1 into bowden. Stepper: 'gear' moved 254.3mm, encoder measured 253.2mm (delta 1.1mm). Pos: @300.0, (299.9mm)
11:29:02 Finding extruder gear position (try #1 of 3)...
11:29:02 - DEBUG: Homing to extruder gear, up to 50.0mm in 3.0mm steps
11:29:02 Modifying MMU gear stepper run current to 27% for collision detection
11:29:03 - - TRACE: Homing step #1. Stepper: 'gear' moved 3.0mm, encoder measured 0.0mm (delta 3.0mm). Pos: @303.0, (300.8mm)
11:29:03 - DEBUG: Extruder entrance found after 3.0mm move (1 steps), encoder measured 0.0mm (delta 3.0mm)
11:29:03 Restoring MMU gear stepper run current to 100% configured
11:29:03 - DEBUG: Setting servo to up (filament released) position at angle: 50
11:29:04 Failed to detect a reliable home position on this attempt
```

This line is crucial:
```
11:29:03 - - TRACE: Homing step #1. Stepper: 'gear' moved 3.0mm, encoder measured 0.0mm (delta 3.0mm). Pos: @303.0, (300.8mm)
```
It tells us that *the very first step* it executed to creep towards the extruder didn't work. It moved the gear 3mm but the filament didn't move at all.
**My guess is that my reduced run current was too low**. And after finding the correct parameter to adjust and bumping it up, I could observe that Happy Hare was now able to creep the remaining distance using 3mm steps.

> Moral of the story: The log file along with some deductive reasoning can help. Even if you aren't able to decipher the log, you might be able to share it with someone (say over discord) who can help as it will give them more specific info about what might be happening


### Ensure your bowden tube is locked to the extruder

I'm using a Sherpa mini with a reverse bowden tube. The reverse bowden tube will pop out of a standard Sherpa mini because it isn't locked onto it with anything, just a hole with a slight friction fit.

I ended up rebuilding it with this ["Sherpa Mini with Zero, ECAS, and Filament Sensor mods"](https://www.printables.com/model/591576-sherpa-mini-with-zero-ecas-and-filament-sensor-mod)


## Setting up "Touch" (Stallguard) for extruder

Like I mentioned earlier, I initially used "collision" method but based on a post from Xon about "touch", I agreed with their description that "touch" is better as it doesn't lead to (as much) grinding of the filament. That is if you can make it work.

Adjust `mmu_hardware.cfg` to enable stallguard (touch). Here is what that section looks like by default:
```yaml
# SELECTOR STEPPER  --------------------------------------------------------------------------------------------------------
#
[tmc2209 stepper_mmu_selector]
uart_pin: mmu:MMU_SEL_UART
uart_address: 1 			# Comment out for ERB board
run_current: 0.4			# NEMA14 motor
hold_current: 0.2			# Recommend this is small to reduce power consumption (unless issues with TMC stallguard)
interpolate: True
sense_resistor: 0.110
stealthchop_threshold: 100		# Stallguard "touch" movement (slower speeds) best done with stealthchop
#
# Uncomment two lines below if you have TMC and want to use selector "touch" movement and homing
#diag_pin: ^mmu:MMU_SEL_DIAG 		# Set to MCU pin connected to TMC DIAG pin for selector stepper
#driver_SGTHRS: 75			# 255 is most sensitive value, 0 is least sensitive
```

Those last two lines need to be uncommented (remove the leading `#` character). 
While testing this and playing with the sensitivity values I found that the default of 60 worked, while a value of 90 was too sensitive

Docs say you can adjust the current when using "collision" method, not sure this setting also applies when using "touch"
I'm gong to try it. For collision I use 45%
```
extruder_homing_current: 35		# % gear_stepper current (10%-100%) to use when homing to extruder homing (100 to disable)
```

Use the `MMU_CALIBRATE_BOWDEN` command as previously described after the above tests. It will not perform that incremental stepping to hit the extruder gears like it does with the "collision" method.


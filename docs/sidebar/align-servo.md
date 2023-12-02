
Again, some quick notes for now. TODO polish this

You cannot install and align the servo arm until you've assembled most of your ERCF as well as installed Happy Hare. This is because
the servo has splines that the servo arm aligns to. You want to make sure the servo arm is in a known position (either Up or Down) before
you attache the servo arm to the servo and tighten it down.

Reference the [Happy Hare section of this document](./happy-hare.md) and have a basic install of Happy Hare running before continuing with the rest of this section.

## Aligning the servo arm
After you've established that you can issue `MMU` commands (via the console) to control the ERCF you can use the following command to set the servo to the `UP` position:
```
MMU_SERVO POS=up
```

Toggle between up and down positions (ending in up) a few times to make sure servo is working and alleviate any backlash in the gearing:
```
MMU_SERVO POS=down
MMU_SERVO POS=up
MMU_SERVO POS=down
MMU_SERVO POS=up
```

Place the servo arm into position so that it looks similar to what you see in the following pictures.

TODO, place pictures here

From the backside notice how the stopper portion of the arm is just about touching the body of the servo, but with a slight gap. This may differ by a tiny amount (compared to my pics) because each servo is different and the splines might line up just a tad bit different than mine has. If it doesn't seem right you can retry and adjust by one spline tooth to see if that looks better.

Once you're happy with the position of the arm snug it down with the screw. The Happy Hare default values for `UP` and `DOWN` position are pretty good but I strongly suggest you test it out and fine tune it. At the very least make sure the values aren't too high or low so that the servo doesn't try to go beyond the range that its physical stopper allows it. Since you've installed the servo arm while the servo was in the `UP` position hopefully you'll only need to fine tune the `DOWN` position (if needed).

Issue the following command to see how the arm looks when in the `DOWN` position
```
MMU_SERVO POS=down
```

Try toggling back and forth between the two positions to make sure you're happy with everything. If the servo is trying to go a little too far past its physical limits you can adjust the servo angles used for `UP` and `DOWN`. I describe how to do that in the following section.

## Fine tuning the servo arm angles

You should first make sure your `DOWN` angle isn't too high that the servo arm bumpstop (portion of the servo arm) isn't colliding with the body of the servo. This will be your maximum angle to use when fine tuning. The default that Happy Hare set for you might be perfectly fine, but it is best to check for yourself.

After that you should fine tune the `DOWN` angle so that the servo arm achieves an ideal position against the tophats of your filament blocks. What that angle is depends on which filament block tophat you have (Triple-Decky vs Thumper Blocks) and also your servo choice. I can provide you some general guidelines based on my own experience.

If you're using Springy, back off on the tensioner screw all the way. Swing up the upper part of the ERCF so you can easily view the servo. Back off that screw while applying slight pressure to the servo and watch and feel until you know it has reached its upper limit of travel. 

> Note: You can leave it like this for now (and tighten down the tensioner screw as needed when you check for filament slippage. Or you can preload the spring by turning it just a bit so that you can see the servo has moved down just a little bit.


You can then swing back this upper assembly and latch it into place and select a gate that you want to work with, in the following example I use the 3rd gate, gate 2.

```
MMU_SELECT TOOL=2
```

Place a short length of filament so it exits the ERCF by a small amount. Next issue the following command to engage the servo so that the BMG gears clamp down on the filament.

```
MMU_SERVO POS=down
```

Grab one end of the filament with one hand, and with the other hand hold onto the knob at the end of the D-Shaft so that it doesn't turn. Tug on the filament and see if the filament slips between the gears. You can either adjust the angle to try and get more leverage, and/or you can adjust the Springy tensioner screw.

### How to set the servo angle
To adjust the servo angle you'll need to figure out how to set a specific numeric value for it. Examine your `mmu_parameters.cfg` file and look for a section that looks like this:

```yaml
# Servo configuration  -----------------------------------------------------------------------------------------------------
#
# Angle of the servo in three named positions:
#   up   = tool is selected and filament is allowed to freely move through gate
#   down = to grip filament
#   move = ready the servo for selector move (optional - defaults to up)
#
# Note that leaving the servo active when down can stress the electronics and is not recommended with EASY-BRD or ERB board
# unless the 5v power supply has been improved and it is not necessary with standard ERCF build.
# Make sure your hardware is suitable for the job!
#
servo_up_angle: 30              # Default: MG90S servo: Up=30    ; SAVOX SH0255MG: Up=140
servo_down_angle: 140           # Default: MG90S servo: Down=140 ; SAVOX SH0255MG: Down=30
servo_move_angle: 30            # Optional angle used when selector is moved (defaults to up position)
```

The `servo_down_angle` is set to 140. That means when the `MMU_SERVO POS=down` command is executed, the angle of the servo arm is set to 140. If that is too much, or too little you the following command provide different values for the `ANGLE` parameter. The example below sets the servo angle to 130.

```
SET_SERVO SERVO=mmu_servo  ANGLE=130
```

So the process I used to set the angle was to issue `MMU_SERVO POS=down` (after selecting a gate of course), then by visually inspecting and/or testing for filament slip I could use `SET_SERVO SERVO=mmu_servo  ANGLE=XXX` (where `XXX` is a guess of what I think might work better) to test an angle. Once I found a value that I liked I then edited the value of `servo_down_angle` in the `mmu_parameters.cfg` file.

> You'll try to get what you think is a good feel or compromise. What the exact angle and/or Springy tensioner adjustment you should have is something you'll need to judge for yourself and will likely want to fine tune even further once you have your ERCF up and running and you work out issues that come up.

### My final angles

Here's what I ended up putting into my `mmu_parameters.cfg` file. What you end up will almost assuredly be be different.
```yaml
# Servo configuration  -----------------------------------------------------------------------------------------------------
#
# Angle of the servo in three named positions:
#   up   = tool is selected and filament is allowed to freely move through gate
#   down = to grip filament
#   move = ready the servo for selector move (optional - defaults to up)
#
# Note that leaving the servo active when down can stress the electronics and is not recommended with EASY-BRD or ERB board
# unless the 5v power supply has been improved and it is not necessary with standard ERCF build.
# Make sure your hardware is suitable for the job!
#
#servo_up_angle: 30            # Default: MG90S servo: Up=30    ; SAVOX SH0255MG: Up=140
#servo_down_angle: 140            # Default: MG90S servo: Down=140 ; SAVOX SH0255MG: Down=30
#servo_move_angle: 30            # Optional angle used when selector is moved (defaults to up position)

# These values are ones I checked using: SET_SERVO SERVO=mmu_servo ANGLE=50
# and work best with my MG90S servo, servo arm and Thumper Blocks configuration
servo_up_angle: 50
servo_down_angle: 135
servo_move_angle: 50
```

I commented out the original values so I could easily refer to them if I ever needed to. I set the `servo_move_angle` to be the same as my `servo_up_angle`.


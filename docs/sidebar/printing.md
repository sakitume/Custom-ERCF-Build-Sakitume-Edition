# Printing parts
The ERCF build manual provides a description on slicer settings. Basically the same as printing Voron parts

* 0.2mm layer
* Forced 0.4mm extrusion width
* 4 walls, 5 layers for top, 5 layers for bottom
* 40% infill
* No need to add supports with your slicer


## Two-tone color scheme
The STL files can be printed with a primary and a secondary (accent) color. It looks pretty nice this way. I'm using red PolyMaker PolyLite ABS and Sunlu Blue ABS.

The filename of an STL will have an `[a]` prefix to indicate if you should use the accent color for it.

# What STL files do we need to print?

The STL files for the printed parts will come from the projects/mods I mentioned earlier. You won't be using any STL files from the original ECRF project.

1. Start by downloading the [original ERCF v1.1 manual](https://github.com/EtteGit/EnragedRabbitProject/blob/main/Documentation/ERCF_Manual.pdf). You will use this even though a lot of the parts are different; the new parts are still close enough to their original counterparts that you will find this manual to be helpful. 

2. Then you should clone the [SturdyBunny project](https://github.com/sneakytreesnake/SturdyBunnyProject). Or download the [zip](https://github.com/sneakytreesnake/SturdyBunnyProject/archive/refs/heads/main.zip) and unzipping it somewhere to work with.

3. Then do the same for [Springy](https://github.com/moggieuk/ERCF-Springy) project.

4. Do the same for [Triple-Decky](https://github.com/gneu42/Triple-Decky) or [Thumper Blocks](https://github.com/kieraneglin/Thumper-Blocks) depending on which one you decided to use.


> Update: I have come across a great resource for keeping track of what STL files you will need to print. It is [Matt's Unofficial ERCF v2 Printed Parts Tracker spreadsheet](https://docs.google.com/spreadsheets/d/1K2i_MtVuokYDMmjRRw3gyZF1DaFUahJZ2FlhEajCJtM/edit). Save a copy of this Google document and check/uncheck some of the boxes to match what you're building and it will tell you the number of parts to print for a specific STL file. However I will still itemize each and every part that I used for my build on this site page as it lets me keep the notes that I made along side the list.

## What I've printed (or are currently printing)

I'm going to keep a list of everything that I think needs to be printed, and from where it is found. I'll update this as I print more and more parts. I'll also update it when I discover something wasn't needed or if something was missed.

## Sturdy Bunny parts
Because SturdyBunny is a fork, it also has the original parts in the repo. **You want to ignore those.** Intead you want to look at the ["Study_FeederV2 (development parts)"](https://github.com/sneakytreesnake/SturdyBunnyProject/tree/main/Study_FeederV2%20(development%20parts)) folder that has subfolders for the STL files you will print as well as CAD (step) file that you can view to see how the assembly goes together.

![image](https://user-images.githubusercontent.com/875866/280436351-cb3bfc8b-42a0-42dc-a1e3-e03fcaa8a6d6.png)


In the following sections I will list the name of a folder in SturdyBunny and the STL files within that foler that you should print


### Linear Axis
Print all of the files in the `Linear axis` folder **except** the `Idler_Block_V1A.stl` file as the Springy mod has a replacement for that part

```
/SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/Linear axis
  [a]_Drag_Chain_Anchor_Bottom.stl
  [a]_Motor_Lock.stl
  Selector_Motor_Support.stl
```

### Gear Box
Print all of the files in the `Gear box` folder
```
/SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/Gear box
  [a]_Bearing_Spacer_x2.stl
  [a]_Knob.stl
  [a]_Logo_Plate.stl
  [a]_M4_80T_Wheel.stl
  [a]_Side_Latch_x2.stl
  [a]_Top_Panel.stl
  [a]Bottom_panel_V1B.stl
  Gear_Box_Back_V2B.stl
  Gear_Box_Front_V3C.stl
  
```

> Note: OrcaSlicer warned about the `[a]_Side_Latch_x2.stl` part. It's okay, you can ignore that warning and print it without having to re-orient the part or enable supports. The part is a print-in-place type that has portion that swivels out.

![image](https://user-images.githubusercontent.com/875866/280809964-c6bf6759-eb2e-454f-8817-5ca97d03928b.png)


I am using the FYSETC ERB board that came with my kit. This board is like the EASY BRD in that you will skip the part in the ERCF manual about using connectors that mount onto the motor arm. This means you'll want to print a motor arm part from the `EASY BRD Option` folder.

Depending on the size of the Nema stepper you're using for the gearbox you will print **one** of the following parts. 

```
/SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/Gear box/EASY BRD Option
  Motor_Arm_NEMA14_EASYBRD.stl
  Motor_Arm_NEMA17_EASYBRD.stl
```

> My FYSETC kit comes with a Nema14 which I'm not going to use. Instead I'll use a Nema17 from my parts bin so I chose to print `Motor_Arm_NEMA17_EASYBRD.stl`

### Tools
There is a printed piece that is used as a gauge/jig to help you place the pulley on your Nema 17 motor at the correct offset from the face of the motor. There's another printed piece to help you insert an MR85ZZ bearing into a filament block. You can find them here:

```
SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/Tools
  Pulley_Tool_NEMA17.stl
  TOOL_FilamentBlock_BearingInstall_V2.stl
```


### Selector
You will ignore many of the parts in this `Selector` folder as (I think) Springy will provide different parts. However there are two parts that you will want to print from SturdyBunny:

```
/SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/Selector
  Belt_Tensionner.stl
  Drag_Chain_Anchor.stl
```

### Filament Blocks
You will ignore many of the parts in this `Filament blocks` folder as (I think) Triple-Decky will provide different parts. However there are a few parts that you will want to print from SturdyBunny:

```
/SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/Filament blocks
  Filament_Blocks_End_Foot_V1B.stl
  Filament_Blocks_End_Nobearing_V2A.stl
```

> Note: When you print `Filament_Blocks_End_Foot_V1B.stl` you should consider printing it in the accent color (if you're doing that) so that it matches the `[a]Bottom_panel_V1B.stl` part. You should also use your slicer's "Auto" orientation option, otherwise the default orientation has some bridging that may not turn out as clean as you'd like. Using the "Auto" orientation worked better for me.

![image](https://user-images.githubusercontent.com/875866/282626330-3ce230e9-8b31-43b8-8ece-61a34325e8e2.png)


### Supports
I initially printed out some parts from this folder thinking they may be useful. It turns out I didn't need them or used something else. So in my opinion, you can ignore this folder.

## EASY_BRD

My kit provided a FYSETC ERB controller board, the following part will let you mount it to the 2020 extrusion of the SturdyBunny. I wasn't able to use the `ESYBRD_COVER_V1A.stl` cover with my ERB since it isn't exactly the same form factor as the Easy BRD.

```
/SturdyBunnyProject/Study_FeederV2 (development parts)/Stls/EASY_BRD
  [a]ERCF_EASY_BRD_BRACKET_V1A.stl
```

## Triple-Decky parts (skip this if using Thumper Blocks)

For each of the following parts print out one for each gate. In my case my ERCF will have 6 gates (ports)
```
Triple-Decky/STL/Sturdy Bunny/Rev_C
  [a]Triple_Decky_Latch_RevC6_0.stl
  
Triple-Decky/STL/Sturdy Bunny/Rev_C/Rev_C7.0_3PS_only
  [a]Triple_Decky_Tophat-integerated_3PS_C7_0.stl
  Triple_Decky_Base_C7_0.stl
  Triple_Decky_Filament_path_3PS_C7_0.stl
```

You can still use the revision C6.3 parts but I thought it might be better to use the latest filament block parts (C7.0 3PS). One important thing to keep in mind is the fitment of the "base" and "filament-path" parts. The upper "filament-path" part hinges/pivots against the "base" part. If this is not freely pivoting then there are additional versions of these parts that have increased clearance. They can be found in the `Clearance_options` subfolder:

```
Triple-Decky/STL/Sturdy Bunny/Rev_C/Rev_C7.0_3PS_only/Clearance_options
  Triple_Decky_Base_C70_clrearance1.stl
  Triple_Decky_Base_C70_clrearance2.stl
  Triple_Decky_Filament_path_3PS_C70_clearance1.stl
  Triple_Decky_Filament_path_3PS_C70_clearance2.stl
```

Be sure to check out the [video](https://www.youtube.com/watch?v=SpWfUNTKa9g) at the bottom of the Triple-Decky [README.md](https://github.com/gneu42/Triple-Decky/blob/main/README.md)

I've also put together a video that describes how I clean up these Triple-Decky parts and assemble them. This will also show you the type of smooth and feely pivoting action you should be going for

[![Video](https://img.youtube.com/vi/eno0Ubs8Q_8/maxresdefault.jpg)](https://www.youtube.com/watch?v=eno0Ubs8Q_8)


Next you need to print out one trap for each port (filament block). They are found in the `Traps` folder. I chose to use the "V Shape" variant:
```
Triple-Decky/STL/Sturdy Bunny/Rev_C/Traps
  TD_Base_Trap_V-Shape_C56.stl
```

There is a setscrew variant. I think the difference is that the setscrew metallic threads impart greater friction against the filament when it is activated as brake. These reportedly work better for some folks compared to the "v" shape traps.

My understanding is that these traps are simply holes that the filament will pass through. When a filament block is active (enaged by the *selector*) the path of the filament as it passes through a trap is straight and clear with minimal resistance. If a block is not active then the trap is lifted slightly and the filament is no longer straight through the trap hole and experiences resistance; this helps keep the filament from moving in/out of the block while the block is not active.

If you have m3x2 or m3x3 setscrews then you might want to try that set screw variant instead:
```
Triple-Decky/STL/Sturdy Bunny/Rev_C/Traps
  TD_Base_Trap_M3x3_C55.stl
```

The last part you'll need from Triple-Decky is the servo arm.
My FYSETC uses an MG90S servo, so I printed out this part
```
Triple-Decky/STL/Sturdy Bunny/Rev_C/ Servo_arms_for_3PS
  Servo_Arm_MG90S_for_3PS.stl
```

## Thumper Blocks (skip this if using Triple-Decky)
I'm using the latest parts (`Rev_2`) that were released on 11/10/2023.
For each of the following parts print out one for each gate. In my case my ERCF will have 6 gates (ports)

```
/Thumper-Blocks/STL/Rev_2
  [a]_latch.stl
  [a]_tophat_with_supports.stl
  base.stl
  filament_path.stl
```

> Note: Thumper Blocks provides a ***copy*** of the Springy servo arm you will use, but I opted to use the servo arm file direct from the Springy project just in case it was updated. I describe the Springy parts in the next section

I've also made a video about these filament blocks
[![Video](https://img.youtube.com/vi/MmB212pJrAc/maxresdefault.jpg)](https://www.youtube.com/watch?v=MmB212pJrAc)


## Springy Parts
```
ERCF-Springy
  [a]_Springy_Selector_Cart.stl
  Spring_Cap.stl
  Springy_Idler_Block.stl
  Springy_Selector_Door.stl
```


My FYSETC kit provides an MG90S servo, so I need to print out this part:
```
ERCF-Springy/MG90S_Servo_Option
  Springy_MG90S_Servo_Mount.stl
```

If you're using Triple-Decky then skip the following (as you'll be printing the servo arm from Triple-Decky).
I'm not using Triple-Decky, I'm using Thumper Blocks. So I'll be using this part for the servo arm:
```
ERCF-Springy/MG90S_Servo_Option
  [a]_Servo_Arm_MG90S.stl
```

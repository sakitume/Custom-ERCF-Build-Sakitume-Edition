# What is this custom build?

I based this build on (what I call) a "recipe" provided by Tea (a member of the Voron discord server) who made a post in the `#ercf_questions` channel around May 2023 on what she would use if she were to [make an ERCF in May 2023](https://discord.com/channels/460117602945990666/909743915475816458/1112241338554011759)

> Note: If you need an invite to reach that Voron discord server post you can try [this](https://discord.gg/voron)

## The basic recipe
The original recipe as described by Tea uses the following ingredients:

* [SturdyBunny](https://github.com/sneakytreesnake/SturdyBunnyProject) - A fork of the original ERCF project. So ***instead*** of the original ERCF project, we start with this.
    * SturdyBunny uses a small length of 2020 extrusion in place of the two 8mm threaded rod of the original ERCF design making this more...uh....*sturdy*
* [Springy](https://github.com/moggieuk/ERCF-Springy) - A modified ***selector*** (the carriage that slides back and forth selecting one port/gate over another)
* [Triple-Decky](https://github.com/gneu42/Triple-Decky) - These are improved ***filament blocks*** that are very popular and well established
* [Binky](https://github.com/mneuhaus/EnragedRabbitProject/blob/main/usermods/Binky/Readme.md) - This is an improved ***encoder***, the subsystem that helps figure out how much filament is being pushed/pulled

That's the "recipe" that Tea describes and what many people consider to be the "Community ERCF v2". It's a fine recipe, however I'm changing things up a little bit with my custom build.

Rather than using Triple-Decky I've opted to use [Thumper Blocks](https://github.com/kieraneglin/Thumper-Blocks). And to avoid tip tuning (which I hear is a time consuming and tricky process), I've opted to use a filament cutter. And I'm going to try out the [ERCF Filament Cutter](https://github.com/kevinakasam/ERCF_Filament_Cutter)

More info on these different mods can be found [here](./the-mods.md)

## That's a lot of ingredients

Yeah...to build this custom beast you are going to have to jump around a bunch of different mods/designs. Each one will have a set of `.stl` files that you need to print. And it isn't very clear which files you actually need and which ones you should skip altogether. Then you have to assemble everything and there isn't going to be an instruction manual for this. 

But don't worry, while it may seem daunting there are others who have traveled this path (or one similar to it) and that makes it easier. There are several resources available that you can turn to:

* The [`#ercf_questions`](https://discord.com/channels/460117602945990666/909743915475816458) channel on the Voron Discord Server has a lot of activity with people posting questions (and often answers) regarding ERCF. To be honest, because it can be a bit busy at times, and due to how Discord works, some posts can get lost (scroll away) due to the activity.
* [Matt's Unofficial ERCF v2 Printed Parts Tracker spreadsheet](https://docs.google.com/spreadsheets/d/1K2i_MtVuokYDMmjRRw3gyZF1DaFUahJZ2FlhEajCJtM/edit)
* The [`#ercf_mmu`](https://discord.com/channels/1102420774993793107/1165500835355176992) channel on fizzy's 3DPrinting Discord server has some helpful folks. Not as busy as the Voron Discord server, but maybe that's a good thing.
* My [ERCF Build Log](https://discord.com/channels/1085579502735872044/1170211560531177544/1170211560531177544) on the Delayed Development discord server (invite for this server is [here](https://discord.gg/upRPU4vNSZ))

And well....of course there are [these notes](https://sakitume.github.io/Custom-ERCF-Build-Sakitume-Edition/) you're reading now, as well as a few videos on [my YouTube channel](https://www.youtube.com/channel/UC6pX9Il67lsxVa1CSkXlb0g).

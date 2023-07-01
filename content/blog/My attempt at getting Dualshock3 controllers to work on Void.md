---
title: "My Attempt at Getting Dualshock3 Controllers to Work on Void"
date: 2023-07-02T01:59:24+08:00
draft: false
---

I'd consider myself something of a retro gamer. AAA titles past the Xbox360/PS3 era never really appealed to me outside of singleplayer experiences. Then again, I've never really had the chance to have those consoles either, since I've mostly been stuck with a PSP. PPSSPP usually worked just fine for me, and I've only taken games that I actually physically owned. There is no way in hell I'm ever going to pay even half of what the games are worth off someone who's trying to sell them to me for thrice the original price.

I digress. I currently daily drive Void Linux, and it doesn't really explicitly state how to get controllers to work; or, at least, I didn't find anything explicitly referencing that. In any case, I was under the assumption that Dualshocks were plug and play, so I just plugged my controllers in expecting them to be detected. They _were_ being detected by lsusb, and the controller does show up on /dev/input/js0, but it's just not registering any input on evdev or xev. I tried installing steam thinking it was a driver or udev problem, and it still didn't work. Then I came across a [steam forum article on controllers](https://steamcommunity.com/app/221410/discussions/0/864980277619457883/) that said that their controller didn't work because of a permission problem. They'd change the permission on the /dev/input/<devid> through `chmod 666 /dev/input/<dev>` and handle it that way. Problem was, whenever they had to reconnect the damned thing, they'd have to repeat the same process. Lo and behold, there is a different group that I had to be included in for me to have permission to the devices.

> You brilliant piece of mind! This is an thread, but I hit that problem since a few days ago up until I saw this post and it worked! someone on #gentoo said you need to be part of 'plugdev' group and really shouldn't need to change the permissions manually.

As soon as I saw this line, I realized that I had to add myself to the `input` group to get the controller to work. After adding myself to the group and a quick reboot, I was able to use the controller as intended. Steam detected the controller, and it would work on the emulator. My goopy goblin gamer brain is satisfied for now.

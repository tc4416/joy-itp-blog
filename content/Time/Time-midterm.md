---
title: "Time: Midterm"
draft: false
---
#### Hardware
I was thinking od using quartz originally, but one problem for my exit sign light box is that it will create a shadow of the black gearbox will be cast onto my box front panel that might look kinda ugly. So i wanted to try using stepper motor to avoid the big shadow, and as a way for me to try out other time-related hardware. For my application, I'm using the basic stepper driver combo and the basic RTC timer:
- 28BYJ-48
- ULN2003 stepper driver
- DS3231 RTC timer 

**step 1: checking if stepper work**
I followed [this tutorial](https://www.instructables.com/How-to-Control-28BYJ-48-Stepper-Motor-With-ULN2003/) for the stepper+driver board config and initial testing
<div align = "center">
<img src = "media/time/time-mt9.png" width = 400px>
</div>
Basic back and forth rotation test:![[IMG_0043.mov]]
**Step 2: check if RTC timer work**
i started by following [this guide](https://learn.adafruit.com/adafruit-ds3231-precision-rtc-breakout/arduino-usage). It was interesting seeing that the day0 in thie RTClib library is Sunday(and i agree first day of the week is sunday!)
<div align = "center">
<img src = "media/time/time-mt10.png" width = 400px>
</div>
**Step 3: RTC+ stepper**
Now i have both Stepper and RTC working, I wanna try to see if i can make my stepper be hour hand.
Converting hour/minute/second to decimal hour:
<div align = "center">
<img src = "media/time/time-mt11.png" width = 200px>
</div>
Now i gotta figure out how to calibrate the stepper so that it knows where is the 12 oclock position. I am thinking of using a magnet sensor or hall effect sensor to as the position switch.
I want to try the hall effects sensor I have (49E) first
<div align = "center">
<img src = "media/time/time-mt12.png" width = 200px>
</div>
Work perfect!! ***Magnet direction matters!***
<div align = "center">
<img src = "media/time/time-mt21.mov" width = 400px>
</div>
I drilled a small hole on the back of the arrow and attach the hall effect at the back of the front panel with hot glue:

![[time-mt23.mov]]




-------------------
#### hardware Exploration
I look into the 555 timers Hbridge and tried them out for controling DC motor(add video)
<div align = "center">
<img src = "media/time/time-mt13.png" width = 300px>
<img src = "media/time/time-mt15.png" width = 300px>
<img src = "media/time/time-mt16.png" width = 300px>
<img src = "media/time/time-mt17.png" width = 300px>
<img src = "media/time/time-mt18.png" width = 300px>
<img src = "media/time/time-mt19.png" width = 300px>
</div>

-----------
#### Animation
It should rotate full revolution! Fushion only have 100 steps available and it make it look like it is spinning like crazy. So I only animate 90 degrees for now. I wanted to be hour hand

<div align = "center">
<img src = "media/time/time-mt8.gif" width = 400px>
</div>

> Far from making our lives meaningful, eternity would make them meaningless, since our actions would have no purpose.

- Really like this piece by Félix González-Torres.
<div align = "center">
<img src = "media/time/time-mt1.png" width = 400px>
</div>
---------------
#### Ideation
1. Threaded Clock
	Unravel as time pass
	<div align = "center">
<img src = "media/time/time-mt2.png" width = 400px>
</div>

2. Alphabet clock that points to momento mori
3. Exit sign?? + frosted acrylic? a lamp?
<div align = "center">
<img src = "media/time/time-mt3.png" width = 200px>
<img src = "media/time/time-mt4.png" width = 200px>
<img src = "media/time/time-mt5.png" width = 200px>
<img src = "media/time/time-mt6.png" width = 200px>
<img src = "media/time/time-mt7.png" width = 200px>
</div>
	- Quartz gear box maybe not a good idea bc need to drive the arrow + need battery
	- Arduino + Stepper Motor + Driver + RTC module



Hank green
Jeff's feedback
- X somewhat change to M?
- Exit sign mirror
- Stepper need power for holding the position
	- some choreography for the arrow


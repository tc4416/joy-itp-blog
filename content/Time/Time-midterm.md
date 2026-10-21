---
title: "Time: Midterm"
draft: false
---
#### hardware 2
I was using quartz but one problem for my exit sign light box is that it will create a shadow of the black gearbox will be cast onto my box front page thaat might look kinda ugly. So i wantto try using stepper motor to avoid that, and as a way for me to try out other time-related hardware
Im using the basic stepper driver combo:
28BYJ-48+ULN2003 
and 
RTC timer
step 1: checking if stepper work
I followed [this tutorial](https://www.instructables.com/How-to-Control-28BYJ-48-Stepper-Motor-With-ULN2003/) for the stepper+driver board config
![[Pasted image 20261019224310.png|271]]

Basic back and forth rotation test![[IMG_0043.mov]]
Step 2: check if RTC timer work
i started by following [this guide](https://learn.adafruit.com/adafruit-ds3231-precision-rtc-breakout/arduino-usage)
![[Pasted image 20261019234958.png]]
interesting that the day[0] in thie RTClib library is Sunday (and i agree first day of the week is sunday!)

-----------
now i have both Stepper and RTC working, I wanna try to see if i can make my stepper be hour hand.
converting hour/minute/second to decimal hour
![[Pasted image 20261020002336.png|286]]

han i gotta figure out how to calibrate the stepper so that it knows where is the 12 oclock position. I am thinking of using a magnet senser or hall effect sensor to as the position switch.
I want to try the hall effectg sensor I have (49E first)
![[Pasted image 20261020010238.png]]

Work perfect!! ***Magnet direction matters!***
![[IMG_0046.mov]]
#### hardware 
I look into the 555 timers Hbridge and tried them out for controling DC motor(add vido )
![[Pasted image 20261016144046.png]]![[Pasted image 20261016154259.png|174]]
![[Pasted image 20261016160535.png|274]]![[Pasted image 20261016154008.png|308]]
![[Pasted image 20261016170802.png|287]]![[Pasted image 20261016170859.png|375]]
#### Animation
It should rotate full revolution! Fushion only have 100 steps available and it make it look like it is spinning like crazy. So I only animate 90 degrees for now. I wanted to be hour hand
![[time-mt8.gif]]

> Far from making our lives meaningful, eternity would make them meaningless, since our actions would have no purpose.

- Really like this piece by Félix González-Torres.
<div align = "center">
<img src = "media/time/time-mt1.png" width = 400px>
</div>

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


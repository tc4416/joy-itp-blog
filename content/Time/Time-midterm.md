---
title: "Time: Midterm"
draft: false
---
#### Keywords
- The Direction of Time
- Spatial Orientation of Time
At first, when I was brainstorming project ideas, I was looking around in my day-to-day life to see if there was something I could replace with a clock. Then I noticed the exit signs everywhere on the floor. And then we discussed the spatial orientation of time in class, like how different cultures place past and future in different orientations to themselves. It kind of just came together. No matter where you place yourself in the stream of time, it is always pointed toward the next moment, and exiting the current one.
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
Basic back and forth rotation test:
![[time-mt21.mov]]Step 2: check if RTC timer work
I started by following [this guide](https://learn.adafruit.com/adafruit-ds3231-precision-rtc-breakout/arduino-usage). It was interesting seeing that the day0 in thie RTClib library is Sunday(and I  agree the first day of the week is Sunday!)
<div align = "center">
<img src = "media/time/time-mt10.png" width = 400px>
</div>
**Step 3: RTC+ stepper**
Now I have both Stepper and RTC working; I wanna try to see if I can make my stepper be the hour hand.
Converting hour/minute/second to decimal hour:
<div align = "center">
<img src = "media/time/time-mt11.png" width = 200px>
</div>
Now I gotta figure out how to calibrate the stepper so that it knows where the 12 o'clock position is. I am thinking of using a magnet sensor or Hall effect sensor as the position switch.
I want to try the hall effects sensor I have (49E) first
<div align = "center">
<img src = "media/time/time-mt12.png" width = 200px>
</div>
Work perfect!!  *Magnet direction matters!** 

![[time-mt22.mov]]
I drilled a small hole on the back of the arrow and attached the Hall effect sensor to the back of the front panel with hot glue, and figured out the sensor value when the arrow is at 12 o'clock. So every time the device is powered up, the stepper motor will start spinning until it hits the position when the sensor is reading the value at 12 o'clock. I had the issue that sometimes it does not find the position on the first rotation, so I programmed it so that it rotates until it finds the spot.
![[time-mt23.mov]]
With the hall effect sensor in place, I got to combine all the electronics together. I added an Adafruit nOods LED filament into the circuit as my main light source. And enclosed them with the back panel.
<div align = "center">
<img src = "media/time/time-mt24.jpeg" width = 400px>
</div>

**Final Product**
<div align = "center">
<img src = "media/time/time-mt28.png" width = 400px>
<video width="400" controls> <source src="media/time/time-mt28.mov" ></video>
</div>

The structure and effect of this light box did not turn out the way I wanted. There are a few problems that I want to fix:
- Originally, I wanted the body to be 3D-printed white so that the electronics inside the box are not visible. I tried the diffusion effect with 1.25mm thickness, and I like the way it looks. The printers in the shop were having bed-adhesion issues, so the print kept failing. And that's why I switched to a laser-cut box body with my leftover material from my last project. It still looks alright, but I might want to try a full 3D-printed version. And perhaps matte white acrylic?
<div align = "center">
<img src = "media/time/time-mt25.jpeg" width = 200px>
<img src = "media/time/time-mt26.jpeg" width = 200px>
</div>
- I want to seal/hide the electronics
- Fix the light diffusion effect.

-------------------
#### hardware Exploration
I looked into the 555 timers, H-bridge, and tried them out for controlling a DC motor(add video)
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
It should rotate a full revolution! Fusion only has 100 steps available, and it makes it look like it is spinning like crazy. So I only animate 90 degrees for now. I wanted to be hour hand

<div align = "center">
<img src = "media/time/time-mt8.gif" width = 400px>
</div>

---------------
#### Ideation
1.  Far from making our lives meaningful, eternity would make them meaningless, since our actions would have no purpose.
2. Really like this piece by Félix González-Torres.
<div align = "center">
<img src = "media/time/time-mt1.png" width = 400px>
</div>
3. Threaded Clock
	Unravel as time passes
	<div align = "center">
<img src = "media/time/time-mt2.png" width = 400px>
</div>

4. Alphabet clock that points to Momento Mori
5. Exit sign?? + frosted acrylic? A lamp?
<div align = "center">
<img src = "media/time/time-mt3.png" width = 200px>
<img src = "media/time/time-mt4.png" width = 200px>
<img src = "media/time/time-mt5.png" width = 200px>
<img src = "media/time/time-mt6.png" width = 200px>
<img src = "media/time/time-mt7.png" width = 200px>
</div>
- Quartz gearbox maybe not a good idea bc need to drive the arrow + need a battery
- Arduino + Stepper Motor + Driver + RTC module

# IDD-Fa18-Lab1: Blink!
### Christophe Rimann (cjr268)

## Part A. Set Up a Breadboard
Image available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/Breadboard1.jpg).
## Part B. Manually Blink a LED
**a) What color stripes are on a 100 Ohm resistor?** My 100 OHM resisotr had the following: Red, Red, black, black, brown.

**b. What do you have to do to light your LED?** Build the circuit as shown [here](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/docs/button_led_resistor_diagram.png), then press the button. Video [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/button_press.MOV).

## Part C. Blink a LED using Arduino

### 1. Blink the on-board LED

**a. What line(s) of code do you need to change to make the LED blink (like, at all)?** I didn't have to change anything, I just flashed the code over and the onboard LED started blinking.

**b. What line(s) of code do you need to change to change the rate of blinking?** There are two calls to the delay function in the loop that regulate the rate of blinking. The first delay corresponds to how much time the light stays on, and the second delay corresponds to how long it is off for.

**c. What circuit element would you want to add to protect the board and external LED?** If we were to build a circuit that included just a single external LED, it would not provide enough resistance to the circuit and cause a short to ground. As such, I would need to add a resistor to protect the board/external LED.

**d. At what delay can you no longer *perceive* the LED blinking? How can you prove to yourself that it is, in fact, still blinking?** I could no longer perceive the LED blinking between around 3 and 4 ms of delay between 500 ms blinks (at 4s, I could only tell it was blinking if I really looked for it). I can prove that its still blinking in a couple fashions: 1. programatically, we know it must be blinking because of the code. 2. We can check that it's still blinking by changing the first delay to something arbitrarily long (e.g. 10000); by doing so, it becomes more noticeable to the naked eye when the light goes off. 3. By videoing the light and then stepping through it frame by frame, we can see when the light is extinguished. 

**e. Modify the code to make your LED blink your way. Save your new blink code to your lab 1 repository, with a link on the README.md.** My blink [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/myblink.ino).

### 2. Blink your LED

**Make a video of your LED blinking, and add it to your lab submission.** Video of my blink [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/PartCQ2.mp4). For some reason, my pin 9 wasn't making good contact with the breadboard, so I held the wire directly to pin 9.

## Part D. Manually fade an LED

**a. Are you able to get the LED to glow the whole turning range of the potentiometer? Why or why not?**

As the professor mentioned in class, because I did not have a potentiometer and could not get to campus all weekend, I used my force sensitive resistor instead. I was able to get almost the whole range (i.e. when I began to press lightly the light lit up slightly, all the way to when I fully pressed and the LED lit brightly), but when fully pressed, the LED looked slightly dimmer than normal. I believe this to be because the force sensitive resistor provides a modicum of resistance even when fully pressed, decreasing the current running through the light.

Video available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/force.MOV).

## Part E. Fade an LED using Arduino

**a. What do you have to modify to make the code control the circuit you've built on your breadboard?**
I changed the led parameter from 9 to 11, and the code worked. Presumably, had I left it, I could've used pin 9 for the fade as well.

A video is available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/programatic_fade.mp4).

**b. What is analogWrite()? How is that different than digitalWrite()?**

A little research suggests that digitalWrite is a binary on/off output (HIGH vs LOW), while analogWrite is specifically for PMW and allows for a series of discrete outputs between 0 and 255, where 0 is always off (i.e. equivalent to LOW), while 255 is always on (equivalent to HIGH), with a linear progression between the two.

My fade is available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/myFade.ino). I tried to make the LED darker without a noticeable pulsation, to fairly limited success.



## Part F. FRANKENLIGHT!!!

I chose to take apart a portable iPhone battery pack that also: A. a flashlight, B. an indicator for how much power was left, C. a built in charging cable. Pressing the button on the pack once would indicate how much power remained, while pressing and holding it would turn on the flashlight. It was also stackable, so if multiple needed to be charged, they could be stacked and only one had to be plugged in. An image of the circuit is available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/circuit.pdf), while my best rendition of it is [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/circuit.JPG).

### 1. Take apart your electronic device, and draw a schematic of what is inside.

**a. Is there computation in your device? Where is it? What do you think is happening inside the "computer?"**
I think there is a little bit of computation necessary, or at least some decision making processes. Namely, there appears to be what research suggests is a small microprocessor.  I think it was necessary to compute: A. on button press, figure out if it was a long press or short press to either turn on the flashlight or indicate how much battery was left, B. Decide how much battery is left and mod by 4 (given there were only 4 lights, indicating the pwer was either at 0, 25%, 50%, 75%, or 100%, with 0 being indicated via absence of any light), and C. decide whether to draw power from the microusb port or the two exposed electrodes that could be connected to other power packs when stacked, as mentioned above.

**b. Are there sensors on your device? How do they work? How is the sensed information conveyed to other portions of the device?** I think there is a sensor for how much power is left. A little research suggests that the button, the battery, the indicator, and the flashlight are all connected to two primary components: a very small microprocessor and something called a Shotky barrier diode. I believe that the button press length is measured in the microprocessor, which determines whether it was an indication press or a flashlight press. The microcontroller then varies the forward voltage to the Shotky barrier diode, which then sends power either to the flashlight or the indicator light. For example, if it is a low voltage, it might do one thing, like cause an indicator light to flash, while if it is high, it could cause the flashlight to go on.

**c. How is the device powered? Is there any transformation or regulation of the power? How is that done? What voltages are used throughout the system?** The battery itself provides power at 3.7 Volts. It receives power via USB, which google confirmed is 5 volts. As mentioned above, there is an alternative power source in the form of the "stack" which is also 3.7 volts. I found another, different device called a Shotsky barrier rectifier between the two power sources. I think this Shotsky barrier is simple: if the voltage from one is high, it will draw from that one, while if it is not, it will attempt to draw from the other (i.e. there is a "default" power source, and an "override" power). Because the battery provides power at 3.7V (see c.), I believe that the stack power source is the default, given it is drawing power from other batteries in that case, while if it is pulling from USB it is at 5V. As such, I think the battery will attempt to pull power from the stack at all times unless plugged in, in which case it will pull from USB. I believe the power is stepped down from the power to the battery via a step down converter. I also found what research shows to be an inductor, which seems to convert from AC to DC as necessary. This makes sense as it is right next to the battery, which means it's probably there to make sure any power flowing in/out of the batter is DC. There is also what google suggests is a circuit breaker near the power, which I'm guessing is there to make sure power coming in won't cause the battery to explode.

**d. Is information stored in your device? Where? How?** I do not believe any information is stored in the device, and that the information is computed on the fly, as mentioned earlier.

### 2. Using your schematic, figure out where a good point would be to hijack your device and implant an LED. 
The most obvious point of contact to me was directly on either side of an LED, given the device contained several. This worked pretty trivially: I connected the 5V and ground from the microcontroller to one of the indicator LEDs and managed to light it up. I did the same with the flashlight. These were pretty simple, so I wanted to confirm my earlier suspicious that the Shotky barrier diode regulated the LED vs flashlight distinction. Upon connecting power to the Shotky barrier diode, however, something perculiar happened: the battery appeared to go into a reset state which I had never seen before, with the indicator lights initially flickering on and off one by one, before blinking on and off continuously until I hit and held the power button. Although this proved that a high power (namely 5V) would activate the indicator lights, I could not prove that a lower level of power would cause the flashlight to activate (the 3V pin on the arduino would not light it up).



### 3. Build your light!

A schematic is [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/mycircuit.pdf), while a video is [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/shotsky.mp4). A video of directly lighting the LEDs is available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/flashlightindicator.mp4) as well, with white being flashlight and green being indicator lights.

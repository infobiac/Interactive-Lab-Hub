# IDD-Fa18-Lab1: Blink!
### Christophe Rimann (cjr268)

## Part A. Set Up a Breadboard

## Part B. Manually Blink a LED
**a) What color stripes are on a 100 Ohm resistor?** Red, Red, black, black, brown.
**b. What do you have to do to light your LED?** Build the circuit as shown [here](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/docs/button_led_resistor_diagram.png), then press the button.

## Part C. Blink a LED using Arduino

### 1. Blink the on-board LED

**a. What line(s) of code do you need to change to make the LED blink (like, at all)?** I didn't have to change anything, I just flashed the code over and the onboard LED started blinking.

**b. What line(s) of code do you need to change to change the rate of blinking?** There are two calls to the delay function in the loop that regulate the rate of blinking. The first delay corresponds to how much time the light stays on, and the second delay corresponds to how long it is off for.

**c. What circuit element would you want to add to protect the board and external LED?** If we were to build a circuit that included just a single external LED, it would not provide enough resistance to the circuit and cause a short to ground. As such, I would need to add a resistor to protect the board/external LED.

**d. At what delay can you no longer *perceive* the LED blinking? How can you prove to yourself that it is, in fact, still blinking?** I could no longer perceive the LED blinking between around 3 and 4 ms of delay between 500 ms blinks (at 4s, I could only tell it was blinking if I really looked for it). I can prove that its still blinking in a couple fashions: 1. programatically, we know it must be blinking because of the code. 2. We can check that it's still blinking by changing the first delay to something arbitrarily long (e.g. 10000); by doing so, it becomes more noticeable to the naked eye when the light goes off. 3. By videoing the light and then stepping through it frame by frame, we can see when the light is extinguished. 

**e. Modify the code to make your LED blink your way. Save your new blink code to your lab 1 repository, with a link on the README.md.** My blink [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/myblink.ino).

### 2. Blink your LED

**Make a video of your LED blinking, and add it to your lab submission.** (For some reason, my pin 9 wasn't making good contact with the breadboard, so I held the wire directly to port 9)

## Part D. Manually fade an LED

**a. Are you able to get the LED to glow the whole turning range of the potentiometer? Why or why not?**

As the professor mentioned in class, because I did not have a potentiometer and could not get to campus all weekend, I used my force sensitive resistor instead. I was able to get almost the whole range (i.e. when I began to press lightly the light lit up slightly, all the way to when I fully pressed and the LED lit brightly), but when fully pressed, the LED looked slightly dimmer than normal.

## Part E. Fade an LED using Arduino

**a. What do you have to modify to make the code control the circuit you've built on your breadboard?**
I changed the led parameter from 9 to 11, and the code worked. Presumably, had I left it, I could've used pin 9 for the fade as well.

**b. What is analogWrite()? How is that different than digitalWrite()?**

A little research suggests that digitalWrite is a binary on/off output (HIGH vs LOW), while analogWrite is specifically for PMW and allows for a series of discrete outputs between 0 and 255, where 0 is always off (i.e. equivalent to LOW), while 255 is always on (equivalent to HIGH), with a linear progression between the two.

My fade is available [here](https://github.com/infobiac/Interactive-Lab-Hub/blob/master/labs/Lab01/files/myFade.ino). I tried to make the LED darker without a noticeable pulsate, to a fairly limited success.

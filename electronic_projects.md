# Electronic projects #

## Contents ##

* [plant monitor](#port-plant-monitor)
* [snake enclosure monitor](#snake-enclosure-monitor)
* [adjustable height desk](#adjustable-height-desk)
* [WiiMotion Quad Copter](#wii-motion-quad-copter)
* [Flashing a bricked motherboard BIOS](#flashing-a-bricked-motherboard-bios)

## 16-port plant monitor ##

This project was created when we found that some moisture sensors consumed their batteries in just a week if left in the plant continually.  there were 
had about 60 total moisture sensors, so changing batteries at that pace wasn't 
practical.  I pulled the moisture sensors apart, and used ethernet wire to 
connect them to an Arduino, in order to make it possible to provide external 
power.  There are a lot of plants to look at, so I ended up using a couple of 
16-port multiplexers, to allow me to address up to 16 sensors from a single 
Arduino, as well as two 8-bit shift registers, to allow me to light an LED on 
each of the moisture sensor sticks.

[Here's the github repository](https://github.com/tnordloh/arduino_16_port_plant_reader)
and a couple of photos.


Here it is, mounted on perfboard:
![perfboard plant reader](./images/plant_reader_perfboard_1mb.jpg)
Here it is, assembled:
![assembled plant reader](./images/plant_reader_assembled_1mb.jpg)

## Snake enclosure monitor ##

This project was created, to ensure that we remembered to feed snakes, once
per week, and to make sure that, whoever fed them could signal to the rest of 
us, that they had been fed.  It has six leds, and lights one up each day.  On 
the seventh day, the six leds start blinking.  Additionally, there is a simple
moisture sensor, that runs into the water bowl, which will blink separately, 
when the water bowl is dry.


[Here's the github repository](https://github.com/tnordloh/home_automation)
and a couple of photos.

The Perfboard:
![perfboard snake_mail](./images/snake_mail_perfboard_1mb.jpg)

Assembled:
![assembled snake_mail](./images/snake_mail_enclosure.jpg)

## adjustable-height desk ##
This project originated with a desire to provide more variety in seating positions.
I get back pain, and being able to change how I sit seems to help a lot.  
I used some metal struts from Lowes, and a couple of 
[linear](https://www.amazon.com/WindyNation-Stroke-Linear-Actuator-Maximum/dp/B00Y1QD9AM)
[actuators](https://www.amazon.com/Inch-Linear-Actuator-Volt-Pounds/dp/B007SJAHW2).

That, in combination with
[relay kits](https://www.amazon.com/MPC-0462-Linear-Actuators-Wiring/dp/B00LON21DQ)
and a 
[wireless controller](https://www.amazon.com/gp/product/B01CCSG2ZY)
completed the project.  This is one the simplest projects I've built, and one of 
the most expensive, but my desk is pretty comfortable.
The desk in 'sit on the floor' mode:
![floor-sitting mode](./images/lowered_desk.jpg)
The desk in 'sit in the chair' mode: 
![chair-sitting mode](./images/raised_desk.jpg)

## wii-motion quad copter ##

My son and I built this quad copter; the controller is an 
[arduino pro mini](https://www.sparkfun.com/products/11113); you can learn more
about it 
[here](http://www.multiwii.com/wiki/index.php?title=Main_Page).

The MutiWii is built from the gyroscope built into the Wii Motion Plus, 
and the accelerometer built into the Wii Nunchuck.  It was a fun little project,
and was actually my first introduction to Arduino.
Here's what the final controller looks like.  You can still see the joystick
from the nunchuck :)
![quad copter controller board](images/copter_close_up.jpg)
Here's a second picture, with my hand, for scale.
![quad copter](images/copter.jpg)

## Flashing a bricked motherboard bios ##

A few days ago, a friend asked me to troubleshoot a motherboard that was locking
up.  I attempted to update the BIOS, and of course, it locked up, effectively
bricking the motherboard.  A little research, and I found that it was possible
to flash the BIOS with the use of a Raspberry PI.  I used these links
as a reference:

[rPI hookup](https://forum-en.msi.com/index.php?topic=283908.msg1608415#msg1608415)

[diagrams and such](https://forum-en.msi.com/index.php?topic=285607.0)

Essentially, you can use a 'chip clip' to directly wire into the chip; the 
chip itself uses the well-known [SPI - Serial Peripheral Interface](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus) protocol.  So, all I needed
to do was feed it power, connect to it correctly.  Since the motherboard was 
a brick at this point, there was no harm in giving it a shot.  Also, looking at 
the 'flashrom' tool, I didn't even have to implement any read/write code.  All
I needed was a solid connection.  The guides helpfully pointed me to something
called a [chip clip, or test clip](https://www.sparkfun.com/products/13153), which I grabbed off of Sparkfun.  This piece is cheaper elsewhere, but I live near 
Sparkfun headquarters, so I was able to go grab it from them less than 12 hours
after ordering it.

The online resources were really good, but they made very generous assumptions
about how much I needed things to be spelled out.  So I'm documenting the 
pieces that the above links failed to provide me.

There were two chunks I had to puzzle out.  First, most people took pics
of the chip clip, connected to the chip on the motherboard, but failed to 
include a good wiring diagram.  Also, my Raspberry PI didn't have the SPI
protocol enabled by default, so I had to do some modifications to get it to
even 'notice' that it was attached to the BIOS chip.


Wiring everything up.  This part was confusing, because I didn't know how to 
map the MISO and MOSI ports -- which one goes to "SO/SI01", and which one 
goes to "SI/SO0".  I eventually found [this link](https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=136912) that labeled all of the ports; here's a pic, with what I ended up with; an external power supply, set to 1.5 volts, the chip clip seen in some of the other links, and the flashrom tool.

Here's a pic of what that looks like
![Raspberry PI wired to chip clip](images/bios_image.jpg)

and a wiring diagram, to really spell it out:
![wiring diagram](images/bios_wiring.jpg)

For the Raspberry Pi, I was missing the /dev/spidev0.0 files.  Here are the 
steps I had to take, to make them appear:

```
sudo apt-get update
sudo apt-get upgrade
```

3.  edit the /config.txt file; I had to uncomment the line containing "dtparam=spi=on", and reboot, which made the spidev files appear.

after that the instructions at the link below worked fine: 

[rPI basic instructions](http://www.win-raid.com/t58f16-Guide-Recover-from-failed-BIOS-flash-using-Raspberry-PI.html)

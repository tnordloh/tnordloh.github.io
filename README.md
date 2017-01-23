# Electronics projects #

## Contents ##

* [plant monitor](#port-plant-monitor)
* [plant monitor](#port-plant-monitor)
* [snake enclosure monitor](#snake-enclosure-monitor)
* [adjustable height desk](#adjustable-height-desk)
* [WiiMotion Quad Copter](#wiimotion-quad-copter)

## 16-port plant monitor ##

This project was created when my spouse found that the moisture sensors
she bought.  Unfortunately, they conumed their batteries in just a week.  She 
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
This project originated with a desire to provid more variety in seating positions.
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
![when I want to sit on the floor](./images/lowered_desk.jpg)
The desk in 'sit in the chair' mode: 
![when I want to sit on the chair](./images/raised_desk.jpg)

## wii-motion quad copter ##

My son and I built this quad copter; the controller is an 
[arduino pro mini](https://www.sparkfun.com/products/11113); you can learn more
about it 
[here](http://www.multiwii.com/wiki/index.php?title=Main_Page)
recipe.

The MutiWii is built from the gyroscope built into the Wii Motion Plus, 
and the accelerometer built into the Wii Nunchuck.  It was a fun little project,
and was actually my first introduction to Arduino.

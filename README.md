# Electronics projects #

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

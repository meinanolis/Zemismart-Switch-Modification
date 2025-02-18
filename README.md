# Zemismart-Switch-Modification

in this project I used the Zemismart Switch (ZM-L02E), flashed ESPEasy onto it, added a PIR (HC-SR501), added a enviromental sensor (BMP280) and used it in a 2-Way-Switch installation.

* Zemismart Switch (ZM-L02E) [Aliexpress](https://www.aliexpress.com/item/4000042024675.html)
* PIR (HC-SR501) [Aliexpress](https://www.aliexpress.com/item/33054839441.html)
* Enviromental sensor (BMP280) [Aliexpress](https://www.aliexpress.com/item/32654011852.html)
* Light sensor (BH1750) [reichelt](https://www.reichelt.de/entwicklerboards-digitaler-lichtsensor-bh1750-debo-bh-1750-p224217.html)

![zm](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/31ce12c5181a6f47db147eadfc0efbb6ba3e0430/img/ZM-switch.jpg "zm")

I chose this switch since i wanted a switch with physical buttons and it is beautiful. Since in my hallway there is a 2-Way-Switch system ([wiki](https://en.wikipedia.org/wiki/Multiway_switching)) I need a dual switch. After buying it I was very pleased to find a big ESP-chip inside with easy accesible contacts.

![Zemismart Switch ZM-L02E Pinout](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/0154c4811b8b5eb5be7da9a4c8c276da7167ca6f/img/Pinout.png "Zemismart Switch ZM-L02E Pinout")

## Flashing

There are quite a lot [tutorials](https://www.letscontrolit.com/wiki/index.php/Basics:_Connecting_and_flashing_the_ESP8266) for flashing an ESP. So brief here:

1. power the ESP with 3,3V max. Powering it via its own powersupply with 230V is a no no.
1. connect Tx->Rx, Rx->Tx, Vcc->3.3V, GND->GND and GPIO0->GND during Boot.
1. flash ESPEasy (ESP_Easy_mega-*****_normal_core_241_ESP8266_1M.bin)

## Connecting the Mains

In my hallway i have two switches. They are connected as shown below or [here](https://en.wikipedia.org/wiki/Multiway_switching). To make my hallway smart I replaced the first 2-way-switch with the dual smart switch as shown in the below figure.

![Connecting the Mains](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/749db8b11b09d6f0e8e6732f02485d24d8ad2c45/img/2-WegeSchaltung.png "Connecting the Mains")

Not at all installations there is the N-wire present at the switches. The n-wire, however, is needed to power the smartswitch.

**Do not forget to not kill yourself while playing with the mains! Don't be alone, always think twice, no hurry!**

## Connecting the Sensors

The Chip is tall, there free pads for VCC, GND and GPIO16. GPIO1 and GPIO3 are unused at the ESP. All easy. I used:

* GPIO16 as input for the PIR
* GPIO1 marked on the ESP with Tx as SDA
* GPIO3 marked with Rx as SCL

![Wireing](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/36a05152045a19ae01fd1d60db242cb51a337bbd/img/Sensors.png "Wireing")

And yes, you can use the HC-SR501 with 3.3V. You just have to connect the power to another pin as shown [here](https://randomnerdtutorials.com/modifying-cheap-pir-motion-sensor-to-work-at-3-3v/).

## Setting up ESPEasy

Now you can setup ESPEasy. Everything is detailed [here](https://www.letscontrolit.com/wiki/index.php?title=ESP_Easy_web_interface). Below I concentrate on the project specific settings.

### Hardware Tab

after powerup the Relais should be one on and the other off for having the regularswitch working. you can do that in the Hardware tab by setting the Bootstate of:

* GPIO13 to Low
* GPIO14 to High

### Devices

* The two push buttons are configured as *switch inputs* and button type *active low*.
* If you like to you can also configure the relais as switches but thats optional.
* Also the PIR is nothing but a switch input.
* The configuration of the BMP280 is explained [here](https://www.letscontrolit.com/wiki/index.php?title=BME280).
* The configuration of the BH1750 is explained [here](https://www.letscontrolit.com/wiki/index.php?title=BH1750).

![ESP_setting](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/3d7dbc4d4c6955987a470c4cf29de6e8435dda06/img/ESP_Devices.png "ESP_setting")

### Rules

For the switch to also work without connection enable the Rules and input

```
on System#Boot do
   gpio,13,1
   gpio,14,0
endon

on RightButton#State do
   if [Relais_1#State]=0
      gpio,13,1
      gpio,14,0
   else
      gpio,13,0
      gpio,14,1
endon
```

In a 2-way switch system you don't know witch state you are in. Therefore a toggle function is helpful.

```
on toggle do
   if [Relais_1#State]=0
      gpio,13,1
      gpio,14,0
   else
      gpio,13,0
      gpio,14,1
endon
```

Use the LED connectetd to GPIO00 to indicate the state of the PIR. Helps maintaining.

```
on Bewegungsmelder#State do
   if [Bewegungsmelder#State]=0
      gpio,0,1
   else
      gpio,0,0
endon
```

## Final result
![Final result](https://raw.githubusercontent.com/meinanolis/Zemismart-Switch-Modification/master/img/IMG_20191001_205900.jpg "Final result")
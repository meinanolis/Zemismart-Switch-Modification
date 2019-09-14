# Zemismart-Switch-Modification

in this project I used the Zemismart Switch (ZM-L02E), flashed ESPEasy onto it, added a PIR (HC-SR501), added a enviromental sensor (BMP280) and used it in a 2-Way-Switch installation.

* Zemismart Switch (ZM-L02E) [Aliexpress](https://www.aliexpress.com/item/4000042024675.html)
* PIR (HC-SR501) [Aliexpress](https://www.aliexpress.com/item/33054839441.html)
* Enviromental sensor (BMP280) [Aliexpress](https://www.aliexpress.com/item/32654011852.html)

![zm](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/31ce12c5181a6f47db147eadfc0efbb6ba3e0430/img/ZM-switch.jpg "zm")

I chose this switch since i wanted a switch with physical buttons and it is beautiful. Since in my hallway there is a 2-Way-Switch system ([wiki](https://en.wikipedia.org/wiki/Multiway_switching)) I need a dual switch. I was very pleased after I ordered it and finding a big ESP-chip inside with easy accesible contacts.

![pinout](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/0154c4811b8b5eb5be7da9a4c8c276da7167ca6f/img/Pinout.png "pinout")

## Flashing

There are quite a lot [tutorials](https://www.letscontrolit.com/wiki/index.php/Basics:_Connecting_and_flashing_the_ESP8266) for flashing an ESP. So brief here:

1. Power the ESP with 3,3V max. Powering it via its own powersupply with 230V is a no no.
1. connect Tx->Rx, Rx->Tx, Vcc->3.3V, GND->GND and GPIO0->GND during Boot.
1. flash ESPEasy (ESP_Easy_mega-*****_normal_core_241_ESP8266_1M.bin)

## Connecting the Mains

In my hallway i have two switches. They are connected as shown [here](https://en.wikipedia.org/wiki/Multiway_switching). To make my hallway smart I replaced the first 2-way-switch with the dual smart switch as shown in the below figure.

![pinout](https://github.com/meinanolis/Zemismart-Switch-Modification/blob/0154c4811b8b5eb5be7da9a4c8c276da7167ca6f/img/Pinout.png "pinout")

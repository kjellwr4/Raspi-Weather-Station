# Resources
* [Adafruit;s DHT Humidity Sensing on Raspberry Pi or Beaglebone Black](https://learn.adafruit.com/dht-humidity-sensing-on-raspberry-pi-with-gdocs-logging/software-install-updated)
* [DHT22](https://www.digikey.com/catalog/en/partgroup/dht22-temperature-and-humidity-sensor/58084?utm_adgroup=xGeneral&slid=&gclid=EAIaIQobChMI9cWtle213gIVQkOGCh0OBQ54EAAYASAAEgIab_D_BwE)
# Instructions
1. Wire the DHT22 to the Raspi.

![DHT22 & BMP280 Wiring Diagram](https://github.com/kjellwr4/Raspi-Weather-Station/blob/BMP280/DHT22/Raspi%20BMP280%20DHT22%20with%20BB_bb.png)

2. Open the Terminal on the Raspi. Navigate to the home directory by typing `cd ~`
3. Type the following in the Terminal: `git clone https://github.com/adafruit/Adafruit_Python_DHT.git`
4. Navigate to the _Adafruit_Python_DHT_ directory by typing `cd Adafruit_Python_DHT`
5. Update and upgrade the Raspi by typing the following commands into the Terminal:
```
sudo apt-get update
sudo apt-get install build-essential python-dev python-openssl
```

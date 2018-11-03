# Resources
* [Adafruit;s DHT Humidity Sensing on Raspberry Pi or Beaglebone Black](https://learn.adafruit.com/dht-humidity-sensing-on-raspberry-pi-with-gdocs-logging/software-install-updated)
* [DHT22](https://www.digikey.com/catalog/en/partgroup/dht22-temperature-and-humidity-sensor/58084?utm_adgroup=xGeneral&slid=&gclid=EAIaIQobChMI9cWtle213gIVQkOGCh0OBQ54EAAYASAAEgIab_D_BwE)
# Instructions
1. Wire the DHT22 to the Raspi.

![DHT22 & BMP280 Wiring Diagram](https://github.com/kjellwr4/Raspi-Weather-Station/blob/BMP280/DHT22/Raspi%20BMP280%20DHT22%20with%20BB_bb.png)

2. Open the Terminal on the Raspi and type `sudo pip3 install Adafruit_DHT`
3. Navigate to the _Adafruit_Python_DHT_ directory by typing `cd Adafruit_Python_DHT`
4. Type the following command in the terminal `sudo python3 setup.py install`
5. Open and save a new python file entitled _DHT22.py_.
   * Copy-and-paste the following code into the file.
   * Execute the file and make sure the terminal displays both the temperature and humidity.
6. hgf

2. Open the Terminal on the Raspi. Navigate to the home directory by typing `cd ~`
3. Type the following in the Terminal: `git clone https://github.com/adafruit/Adafruit_Python_DHT.git`
4. Update the Raspi by typing `sudo apt-get update`
5. Type `sudo apt-get install build-essential python-dev python-openssl` in the Terminal. These packages were installed when setting up the BMP280.
6. Navigate to the _Adafruit_Python_DHT_ directory by typing `cd Adafruit_Python_DHT`
7. Install the DHT library by typing `sudo python setup.py install` once inside the _Adafruit_Python_DHT_ directory.

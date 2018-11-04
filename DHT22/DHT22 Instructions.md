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
```
import sys
import Adafruit_DHT

#First argument is the sensor type. Second argument is the pin.
humidity, temperature = Adafruit_DHT.read_retry(22, 4)

# Fahrenheit conversion. Default is Celcius.
temperature = temperature * 9/5.0 + 32

if humidity is not None and temperature is not None:
    print('Temp={0:0.2f}*  Humidity={1:0.2f}%'.format(temperature, humidity))
else:
    print('Failed to get reading. Try again!')
    sys.exit(1)
```
6. Troubleshoot any error messages as necessary.
7. Navigate to the _weather-station_ directory by typing `cd ../weather-station`
8. Create a new file named _BMP280-and-DHT22.py_ in the _weather-station_ directory.
9. Open the file and copy-and-paste the following code. Execute the script and check for correct readings.
```
import board
import digitalio
import busio
import time
import adafruit_bme280
import sys
import Adafruit_DHT

i2c = busio.I2C(board.SCL, board.SDA)
bme280 = adafruit_bme280.Adafruit_BME280_I2C(i2c)

# BMP280: Change 181 to the altitude (meters) of device location.
# 8.3 is a constant.
seaLevelPressure = bme280.pressure + (181/8.3)

# BMP280: Fahrenheit conversion.
tempFahrenheit = (bme280.temperature * 9/5) + 32

# DHT22: First argument is the sensor type. Second argument is the pin.
humidity, temperature = Adafruit_DHT.read_retry(22, 4)

# DHT22: Fahrenheit conversion. Default is Celcius.
temperatureDHTF = temperature * 9/5.0 + 32

while True:
    print("\nTemperatureBMP: %0.2f C" % bme280.temperature)
    print("TemperatureDHT22: %0.2f C" % temperature)
    print("Temperature: %0.2f F" % tempFahrenheit)
    print("TemperatureDHT: %0.2f F" % temperatureDHTF)
    print("Humidity: %0.2f P" % humidity)
    print("Absolute Pressure: %0.2f hPa" % bme280.pressure)
    print("Sea Level Pressure: %0.2f mb" % seaLevelPressure)
    time.sleep(5)
```
10. Save the file.
11. Follow the instructions for the weather vane.

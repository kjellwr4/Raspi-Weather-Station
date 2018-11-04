# Resources
* [Raspberry Pi Foundation's Weather Station Tutorial](https://projects.raspberrypi.org/en/projects/build-your-own-weather-station/3)
* [Adafruit Python Tutorial](https://circuitpython.readthedocs.io/projects/bme280/en/latest/)
* [BMP280](#) or [BME280](https://www.adafruit.com/product/2652?gclid=EAIaIQobChMI987N-6ip3gIVjFqGCh1sTQxHEAQYASABEgLhyfD_BwE)
# Instructions
_Note: There are two sensors that have very similar names. One is the BME280 which measures temperature, pressure, and humidity. The other is a BMP280 which measures temperature and pressure (no humidity). These instructions use a BMP280 but it refers to drivers that work with both sensors. The drivers and calls refer to BME280._
1. Wire the BMP280 to the Raspi.

![BMP280 Wiring Diagram](https://github.com/kjellwr4/Raspi-Weather-Station/blob/BMP280/BMP280/Raspi%20BMP280%20with%20BB_bb.png)

2. [Adafruit Driver Instructions](https://circuitpython.readthedocs.io/projects/bme280/en/latest/)
   * `sudo pip3 install adafruit-circuitpython-bme280`
   * `sudo nano /usr/local/python3.5/dist-packages adafruit_bme280.py`
   * Change `_BME280_CHIPID = const(0x60)` to `_BME280_CHIPID = const(0x58)`
3. Create a python file named _bmp280_sensor.py_. Copy-and-paste the following code into the file and then execute the script. The output should be four readings.
```python
import board
import digitalio
import busio
import time
import adafruit_bme280

i2c = busio.I2C(board.SCL, board.SDA)
bme280 = adafruit_bme280.Adafruit_BME280_I2C(i2c)

#Change 181 to the altitude (meters) of device location. 8.3 is a constant.
seaLevelPressure = bme280.pressure + (181/8.3)

#Fahrenheit
tempFahrenheit = (bme280.temperature * 9/5) + 32

while True:
    print("\nTemperature: %0.1f C" % bme280.temperature)
    print("Temperature: %0.1f F" % tempFahrenheit)
    print("Absolute Pressure: %0.1f hPa" % bme280.pressure)
    print("Sea Level Pressure: %0.1f mb" % seaLevelPressure)
    time.sleep(5)
```
4. Add the DHT22 by completing these instructions: ???

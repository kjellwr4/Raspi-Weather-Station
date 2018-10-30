# Resources
* [Raspberry Pi Foundation's Weather Station Tutorial](https://projects.raspberrypi.org/en/projects/build-your-own-weather-station/3)
* [Adafruit Python Tutorial](https://circuitpython.readthedocs.io/projects/bme280/en/latest/)
* [BME280](https://www.adafruit.com/product/2652?gclid=EAIaIQobChMI987N-6ip3gIVjFqGCh1sTQxHEAQYASABEgLhyfD_BwE)
# Instructions
The tutorial from the Raspberry Pi Foundation uses a deprecated library. I was able to run the script with the BME280 wired to the Raspi, but the output did not show humidity values.
1. Wire the BME280 to the Raspi

![BME280 Wiring Diagram](https://github.com/kjellwr4/Raspi-Weather-Station/blob/BME280/BME280/Raspi%20Weather%20Station%20BME280_bb.png)

2. [Adafruit Driver Instructions](https://circuitpython.readthedocs.io/projects/bme280/en/latest/)
   * `sudo pip3 install adafruit-circuitpython-bme280`
   * `sudo nano /usr/local/python3.5/dist-packages adafruit_bme280.py`
   * Change `_BME280_CHIPID = const(0x60)` to `_BME280_CHIPID = const(0x58)`
3. Create a python file named _bme280_sensor.py_. Copy-and-paste the following code into the file and then execute the script. The output should be all three readings from the sensor (2 second interval).
```
import board
import digitalio
import busio
import time
import adafruit_bme280

# Create library object using our Bus I2C port
i2c = busio.I2C(board.SCL, board.SDA)
bme280 = adafruit_bme280.Adafruit_BME280_I2C(i2c)

# OR create library object using our Bus SPI port
#spi = busio.SPI(board.SCK, board.MOSI, board.MISO)
#bme_cs = digitalio.DigitalInOut(board.D10)
#bme280 = adafruit_bme280.Adafruit_BME280_SPI(spi, bme_cs)

# change this to match the location's pressure (hPa) at sea level
bme280.sea_level_pressure = 1013.25

while True:
    print("\nTemperature: %0.1f C" % bme280.temperature)
    #print("Humidity: %0.1f %%" % bme280.humidity)
    print("Pressure: %0.1f hPa" % bme280.pressure)
    #print("Altitude = %0.2f meters" % bme280.altitude)
    time.sleep(2)
```
4. STOPPED HERE. Figure out how to change the pressure reading and do Fahrenheit for temp.
5. ADD THE DHT22.

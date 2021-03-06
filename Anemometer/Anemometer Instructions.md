# Resources
* [Raspberry Pi Anemometer Instructions](https://projects.raspberrypi.org/en/projects/build-your-own-weather-station/6)
* [RSensing the Weather - Wind Speed Worksheet](https://www.raspberrypi.org/learning/sensing-the-weather/lesson-2/worksheet/): See [_wind_calc.py_ solution worksheet](https://www.raspberrypi.org/learning/sensing-the-weather/lesson-2/code/wind_calc.py)
  * [GPIOZERO Bounce Edge Error](https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=226053&p=1387758#p1387758)
  * [GPIOZERO Fix](https://github.com/RPi-Distro/python-gpiozero/issues/687#issuecomment-435620598)
* [Anemometer](https://www.argentdata.com/catalog/product_info.php?products_id=145)
* [RJ11 Connectors](https://www.amazon.com/Electronics-Salon-Right-Breakout-Terminal-Connector/dp/B01GNO4L6K/ref=sr_1_1_sspa?ie=UTF8&qid=1541341497&sr=8-1-spons&keywords=rj11+breakout&psc=1)
* Optional: [Calipers for Measuring Anemometer Diameter](https://www.amazon.com/Neiko-01407A-Electronic-Digital-Stainless/dp/B000GSLKIW/ref=sr_1_3?s=industrial&ie=UTF8&qid=1541366805&sr=1-3&keywords=digital+calipers&dpID=41WMvppQQrL&preST=_SY300_QL70_&dpSrc=srch)
* Optional: [Handheld Anemometer for Baseline Testing](https://www.amazon.com/Digital-Handheld-Anemometer-Measuring-Temperature/dp/B01NATTEWW/ref=sr_1_8?ie=UTF8&qid=1541343315&sr=8-8&keywords=handheld+anemometer)
# Instructions
1. Wire the anemometer to the RJ11 breakout board. Connect the RJ11 breakout board to the Raspi.

![Anemometer](https://github.com/kjellwr4/Raspi-Weather-Station/blob/BMP280/Anemometer/Raspi%20BMP280%20DHT22%20Anemometer%20with%20BB_bb.png)

2. Open the Terminal and navigate to the home directory by typing `cd ~`
3. Make a new directory named _Anemometer_ by typing `sudo mkdir Anemometer`
4. Navigate inside of the _Anemometer_ directory by typing `cd Anemometer`.
5. Create a new python file named _Wind_Speed.py_ by typing `sudo touch Wind_Speed.py`
6. Change the read/write permissions for the file by typing `sudo chmod a+rwx Wind_Speed.py`
7. Open the _Wind_Speed.py_ file.
   * Copy-and-paste the code below into the file.
   * Save the file.
```python
from gpiozero import DigitalInputDevice
from time import sleep
import math

count = 0       # Counts how many half-rotations
radius_cm = 9.0 # Radius of your anemometer
interval = 5    # How often (secs) to report speed

# Every half-rotation, add 1 to count
def spin():
	global count
	count = count + 1
	print( count )

# Calculate the wind speed 
def calc_speed(time_sec):
        global count  
        circumference_cm = (2 * math.pi) * radius_cm        
        rotations = count / 2.0

        # Calculate distance travelled by a cup in cm
        dist_cm = circumference_cm * rotations

        speed = dist_cm / time_sec

        return speed

wind_speed_sensor = DigitalInputDevice(5)
wind_speed_sensor.when_activated = spin

# Loop to measure wind speed and report at 5-second intervals
while True:
        count = 0
        sleep(interval)
        print( calc_speed(interval), "cm/h")
```
8. Execute the script and spin the anemometer. There should be counts and readings in the terminal window.
## _Wind_Speed.py_ File Changes
There are a number of changes that must be made to the code in _Wind_Speed.py_. Many of these changes depend on the type of Anemometer used in the project. The changes below reflect the _[Argent Data Systems Anemometer](https://www.argentdata.com/catalog/product_info.php?products_id=145)_.
1. Change Line 

Include something about measuring with a professional anemometer

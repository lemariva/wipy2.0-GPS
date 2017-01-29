Driver for GPS module using WiPy 2.0
------------------------------------------------
This library allows to connect a Ublox NEO-6M GPS module to a WiPy 2.0

Wiring
-----------------------

|		|		|
|:-----:|:-----:|
|**Wipy 2.0**|**NEO-6M**|	
| `3.3v`| `VCC` | 
| `GND` | `GND` | 
| `P3`(`G12`) | `RX`  |	   
| `P4`(`G11`) | `TX`  |	   

Use:
----------
```
from ublox_gps import MicropyGPS
import time, utime

# GPS initialization
UPDATE_GPS = const(10000)					  # GPS update rate (in ms)

uart = UART(1, 9600)                          # init with given baudrate
uart.init(9600, bits=8, parity=None, stop=1)  # init with given parameters

my_gps = MicropyGPS()
stat = None
updateGPS = utime.ticks_ms()

while True:        
    try:
		# Updating GPS position
        if(utime.ticks_ms() - updateGPS >= UPDATE_GPS):
            updateGPS = utime.ticks_ms()
            stat = my_gps.updateall(uart.readall())   
		        
        if(stat != None):
			# do something with the data		
		
	except:     # gps problems
        my_gps.stringclean()  # cleaning string and starting again
		
	time.sleep_ms(1000)   # sleeping 1 second
```

More Info:
-----------
* Blog article: http://lemariva.com/blog/2017/01/wipy-2-0-weather-report-box

Credits:
---------------
* forked from: https://github.com/inmcm/micropyGPS

License:
---------------
* Check files

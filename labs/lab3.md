#### Prelab
To use 2 ToF sensors, the address of one ToF sensor was changed. This approach was taken because it required a one-time operation during setup compared to the overhead of enabling/disabling the sensors thousands of times as measurements were taken. This also required writing across the wire to the XSHUT pin twice for a run of the program whereas the second approach involved thousands of transmissions, increasing the risk of error especially as the robot runs in its physical environment. 

The sensors could be placed 90 degrees apart, on the front and side of the robot, to create front and side maps. However since the sensors have a field of view of 27 degrees, centered along the normal to surface of each sensor, there's a 63 degree 'blind spot' range between sensors that will be missed. An alternative is to place the sensor on the diagonal (45 degrees apart) from the first, reducing the blind spot range to about 18 degrees, effectively allowing a map of 72 degrees (including the blind spot) around the front of the car. However, the sides are missed and attaching the sensors is harder than in the first case, where they are simply attached to sides of the vehicle. Overall, the second approach seems preferable since it's better at detecting medium-to-small obstacles, only missing very small or distant, and more reliably creates a map of whichever direction it's driving (vs just of a 27 degree range+side). 

##### Wiring diagram <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab3/IMG_6070.jpg" width="350" height="350" style="object-fit: fill;"> <br>

#### I2C Address & Scanner
Running the scanner with a single ToF attached directly or via the breakout board returned 0x29. This matches the default address on the [Pololu page](https://www.pololu.com/product/3415) for the sensor--linked at the top of the lab--0101001b. 
However the sensor's [datasheet](https://www.pololu.com/file/0J1506/vl53l1x.pdf) (pg 19) lists 0x52 as the default address. When the program prints this address it doesn't include the last read/write bit, so the remaining bits get shifted and 0x52 becomes 0x29. <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab3/i2c_scanner.png" width="500" height="400" style="object-fit: fill;"> <br>

Running the scanner with two ToFs returned conflicting results (all possible addresses)--since the sensors are default assigned the same address, I2C messages clash. <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab3/i2c_scan_mult_sensors.png" width="500" height="400" style="object-fit: fill;"> <br>

##### Connecting without USB
Code needs to be uploaded over USB connection first then board can be detached and battery powered. To establish bluetooth connectivity at minimum uploaded code needed to begin BLE, add service and settings, advertise, and listen for central device. However print statements and data cannot be viewed in the Arduino environment so gatt characteristics must be set up and data sent to computer. 

##### Sensing Mode--Long vs Short
Short mode is less affected by ambient light and has faster sampling so better maps close environment. Given the blind spot this is an advantage. Long maps further away so may allow detecting obstacles sooner if within field of view and avoiding unneeded movement; however obstacles further away fall within a narrower range so are more likely to be in the blind spot and missed, at least are closer. Short mode was used for ToF characterization and likely in final car.
(range. repeatability, accuracy, ranging time.)

##### Sensors in Parallel
From the documentation I initially thought a sensor had to have its address changed, get shut off and then restarted for the change to take effect. I also thought a sensor had to first begin to be shut off, so getting the sequence of steps correct took several attempts. To do this, one sensor was turned on and had its address changed while the other sensor remained off. The other sensor was then turned on, and would be auto-assigned to the same default address that the first sensor had before its address was changed. I also thought XHSUT was an internally programmed register/sensor mode on the ToF, and didn't require connection to an Artemis pin, so it took several 'freeze' messages until both sensors were working. <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab3/2ToF.jpg" width="500" height="650" style="object-fit: fill;"> <br>
###### Measurements taken with both sensors. Sensor 1 is lying face up and measures the distance to the ceiling. Sensor 2 initially gets shut off across the wire to XSHUT (pcitured code) and is facing my finger (0 distance).

##### 2 ToF + IMU
The IMU could be connected in series to the Artemis board and then to the breakout at its other port, or connected at the third QWIIC port. Its I2C address was different from the ToFs so there were no clashes. <br>
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/lab2/part1_vid2.mp4" controls="controls" width="400" height="700"></video> <br>

##### ToF Speed
It was expected the limiting factor of data gathering/sending would the sensor measurements. Each sensor had a ranging time between which it started ranging and until an interrupt was set once data was available. Getting the current time was a momentary operation. <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab3/loop_tof_speed.png" width="650" height="400" style="object-fit: fill;"> <br>
To find the loop speed and measure the limitng factor the time was repeatedly checked and sensor interrupts were polled (checkForDataReady()) to display data only when new was ready and prevent hanging up the loop waiting for sensing to complete. <br>
The loop speed measured from the listed times was around 4mS on average while the sensors' measurement speed was close to 100 mS on average. <br>
<br>
Time_TOF_IMU_data
-ToF data/distance vs time
-IMU data/angle vs time

#### Prelab
Batteries for the Artemis and motor drivers are separate so that current from one battery doesn't get split across devices. This is important especially for the motor drivers which need a consistent current of at least a certain amount. Splitting may not give the same amount across runs dependent on duty cyclce, duty ratios across motors, delays and other factors
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/diagram.jpg" width="400" height="300" style="object-fit: fill;"> <br>
To select pins first the Artemis datasheet was referenced for PWM compatible pins. From the list adjacent pins, 15 & 16 and 0 & 1, to simplify wiring for a given motor driver. High/signal-carrying wires for each driver coming from different areas of the board and in different directions also reduced interference risk. <br>

#### Setup

lower limit PWM: 75 pin 15 & 16 (side closer to camera in video), ~80 for pins 0 & 1 (side further). <br>
overall sides similar strength. when initially disproprtional balanced by fixing (resoldering) tri-connected ground between drivers and motor controllers <br>
(wheels turned on briefly when ground was initially being fixed) <br>
<br>
calibration factor ~ .85 when not on floor (wheels rotating but car not moving)
-

<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/setup.jpg" width="500" height="300" style="object-fit: fill;"> <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/oscilloscope_code.jpg" width="400" height="300" style="object-fit: fill;"> <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/oscilloscope_input_v.jpg" width="400" height="300" style="object-fit: fill;"> <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/oscilloscope_output_i.jpeg" width="400" height="600" style="object-fit: fill;"> <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/car_diag.jpg" width="400" height="650" style="object-fit: fill;"> <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/spin_wheels_1.jpg" width="400" height="300" style="object-fit: fill;"> <br>
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/spin_wheels_1.mp4" controls="controls" width="400" height="700"></video> <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/spin_wheels_2.jpg" width="400" height="300" style="object-fit: fill;"> <br>
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/spin_wheels_2.mp4" controls="controls" width="400" height="700"></video> <br>
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/drive.mp4" controls="controls" width="400" height="700"></video> <br>
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab4/spin.mp4" controls="controls" width="400" height="700"></video> <br>

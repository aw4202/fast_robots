## Lab 2

Output of board at {-90, 0, 90} pitch & roll\
Also demonstrating the correct working of the IMU readings
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/lab2/part1_vid1.mp4" controls="controls" width="300" height="500"></video> \
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/rollpitcheqns.png" width="300" height="500" style="object-fit: fill;"> \
*x, y, z in the image refer to components of acceleration or (when used for the gyroscope) angular speed <br>
Yaw wasn't calculated because in the sensor's expected position laying flat, there wouldn't usually be a y component or x component of accleration, leaving yaw undefined as long as the x component is zero. Meanwhile, due to the weight of the board, a z component of acceleration is present at all times allowing pitch and roll calculation.<br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/acc_reference.png" width="200" height="500" style="object-fit: fill;"> \
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/from_datasheetacc.png" width="800" height="500" style="object-fit: fill;"> 

The AD0 value is the last bit of the board's address for I2C communication. Per board specifications this allows 2-slave I2C where the additional device has the opposite AD0 bit value as the board. Since the board always acts as slave and computer as master, this supports a third device.<br>

The output of the board was measured against box angles. Since the readings were almost exactly as expected at pitch and roll = +/-90 degrees, calibration wasn't necessary.
<video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/lab2/part1_vid2.mp4" controls="controls" width="300" height="500"></video> <br>

### Fourier Transforms and Filters - Accelerometer
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/fft_code.png" width="300" height="500" style="object-fit: fill;"> 

The stationary accelerometer shows a consistent level of noise above near-zero frequencies:<br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/stat_acc1.png" width="300" height="500" style="object-fit: fill;"> \
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/stat_acc2.png" width="300" height="500" style="object-fit: fill;"> <br>
###### without DC <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/stat_acc3.png" width="300" height="500" style="object-fit: fill;"> <br>
Though the level of noise is low compared to the DC offset, the noise isn't meaningful data, and it's large compared to gyroscope data (see below), so it should be filtered out. A cutoff frequency slightly above the DC is picked. Since the sampling period T is on average 1/80-1/120 sec, and it takes about 10 sampling frequencies to remove the DC for the stationary accelerometer (see FFT images below), fc approx. = 10 * fsamp ~ 1 is chosen, fc = 2 Hz for slight margin.<br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/lpf_form.png" width="400" height="100" style="object-fit: fill;"><br>
Since the cutoff frequency is inversely proportional to RC, and RC is inversely proportional to the filter constant alpha, a low cutoff frequency sets a low alpha. Alpha weighs the current reading against the past, with a low value corresponding to lower reliance on new data and higher reliance on the previous. This makes sense given the noisiness of the sensor: the high frequency fluctuations aren't meaningful and are best filtered out with use of the average or other readings, which are dominated by the large DC offset. <br>
<br>
Using fc=2, RC=1/(2pi*2), and with T~0.1, alpha=T/(T+RC)=0.56:<br>
###### roll and pitch from accelerometer, without and with filter:
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/acc_w_filter.png" width="300" height="600" style="object-fit: fill;"> <br>
###### DC excluded<br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/acc_w_filter_fft.png" width="300" height="600" style="object-fit: fill;"> <br>
The resulting signals show noise improvements especially at higher frequencies compared to the unfiltered signal, while not going too far with eliminating noise. >50% weight is given to current data, which creates a margin of caution for unusual signals that may not be noise. In addition the noise level is relatively low, so further improving it at the cost of this margin wouldn't be worth it.<br>

### Gyroscope
The equations for the gyroscope's yaw, pitch and roll are simply time interval updates (times speed) to its initial position, since it measures rotation about the x, y, and z axes per second (equivalent to change in roll, pitch, and yaw per second, respectively) <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/gyr_data_ypr.png"  width="400" height="200" style="object-fit: fill;"><br>
The gyroscope has lower noise than the acceleromater, with a fast decay (compared to the accelerometer's continuous oscillation) to values far lower than the accelerometer's. (See images below). The gyr may start at higher DC values than the accelerometer but quickly decays to values at least as low. There are at least a few degrees of drift per less than 10 s of data; the complementary filter value is chosen accordingly to correct this while is kept as 
low as possible to avoid introducing noise from the accelerometer.<br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/gyro_update.png"  width="650" height="200" style="object-fit: fill;"><br>
Through a few attempts a filter value of alpha=0.05 was found to eliminate drift while also minimizing noise due to the accelerometer. <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/stat_gyr_1.png"  width="300" height="600" style="object-fit: fill;"><br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/stat_gyr_2.png"  width="300" height="600" style="object-fit: fill;"><br>

### Vibration Testing the Gyro and Accelerometer
With filter parameters set for both, the two were tested by placing them on top of a cover and thumping a finger against the cover from above, by knocking on the cover, and by being placed near a washing machine while on spin cycle. All tests produced similar time-amplitude profiles with similar filtering results. <br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/vibrations.png"  width="300" height="600" style="object-fit: fill;"><br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/vibrations_acc_fft.png"  width="300" height="600" style="object-fit: fill;"><br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/gyr_a=0.05_vib.png"  width="300" height="600" style="object-fit: fill;"><br>
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab2/gyr_a=0.05_fft_vib.png"  width="300" height="600" style="object-fit: fill;"><br>


  ### Car Video
  <video src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/lab2/part_vid3.mp4" controls="controls" width="300" height="500"></video> <br>


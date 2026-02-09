## Lab 2
\
-low noise sensor: low noise mode on chip selected? and kit
-testing vibrations on low noise sensor: cutoff frequency high/close to total available freq so hard to see improvement if all
  & picking lower freq doesn't improve data quality (slightly lower a helps a bit--.6 instead of max=.73 for accelerometer
  corresp to freq=1/2 * max freq available
  -for gyro complementary filter alpha set by accelerometer being much noisier, higher noise amplitudes including when vibrations
  (vibrations often cause acc as well)
  so low alpha(~.1)->enough to cancel drift, low to introduce as little acc distrubance as possible
    -drift cancelled. filter fft amplitude often larger near dc due to much higher acc than gyro noise but drops quickly to similar magnitude
    as acc noise, so dc vs noise contrast clear
  

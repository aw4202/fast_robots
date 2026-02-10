## Lab 2

Output of board at {-90, 0, 90} pitch & roll
Also demonstrating the correct working of the sensor readings
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/lab2/part1_vid1.mp4"> \
-calibration: not needed, accurate and low noise (see below)
\
-Compared to previous years' pages accelerometer is very low noise, with nearly all time-amplitude data within one degree
of the average. Most previious year pages had variations on the scale of 50+ degrees.
The low noise may be due to the chip being in low noise mode (see chip specifications) though is mostly kit specific. 
-The gyroscope is even lower noise so to plot the FFT the first 100 or so points near the DC offset/zero frequency are skipped.
-fft plotting: due to low noise often helps to exclude DC offset + nearby frequencies (first ~100 or so)
For the accelerometer the DC offset was just at exactly 0 with magnitudes at all remaining frequencies being at least a few thousand times smaller.
This was expected from the low level of noise. Due to the difference on the scale of at least a thousand the noise level at higher frequencies was taken
as insignificant, so any data higher frequencies would be expected to be meaningful and kept, corresponding to a high cutoff frequency. 
This translated to a higher alpha filter, relying more on present data and less on past due to the higher quality of present data.
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
  -roll: drift outweighs noise (noise so small) that oscillations very small, along/centered at line of drift

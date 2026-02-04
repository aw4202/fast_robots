---
layout: default
---

## Lab 1b

#### Prelab Setup
I updated pip, installed and activated the virtual environment, downloaded the codebase and started the JupyterLab server. I then installed the Arduino BLE library from the Library Manager, opened ble_arduino.ino from the codebase and ran it for the first time to obtain the board MAC address. I updated connections.yaml to match the MAC address. \
I then generated a new uuid from my computer in Python and used it as the BLE service address in Python and Arduino (connections.yaml and ble_arduino). Since I'd modified connections.yaml, I called get_ble_controller to process the changes in Python. 
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/pre_1b.jpg" width="500" height="700" style="object-fit:contain;">
As I ran code between the computer and Arduino, one initial difficulty was that after each update to the Arduino file, the computer would throw errors and/or unexpected output. I found that it had to be disconnected and reconnected at each Arduino file update.

#### Task 1
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task1_2.png">

#### Task 2
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task2_1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task2_2.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task2_3.png">

#### Task 3
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task3_1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task3_2.png">


#### Task 4
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task4.png">

#### Task 5
(295348 - 294703 mS)/100 = ~6.45 mS/timestamp or 155 timestamps/sec \
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_1.png" width="900" height="450" style="object-fit:contain;">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_2.png" width="500" height="750" style="object-fit:contain;">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_3.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_4.png">

#### Task 6
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task6_1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task6_2.png">

#### Task 7
(842160 - 842114 mS)/100 = .46 mS/time-temp reading or 2.17k readings/sec \
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task7_1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task7_2.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task7_3.png">

#### Discussion
The second method is significantly faster (by over a factor of ten) than the first method. In the way that I've completed Task 5, calls for reading and sending 100 timestamps are made between the Arduino loop's regular read and write, so the difference may be even larger and the first method slower if I had allowed the regular loop to run in between calls to the method for Task 5. Also the calculation is for the method that sends both timestamps and temperatures. Overall, collecting data and then sending it is much faster than collecting and writing each individual reading, and the difference would be even larger if I had issued a separate command with call to handle_command for each data such as by calling SEND_TIME_DATA in a loop in Python. \
Since an integer in C is 4 bytes, the Artemis can store approximately 96k timestamps before sending any data without running out of memory. \
\

For this first lab significant time was spent properly linking and formatting content including pages, images, and videos. I am still working on videos since they may not properly display on a non-Mac OS or certain browsers. \

#### Lab 1a & b Credit
For tasks 5-7 I compared my approach with last year's websites of TAs [Jack](https://jack-d-long.github.io/fast-robots/lab1a/#next-lab-1b), [Trevor](https://trevordales.github.io/MAE4190/lab1/) and [Selena](https://ssy37.github.io/labs/lab1B.html). I also wasn't sure how much to write so checked.

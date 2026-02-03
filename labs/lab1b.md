---
layout: default
---

## Lab 1b

#### Prelab Setup
I updated pip, installed and activated the virtual environment, downloaded the codebase and started the JupyterLab server. I then installed the Arduino BLE library from the Library Manager, opened ble_arduino.ino from the codebase and ran it for the first time to obtain the board MAC address. I updated connections.yaml to match the MAC address. \
I then generated a new uuid from my computer in Python and used it as the BLE service address in Python and Arduino (connections.yaml and ble_arduino). Since I'd modified connections.yaml, I called get_ble_controller to process the changes in Python. 
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/pre_1b.jpg width="500" height="700" style="object-fit:contain;">
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
(295348 - 294703 mS)/100 = ~6.45 mS/timestamp
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_1.png" width="900" height="450" style="object-fit:contain;">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_2.png" width="500" height="750" style="object-fit:contain;">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_3.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task5_4.png">

#### Task 6
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task6_1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task6_2.png">

#### Task 7
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task7_1.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task7_2.png">
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/images/lab1/1b_task7_3.png">
(842160 - 842114 mS)/100 = .46 mS/time-temp reading

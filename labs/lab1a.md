---
layout: default
---

## Lab 1a
Task 1
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/IMG_6018.mov">
Task 2
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/IMG_6008.mov">
Task 3 \
To get an output in degrees Fahrenheit temp_raw in the print statement had to be changed to temp_f and converted to int. \
In the video I am blowing at a few times at the board. \
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/IMG_6013.mov">
Task 4
<img src="https://raw.githubusercontent.com/aw4202/fast_robots/main/videos/IMG_6016.mov">

#### Prelab Setup (1a)
To setup the board I first added the board link* in the Additional Boards Url in Settings (Mac IDE) and then installed the board under Boards Manager. After selecting the board and USB port, I ran blink and the other sketches.
I later installed the BLE library through Manage Libraries and set up the other code and environments (see Lab 1b). I ran ble_arduino for the first time to obtain the board's MAC address (screenshot in Lab 1b.)
*source https://learn.sparkfun.com/tutorials/installing-board-definitions-in-the-arduino-ide/installing-a-third-party-board-definition

#### Codebase
The Arduino board and computer communicate via Bluetooth with the use of the ArduinoBLE library, with the computer acting as the central device (client) and the Arduino as the peripheral device (server). In this library, GATT characteristics are the services presented by the peripheral to the client. ble_arduino instantiates and writes to the GATT characteristics (which are defined in BLECStringCharacteristic.h) and the computer reads them through the receive command for each characteristic. The Arduino writes to the GATT characteristics when certain values are updated or commands issued, and the computer receives only the latest value. The GATT characteristics can also be written to by the computer via send_command and read by the Arduino such as in read_data and handle_command.

Since GATT characteristics only store their latest value, the computer would need to call receive after each update and the Arduino could only write one value at a time to avoid overwriting unread values; to overcome these limitations the BLE library supports an instant notification mechanism that calls a specified handling method whenever a characteristic changes. By implicitly calling the handler at each update, multiple characteristic values can be written during one function call in Arduino and the handler can quickly process each one. Instant notifications can be activated from the computer using start_notify, and the handler associated with a characteristic using the characteristic's UUID.

The connection between the central device (computer) and peripheral (Arduino) is consistently monitored in the Arduino loop function, which checks if the central is connected and if it is, iterates between writing data and reading data sent by the computer, with the same string GATT characteristic used for either. Connect and disconnect are invoked by the central device/computer, 
which are supported by a BLE controller object returned by get_ble_controller and connection.yaml containing the addresses of the Arduino and BLE service.

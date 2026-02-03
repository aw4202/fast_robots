---
layout: default
---

## Lab 1a
![Task1](/IMG_6018.MOV)
![Task2](/IMG_6008.MOV)
![Task1](/IMG_6013.MOV)
![Task1](/IMG_6016.MOV)

#### Prelab Setup (1a)
-Arduino IDE installation, testing blink
-installing RedBoard Artemis Nano board definition (Board Manager) using https://learn.sparkfun.com/tutorials/installing-board-definitions-in-the-arduino-ide/installing-a-third-party-board-definition,
json link in Additional Boards Url
-board + port (usb) selection, running Apollo library specific temperature read (correction of pre-written code to get degrees F reading)

Prelab 1b
-updating pip, installing virtual environment, downloading codebase + activation of Jupyter lab
later reading codebase Arduino, python (demo.py) files
-Arduino BLE library install + running ble_arduino.ino (getting MAC address for first time)
-UUID generation, updating Arudino and connection.yaml (also w MAC), calling get_ble_controller after changing configuration file

#### Codebase
The Arduino board and computer communicate via Bluetooth with the use of the ArduinoBLE library, with the computer acting as the central device (client) and the Arduino as the peripheral device (server). In this library, GATT characteristics are the services presented by the peripheral to the client. ble_arduino instantiates and writes to the GATT characteristics (which are defined in BLECStringCharacteristic.h) and the computer reads them through the receive command for each characteristic. The Arduino writes to the GATT characteristics when certain values are updated or commands issued, and the computer receives only the latest value. The GATT characteristics can also be written to by the computer via send_command and read by the Arduino such as in read_data and handle_command.

Since GATT characteristics only store their latest value, the computer would need to call receive after each update and the Arduino could only write one value at a time to avoid overwriting unread values; to overcome these limitations the BLE library supports an instant notification mechanism that calls a specified handling method whenever a characteristic changes. By implicitly calling the handler at each update, multiple characteristic values can be written during one function call in Arduino and the handler can quickly process each one. Instant notifications can be activated from the computer using start_notify, and the handler associated with a characteristic using the characteristic's UUID.

The connection between the central device (computer) and peripheral (Arduino) is consistently monitored in the Arduino loop function, which checks if the central is connected and if it is, iterates between writing data and reading data sent by the computer, with the same string GATT characteristic used for either. Connect and disconnect are invoked by the central device/computer, 
which are supported by a BLE controller object returned by get_ble_controller and connection.yaml containing the addresses of the Arduino and BLE service.

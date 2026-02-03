---
layout: default
---

## Lab 1a


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
The Arduino board and computer communicate via Bluetooth with the use of the ArduinoBLE library, with the computer acting as the central device (client) and the Arduino as the peripheral device (server). In this library, GATT characteristics are the services presented by the peripheral to the client. ble_arduino instantiates and writes to the GATT characteristics (which are defined in BLECStringCharacteristic.h) and the computer reads them through the receive command for each characteristic. (The BLE GATT characteristic can also be written to by the computer and read by the Arduino via send_command.)

The Arduino writes to a characterstic whenever certain program-specific values are updated, such as with new sensor readings, and the computer should receive the new value. To see updated values, the computer calls the receive method for a characteristic to see the characteristic's latest value. The value stored in the characteristic depends on the variable most recently copied into it, so to modify or read specific variables, or to make other requests from the client computer to the Arduino, a send_command method is included in ble.py. This method also uses the GATT characteristic, to pass the command, this time with the client writing to it and the peripheral reading it. On the reading/receiving end, the Arduino processes commands in ble_arduino, with additional support from RobotCommand.h. 

Since explicitly invoking a receive method each time to see a characteristic's newest value would be tedious and inefficient, the BLE library also supports an instant notification mechanism that calls a selected handling method whenever a peripheral's characteristic changes. Without this the Arduino could only write one value to characteristic value at a time between receive method calls; otherwise each value couldn't be recorded by the comupter. By implicitly calling the handler at each update, multiple characteristic values can be written at a time, and the central device's handler can quickly and process each one. Instant notifications can be turned on and handler set using ble.py's start_notify method.


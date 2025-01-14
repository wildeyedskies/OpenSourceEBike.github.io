# DIY EBike board

The DIY EBike board task is to run the EBike software application. This software is high level Pyhton (easy and fast to develop) and we can edit/program the Pyhton software text files wirelessly, using our phone or computer.

The EBike application reads the input sensors as the throttle, maps the throttle value to a motor current (motor torque), and finally send this value to VESC motor controller, that will make the motor rotate with this specific current / torque.
It also sends and receives data to the display.

There are 4 sensors on Bafang M500:
* **Torque sensor:** has a CANBUS connection and outputs the pedal torque and pedal cadence values.
* **Throttle:** is a simple analog signal between 0 and 3.3V that represents the throttle position.
* **Brake:** is a simple digital signal between 0 and 3.3V, that stays at 3.3V while the brakes are not pressed.
* **Motor temperature:** is a simple analog signal between 0 and 3.3V that represents the motor temperature.

The communication between the EBike board and VESC is digital UART.

The communication between the EBike board and display is also digital UART.

This is the EBike board schematic, that is very easy to build due to easy to solder boards and connectors:<br>
[<img src="EBike_board-schematic.png" width="1800"/>](EBike_board-schematic.png)

The main component is the ESP32-S3-DevKitC-1 N8R2 board. This is the microcontroller board, that runs the high level Pyhton software, has Wifi and Bluetooth.

The connection to VESC is by the 4 wires: 2 wires for UART TX and UART RX that provides the comunication. The other 2 wires and GND and +5V, as the power to the EBike board comes from the VESC.

The throttle wire needs to have a 47K resistor connected to ground. This is a must for the case the throttle disconnects by accident, and this resistor will force the throttle signal to be zero.

The only other board is the TJA1050 (you can buy in Aliexpress), is small and is a CANBUS module. This board is needed to make the ESP32-S3 board being able to communicate with the Bafang M500 torque sensor.
The torque sensor needs also to be powered from 5V.

The brake signal needs to have a 47K resistor connected to +3.3V otherwise it will not work.

The temperature sensor signal needs to have a 1K resistor connected to GND.

You can buy all the boards, components, connectors and even wires, on Aliexpress.
Note that the connectors are:
* big connector with various signals: PHB connector 2.0mm 2x11P
* torque sensor connector: PHB connector 2.0mm 2x3P
* motor temperature sensor connector: PHB connector 2.0mm 2x3P

Here are the connectors pins:

The 2x11P connector::<br>
[<img src="Bafang_M500-big_connector.png" width="1200"/>](Bafang_M500-big_connector.png)

The 2x3P connector for motor temperature sensor:<br>
[<img src="Bafang_M500-torque_sensor_connector.png" width="500"/>](Bafang_M500-torque_sensor_connector.png)

## Pictures with details

The purple board is the ESP32-S3-DevKitC-1 N8R2 board. I used kapton tape, that is a yellow, strong plastic tape that can withstand high temperatures, under the ESP32 board, to isolate it from the VESC board.

[<img src="EBike_board-12.jpg" width="500"/>](EBike_board-12.jpg)

The ESP32-S3-DevKitC-1 N8R2 board from the top side. Bellow is the VESC motor controller.

Basically, the ESP32 board is just the righ size to be placed on top of that VESC and even keep free the VESC connectors.

[<img src="EBike_board-1.jpg" width="500"/>](EBike_board-1.jpg)

The next pictures were taken on a previous prototype I did, not on the final version. But you can take as example to see how I solder that small blue board, that is the TJA1050 CANBUS module.

I used a little of a perforated board to hold the TJA1050 board and solder some wires there, like a dedicated line for GND and +5V, as I will need to solder a few wires to each of them.

[<img src="EBike_board-13.jpg" width="500"/>](EBike_board-13.jpg)

And here the example how I solder the wires to each pad of the ESP32 board.

[<img src="EBike_board-14.jpg" width="500"/>](EBike_board-14.jpg)

But here is the final EBike board fully built. That small blue board is the TJA1050 CANBUS module.
I used a little of a perforated board to hold the TJA1050 board and solder some wires there, like the GND, +5V and 3.3V. Also the resistors, I used a SMD 0805 resistors, that are small but not to much.

I used double face tape to fix the boards between them. And I also use Kapton tape a lot for isolation.

That wires are kind of big, but at least they are resistant but also soft, as the exterior seems to be silicone. I bought them on Aliexpress.

And there is only one connector to connect to the VESC (bottom right side on the picture). That connector came with the VESC and as you can see, I am using the black and red wires for GND and +5V. The yellow and white wires for UART TX and UART RX.

[<img src="EBike_board-2.jpg" width="500"/>](EBike_board-2.jpg)

Note that I did a few tests while I was building the board, to make sure everything would fit inside the Bafang M500.

[<img src="EBike_board-3.jpg" width="500"/>](EBike_board-3.jpg)

Detail of the VESC (the EBike/EScooter board is placed on the top).

[<img src="EBike_board-15.jpg" width="500"/>](EBike_board-15.jpg)

I built the board following the schematic and I were testing it as I was progressing. I used a simple specific software to read the sensors (available on the software repository) and make sure they were working.

[<img src="testing_sensors.png" width="500"/>](testing_sensors.png)

And after I tested that everything was working, I put silicone on the wires and board. This makes all more robust and in long term, avoid possible wires brake due to vibrations while riding.<br>
Note that I had great care to not put silicone on the USB connectors as I may need to use them again later.

[<img src="EBike_board-4.jpg" width="500"/>](EBike_board-4.jpg)

Also silicone on the connectors.

[<img src="EBike_board-5.jpg" width="500"/>](EBike_board-5.jpg)

And finally I isolated the board and motor controller with kapton tape, since all this will be in contact with the metal case of the motor.

[<img src="EBike_board-6.jpg" width="500"/>](EBike_board-6.jpg)

And here is the VESC + the EBike board installed inside the Bafang M500.

[<img src="EBike_board-7.jpg" width="500"/>](EBike_board-7.jpg)

As there is more used space compared to original motor controller, I designed and 3D printed in ABS plastic, a new motor cover but with a bit more space to acomodate the wires.

[Download here the motor cover source file for FreeCAD](motor_cover.FCStd) and [the file for 3D print](motor_cover.amf).

[<img src="EBike_board-8.jpg" width="500"/>](EBike_board-8.jpg))

And I put a nice amount of silicone on the cover, to make sure it will keep water prof.

[<img src="EBike_board-9.jpg" width="500"/>](EBike_board-9.jpg)

And the final result.

[<img src="EBike_board-10.jpg" width="1200"/>](EBike_board-10.jpg)

[<img src="EBike_board-11.jpg" width="1200"/>](EBike_board-11.jpg)

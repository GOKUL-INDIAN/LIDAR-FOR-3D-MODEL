# LIDAR-FOR-3D-MODEL
This project presents the design and implementation of a low-cost, microcontroller-based 3D LiDAR scanner. The system uses laser-based ranging to generate point cloud data representing objects in three-dimensional (X, Y, Z) space. It scans from 0° to 180° in the X direction and 26° to 125° in the Y direction, with a detection range of up to 1.2 meters. Real-time distance and angle data are displayed on an LCD. All components are implemented using SMD packages for compact design and portability.

# PROCESSING UNIT
The ATmega328P microcontroller serves as the central processing unit of the system. It receives input signals from the LiDAR sensor and control switches through its input pins. The controller processes the acquired data, performs the required computations, and transmits the processed output to the PC, LCD display, and Bluetooth module.

Capacitors are incorporated to suppress noise and ensure stable circuit operation. Resistors in the switch network are used to generate distinct voltage levels corresponding to different switch activations.

In terms of specifications, the ATmega328P is an 8-bit AVR RISC-based microcontroller featuring 32 KB of Flash program memory, 2 KB of SRAM, and a total of 32 pins, including 8 analog input pins and 14 digital I/O pins. For this design, the SMD package of the ATmega328P is selected.

# BATTERY MANAGEMENT CIRCUIT
The primary power source of the device is a 3.7V lithium-ion battery. While the cell is capable of supplying the required power efficiently, it must be handled with extreme care due to safety concerns. Improper handling can lead to serious hazards, including overheating, fire, or explosion. Therefore, preventing short circuits is critically important.

To enhance safety, the design incorporates a protection circuit that safeguards the battery against short circuits, overcharging, and overvoltage conditions. An intelligent charging system is included to maintain optimal battery health and ensure safe charging operation.

The system also features a full-charge indicator to signal when the battery has reached its maximum charge level, allowing timely disconnection from the charger. Additionally, an automatic cut-off mechanism is implemented to prevent overcharging and protect the battery from potential damage.

The battery management circuit primarily consists of three integrated circuits: TP4056 (charging controller), DW01A (protection IC), and 8205A (dual MOSFET for protection switching).The TP4056 is a constant current/constant voltage linear charger designed for single-cell lithium-ion batteries. Its SOP package and minimal external component requirement make it ideal for portable applications. It supports charging through USB or wall adapters and includes an internal PMOSFET, eliminating the need for a blocking diode. Thermal regulation limits charging current to prevent overheating during high-power or high-temperature operation.

The DW01A is a lithium-ion battery protection IC that safeguards the cell from overcharge, over-discharge, and overcurrent conditions. It requires very few external components, making it compact and efficient. The S8205A is a dual MOSFET IC controlled by the DW01A, functioning as a switch to disconnect the battery during unsafe conditions such as deep discharge or overcharge. Its internal body diode allows charging current to flow appropriately.

Together, these components provide complete protection and efficient battery management. Testing confirmed reliable overcharge, deep-discharge, and short-circuit protection, along with stable constant-current charging and continuous voltage monitoring, ensuring improved battery life and safe operation.

# 5VOLT BOOST CONVERTER
This section is one of the most critical parts of the design, as it generates the required supply voltages for all system components. The device is powered by a 3.7V lithium-ion battery, ensuring portability. However, most components such as the microcontroller, LiDAR sensor, Bluetooth module, LCD, and servo motors require a 5V supply. Therefore, a boost converter is used to step up the battery voltage to a stable 5V output.

The boost converter is implemented using the MT3608 DC-DC step-up converter IC. It is a 6-pin SOT23 constant-frequency current-mode converter operating at 1.2 MHz, suitable for low-power applications. Its high switching frequency allows the use of compact, low-cost SMD inductors and capacitors. The internal soft-start feature minimizes inrush current and improves battery life.

After implementation, the converter provided stable 5V output as designed. The use of shielded SMD inductors reduced noise interference, and efficient power conversion ensured low power dissipation and compact circuit size.
# LCD CIRCUIT
The LCD interface circuit drives a 16×2 LCD display operating at 5V, supplied by the boost converter. It consists of basic components such as resistors and capacitors, where the capacitors help reduce noise. An MMBT3904 transistor is used to control the backlight brightness of the LCD.
# BLUETOOTH CIRCUIT
The Bluetooth circuit enables wireless communication between the system and a smartphone for generating object point clouds. It uses the HC-05 Bluetooth module along with supporting resistors and capacitors.

The HC-05 is a Serial Port Protocol (SPP) module that provides transparent wireless serial communication, making it easy to interface with the microcontroller and smartphone. It operates at a 3.3V supply and allows communication between serial-enabled devices via Bluetooth.

A red LED on the module indicates connection status: it blinks continuously when not connected and slows to a 2-second interval after successful pairing. A BS870 MOSFET is used to digitally control the ON/OFF state of the module, while capacitors are included to minimize power supply noise.
# USB INTERFACE
The USB interface enables communication between the microcontroller and a PC, allowing data transfer and firmware updates. It also provides a convenient way to modify or upgrade the program when required.

The interface is implemented using the CH340 USB-to-serial converter IC. This chip converts USB signals to serial communication, enabling the microcontroller to connect directly to a computer. It complies with USB 2.0 full-speed specifications and requires only minimal external components such as a crystal and capacitors.

The CH340 emulates a standard serial port, making it fully compatible with Windows-based serial applications. Additionally, it can supply input power to the system from the PC through the USB connection.

# PROGRAM FLOW FOR CONTROLLER

• Including necessary library files.
• Defining the pins of LCD screen, servos, etc.
• Defining all the necessary variables.
• Initialization of communication to LiDAR sensor, PC and LCD.
• Setting the angle values of servo motors to initial position (00 in X axis 260 in Y
axis).
• Read distance data from the sensor and send data to the PC, Bluetooth and LCD.
• Increment the angle values of servos and read distance data again and continue it
up to 1800 in X axis and 1250 in Y axis

# PROGRAM FLOW FOR PROCESSING SOFTWARE

• Importing required library files.
• Defining all the necessary variables.
• Define the serial ports for input data.
• Initialization of input port.
• Splitting the received data into three components.
• Saving the splitted data into 3 variable.
• Draw a line to show the added scan points.
• Draw points against received data

# RANGING AN OBJECT

Ranging an object means that to find out the distance at which the sensor can detect
and scans an object accurately.
# RANGING AND PLOTTING OF 2D SHAPE OF OBJECT

Ranging and plotting of 2D shape of object means that drawing the shape of object
in 2D (plain) ie, in X and Z (distance to the object) axis.

#  RANGING AND PLOTTING OF 3D POINT CLOUDS OF OBJECT

5.3 Ranging and Plotting of 3D point clouds of object
Ranging and plotting of 3D point clouds of object means that drawing the shape of
object as in 3D ie, in X, Y and Z (distance to the object) axis.

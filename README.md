# Parking System using ESP8266 and Servo Motor

This project implements a simple parking system using an ESP8266 microcontroller, an IR sensor array, a servo motor for controlling the parking gate, and a Liquid Crystal Display (LCD) for displaying the parking slot status.

### Features:
- Detects available and occupied parking slots using infrared (IR) sensors.
- Controls a servo motor to open or close the parking gate.
- Displays the parking status (empty or occupied slots) on an LCD screen.

### Hardware Requirements:
- **ESP8266 Microcontroller** (e.g., NodeMCU)
- **IR Sensors**: 3 IR sensors (used to detect car presence in parking slots) and 1 IR sensor (used for gate control)
- **Servo Motor**: For controlling the parking gate
- **LCD Display**: To display the status of the parking slots
- **Jumper Wires & Breadboard**: For connections

### Circuit Diagram:
- **IR Sensors (IR1, IR2, IR3)**: Connected to pins D0, D3, and D4 on ESP8266.
- **IR Gate Sensor (IR4)**: Connected to pin D6.
- **Servo Motor**: Connected to pin D5.
- **LCD Display**: Connected to the I2C pins (SCL, SDA) on the ESP8266.

### Installation:

1. **Install the Arduino IDE**:
   If you haven't already, install the [Arduino IDE](https://www.arduino.cc/en/software).

2. **Install ESP8266 Board in Arduino IDE**:
   - Open the Arduino IDE, go to **File** > **Preferences**.
   - In the **Additional Boards Manager URLs** field, add the following URL:  
     `http://arduino.esp8266.com/stable/package_esp8266com_index.json`
   - Go to **Tools** > **Board** > **Boards Manager**, search for **ESP8266**, and click **Install**.

3. **Install Required Libraries**:
   - Install the **Servo** library and **LiquidCrystal_I2C** library:
     - Go to **Sketch** > **Include Library** > **Manage Libraries**.
     - Search for **Servo** and **LiquidCrystal I2C**, then click **Install**.

4. **Upload the Code**:
   - Open the provided `Parking System` code in the Arduino IDE.
   - Select the appropriate **ESP8266** board and **port** from the **Tools** menu.
   - Upload the code to the ESP8266.

### How it Works:

1. **Initial Setup**:
   - The ESP8266 initializes the LCD display and shows the message **"WELCOME!"** and **"SLOT EMPTY"** for 3 seconds.
   - The servo motor is set to its initial position, and the parking slot status is checked based on the IR sensors.

2. **Parking Slot Detection**:
   - **IR1, IR2, and IR3** detect the presence of a car in parking slots. If any of these sensors detect a car (i.e., when the sensor reads a LOW signal), the corresponding parking slot is marked as occupied.
   - The system counts the number of empty parking slots and displays the count on the LCD.
   
3. **Gate Control**:
   - If at least one parking slot is empty, the system checks the **IR Gate Sensor (IR4)** for the gate status.
   - If the gate is closed (IR4 reads LOW), the system opens the gate by rotating the servo motor from 180° to 0°.
   - The gate remains open for 3 seconds, after which the servo motor returns to its initial position (180°).
   
4. **LCD Display**:
   - The LCD displays the number of empty parking slots.
   - If the gate is opened, the LCD displays **"YES"**; otherwise, it displays **"NO"**.
   - The display continuously updates the parking status.

### Code Explanation:

- **Pin Setup**: 
  - IR Sensors are connected to pins D0, D3, D4 for parking slot detection.
  - IR Gate Sensor is connected to pin D6 for controlling the gate.
  - Servo motor is connected to pin D5 to control the parking gate.

- **LCD Initialization**:
  - The LCD is initialized and displays a welcome message, followed by the current parking status.

- **Servo Motor**:
  - The servo motor is used to control the gate's position, rotating to 0° to open and back to 180° to close.

- **Sensor Reading**:
  - The code checks the state of each IR sensor and increments a counter if the slot is occupied.
  - The gate is opened or closed based on the IR Gate sensor's status.

- **Conditional Logic**:
  - The servo motor is only activated when there is an empty slot and the gate is closed.

### How to Use:

1. **Start the System**: 
   - Once the code is uploaded, the LCD will display **"WELCOME!"** and **"SLOT EMPTY"** for 3 seconds.

2. **Parking Slot Detection**:
   - Place vehicles in any of the parking slots. The LCD will update to show how many slots are available.
   
3. **Gate Control**:
   - If there is an empty slot, the system checks the status of the gate. If the gate is closed, it will automatically open for 3 seconds.
   - The gate will return to its closed position after 3 seconds, and the system will resume monitoring the parking slots.

4. **Exit**: 
   - The system continuously monitors the parking slots and updates the display until the ESP8266 is powered off.

### Notes:
- Ensure that all IR sensors and servo motor are properly connected to the specified pins on the ESP8266.
- The LCD display uses I2C communication, so make sure the SDA and SCL pins are connected correctly.
- The servo motor used should be capable of rotating between 0° and 180°.

### License:
This project is open-source and available under the [MIT License](LICENSE).

---

Feel free to modify or enhance this code to fit your needs. Enjoy building the Parking System with ESP8266!

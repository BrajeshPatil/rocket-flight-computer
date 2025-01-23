# rocket-flight-computer
The project involves developing a low-cost, open-source, multi-purpose flight computer designed specifically for model rockets. This platform will be capable of logging flight data, including acceleration and rotation, performing basic atmospheric measurements, and providing a foundation for implementing an active stability system. It aims to deliver an accessible avionics and data logging solution for hobbyists and enthusiasts.

### Hardware Interfacing
<img src="https://github.com/user-attachments/assets/b24a9e34-9494-474a-ae65-679b7b1727cb" width="600">

### List of Components:
1. Arduino NANO - This is the microcontroller which is used for interfacing the sensors,  receiving data and perform calculations for the stability of the system.
2. BMP180 - It is a Sensor which is used to sense Temperature and Pressure.
3. MPU6050 - It is a Sensor used to sense the acceleration and orientation of the rocket.
4. µSD Card Reader - Used to store the data in the form of a .csv file.
5. µSD Card with SD Adapter
6. 3 x 5mm LEDs - Used
7. 2 x 220Ω Resistor
8. Normally Open Tactile Switch
9. Piezo Buzzer
10. 22 AWG Wires
11. 9V Battery

### Module Pin Connections
1. BMP180

| **BMP180 Pin** | **Arduino Pin** | **Description**                                |
|----------------|------------------|-----------------------------------------------|
| VCC            | 3.3V            | Power supply pin for the BMP180 sensor.       |
| GND            | GND             | Ground connection.                            |
| SCL            | A4              | Serial clock line for I2C communication.      |
| SDA            | A5              | Serial data line for I2C communication.       |

2. MPU6050
   
| **MPU6050 Pin** | **Arduino Pin** | **Description**                                |
|-----------------|------------------|-----------------------------------------------|
| VCC             | 3.3V            | Power supply pin for the MPU6050 sensor.      |
| GND             | GND             | Ground connection.                            |
| SCL             | A4              | Serial clock line for I2C communication.      |
| SDA             | A5              | Serial data line for I2C communication.       |
| INT             | D2              | Interrupt pin for handling events from MPU6050. |

3. µSD Card Module
   
| **µSD Card Module Pin** | **Arduino Pin** | **Description**                                   |
|--------------------------|------------------|--------------------------------------------------|
| GND                     | GND             | Ground connection.                               |
| VCC                     | 5V              | Power supply pin for the µSD Card Module.        |
| MISO                    | D12             | Master-In-Slave-Out pin for SPI communication.   |
| MOSI                    | D11             | Master-Out-Slave-In pin for SPI communication.   |
| SCK                     | D13             | Serial Clock pin for SPI communication.          |
| CS                      | D4              | Chip Select pin for SPI communication.           |

### Working
Following steps explain the working clearly:

- Step 1: MODE 1 (Initialization)
  - Red LED lights up, indicating Mode 1.
  - The system initializes sensors (BMP180, MPU6050).
  - It attempts to connect to the microSD card and opens the data file.
  - If the connection or file open fails, it stays in Mode 1.
  - If successful, it transitions to Mode 2.
- Step 2: MODE 2 (Data Logging)
  - LED: Yellow LED lights up, indicating Mode 2.
  - Sensors collect and log data to the microSD card at the set dataRate.
  - Data is saved in a file on the microSD card, each line includes timestamp and readings.
- Step 3: Saving Data
  - Data is saved in a file named "FILE" on the microSD card.
  - Data lines have values separated by commas.
- Step 4: Mode 3 (File Closure)
  - LED: Blue LED lights up, indicating Mode 3.
  - Pressing the button on D7 transitions to Mode 3.
  - The program ensures data is safely saved to the microSD card.
  - The file is closed, and it’s safe to remove the microSD card.
- Step 5: Data File Handling
  - Remove the microSD card from the Arduino.
  - Insert the microSD card into a computer.
  - Open the file in a text editor and save it as .csv for analysis.

### Connection on a Breadboard for testing
<img src="https://github.com/user-attachments/assets/e4082656-f755-482c-94e1-e4264c78e7c4" width="400">

Due to absence of an actual rocket to test our module, we decided to test the module inside an elevator and go from ground floor to the top floor. This acts as a flight for our testing. However this is not the best way and testing under the velocity at which the rocket would move would be much more efficient. Now once the flight has been done inside the elevator we need to analyze the readings. Follow these steps for analysis of data: 

- Safely remove the microSD card from the flight module and insert it into the laptop to access the raw data.
- Open the saved .csv file in Excel and verify the columns for Time Stamp, Temperature, Pressure, etc.
- Convert the raw acceleration data into g-force by dividing the raw sensor values by 16384. Multiply by 9.81 to convert g-force into m/s².
- This data can be used to plot insightful graphs. 
- Find absolute height using the formula: `h = {1 - e^[P/(m-P0)]} / b`
  - P is the pressure (in Pa)
  - P0 = 101325 Pa (standard pressure at sea level)
  - b = 2.2557 × 10^(−5)
  - m = 5.25588
- The height can be helpful in mission objectives such as deciding the time to open a parachute or analysis of flight performance.

### PCB Design
Further, a PCB was designed for this circuitry. The microcontroller was changed to a Raspberry Pico and an Digi XBee 3.0 (2.4GHz) antenna interfacing was added in order to increase the range.

<img src="https://github.com/user-attachments/assets/bd98d64f-f3b8-4ed9-82e5-6e3099705414" width="600">

## File structure

## Contributors
- [Brajesh Patil](https://github.com/BrajeshPatil)
- [Karteek Nayak](https://github.com/Karteek-N)


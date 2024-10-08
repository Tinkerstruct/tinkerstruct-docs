# Getting started with the TS host board

## Download the software

<details><summary>For Windows</summary>
<ol> 
<li>Install the Arduino IDE using one of the links below: </li>
    <p><a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_Windows_64bit.exe">Windows 10 or newer, 64 bits (recommended) </a> </li> </p>
    <p><a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_Windows_64bit.msi">MSI Installer </a> </p>
    <p><a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_Windows_64bit.zip">ZIP File </a> </p>
<li> Install the latest STM Cube Programmer on the ST website <a href="https://www.st.com/en/development-tools/stm32cubeprog.html"> here. </a> </li>
</ol>
</details>

<details><summary>For MacOS</summary>
<ol>
<li>Install the Arduino IDE using one of the links below: </li>
    <p><a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_macOS_64bit.dmg">Intel, 10.15: “Catalina” or newer, 64 bitsE</a> </p>
    <p><a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_macOS_arm64.dmg">Apple Silicon, 11: “Big Sur” or newer, 64 bits</a> </p>
<li> Install the latest STM Cube Programmer on the ST website <a href="https://www.st.com/en/development-tools/stm32cubeprog.html"> here. </a> </li>
</ol>
</details>

---

## Set Up the Tinkerstruct host board

To start tinkering with your new kit, plug your Tinkerstruct board into your computer using a USB-C cable.  
The green power light will turn on to confirm that the board is plugged in correctly.
If using a Mac, you may see a prompt asking you to allow the accessory to connect.

<img src="../images/plugin.png" width="40%" style="display: block; margin: 0 auto;"/>

In your Downloads folder, double click on the Ardiuno IDE installation file to complete the installation. Do the same
for the STM32 programmer. <br>

Once the Arduino IDE software is installed, open the software, and go to Settings->Settings>"Additional boards manager
URL". Paste the following link for the Tinkerstruct board manager into the
settings: <a href="https://raw.githubusercontent.com/ellipticsystems/ArduinoBoardManager/main/tinkerstruct.json">
https://raw.githubusercontent.com/ellipticsystems/ArduinoBoardManager/main/tinkerstruct.json</a>. Press "OK".

<img src="../images/load_boards.png" width="100%" style="display: block; margin: 0 auto;"/>

Now press on the drop down menu at the top of the screen, and "Select other board and port". In the pop up, select the
Tinkerstruct board on the left and correct USB port on the right side and press "OK".
<img src="../images/github_link_upload.png" width="100%" style="display: block; margin: 0 auto;"/>

Once this is done, slide the toggle to PRG and then RST on your Tinkerstruct host board to reset the board. Now you are
ready for programing!

---

## RUN vs PRG

The Tinkerstruct boards have a sophisticated programming circuit inbuilt into the board. This allows users to develop
software within an IDE environment and experience dynamic compilation and upload, whilst providing the ability to store
software in non-volatile memory to load user firmware automatically after power outages or resets. No extra hardware is
required to program the board apart from a USB-C cable.

The board has two main physical switches that are necessary to use during normal operation:

- RUN/PRG slider switch
- RST toggle switch

The RUN/PRG switch is a slide switch and indicates the mode of operation for the board:

### RUN Mode:

- The board will always start and run the last uploaded program.
- You cannot change the program in this mode.
- This mode is ideal when you want the board to do the same thing every time, even after a power outage or reset.

### PRG Mode:

- The board is ready to receive a new program.
- To upload a new program, press a button to stop the current one.
- You can then send a new program to the board.
- This mode is useful for testing and trying out new programs quickly.

### RST Button:

- Pressing the RST button restarts the board.
- Depending on the mode switch, the board will start in either RUN or PRG mode.
- In PRG mode, pressing RST clears the current code and prepares the board for new code to be uploaded.

## 3. Challenges via workbooks

Click<a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_Windows_64bit.exe"> here </a> to download the
workbooks.

## 3. Challenges via software

See below some example codes.

#### Starter code - all lights flashing

In this code, an array of pins is declared of type char. A for loop is initiated to cycle through pins A-L on the
Tinkerstruct board. i is used as an iterator and is incremented by 1 in every repeat of the loop (i++). The pin()
function is called to switch on the pin, to delay 100ms and then switch the pin off for every loop. 

```

void setup() {
  // This is the tinkerstruct base PIN mapping. DO NOT edit this unless you know what you're doing:
  #define A PA0
  #define B PA1
  #define C PA2
  #define D PA3
  #define E PA4
  #define F PA5
  #define G PA6
  #define H PA7
  #define I PA8
  #define J PB6
  #define K PB7
  #define L PC14
  #define M PC15

  // Setting up the GPIO pin modes: 
  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(H, OUTPUT);
  pinMode(I, OUTPUT);
  pinMode(J, OUTPUT);
  pinMode(K, OUTPUT);
  pinMode(L, OUTPUT);

  // Setting up some helper aliases
  #define ON HIGH
  #define OFF LOW
  #define pin digitalWrite
}

void loop() {
  // This is user code land, put your code here.
  char pins[] = {A, B, C, D, E, F, G, H, I, J, K, L};
  for (int i=0; i<12; i++){
    pin(pins[i], ON);
    delay(100);
    pin(pins[i], OFF);
  }
}

```

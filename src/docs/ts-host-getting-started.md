# Getting started with the TS host board

## Download the software.

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

## Set Up the Tinkerstruct host board.

To start programming, plug your Tinkerstruct board into your computer using a USB-C cable. Click “Allow Accessory to
Connect”. The green power light will turn on to confirm that the board is plugged in correctly.

Press PRG on board then RST after loading the board.

<img src="/images/plugin.png" width="40%" style="display: block; margin: 0 auto;"/>

In your Downloads folder, double click on the Ardiuno IDE installation file to complete the installation. Do the same
for the STM32 programmer. Once you open the Arduino IDE software, search for _Tinkerstruct in_ the boards list on the
left hand side. If this doesn’t automatically show up when opening the menu….
Paste the link for the Tinkerstruct board manager into the settings: 

https://github.com/ellipticsystems/ArduinoBoardManager/blob/main/tinkerstruct.json

<img src="/images/load_board.png" width="100%" style="display: block; margin: 0 auto;"/>

<img src="/images/github_link_upload.png" width="100%" style="display: block; margin: 0 auto;"/>


RUN 
The board can also be run
when plugged into a power outlet.
---

## 3. Challenges via workbooks

<a href="https://downloads.arduino.cc/arduino-ide/arduino-ide_2.3.2_Windows_64bit.exe">Click here </a> to download the workbooks.

## 3. Challenges via software

You can access Tinkerstruct challenges using our online software (link) or using workbooks which can be downloaded
below.

#### Starter code

```

void setup() {
  // This is the tinkerstruct base PIN mapping. DO NOT edit this unless you know what you're doing.
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

  // Setting up the GPIO pin modes
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
  pinMode(M, OUTPUT);

  // Setting up some helper aliases
  #define ON HIGH
  #define OFF LOW
  #define pin digitalWrite
}

void loop() {
  // This is user code land, put your code here.
  char pins[] = {A, B, C, D, E, F, G, H, I, J, K, L, M};
  for (int i=0; i<12; i++){
    pin(pins[i], ON);
    delay(100);
    pin(pins[i], OFF);
  }
}

```

(Disinction between hardware programming and software programming and why we teach both)
(QR codes for installations)

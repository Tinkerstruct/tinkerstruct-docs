# Example Codes

### Light up all gems in sequence

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

### Light up a random gem (out of the first 6)

In this code, an array of pins is declared of type char. A for loop is initiated to cycle through pins A-L on the
Tinkerstruct board. i is used as an iterator and is incremented by 1 in every repeat of the loop (i++). The pin()
function is called to switch on the pin, to delay 100ms and then switch the pin off for every loop. 
```
void setup() {
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

  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  // pinMode(G, OUTPUT); // Use Default Analog Input
  // pinMode(H, OUTPUT); // Use Default Analog Input
  pinMode(I, OUTPUT);
  pinMode(J, OUTPUT);
  pinMode(K, OUTPUT);
  pinMode(L, OUTPUT);

  #define ON HIGH
  #define OFF LOW
  #define pin digitalWrite

  // Initialise the randomness engine
  randomSeed(analogRead(G)*analogRead(H)); // Init the random seed from 2 analog pins
}

void loop() {
  char pins[] = {A, B, C, D, E, F};
  // Pick random LED from A-F
  int rand = random(6);
  pin(pins[rand], ON);
  delay(1000);
  pin(pins[rand], OFF);
}
```

### Light up a random number of gems between 1-6 (6-die)
```
void setup() {
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

  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  // pinMode(G, OUTPUT); // Use Default Analog Input
  // pinMode(H, OUTPUT); // Use Default Analog Input
  pinMode(I, OUTPUT);
  pinMode(J, OUTPUT);
  pinMode(K, OUTPUT);
  pinMode(L, OUTPUT);

  #define ON HIGH
  #define OFF LOW
  #define pin digitalWrite

  // Initialise the randomness engine
  randomSeed(analogRead(G)*analogRead(H)); // Init the random seed from 2 analog pins
}

void loop() {
  char pins[] = {A, B, C, D, E, F};
  // Roll new die
  int rand = random(6);
  for (int i=0; i<=rand; i++) {
    pin(pins[i], ON);
  }
  while(1);
}
```
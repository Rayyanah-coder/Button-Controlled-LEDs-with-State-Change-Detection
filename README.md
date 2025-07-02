# Button-Controlled LEDs with State Change Detection

This Arduino project demonstrates how to use push buttons to toggle LEDs using **state change detection** without any external libraries. It uses internal pull-up resistors for button inputs.

##  Features
- 3 push buttons connected with internal pull-up resistors.
- 3 LEDs that toggle based on button press combinations.
- Uses `millis()` for efficient, non-blocking switch polling.
- No delay() used in the code.

##  Circuit Overview
### Buttons:
Each button is wired using internal pull-up resistors:
```
+5V -- Internal Pullup -- Arduino Pin -- Button -- GND
```

### LEDs:
Each LED is connected in active-low configuration:
```
+5V -- LED anode -- 220Ω resistor -- Arduino Pin
```
Writing `LOW` to the pin turns the LED **on**.

## Pin Configuration

| Component | Arduino Pin |
|----------|-------------|
| Button 1 | 7           |
| Button 2 | 8           |
| Button 3 | 9           |
| LED 1    | 10          |
| LED 2    | 11          |
| LED 3    | 12          |

##  Behavior

- **Button 1** toggles **LED 1**
- **Button 2** toggles **LED 1** and **LED 2**
- **Button 3** toggles **LED 2** and **LED 3**

##  Requirements

- Arduino Uno (or compatible board)
- 3 push buttons
- 3 LEDs
- 3 × 220Ω resistors
- Breadboard and jumper wires


## Arduino Code
```cpp
//when the button is not pressed, the pin reads HIGH
//When the button is pressed, the pin reads LOW.
#define Pressed  LOW
#define Released HIGH

//Writing LOW turns the LED on.
//Writing HIGH turns it off.
#define LEDon    LOW
#define LEDoff   HIGH

//pins connected to buttons.
const byte  switchOne     = 7;
const byte  switchTwo     = 8;
const byte  switchThree   = 9;

// pins connected to LEDs
const byte  LED_One       = 10;
const byte  LED_Two       = 11;
const byte  LED_Three     = 12;

//store the last state of the buttons, to detect when their state changes (press or release).
byte switchOneState;
byte lastswitchOneState;
byte lastswitchTwoState;
byte lastswitchThreeState;


void setup()
{
  pinMode(switchOne, INPUT_PULLUP);
  pinMode(switchTwo, INPUT_PULLUP);
  pinMode(switchThree, INPUT_PULLUP);



  pinMode(LED_One, OUTPUT);
  digitalWrite(LED_One, LEDon);

  pinMode(LED_Two, OUTPUT);
  digitalWrite(LED_Two, LEDon);
  
  pinMode(LED_Three, OUTPUT);
  digitalWrite(LED_Three, LEDon);

} 


void loop()
{
  
    //check switchOne
    if (checkSwitch(switchOne, lastswitchOneState) == true)
    {
  
      digitalWrite(LED_One, !digitalRead(LED_One));
      
    }
  
    //check switchTwo
    if (checkSwitch(switchTwo, lastswitchTwoState) == true)
    {
      //toggle LED
      digitalWrite(LED_One, !digitalRead(LED_One));
      digitalWrite(LED_Two, !digitalRead(LED_Two));
      
    }
    //***************
    //check switchThree
    if (checkSwitch(switchThree, lastswitchThreeState) == true)
    {
      //toggle LED
      digitalWrite(LED_Two, !digitalRead(LED_Two));
      digitalWrite(LED_Three, !digitalRead(LED_Three));
      
    }
    
}


//check if a switch has changed state
bool checkSwitch(byte switchPin, byte &lastState)
{
  byte thisSwitchState = digitalRead(switchPin);

  //was there a change in state?
  if (thisSwitchState != lastState)
  {
    //update the switch state
    lastState = thisSwitchState;

    if (thisSwitchState == Pressed)
    {
      //this switch was pressed
      return true;
    }

    else
    {
      //this switch was released
      //nothing to do here
    }

  }

  return false;

}


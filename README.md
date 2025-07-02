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


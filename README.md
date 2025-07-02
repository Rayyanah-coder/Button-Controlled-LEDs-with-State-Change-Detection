# Button-Controlled-LEDs-with-State-Change-Detection
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

##  Pin Configuration
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


## Requirements
- Arduino Uno (or compatible board)
- 3 push buttons
- 3 LEDs
- 3 × 220Ω resistors
- Breadboard and jumper wires




# Arduinocode
```
// include the library code:
#include <LiquidCrystal.h>
int sensorValue = 0;
int initalVal = sensorValue;

byte arrow[9] = {
  B00000,
  B00000,
  B00100,
  B01000,
  B11111,
  B01000,
  B00100,
  B00000,
  B00000
};
byte clear[9] = {
  B00000,
  B00000,
  B00000,
  B00000,
  B00000,
  B00000,
  B00000,
  B00000,
  B00000
};



// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  Serial.begin(9600);
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  lcd.createChar(0, arrow); // Create a custom character
  lcd.createChar(1, clear); // Create a custom character
  // Print a message to the LCD.
  lcd.clear();
  pinMode(10, INPUT);
 
}

void loop() {
  // read the input on analog pin 0:
  sensorValue = analogRead(A0);
  // map 3.3V to 5V
  sensorValue = map(sensorValue, 0, 1024, 0, 16);
  // conditional clear screen
 
  // set the cursor to column 0, line 0:
  lcd.setCursor(0, 0);
  lcd.print("I:");
  lcd.setCursor(0, 1);
  lcd.print("D:");
  // print out the value at Serial Monitor:
   
  if (digitalRead(10) == LOW) {
    lcd.setCursor(2, 0);
    lcd.print(sensorValue);
    lcd.setCursor(8, 0);
    lcd.write(byte(0));   
     
      if (digitalRead(10) == HIGH) {
     lcd.setCursor(8, 0);
    lcd.write(byte(1));
    Serial.println(sensorValue);
      }
     
    }
 
  if (digitalRead(10) == HIGH) {
     lcd.setCursor(2, 1);
     lcd.print(sensorValue);
         lcd.setCursor(8, 1);
    lcd.write(byte(0));
   
    if (digitalRead(10) == LOW) {
     lcd.setCursor(8, 1);
    lcd.write(byte(1));
    Serial.println(sensorValue);
      }
    }
}

```

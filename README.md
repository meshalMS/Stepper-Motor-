Bush-button
Turn on the Push button

1- Login to tinkercad

2-Work for Push-button circuit

3-Writing code to operate the Push-button circuit

//Define a pin for the LED
const byte ledpin = 4;
//Define a pin for the pushbutton
const byte pushbuttonpin = 2;
//Variable for saving LED state (LOW or HIGH)
int ledstate = LOW;
//Delay time for bouncing period
int debouncedelay = 50;
//Save the last button state
int lastbuttonstate = LOW;
//Save the current button state
int buttonstate = LOW;
//Save the last time for state change
unsigned long lastdebouncetime = 0;

void setup() 
{
 pinMode(ledpin,OUTPUT);
 pinMode(pushbuttonpin,INPUT);
}

void loop() 
{
 //ButtonWithoutDebounce();
  ButtonDebounce();
}

void ButtonDebounce()
{
  // Read the button state
  int readbutton = digitalRead(pushbuttonpin);
  //If the state has changed from the last state, start the timer
  if(lastbuttonstate != readbutton)
  {
    lastdebouncetime = millis();
  }
  //Wait for debouncedelay(50ms) to have a stable state
  if(millis() - lastdebouncetime > debouncedelay)
  {
   //Save the actual reading and when
   // the state is HIGH -> Buttonpressed change the led state
   if(buttonstate!=readbutton) 
   {
     buttonstate = readbutton;
     if(buttonstate == HIGH)
     {
       ledstate = !ledstate;
     }
   }
  }
  //Write the ledstate and save the last button read
  digitalWrite(ledpin,ledstate);
  lastbuttonstate = readbutton;
}
//This function is to show the difference without debouncing
void ButtonWithoutDebounce()
{
  int readbutton = digitalRead(pushbuttonpin);
 if(readbutton == HIGH)
 {
   ledstate = !ledstate;
 }
 digitalWrite(ledpin,ledstate);
}

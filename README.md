# Bluetooth-module
char rx,returnedInput;
 const int a1  = 5;  
 const int a2  = 6; 
 const  int b1  = 10;
 const int b2  = 9;


void PinInit()
{
  pinMode(a1, OUTPUT); //A1=motor Left Forward
  pinMode(a2, OUTPUT);//A2=motor Left Bakward
  pinMode(b1, OUTPUT);//B1=motor righttForward
  pinMode(b2, OUTPUT);//B2=motor right backward

}


void setup() 
{
    Serial.begin(9600);
    PinInit();
    while (!Serial) {
    ; // wait for serial port to connect
    } 
    
}


char ReceiveBluetooth()
{
  if (Serial.available()>0) 
      rx=Serial.read();
  return rx;    
}



void move_forward(){
digitalWrite(a1,HIGH);
digitalWrite(a2,LOW);
digitalWrite(b1,HIGH);
digitalWrite(b2,LOW); 
}


void move_backward(){
digitalWrite(a1,LOW);
digitalWrite(a2,HIGH);
digitalWrite(b1,LOW);
digitalWrite(b2,HIGH); 

  
}

void move_right(){
digitalWrite(a1,HIGH);
digitalWrite(a2,LOW);
digitalWrite(b1,LOW);
digitalWrite(b2,LOW); 
 
}

void move_left(){
digitalWrite(a1,LOW);
digitalWrite(a2,LOW);
digitalWrite(b1,HIGH);
digitalWrite(b2,LOW);   
}


void CarControls(char inp)
{
  switch(inp)
  {
    case 'f':
    move_forward();
    case 'b':
    move_backward();
    case 'r':
    move_right();
    case 'l':
    move_left();
  }
  
}


void loop() { 
  returnedInput=ReceiveBluetooth();
  CarControls(returnedInput);  
}

/* SerialController
A usb Hid Controller to Serial data output. All info to setup your own. Can be used for diferent HID controlle such as the keyboard or the mouse etc.

GitHub : https://github.com/Pant/HID-Game-Controller-to-Serial-Out.
Writen by Pantelis Sarantos with the use of "processing.serial" and "procontroll" libraries.
*/
import processing.serial.*;
import procontroll.*;

Serial myPort;

ControllIO controll;
ControllDevice serialcontroller;
ControllStick leftStick;
ControllStick rightStick;
ControllCoolieHat cooliehat;




float leftX = 0;
float leftY = 0;

float rightY = 0;
float rightX = 0;

float lXmin = 0;
float lYmin = 0;
float rXmin = 0;
float rYmin = 0;

int hatX = 0;
int hatY = 0;

float tolerance = 0.0001;  // set tolerance value for joysticks

ControllButton A;
ControllButton B;
ControllButton Y; 
ControllButton X;
ControllButton L1;
ControllButton L2;
ControllButton L3;
ControllButton R1;
ControllButton R2;
ControllButton R3;
ControllButton Select;
ControllButton Start;
ControllButton Up;
ControllButton Down;
ControllButton Left;
ControllButton Right;

void setup(){
  
  // Set the serial port to the correct virtual port & the baud rate at the same the nodejs uses.

  //println(Serial.list());// Print all serial ports available.
  //myPort = new Serial(this, Serial.list()[0], 9600);
    myPort = new Serial(this, "COM3", 19200);

  controll = ControllIO.getInstance(this);
  
   serialcontroller = controll.getDevice("USB Joystick          ");//Name of Controller. Replace with your own. (! It is case sensitive so it needs all the spaces)
  
  serialcontroller.printSliders(); // Print all available Sliders of the selected device
  serialcontroller.printButtons(); // Print all available Buttons of the selected device
  

 
    //Asign Sliders X Y - Z RZ to the Sticks
  leftStick = new ControllStick(serialcontroller.getSlider(1), serialcontroller.getSlider(0));
  rightStick = new ControllStick(serialcontroller.getSlider(3), serialcontroller.getSlider(2));
    
     //CoolieHat
  cooliehat = serialcontroller.getCoolieHat(0); // We got this value from "  gamepad.printButtons();" There is no special command to detect cooliehat.
                                       // It is detected as a button.
  cooliehat.setMultiplier(4); // So that values are -4 -2 0 2 4
  
    //Asign variable Names to Buttons of the controller
  Y = serialcontroller.getButton(1);
  B = serialcontroller.getButton(2);
  X = serialcontroller.getButton(3);
  A = serialcontroller.getButton(4);
  L1 = serialcontroller.getButton(5);
  R1 = serialcontroller.getButton(6);
  L2 = serialcontroller.getButton(7);
  R2 = serialcontroller.getButton(8);
  Select = serialcontroller.getButton(9);
  Start = serialcontroller.getButton(10);
  L3 = serialcontroller.getButton(11);
  R3 = serialcontroller.getButton(12);



}

void draw(){ //The loop. We have nothing to draw thought

  //Asign these variables to the data got from the sticks
  leftX = leftStick.getX();
  leftY = leftStick.getY();
  rightX = rightStick.getX();
  rightY = rightStick.getY();
  


  //Remap leftY rightY leftX rightX to the values we want to get. For my convinience I use these.
    //Remap leftY
  if(leftY < -tolerance) {
      leftY = map(leftY , -1, -tolerance, 0, 127);//For LY the -127 to 0 becames 0 to 127
    }  
    else if(leftY > tolerance) {
      leftY = map(leftY, tolerance, 1, 127, 255);//For LY the 0 to 127 becames 127 to 256
    }  
    else {
      leftY = 127;
    }
    
    //Remap rightY
  if(rightY < -tolerance) {
      rightY = map(rightY, -1, -tolerance, 0, 127);//For RY the -127 to 0 becames 0 to 127
    }  
    else if(rightY > tolerance) {
      rightY = map(rightY, tolerance, 1, 127, 255);//For RY the 0 to 127 becames 127 to 256
    }  
    else {
      rightY = 127;
    }
      //Remap leftX
     if(leftX < -tolerance) {
    leftX = map(leftX, -1, -tolerance, 0, 127);//For LX the -127 to 0 becames 0 to 127
  }  
  else if(leftX > tolerance) {
    leftX = map(leftX, tolerance, 1, 127, 255);//For LX the 0 to 127 becames 127 to 255
  }  
  else {
    leftX = 127;
  }
      //Remap rightX
     if(rightX < -tolerance) {
    rightX = map(rightX, -1, -tolerance, 0, 127);//For RX the -127 to 0 becames 0 to 127
  }  
  else if(rightX > tolerance) {
    rightX = map(rightX, tolerance, 1, 127, 255);//For RX the 0 to 127 becames 127 to 255
  }  
  else {
    rightX = 127;
  }
  
//Sending to Serial Port the comma seperated data 

print(int(leftY) + ",");
print(int(leftX) + ",");
print(int(rightY) + ",");
print(int(rightX) + ",");

//Sending the Sticks
myPort.write(int(leftY) + ","); //0
myPort.write(int(leftX) + ","); //1
myPort.write(int(rightY) + ","); //2
myPort.write(int(rightX) + ","); //3

//Sending the Buttons
    if(Y.pressed()){ //4
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(B.pressed()){ //5
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(X.pressed()){ //6
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }

  if(A.pressed()){ //7
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(L1.pressed()){ //8 
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(R1.pressed()){ //9
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(L2.pressed()){ //10
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(R2.pressed()){ //11
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(Select.pressed()){ //12
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(Start.pressed()){ //13
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(L3.pressed()){ //14
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  if(R3.pressed()){ //15
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
  
  //Cooliehat
  //Asign the cooliehat X Y values to these variables.
    hatX = int(cooliehat.getX());
    hatY = int(cooliehat.getY());
    
  //Sending the cooliehat 
    myPort.write(str(hatX) + ","); //16 ( Stringify the Hat Values. )
    myPort.write(str(hatY) + ","); //17 ( Stringify the Hat Values. )// Last comma in case we want to add something
                                                                     // later. For a example in a diferent port nodejs
                                                                     // reads the Arduino serial port and then combines
                                                                     // these data and sends the message to the client.
    
    print(hatX + ",");
    print(hatY + ",");

println();
myPort.write("\n"); //We need this for Nodejs Parser to recognize each packet.
}


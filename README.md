HID-Game-Controller-to-Serial-Out.
==================================

Write HID controller's data to serial with Processing and ProControll Library.


Use this SerialController to write HID game Controller's data to a Serial Port.

Can be used for communication with arduino - nodejs - or whatever you want.


#### Setup:
From println(Serial.list()); we get all the available serial ports. Replace the name and baud rate to fit with you.
```
    myPort = new Serial(this, "COM3", 19200);
```
From controll.printDevices(); we get a number of devices. Replace the following with the device you want.
#####!Important: You need to include all the characters because it is case sensitive
```
   serialcontroller = controll.getDevice("USB Joystick          ");
```


From command serialcontroller.printSliders(); we get all the available Sliders.

"ControllStick" command will create our 2 sticks made of 2 sliders each.
```
  leftStick = new ControllStick(serialcontroller.getSlider(1), serialcontroller.getSlider(0));
  rightStick = new ControllStick(serialcontroller.getSlider(3), serialcontroller.getSlider(2));
```

From command serialcontroller.printButtons(); we get all the available buttons of our controller.

Replace the number of the following with yours HAT address.
```
  cooliehat = serialcontroller.getCoolieHat(0);
```

Finally assign every button to a variable you want. Example:
```
Y = serialcontroller.getButton(1);
```


#### USAGE:
To get a button state use:
```
   Y.pressed()
```
If we want to write the data to serial port we place that as a statement.
```
    if(Y.pressed()){ //4
    myPort.write("1,");
    print("1,");
  }else{
    myPort.write("0,");
    print("0,");
  }
```
To get the hat X Y values:

#####NOTE: We need to stringify the values because some apps will not recognize the values.
#####NOTE*: The assign of hatX and hatY must be in the void draw loop in order to work right.
```
    hatX = int(cooliehat.getX());
    hatY = int(cooliehat.getY());
    

    myPort.write(str(hatX) + ",");
    myPort.write(str(hatY) + ","); 
```
In order to get each Stick's X Y Value:

#####!Important: We need to map our leftX leftY rightX rightY like in the sketch in order to work.
```
  leftX = leftStick.getX();
  leftY = leftStick.getY();
  rightX = rightStick.getX();
  rightY = rightStick.getY();
```
And if we want to write to serial
```
  myPort.write(int(leftY) + ","); //0
  myPort.write(int(leftX) + ","); //1
  myPort.write(int(rightY) + ","); //2
  myPort.write(int(rightX) + ","); //3
```
#### Note: I write a comma (",") at every myPort.write so that I can use a simple comma parser to split the data.
Finally send a "\n" so that the receiver app knows that this packet of data finished. Use this to your parser.
```
myPort.write("\n");
```
#### Thanks to
[Processing](https://www.processing.org/)

[Processing Serial]( https://processing.org/reference/libraries/serial/)

[ProControll](http://creativecomputing.cc/p5libs/procontroll/) - This application totally depends on this library.

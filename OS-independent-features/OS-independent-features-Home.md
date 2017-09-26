# (mostly) OS-Independent HID Features

**Every listed command is Operating System independent and is accessible from the payload, as well as the commandline.**

Every command takes input from stdin which enables a number of ways they can be used.  
* single line commands:  
  `echo <string> | <command>`
* multi line command:  
```
  cat << EOF | <command>
      <string that spans multiple lines>
  EOF
```

This is called a [here-doc](http://tldp.org/LDP/abs/html/here-docs.html).  

## RawOut
`outhid`  
Pipe ASCII into this command to output via HID keyboard on target.  
The output keyboard layout is derived from the "lang" option (Keyboard config).  
Note: A newline character (ASCII 0x0A) is interpreted as RETURN key.  
outhid only works if USE_HID=true.  

## DuckyScript
`duckhid`  
Pipe [DuckyScript](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Duckyscript) into this command to output via HID keyboard on target.  
The output keyboard layout is derived from the "lang" option (Keyboard config).  
duckhid only works if USE_HID=true.  

## MouseScript

**Selfmade DuckyScript-Style language**

#### MOVE
`MOVE [x] [y]`  
accept relative movement values between -127 and 127.  
the values represent how many mouseunits the pointer should been moved.  
how many pixels the pointer moves on screen depends on system settings (DPI, mouse acceleration, screen resolution)  
This method introduces an error, caused by "mouse acceleration", which could be shown with the following MouseScript.  
command sequence:  
```
MOVE 0 -100    # Move the pointer 100 units down on y axis  
MOVE 100 0     # Move the pointer 100 units on positive x axis  
MOVE -100 100  # Move the pointer 100 units on negative x axis and 100 units down on y axis  
```
Although this should en up in the starting point, the final mouse coordinate has an offset, due to acceleration on diagonal movement (longer way in same time).  
the advantage of using MOVE is that it is fast (in its limited range) and works out quite well for horizontal/vertical moves.  

#### MOVESTEPPED
`MOVESTEPPED [x] [y]`  
does the same as MOVE but isn't limited to the 127 limit.  
advantage: returning to the origin with high precision is possible.  
disadvantage: much slower, as many status updates are needed to move to the final coordinate.  

#### MOVETO
`MOVETO [x] [y]`  
utilizes absolute instead of relative coordinates.  
MOVETO uses float values between 0.0 and 1.0 on both, the x and the y axis.  
positioning could be done accurately, precision is at 15 bit (float is internally represented by values between 0x0000 and 0x7FFF), which should be enough for todays screen resolutions.  
as coordinates are given in float with equal distribution on both axes, one has to manually account for current aspect radio and screen resolution (coordinate translation) to hit a screen pixel precisely.  
the test doesn't account on aspect radio and tries to draw the picture a third time.  
advantage: accurate , pixel perfect mouse positioning (if coordinates are calculated correctly).  
disadvantage: Absolute positioning doe work on Windows 10, but doesn't work on Android (a digitizer has to be emulated for this). It isn't tested against \*nix OS'es, but X11 is known to have problems with absolute mice.  
on most OS'es except Windows, this test shouldn't produce a mouse movement. If it does, absolute
positioning is supported.  

#### CLICK
`CLICK [btn1] [btn2] [btn3]`  
clicks the respective button one time ("1" for click, "0" for don't click)  
Example for left click:  
  `CLICK 1 0 0`  
Example for right click:  
  `CLICK 0 1 0`  

#### DOUBLECLICK
`DOUBLECLICK [btn1] [btn2] [btn3]`  
like CLICK, but double clicks

#### BUTTONS
`BUTTONS [btn1] [btn2] [btn3]`  
this command is used, if a button state should be kept during movement (drag while button down)  
Example for relative movement with button pressed:  
```
     BUTTONS 0 0 0        # release all buttons  
     MOVETO 0.5 0.5       # move to screen center (if absolute movement supported)  
     BUTTONS 1 0 0        # press down left button  
     MOVESTEPPED 100 0    # move 100 steps right while button pressed  
     MOVESTEPPED 0 -100   # move 100 steps up while button still pressed  
     BUTTONS 0 0 0        # release all buttons  
```

#### DELAY
`DELAY [milliseconds]`  
pauses the execution for the specified amount of milliseconds.  

#### UPDATE
`UPDATE`  
pushes the changes to the mouse instantly but is not needed since every function calls it anyways.  

# Grbl for CPCBM with an Arduino Uno
This is a preconfigured version of grbl for the The Ant compact pcb maker with an Arduino uno

## Getting Started
### Hardware
The connections are a bit funky. The motors are like in the tutorial and I have 32/1 microstepping. The connections are as follows (I would suggest testing the endstops after flashing the software with ugs):
![_](https://raw.githubusercontent.com/MrMugame/grbl/master/doc/Pinout.png)

### Software
To get the modified grbl version flashed on your Arduino Uno, you can simply use the [instructions](https://github.com/gnea/grbl/wiki/Compiling-Grbl) given by grbl. After grbl has flashed you have to set a few settings:
```
$0 = 10    (step pulse, usec)
$1 = 25    (step idle delay, msec)
$2 = 0    (step port invert mask:00000000)
$3 = 0    (dir port invert mask:00000000)
$4 = 0    (step enable invert, bool)
$5 = 1    (limit pins invert, bool)
$6 = 0    (probe pin invert, bool)
$10 = 19    (status report mask:00010011)
$11 = 0.010    (junction deviation, mm)
$12 = 0.002    (arc tolerance, mm)
$13 = 0    (report inches, bool)
$20 = 1    (soft limits, bool)
$21 = 0    (hard limits, bool)
$22 = 1    (homing cycle, bool)
$23 = 3    (homing dir invert mask:00000011)
$24 = 25.000    (homing feed, mm/min)
$25 = 500.000    (homing seek, mm/min)
$26 = 250    (homing debounce, msec)
$27 = 1.000    (homing pull-off, mm)
$29 = 1860    (Spindle pwm Max time-on, us)
$30 = 1060    (Spindle pwm min time-on, us)
$31 = 1    (Spindle pwm Enabled at startup)
$100 = 100.000    (x, step/mm)
$101 = 100.000    (y, step/mm)
$102 = 800.000    (z, step/mm)
$110 = 500.000    (x max rate, mm/min)
$111 = 500.000    (y max rate, mm/min)
$112 = 500.000    (z max rate, mm/min)
$120 = 10.000    (x accel, mm/sec^2)
$121 = 10.000    (y accel, mm/sec^2)
$122 = 10.000    (z accel, mm/sec^2)
$130 = 72.000    (x max travel, mm)
$131 = 118.000    (y max travel, mm)
$132 = 6.000    (z max travel, mm)
```
## Important notes
* To stop the esc from beeping you have to send ```M3``` and then ```S0```.
* Be carful then homing for the first time it can happen that your homing switches aren't set correctly. **I AM GIVING ABSOLUTELY NO WARRANTY**
* English is not my native language and I apologize for any mistakes.

## What I have changed
In the config.h I have set it to use CoreXY so the axis work properly, I have inverted the Z switch(because mine is not an NC), and changed the homing cycle. I have also set the spindle max rpm to 10000 and min to 0 (these are arbitrary numbers because i dont know how fast the spindle goes)\
In the spindle_control.h I have changed many single lines so it makes a signal for an ESC (If you want to know more about pwm signals for ESC look at this [link](https://howtomechatronics.com/tutorials/arduino/arduino-brushless-motor-control-tutorial-esc-bldc/))


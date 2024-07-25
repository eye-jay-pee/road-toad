# road-toad
lightweight media center and obd2 reading program for linux.



###  supply needs
- Raspberry pi 4        3A
- PCM5122               fraction of an amp. we'll provide 1A
- B0CRR8GZCH (display)  1A

## conclusion
the current 6A setup is overkill, but not by so much it matters. Change nothing.


## plug: (Japan Solderless Conector) JSC XH 5-pin


```
DEPRECIATED!! do NOT use.     / / / / / / / /
DEPRECIATED!! do NOT use.    / / / / / / / / 
DEPRECIATED!! do NOT use.   _|_|_|_|_|_|_|_|__  
DEPRECIATED!! do NOT use.  / | | | | | | | | /|
DEPRECIATED!! do NOT use. /_/_/_/_/_/_/_/_/_/ |   7-prong JSC xh plug to 
DEPRECIATED!! do NOT use. | ---         --- | /         car wiring harness
DEPRECIATED!! do NOT use. |_| |_________| |_|/  
DEPRECIATED!! do NOT use.   ________________   
DEPRECIATED!! do NOT use.  //_/_/_/_/_/_/_//|  
DEPRECIATED!! do NOT use.  |_^___________^_|/  
DEPRECIATED!! do NOT use.     \ \ \ \ \ \ \     
DEPRECIATED!! do NOT use.      \ \ \ \ \ \ \     
DEPRECIATED!! do NOT use.       \ \ \ \ \ \ \
DEPRECIATED!! do NOT use.        \ \ \ \ \ \ \_ reserved for anntenna control
DEPRECIATED!! do NOT use.         \ \ \ \ \ \_ 0-12v dimmer  (analog input)
DEPRECIATED!! do NOT use.          \ \ \ \ \_ 0/12v digital signal from ign. 
DEPRECIATED!! do NOT use.           \ \ \ \_ GND
DEPRECIATED!! do NOT use.            \ \ \_ GND 
DEPRECIATED!! do NOT use.             \ \_ 5v always on
DEPRECIATED!! do NOT use.              \_ 5v always on
DEPRECIATED!! do NOT use.
DEPRECIATED!! do NOT use. 
```

#### verion 0.0.0 functionality:
 - [X] not a fire hazard
 - [X] doesnt destroy hardware
 - [X] raspberry pi and screen can draw 5v power from the car battery
 - [X] enough power is avalible that
 - [X] plug choice that will not need to be changed significantly later
 - [ ] plays music 

### current ratings for plug:
 - JSC XH rated for 3 amps per pin. VCC and GND have 2 pins each.
 - radio cicuit in car has 10 amp fuse -- should probably replace with 5-amp.  

### left to do as of Sat Jun 22 21:39:11 CDT 2024
 - [ ] find benchtop power supply cord
 - [ ] 5 volts from 12 v power 
 - [ ] read I2C writeup to see how to do multiple slaves

##### I2C notes:
 - 2 pins: sck sda
 - any GPIO 5v or 3.3v allowed
 - no minimum baud rate
    - 10kb/s, 200 kb/s, 400kb/s, 1Mb/s, 3.4Mb/s speeds
 - 7-bit addressing
 - 4 states: START,STOP,HIGH,LOW
 

#### Sun Jun 23 20:22:20 CDT 2024

 - [x] DAC setup and it seems to use I2C address `0x4D`. 
 - [ ] get high on own supply
 - [ ] find verify i2c addr of voltmeter


### problem: pi shuts itself off when power supply is connected.

maybe a short? isolate all 5v and gnd connections.

### Voltage regulators cannot be used in parelell. 
Had to order an external regulator to power all relevent 5V hardware. 

- bought a buck converter. It drains the battery a little when at idle. need to
  see if this is enogh to worry about.  

- buck converter is to be switched on a transistor amplifiying ignition
  signal. igntion signal should draw minimum current. 


# Fri Jul 19 22:06:28 CDT 2024


### verion 0.0.1 functionality:
 [ ] can shut it'self offf


#### todo:
 [ ] select powerdown gpio pin
 [ ] verify selected pin is high by default
 [ ] 12 volt NOT & OR gate circuits
 [ ] inverted and amplify input from appropriate gpio pin
 [ ] write a powerdown executable


# Mon Jul 22 23:43:19 CDT 2024
 single plug to connect to the truck should be used. Integrating it into the
 wiring harness is retarded.

## new plug designs
```
                      / / / / / / / / 
                     / / / / / / / / 
                    _|_|_|_|_|_|_|_|__  
                   / | | | | | | | | /|
                  /_/_/_/_/_/_/_/_/_/ |   7-prong JSC xh plug to 
                  | ---         --- | /         car wiring harness
                  |_| |_________| |_|/  
                    ________________   
                   //_/_/_/_/_/_/_//|  
                   |_^___________^_|/  
                      \ \ \ \ \ \ \     
                       \ \ \ \ \ \ \_ reserved for anntenna control
                        \ \ \ \ \ \_ 0-14v dimmer (analog input)
                         \ \ \ \ \_ 0/14v digital signal from ign. 
                          \ \ \ \_ 14v always on
                           \ \ \_ 14v always on 
                            \ \_ GND
                             \_ GND
```
```
     / / / / / / / 
    / / / / / / / 
   _|_|_|_|_|_|_|__  
  / | | | | | | | /|
 /_/_/_/_/_/_/_/_/ |   6-prong JSC xh plug to 
 | ---       --- | /         power supply
 |_| |_______| |_|/  
   ______________   
  //_/_/_/_/_/_//|  
  |_^_________^_|/  
     \ \ \ \ \ \     
      \ \ \ \ \ \_ 14v always on
       \ \ \ \ \_ 14v always on
        \ \ \ \_  NFET source
         \ \ \_ NFET source
          \ \_ 5v in  
           \_ 5v in
```






## raspberry pi pintout: 
 DAC is a clone of this: <https://pinout.xyz/pinout/dac_hat>


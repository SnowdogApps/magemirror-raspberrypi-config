# magemirror-raspberrypi-config

This document describes how to configure touch frame on Raspbian (RaspberryPI) to work in portrait mode.

## Rotate display and turn of overscan

`sudo nano /boot/config.txt`

uncomment:

`disable_overscan=1`

add to the end of file:

`display_rotate=1`

## Rotate touch frame input

install xinput:

`sudo apt-get install xinput`

find your frame device:

`xinput --list`

swap and invert axes (for portrait mode):

`xinput set-prop 6 'Evdev Axes Swap' 1`  
`xinput set-prop 7 'Evdev Axes Swap' 1`  
`xinput set-prop 6 'Evdev Axis Inversion' 1 0`  
`xinput set-prop 7 'Evdev Axis Inversion' 1 0`  

If touch frame works upside-down then switch `1 0` to `0 1`

## Rotate touch frame input on system boot

Create the script:

`sudo nano /etc/xdg/lxsession/LXDE-pi/screenflip.sh`

Write down commands into script:

`xinput set-prop 6 'Evdev Axes Swap' 1`  
`xinput set-prop 7 'Evdev Axes Swap' 1`  
`xinput set-prop 6 'Evdev Axis Inversion' 1 0`  
`xinput set-prop 7 'Evdev Axis Inversion' 1 0`  

Setup access:

`sudo chmod 755 /etc/xdg/lxsession/LXDE-pi/screenflip.sh`

Add line:

`@/etc/xdg/lxsession/LXDE-pi/screenflip.sh`

in files:

`sudo nano /etc/xdg/lxsession/LXDE-pi/autostart`  
`sudo nano /home/pi/.config/lxsession/LXDE-pi/autostart`  

# Volumio plugin for Raspberry Pi touch display

This is a rewrite of Volumio's original touch display plugin. The plugin provides the following configuration options:

## Screensaver
The options allow setting the timeout in seconds until the screensaver (DPMS state "off") gets invoked. A value of 0 disables the screensaver.
Further more it is possible to block the screensaver as long as Volumio is in playing state.

## Screen brightness
For the Raspberry Foundation 7" touch screen the screen brightness can be set.
If current screen brightness should be above 14 and then set to a value below 15 a modal shows up to warn for a very dark screen. The modal offers to test the new (low) value by applying it for 5 seconds before the previous brightness gets restored. After that the user can decide if the new or the previous setting should be kept.

The plugin is also prepared for automatic brightness regulation. The option to use automatic brightness regulation will only show up on the plugin's configuration page if a file named /etc/als exists.

Obviously automatic brightness requires additional hardware in the shape of an ambient light sensor. This is typically an LDR with a voltage divider connected to an ADC like the TI ADS1115. For example if the LDR would be connected to input AIN0 of an ADS1115 measuring single-ended signals in continuous conversion mode the current converted LDR value would appear in /sys/devices/platform/soc/\*04000.i2c/i2c-1/1-0048/in4_input. This file would need to be symlinked to /etc/als as the plugin awaits the current value of an ambient light sensor in /etc/als.

When automatic brightness gets enabled for the first time the light sensor obligatorily has to be "calibrated" according to minimum and maximum screen brightness. The calibration process consists of measuring the ambient light in a first setting (e.g. darkness or twilight) where the lowest screen brightness should be reached and a second setting (e.g. "normal" daylight or bright sunshine) where the highest screen brightness should be reached. Through a dedicated button the calibration process can be repeated anytime if needed. The range of possible screen brightness values can be adjusted through the minimum and maximum screen brightness settings.

Further more when using automatic brightness it is possible to define a third "reference" point to form a brightness curve between minimum and maximum screen brightness reaching a "reference" screen brightness at a certain ambient brightness. This can be useful if the progression of screen brightness in accordance to ambience brightness needs to be slowed down or accelerated.

## Display orientation
For the Raspberry Foundation 7" touch screen the display can be rotated by 180°.
When this setting is changed a modal shows up to inform about a reboot is required. The user has the option to initiate the reboot or proceed (and reboot later).

## Show/hide mouse pointer
Self explanatory. By default the mouse pointer is hidden.


# Installation advice
If the previous/original version of the plugin has or had been installed it is necessary to remove /data/volumiokiok.

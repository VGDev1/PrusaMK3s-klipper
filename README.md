# PrusaMK3s-klipper

These configs are for my own printer and they are still under development. See my Voron configs for more advanced example: https://github.com/VGDev1/Voron-V2.4928

### Pre-Check

- Get Z offset value from your current firmware (Menu -> Calibration -> Z-offset), you will need it for the Klipper config.
- Your bed needs to be perpendicular (based on XYZ Calibration). If not you will have to do the skew calibration before printing or you risk crashing your nozzle to the bed.

### Hardware
- Rock 4 SE running Armbian
- Logitech webcam via USB

### Software
- I have copied most of my config from here: https://github.com/dz0ny/klipper-prusa-mk3s
- I have written my own PRINT_START and PRINT_END macros
- I have incorporated this https://gist.github.com/ChipCE/95fdbd3c2f3a064397f9610f915f7d02 Adaptive Bed Mesh
- I have an Adaptive Purge Macro which I currently do not use
- I am running Input Shaper, I have tuned it using my own ADXL/Pi pico sensor
- I am using Crownsnest for my camera, update your device to match your own ex: `device: /dev/video5`
- Do not use stealth mode if you want fast accelerations and speeds
- Tune PID

### Tips
- Tune belts using Prusa https://belt.connect.prusa3d.com/
- Grease bearings with Mobilux EP2

### Slicer
I am using Prusaslicer, put this in Custom G-code if you want my macros to work:

#### Start gcode
- `M104 S0 ; Stops PS/SS from sending temp waits separately`
- `M140 S0`
- `PRINT_START BED=[first_layer_bed_temperature] HOTEND=[first_layer_temperature] MATERIAL=[filament_type] AREA_START={first_layer_print_min[0]},{first_layer_print_min[1]} AREA_END={first_layer_print_max[0]},{first_layer_print_max[1]}`

#### End gcode
- `PRINT_END`

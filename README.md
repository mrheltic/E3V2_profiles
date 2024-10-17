# Creality Ender 3 V2 with BL-Touch and latest Marlin UBL firmware installed and Cura Slicer

This repository contains the custom start and end G-Code for the Creality Ender 3 V2 with BL-Touch and latest Marlin UBL firmware installed and Cura Slicer.

## Custom Start G-Code

```gcode

; --- Start of custom START G-Code for Creality Ender 3 V2 with BL-Touch and latest https://github.com/Jyers/Marlin/releases UBL firmware installed and Cura Slicer ---

; --- (Optional) Start G-Code for Octoprint Octolapse Plugin ---

; Script based on an original created by tjjfvi (https://github.com/tjjfvi)
; An up-to-date version of the tjjfvi's original script can be found
; here:  https://csi.t6.fyi/
; Note - This script will only work in Cura V4.2 and above!
; layer_height = {layer_height}
; smooth_spiralized_contours = {smooth_spiralized_contours}
; magic_mesh_surface_mode = {magic_mesh_surface_mode}
; machine_extruder_count = {machine_extruder_count}
; Single Extruder Settings:
; speed_z_hop = {speed_z_hop}
; retraction_amount = {retraction_amount}
; retraction_hop = {retraction_hop}
; retraction_hop_enabled = {retraction_hop_enabled}
; retraction_enable = {retraction_enable}
; retraction_speed = {retraction_speed}
; retraction_retract_speed = {retraction_retract_speed}
; retraction_prime_speed = {retraction_prime_speed}
; speed_travel = {speed_travel}

; --- (Optional) End G-Code for Octoprint Octolapse Plugin ---

G92 E0 ; Reset Extruder

M140 S{material_bed_temperature_layer_0} ; Set Heat Bed temperature
G28 ; Home Axis
M190 S{material_bed_temperature_layer_0} ; Wait for Heat Bed temperature

M104 S165; start warming extruder with temporarily temperature of 165 degrees

G29 A ; Enable UBL -  BL-Touch mesh alignment
G29 L0 ; Load saved UBL mesh from slot 0
G29 J ; Level the bed / mesh on 3 points for quick alignment

M104 S{material_print_temperature_layer_0} ; Set final extruder temperature

G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position

M109 S{material_print_temperature_layer_0} ; Wait for Extruder temperature

G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
M400 ; Wait for current moves to finish
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
M400 ; Wait for current moves to finish
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
M400 ; Wait for current moves to finish

G92 E0 ; Reset Extruder

G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
M400 ; Wait for current moves to finish

; --- End of custom START G-Code for Creality Ender 3 V2 with BL-Touch and latest https://github.com/Jyers/Marlin/releases UBL firmware installed and Cura Slicer ---

```

## Custom End G-Code

```gcode
; --- Start of custom END G-Code for Creality Ender 3 V2 with BL-Touch and latest https://github.com/Jyers/Marlin/releases UBL firmware installed and Cura Slicer ---

M400 ; Wait for current moves to finish

M220 S100 ; Reset Speed factor override percentage to default (100%)
M221 S100 ; Reset Extrude factor override percentage to default (100%)

G91 ; Set coordinates to relative
G1 F2400 E-5 ; Retract filament 5mm at 40mm/s to prevent stringing
G0 F5000 Z20 ; Move Z Axis up 20mm to allow filament ooze freely
G90 ; Set coordinates to absolute

G0 Y220; Move bed to the front for easy print removal

M84 ; Disable stepper motors

M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed

; --- END of custom END G-Code for Creality Ender 3 V2 with BL-Touch and latest https://github.com/Jyers/Marlin/releases UBL firmware installed and Cura Slicer ---
```
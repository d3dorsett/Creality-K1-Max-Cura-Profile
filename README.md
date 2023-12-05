# Creality-K1-Max-Cura-Profile
My profiles for the Creality K1 Max using Ultimaker Cura 5.6.0
  - Fine 0.12mm @ 300mm/s 12k acceleration
  - Normal 0.2mm @ 600mm/s 12k acceleration
  - Fast 0.25 @ 600mm/s 20k acceleration (Benchy Speed Test)
  - Personal 0.2 @ 600mm/s with combination of all 3 profiles to suite my personal preference


My personal printer is a Creality K1 Max with a 0.6 nozzle, rooted and running fluidd (using Guilouz Installion Helper Script).
https://github.com/Guilouz/Creality-K1-and-K1-Max


Gcode Viewer is also an excellent add-on for fluidd. Use it to stop sections that have failed.
https://docs.fluidd.xyz/features/gcode-viewer


**NOTE:** A bug in Cura 5.3 has been fixed in 5.6.0 making the use of KAMP and Gcode Viewe_ useable if you add the follow macros to gcode_macro.cfg file:

[gcode_macro DEFINE_OBJECT]
gcode:
  EXCLUDE_OBJECT_DEFINE {rawparams}

[gcode_macro START_CURRENT_OBJECT]
gcode:
  EXCLUDE_OBJECT_START NAME={params.NAME}

[gcode_macro END_CURRENT_OBJECT]
gcode:
  EXCLUDE_OBJECT_END {% if params.NAME %}NAME={params.NAME}{% endif %}

[gcode_macro LIST_OBJECTS]
gcode:
  EXCLUDE_OBJECT_DEFINE

[gcode_macro LIST_EXCLUDED_OBJECTS]
gcode:
  EXCLUDE_OBJECT

[gcode_macro REMOVE_ALL_EXCLUDED]
gcode:
  EXCLUDE_OBJECT RESET=1

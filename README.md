# Creality-K1-Max-Cura-Profile
My Creality K1 Max Cura Profile 0.6 Nozzle for Ultimaker Cura 5.6.0
These are my personal settings for the Creality K1 Max with a 0.6 nozzle, rooted and running fluidd. 


Many of the features from Guilouz installer are used in my configuration files for fluidd, they are not needed for the Cura profile
https://github.com/Guilouz/Creality-K1-and-K1-Max

Gcode Viewer is also an excellent add-on for fluidd. Use it to stop sections that have failed.
https://docs.fluidd.xyz/features/gcode-viewer

**NOTE:** A bug in Cura 5.3 has been fixed in 5.6.0 making the use of _KAMP_ and _Gcode Viewer_ useable if you add the follow macros to gcode_macro.cfg file:

## exclude object macros
[gcode_macro DEFINE_OBJECT]
gcode: EXCLUDE_OBJECT_DEFINE {rawparams}

[gcode_macro START_CURRENT_OBJECT]
gcode: EXCLUDE_OBJECT_START NAME={params.NAME}

[gcode_macro END_CURRENT_OBJECT]
gcode: EXCLUDE_OBJECT_END {% if params.NAME %}NAME={params.NAME}{% endif %}

[gcode_macro LIST_OBJECTS]
gcode: EXCLUDE_OBJECT_DEFINE

[gcode_macro LIST_EXCLUDED_OBJECTS]
gcode: EXCLUDE_OBJECT

[gcode_macro REMOVE_ALL_EXCLUDED]
gcode: EXCLUDE_OBJECT RESET=1

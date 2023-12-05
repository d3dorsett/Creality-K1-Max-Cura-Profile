# Creality-K1-Max-Cura-Profile
My Creality K1 Max Cura Profile 0.6 Nozzle for Ultimaker Cura 5.6.0
These are my personal settings for the Creality K1 Max with a 0.6 nozzle, rooted and running fluidd. 


Many of the features from Guilouz installer are used in my configuration files for fluidd, they are not needed for the Cura profile
https://github.com/Guilouz/Creality-K1-and-K1-Max

Gcode Viewer is also an excellent add-on for fluidd. Use it to stop sections that have failed.
https://docs.fluidd.xyz/features/gcode-viewer

**NOTE:** To use _KAMP_ or _Gcode Viewer_, Cura 5.6.0 has a bug. The follow steps need to be added as a post process.

Cura -> Menu -> Extensions -> Post Processing -> Modify GCode
Then Add a Script -> Search and Replace
Search is NOMESH
Replace is NONMESH

Also add this to macros...
https://www.teamfdm.com/forums/topic/503-region-exclude-for-mainsailklipper/?do=findComment&comment=2461
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

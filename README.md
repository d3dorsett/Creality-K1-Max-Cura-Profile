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


**NOTE:** A bug in Cura 5.3 has been fixed in 5.6.0 making the use of KAMP and Gcode Viewer useable if you add the follow macros to gcode_macro.cfg file:

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

**FAN CONTROL:**
The K1 has a side fan and a rear fan. Cura can only control one and by default it is the rear fan. In order, to switch this open the printer.cfg and switch the pin for Fan1 with Fan2

[output_pin fan1]
#Switch for Fan2
_#pin: PC0_
pin: **PB1**
pwm: True
cycle_time: 0.0100
hardware_pwm: false
value: 0.00
scale: 255
shutdown_value: 0.0

[output_pin fan2]
#Switch for Fan1
_#pin: PB1_
pin: **PC0**
pwm: True
cycle_time: 0.0100
hardware_pwm: false
value: 0.00
scale: 255
shutdown_value: 0.0

**504 Gateway Timeout error on large prints:**
504 Gateway Timeout error using Nginx as Proxy

For Nginx as Proxy for Apache web server, this is what you have to try to fix the 504 Gateway Timeout error:

Add these variables to  /usr/data/nginx/nginx/**nginx.conf** file:

  proxy_connect_timeout       600;
  proxy_send_timeout          600;
  proxy_read_timeout          600;
  send_timeout                600;
Then restart nginx:

service nginx reload

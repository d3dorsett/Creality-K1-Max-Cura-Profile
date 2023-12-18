# Creality-K1-Max-Cura-Profile
My profiles for the Creality K1 Max using Ultimaker Cura 5.6.0
  - Fine 0.12mm @ 300mm/s 12k acceleration
  - Normal 0.2mm @ 600mm/s 12k acceleration
  - Fast 0.25 @ 600mm/s 20k acceleration (Benchy Speed Test)
  - Personal 0.2 @ 600mm/s with combination of all 3 profiles to suite my personal preference


My personal printer is a Creality K1 Max with a 0.6 nozzle, rooted and running fluidd (using Guilouz Installion Helper Script).
https://github.com/Guilouz/Creality-K1-and-K1-Max


**Gcode Viewer** is also an excellent add-on for fluidd. Use it to stop sections that have failed.
https://docs.fluidd.xyz/features/gcode-viewer


**NOTE:** A bug in Cura 5.3 has been fixed in 5.6.0 making the use of KAMP and Gcode Viewer useable if you add the follow macros to gcode_macro.cfg file:
```ruby
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
```
**Fan Control:**
The K1 has a side fan and a rear fan. Cura can only control one and by default it is the rear fan. In order, to switch this open the printer.cfg and switch the pin for Fan1 with Fan2

```ruby
[output_pin fan1]
#Switch for Fan2
#pin: PC0
pin: **PB1**
pwm: True
cycle_time: 0.0100
hardware_pwm: false
value: 0.00
scale: 255
shutdown_value: 0.0

[output_pin fan2]
#Switch for Fan1
#pin: PB1
pin: **PC0**
pwm: True
cycle_time: 0.0100
hardware_pwm: false
value: 0.00
scale: 255
shutdown_value: 0.0
```

**504 Gateway Timeout Eeror in Slicer on Large prints:**

The 504 Gateway Timeout Error is an issue using Nginx as Proxy.

To fix this, ssh into the OS.

Navigate to /usr/data/nginx/nginx

Edit **nginx.conf** file:

Find the following section...
```rubt
http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  0;
```

Change and add the following...
```ruby
  #keepalive_timeout  0;
  keepalive_timeout           65;
  proxy_connect_timeout       1600;
  proxy_send_timeout          1600;
  proxy_read_timeout          1600;
  send_timeout                1600;
```

Then restart nginx:
```ruby
service nginx reload
```

**Optional Camera Settings**

Improve the visual quality of the built-in camera by adding the following to the end of the **camera-settings.cfg** file...

```ruby
[delayed_gcode LOAD_CAM_SETTINGS]
initial_duration: 2
gcode:
  CAM_BRIGHTNESS BRIGHTNESS=8
  CAM_CONTRAST CONTRAST=48
  CAM_SATURATION SATURATION=56
  CAM_SHARPNESS SHARPNESS=6
  CAM_HUE HUE=10
  CAM_WHITE_BALANCE_TEMPERATURE_AUTO WHITE_BALANCE_TEMPERATURE_AUTO=1
  #CAM_WHITE_BALANCE_TEMPERATURE WHITE_BALANCE_TEMPERATURE=4600
  CAM_GAMMA GAMMA=80
  CAM_GAIN GAIN=0
  CAM_POWER_LINE_FREQUENCY POWER_LINE_FREQUENCY=1
  CAM_BACKLIGHT_COMPENSATION BACKLIGHT_COMPENSATION=1
  CAM_EXPOSURE_AUTO EXPOSURE_AUTO=3
  #CAM_EXPOSURE_ABSOLUTE EXPOSURE_ABSOLUTE=156
  CAM_EXPOSURE_AUTO_PRIORITY EXPOSURE_AUTO_PRIORITY=0
```



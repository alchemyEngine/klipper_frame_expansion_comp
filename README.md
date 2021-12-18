# Frame Expansion Compensation
A Moonraker plug-in for real-time compensation of frame thermal expansion.

## Installation
**Credit to protoloft**, from whom I plagarized in near entirety the `install.sh`
script -> [Z Auto Calibration](https://github.com/protoloft/klipper_z_calibration)

-----------
Clone this repo into you home directory. For example:
```bash
cd /home/pi
git clone https://github.com/alchemyEngine/klipper_frame_expansion_comp
```
Copy the `frame_expansion_compensation.py` module to the Klippy extras folder:
```bash
cp /home/pi/klipper_frame_expansion_comp/frame_expansion_compensation.py /home/pi/klipper/klippy/extras/
```
## [Optional] Configure Moonraker Updates
Run the install shell script:
```bash
bash /home/pi/klipper_frame_expansion_comp/install.sh
```
Configure the update manager. Add the following section to `moonraker.conf`:
```config
[update_manager client frame_expansion]
type: git_repo
path: /home/pi/klipper_frame_expansion_comp
origin: https://github.com/alchemyEngine/klipper_frame_expansion_comp.git
install_script: install.sh
```

## Configuration
```py
[frame_expansion_compensation]
#temp_coeff:
#   The temperature coefficient of expansion, in mm/K. For example, a
#   temp_coeff of 0.01 mm/K will move the Z axis downwards by 0.01 mm for every
#   Kelvin/degree celcius that the frame temperature increases. Defaults to 0.0,
#   no offset.
#temp_sensor:
#   Temperature sensor to use for frame temp measurement. Use full config
#   section name without quoutes. E.g. temperature_sensor frame
#smooth_time:
#   Smoothing window applied to the temp_sensor, in seconds. Can reduce motor
#   noise from excessive small corrections in response to sensor noise. The
#   default is 2.0 seconds.
#max_comp_z:
#   Disables compensation above this Z height [mm]. The last computed correction
#   will remain applied until the toolhead moves below the specified Z position
#   again. The default is 0.0mm (always on).
#max_z_offset:
#   Maximum absolute compensation that can be applied to the Z axis [mm]. The
#   default is 99999999.0mm (unlimited).
z_stepper:
#   The Z stepper motor linked with the Z endstop, as written in printer.cfg.
#   Used for triggering reference temperature measurement. Usually 'stepper_z'
#   unless otherwise defined.
```

## G-Code Commands
The following commands are available when the frame_expansion_compensation config section is enabled:

- SET_FRAME_COMP ENABLE=[<0:1>]: enable or disable frame expansion compensation. When disabled, the last computed compensation value will remain applied until next homing.
- QUERY_FRAME_COMP: report current state and key parameters of the frame expansion compensation.


## Overview
TODO
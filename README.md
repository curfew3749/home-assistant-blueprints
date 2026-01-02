Motion Lighting by House Mode

A Home Assistant automation blueprint for motion-activated lighting that adapts behavior based on a global house mode such as Day, Evening, and Night.

This blueprint is designed to be reusable across multiple rooms while keeping behavior predictable and easy to control from the UI.

What This Blueprint Does

When motion is detected:
Turns lights on automatically
Sets brightness based on house mode
Day → 100%
Evening → configurable (default 20%)
Night → configurable (default 10%)

When no motion is detected:
Turns lights off after a configurable delay

Additional features:
Global enable/disable for motion lighting
Ability to disable motion lighting for specific house modes
Automatic re-enable of motion lighting after a period of no motion

Required Helpers

This blueprint assumes the following helpers exist in Home Assistant.

House Mode (input_select)

An input select that represents the current house mode.

Example options:
Day
Evening
Night

The option names must match exactly.

Motion Lighting Enabled (input_boolean)

A toggle used to temporarily disable motion-activated lighting.

When turned off:
Motion will not turn lights on
The blueprint can automatically turn motion lighting back on after no motion

Blueprint Inputs

Motion Sensor
Binary motion sensor for the room

Lights
One or more lights to control

House Mode Selector
Global house mode input_select

Motion Lighting Enabled Toggle
Enable or disable motion lighting entirely

Disable Motion In These Modes
House modes where motion should not turn lights on

Evening Brightness
Brightness percentage used in Evening mode

Night Brightness
Brightness percentage used in Night mode

Minutes to Turn Lights Off
Time after no motion before lights turn off

Minutes to Auto Re-Enable Motion
Time of no motion before motion lighting is automatically re-enabled

Example Configurations

Bedroom
Disable Motion In These Modes: Night
Evening Brightness: 20%
Motion Lighting Enabled: ON

Result:
Lights turn on during Day and Evening, but never automatically at night.

Hallway or Bathroom
Disable Motion In These Modes: none
Night Brightness: 10%

Result:
Dim lighting at night for safe navigation.

Installation

Import the blueprint into Home Assistant using its raw GitHub URL
Create an automation from the blueprint
Configure the inputs for the room
Save

Repeat for each room where motion lighting is desired.

Design Notes

Uses house mode instead of time-based logic
All behavior is configurable through the UI
One blueprint can be reused across the entire home
Manual light control is never blocked

Known Limitations

No lux or light-level sensing
No fade transitions by default
Assumes house mode is managed elsewhere

License

MIT License

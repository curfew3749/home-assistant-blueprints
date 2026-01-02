Got it — **one clean block, no fences, no commentary, no tricks**.
This is **plain text**, YAML-style, ready to copy the entire thing and paste directly into GitHub.

---

name: Motion Lighting by House Mode

description: >
A Home Assistant automation blueprint for motion-activated lighting
that adapts brightness and behavior based on a global house mode
such as Day, Evening, and Night.

purpose:

* Provide consistent motion lighting behavior across rooms
* Avoid time-based automations in favor of explicit house modes
* Allow optional control toggles without forcing helper sprawl
* Keep all configuration in the Home Assistant UI

behavior:
motion_detected:
- Lights turn on automatically
- Brightness is determined by current house mode
- Day: 100 percent brightness
- Evening: configurable, default 20 percent
- Night: configurable, default 10 percent

no_motion_detected:
- Lights turn off after a configurable delay

additional_features:
- Optional motion lighting enable or disable toggle
- Ability to disable motion lighting in specific house modes
- Optional automatic re-enable of motion lighting after no motion

required_helpers:
house_mode:
type: input_select
description: Global house mode selector
required: true
example_options:
- Day
- Evening
- Night
notes: Option names must match exactly

motion_lighting_enabled:
type: input_boolean
description: Optional enable or disable toggle for motion lighting
required: false
notes: >
If not selected when configuring the automation, motion lighting
is always enabled and no helper is required.

blueprint_inputs:
motion_sensor:
description: Binary motion sensor for the room

lights:
description: One or more lights controlled by the automation

house_mode_selector:
description: Global input_select defining the house mode

motion_lighting_enabled_toggle:
description: Optional input_boolean to enable or disable motion lighting

disable_motion_in_modes:
description: House modes where motion should not turn lights on

evening_brightness:
description: Brightness percentage used in Evening mode

night_brightness:
description: Brightness percentage used in Night mode

no_motion_off_delay:
description: Minutes to wait before turning lights off after no motion

auto_reenable_delay:
description: >
Minutes of no motion before automatically re-enabling motion lighting.
Only used if a motion lighting toggle is selected.

example_configurations:
bedroom:
disable_motion_in_modes:
- Night
evening_brightness: 20
motion_lighting_enabled_toggle: selected
result:
- Lights turn on during Day and Evening
- Lights never turn on automatically at night

hallway:
disable_motion_in_modes: none
night_brightness: 10
motion_lighting_enabled_toggle: not_selected
result:
- Lights always turn on via motion
- Brightness adapts safely for night movement

installation:

* Import the blueprint using its raw GitHub URL
* Create an automation from the blueprint
* Configure the inputs for the room
* Save the automation
* Repeat for additional rooms as needed

design_notes:

* Uses house mode instead of clock-based logic
* All behavior is configurable through the UI
* One blueprint can be reused across the entire home
* Manual light control is never blocked

known_limitations:

* No lux or light-level sensing
* No fade transitions by default
* Assumes house mode is managed elsewhere

license: MIT License

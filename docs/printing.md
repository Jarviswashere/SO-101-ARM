# 3D printing

Printer: Bambu Lab X2D Combo, single nozzle, 0.4 mm. Material: PLA, white for the body and orange for the gripper, handle and trigger. Heated chamber off for PLA.

Files: the STL folder of [TheRobotStudio/SO-ARM100](https://github.com/TheRobotStudio/SO-ARM100). Use the SO101 folder only. SO100 is the older arm.

## Settings that worked

- 0.20 mm layer height, Standard profile
- 15 % infill
- Tree supports, 45 degree threshold
- Brim, outer only, 5 mm. Needed for Rotation_Pitch and Wrist_Roll_Pitch, which have very little bed contact

## Mistake 1: individual STLs load in the wrong orientation

The files in `SO101/Individual/` load in their design orientation, not a printable one. Measured on Upper_arm: 67 mm tall with 86 mm² of bed contact as loaded, against 24 mm tall with 3963 mm² of contact in the plate file. Printed as loaded, the parts fail.

Fix: import the plate file instead (`SO101/Follower/Ender_Follower_SO101.stl` or `SO101/Leader/Ender_Leader_SO101.stl`), accept the split prompt, right-click, Split to Objects, delete the parts you do not want, then arrange. The plate files are laid out for a 220 × 220 mm bed and fit the X2D's 256 × 256 mm bed as is.

## Mistake 2: supports that will not come off

The first orange print used supports that fused to the parts. Five parts were scrapped and reprinted. The third attempt with tree supports at the settings above separated cleanly.

## Parts and colours

Per arm pair (one follower, one leader):

| Part | Qty | Colour |
| --- | --- | --- |
| Base_SO101 | 2 | white |
| Base_motor_holder_SO101 | 2 | white |
| Motor_holder_SO101_Base | 2 | white |
| Motor_holder_SO101_Wrist | 2 | white |
| Under_arm_SO101 | 2 | white |
| Upper_arm_SO101 | 2 | white |
| Rotation_Pitch_SO101 | 2 | white |
| Wrist_Roll_Pitch_SO101 | 2 | white |
| WaveShare_Mounting_Plate_SO101 | 2 | white |
| Moving_Jaw_SO101 | 1 | orange, follower |
| Wrist_Roll_Follower_SO101 | 1 | orange, follower |
| Handle_SO101 | 1 | orange, leader |
| Trigger_SO101 | 1 | orange, leader |
| Wrist_Roll_SO101 | 1 | orange, leader |

Skip `SO101 Assembly.stl` (display model) and `Seeedstudio_Mounting_Plate_SO101.stl` (for the Seeed board, not the Waveshare board).

## Gauges

`Gauges/Gauge_0.STL` and `Gauges/Gauge_tight_1.STL` test whether a servo fits your printer's tolerance. Print both and see which one is snug before trusting the arm parts.

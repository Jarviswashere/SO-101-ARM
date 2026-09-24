# SO-101 Arm

A 3D-printed, 6-axis robot arm pair (leader and follower) that learns tasks by imitation. You move the leader arm by hand, the follower copies you, the episodes are recorded, and a neural network trained on those recordings then runs the follower on its own.

Status: in progress. Both arms are printed and cleaned. Servos and cameras are on the way. Assembly, calibration and the first trained policy come next.

![SO-101 follower arm, printed parts](media/hero.jpg)

## What it does

Target task for the first version: pick a block from the table and drop it into a cup, with a success rate measured over 20 trials. Later versions will move to a task that is harder and more useful. That choice is open.

## What you can take from this repo

- A complete parts list with the choices explained, including why both arms run 12 V servos.
- 3D-printing notes for the Bambu Lab X2D that avoid the two failures we hit: parts loading in the wrong orientation and supports that would not separate.
- A macOS (Apple Silicon) software setup for LeRobot that works today, with the one dependency pin that the official guide does not make.
- A troubleshooting log with the real error text and the fix.
- Results measured against a fixed 20-trial test, before and after every change, once the arm is running.

## Hardware

| Part | Qty | Note |
| --- | --- | --- |
| Feetech STS3215 servo, 12 V, 1/345 | 7 | Follower, all 6 joints. Leader, shoulder lift |
| Feetech STS3215 servo, 12 V, 1/191 | 2 | Leader, base pan and elbow flex |
| Feetech STS3215 servo, 12 V, 1/147 | 3 | Leader, wrist flex, wrist roll, gripper |
| Waveshare bus servo driver board | 2 | One per arm, USB to the computer |
| 12 V power supply | 2 | One per arm, must match the 12 V servos |
| USB webcam, 1080p | 2 | Top and front views |
| Wrist camera | 1 | Mounted on the follower gripper |
| Powered USB hub | 1 | Two boards and three cameras on one machine |
| Printed parts | 1 set | See [docs/printing.md](docs/printing.md) |
| Computer | 1 | Mac mini M4, 16 GB. Training runs on a cloud GPU |

Full list, with the reasoning, in [docs/hardware.md](docs/hardware.md).

## 3D printing

Printer: Bambu Lab X2D Combo. Material: PLA. White body, orange gripper and handle parts. Settings and the two mistakes to avoid are in [docs/printing.md](docs/printing.md).

## Software

LeRobot on macOS in a conda environment, with ffmpeg pinned to 7.1.1 because TorchCodec does not load against ffmpeg 9. Step by step in [docs/software-setup.md](docs/software-setup.md). Known errors and fixes in [docs/troubleshooting.md](docs/troubleshooting.md).

## Results

Not measured yet. The arm is not assembled. This section will hold the 20-trial success rate for every version of the policy, with the change made between versions.

## Roadmap

1. Assemble and calibrate both arms.
2. Teleoperate and record 50 episodes of the block-to-cup task.
3. Train an ACT policy on a cloud GPU, run it on the arm, measure 20 trials.
4. Break it on purpose, fix one thing at a time, re-measure.
5. Pick a harder task for version 2.

## Credits

Arm design: [TheRobotStudio/SO-ARM100](https://github.com/TheRobotStudio/SO-ARM100). Software: [Hugging Face LeRobot](https://github.com/huggingface/lerobot).

## License

MIT. See [LICENSE](LICENSE).

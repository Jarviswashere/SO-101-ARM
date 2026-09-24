# Software setup, macOS Apple Silicon

Tested on macOS 26.5, Mac mini M4, September 2026. Follows the [official LeRobot install guide](https://huggingface.co/docs/lerobot/installation) with one pin added.

## 1. Miniforge

```bash
brew install --cask miniforge
conda init zsh
```

Open a new terminal after this.

## 2. Environment

```bash
conda create -y -n lerobot python=3.12
conda activate lerobot
conda install -y ffmpeg=7.1.1 -c conda-forge
```

The pin matters. Without it conda installs ffmpeg 9, and TorchCodec, the video decoder LeRobot uses, only supports ffmpeg 4 to 8. See [troubleshooting.md](troubleshooting.md).

## 3. LeRobot

```bash
pip install 'lerobot[core_scripts,training,feetech,pusht]' mujoco
```

Extras: `core_scripts` for record, replay and calibrate; `training` for training; `feetech` for the STS3215 servos; `pusht` for a simulation environment to test the training loop before the hardware is ready.

## 4. Check

```bash
python -c "import lerobot, torch, torchcodec, mujoco; print(lerobot.__version__, torch.__version__, torch.backends.mps.is_available())"
lerobot-find-port
```

Versions in use: lerobot 0.6.1, torch 2.11.0 with MPS, torchcodec 0.11.1, mujoco 3.13.0.

## Training

Training runs on a cloud GPU, not on the Mac. Flow: record on the Mac, push the dataset to the Hugging Face Hub, train with `lerobot-train` on Colab, push the policy to the Hub, pull it back and run it on the arm.

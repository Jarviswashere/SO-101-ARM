# Troubleshooting

Real errors met on this build, with the cause and the one change that fixed each.

## TorchCodec fails to load after install

```
RuntimeError: Could not load libtorchcodec. ...
Library not loaded: @rpath/libavutil.60.dylib
```

Cause: `conda install ffmpeg -c conda-forge` installed ffmpeg 9.0.1. TorchCodec 0.11.1 supports ffmpeg 4 to 8. The official guide says the command "usually installs ffmpeg 8.X", which is no longer true.

Fix:

```bash
conda install ffmpeg=7.1.1 -c conda-forge
```

## Official ACT Colab notebook installs a non-existent extra

The install cell in the LeRobot ACT training notebook runs `pip install -e ".[train, dataset]"`. The extra is named `training`, so pip skips it. The notebook also installs no simulation environment.

Fix, replace the cell with:

```
!cd lerobot && pip install -e ".[training,pusht]"
```

# Stereo Vision Dataset

Stereo image pairs of tabletop objects, captured with a 3D-printed stereo rig whose right camera is misaligned by known, designed amounts. The dataset accompanies the paper *Detecting and Measuring Stereo Camera Misalignment Using Object Detection and Self-Supervised Visual Features* (Lam Cao), which is under review.

## Overview

- **5 scenes** containing everyday objects
- **7 conditions** per scene: one aligned reference, three pitch rotations and three vertical translations of the right camera
- **10 stereo pairs** per condition, captured one after another with the setup untouched
- **700 images (350 pairs)** in total, 1920 × 1080 PNG, about 1.1 GB

## How the data was captured

Two identical USB camera modules (OmniVision OV2720 sensor, 1.68 mm fixed-focus lens, 1920 × 1080) were mounted on a 3D-printed baseplate with a nominal 60 mm distance between the lens centres. The left camera is the fixed reference. For each condition, the deviation of the right camera is built into the geometry of its own baseplate, so seven baseplates were used in total. The same pair of camera modules was moved from plate to plate. The capture script requested MJPG streams from the cameras and saved the frames as PNG. All scenes are static, indoor, bright and well textured.

## Structure

```
<scene>_data/
├── default/          # aligned reference baseplate (no deliberate misalignment)
├── pitch_2degs/      # right camera pitched by 2° (designed value)
├── pitch_4degs/      # right camera pitched by 4° (designed value)
├── pitch_6degs/      # right camera pitched by 6° (designed value)
├── trans_y_2mm/      # right camera shifted vertically by 2 mm (designed value)
├── trans_y_4mm/      # right camera shifted vertically by 4 mm (designed value)
└── trans_y_6mm/      # right camera shifted vertically by 6 mm (designed value)
    ├── 000_L.png     # left image of pair 0
    ├── 000_R.png     # right image of pair 0
    └── ...
```

## Scenes

| Folder | Content |
| --- | --- |
| `Bowl_90cm_data` | Bowl, labelled 90 cm |
| `Cup_30cm_data` | Cup, labelled 30 cm |
| `Mouse_60cm_data` | Mouse, labelled 60 cm |
| `Bowl_Cup_data` | Bowl and cup together |
| `Remote_30_Bottle_60_Cup_90_data` | Remote (30 cm), bottle (60 cm) and cup (90 cm) together |

The distances in the folder names were estimated by eye and turned out to be unreliable (see the paper). Treat them as labels for the scenes, not as measurements.

## Conditions

| Folder | Right-camera deviation (designed) |
| --- | --- |
| `default` | None |
| `pitch_{2,4,6}degs` | Pitch rotation of 2°, 4°, 6° about the horizontal axis |
| `trans_y_{2,4,6}mm` | Vertical (y-axis) translation of 2, 4, 6 mm |

## Notes on using the data

- **The deviations are designed values, not measured ones.** Printing and mounting add error. The paper estimates a systematic error of about 7.6 pixels (roughly 0.36°), and the `default` baseplate itself shows a residual vertical offset of about 12 pixels in the Mouse 60 cm scene. Compare each condition with the `default` condition of the same scene rather than with zero.
- **Each condition uses a different baseplate**, so differences between conditions include differences in printing and mounting, not only the intended misalignment.
- This repository contains the images only. The baseplate designs are not included.

## Usage

Files are named `<index>_L.png` / `<index>_R.png`. Load a pair like this:

```python
from PIL import Image

left = Image.open("Bowl_90cm_data/default/000_L.png")
right = Image.open("Bowl_90cm_data/default/000_R.png")
```

Or load every pair in a condition:

```python
from pathlib import Path
from PIL import Image

condition = Path("Bowl_90cm_data/default")
for left_path in sorted(condition.glob("*_L.png")):
    right_path = left_path.with_name(left_path.name.replace("_L", "_R"))
    left, right = Image.open(left_path), Image.open(right_path)
```

## License

This dataset is released under the Creative Commons Attribution 4.0 International license (CC BY 4.0). See `LICENSE`.

## Citation

The paper is under review. Citation details will be added here once it is published.

## Questions

Please open an issue on this repository.

# Stereo Vision Dataset

Stereo image pairs of tabletop objects, captured under controlled camera misalignments. This dataset accompanies our research paper.

> **Paper:** _TODO: title, authors, venue/year_ · [link](#) · [arXiv](#)

## Overview

- **5 scenes** with different objects at different distances from the camera
- **7 conditions** per scene: the default (calibrated) setup plus controlled pitch rotations and vertical translations
- **10 stereo pairs** per condition (9 for `Mouse_60cm_data/pitch_6degs`)
- **698 images** in total, 1920 × 1080 PNG, ~1.1 GB

## Structure

```
<scene>_data/
├── default/          # calibrated setup
├── pitch_2degs/      # camera pitched by 2°
├── pitch_4degs/      # camera pitched by 4°
├── pitch_6degs/      # camera pitched by 6°
├── trans_y_2mm/      # camera shifted vertically by 2 mm
├── trans_y_4mm/      # camera shifted vertically by 4 mm
└── trans_y_6mm/      # camera shifted vertically by 6 mm
    ├── 000_L.png     # left image of pair 0
    ├── 000_R.png     # right image of pair 0
    └── ...
```

## Scenes

| Folder | Content |
| --- | --- |
| `Bowl_90cm_data` | Bowl at 90 cm |
| `Cup_30cm_data` | Cup at 30 cm |
| `Mouse_60cm_data` | Mouse at 60 cm |
| `Bowl_Cup_data` | Bowl and cup together |
| `Remote_30_Bottle_60_Cup_90_data` | Remote at 30 cm, bottle at 60 cm, cup at 90 cm |

## Conditions

| Folder | Perturbation |
| --- | --- |
| `default` | None |
| `pitch_{2,4,6}degs` | Pitch rotation of 2°, 4°, 6° |
| `trans_y_{2,4,6}mm` | Vertical (y-axis) translation of 2, 4, 6 mm |

## Usage

Files are named `<index>_L.png` / `<index>_R.png`. Load a pair like this:

```python
from PIL import Image

left = Image.open("Bowl_90cm_data/default/000_L.png")
right = Image.open("Bowl_90cm_data/default/000_R.png")
```

## Citation

```bibtex
@inproceedings{TODO,
  title     = {TODO},
  author    = {TODO},
  booktitle = {TODO},
  year      = {TODO}
}
```

## License

_TODO: e.g. CC BY 4.0_

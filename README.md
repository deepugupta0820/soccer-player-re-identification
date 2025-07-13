# Soccer Player Tracking and Re-Identification using YOLOv11 and Deep SORT

## Overview

This project uses YOLOv11 for player detection and Deep SORT with a MobileNet embedder for real-time tracking. It assigns consistent IDs to players across frames, filters noisy detections, and saves the output as a video (output).

## Features

- Uses YOLOv11 for real-time object detection
- Uses Deep SORT for multi-object tracking with built-in re-identification support.
- Maintains consistent player IDs using motion and appearance features
- Filters out low-confidence and small detections
- Uses a lightweight MobileNet embedder for better speed-performance
- Saves annotated output as a video

## Input and Output

- **Input Video:** `15sec_input_720p.mp4`
- **Output Video:** `output.mp4` (with bounding geen boxes and player IDs)


## Setup Instruction

### 1. Clone the Repository

```bash
git clone https://github.com/deepugupta0820/soccer-player-re-identification.git
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
venv\Scripts\activate  # for Windows
```
### 3. Install Required Packages

```bash
pip install -r requirements.txt
```
or manually install:

```bash
pip install opencv-python matplotlib numpy IPython ultralytics deep-sort-realtime
```

### 4. Download model `best.pt`

[Download best.pt from Google Drive](https://drive.google.com/file/d/1-5fOSHOSB9UXyP_enOoZNAMScrePVcMD/view)

Place your model `best.pt` in the project directory.

### 5. Add Input Video

Place your input video `15sec_input_720p.mp4` in the project directory.

## Run the Code
Run each cell of `soccer.ipynb` sequentially from top to bottom.

## Output
- **`output.mp4`** a new final video file will generate with bounding boxes and consistent `Player {ID}` labels.
- Players who re-enter the frame retain their original IDs through re-identification.

## Environment Notes
- Tested on windows
- Python 3.8–3.11 recommended
- GPU support is optional but recommended for better performance

## Conclusion
The project successfully tracks football players in real-time, assigns consistent IDs, and saves the result as a labeled video.


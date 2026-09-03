# Drone Catcher: YOLO Training Notebook

A Google Colab workflow for training an Ultralytics YOLO11 object detector on a Roboflow dataset and testing the resulting model on drone images or video.

## What the notebook does

1. Installs Ultralytics and Roboflow.
2. Downloads a configured Roboflow dataset in YOLO11 format.
3. Fine-tunes `yolo11s.pt` for object detection.
4. Loads the best checkpoint and runs image/video inference.
5. Displays annotated predictions in Colab.

## Run in Google Colab

Upload or open `YOLO_Colab_Trainer (1).ipynb` in Colab and select a GPU runtime. Then:

1. Create a Roboflow API key and dataset version.
2. Fill in the empty workspace/project values in the dataset cell.
3. Keep API keys in Colab Secrets or environment variables; do not commit them.
4. Run the notebook cells in order.

The central training command is equivalent to:

```bash
yolo task=detect mode=train \
  model=yolo11s.pt \
  data=/path/to/dataset/data.yaml \
  epochs=50 \
  imgsz=640
```

Training artifacts are written under `runs/detect/train/`; the best weights are normally at `runs/detect/train/weights/best.pt`.

## Local inference example

With Python 3.9+ and a trained checkpoint:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install ultralytics
yolo predict model=/path/to/best.pt source=/path/to/image-or-video.jpg save=True
```

## Repository contents

| File | Purpose |
| --- | --- |
| `YOLO_Colab_Trainer (1).ipynb` | Training and inference workflow |
| `test0` | Legacy placeholder file; not used by the notebook |

## Data and model notes

The repository does not contain a dataset, Roboflow credentials, or trained weights. Check the license and permitted uses of your dataset and pretrained model before distributing derived checkpoints. Report the dataset version, split, YOLO checkpoint, epoch count, image size, and validation metrics when publishing results.

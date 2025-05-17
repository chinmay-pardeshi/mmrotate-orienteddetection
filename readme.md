# 🌀 Oriented Object Detection using MMRotate

This repository showcases advanced **oriented object detection** using the **MMRotate** framework.  
It includes training and evaluation for two popular detection architectures:
- 📐 **ReDet** (Rotated Detection Transformer)
- 🎯 **Oriented R-CNN**

These models are ideal for aerial imagery, remote sensing, document layout, and other tasks where **bounding box orientation matters**.

---

## 📦 Framework

This project is built on:

- [MMRotate](https://github.com/open-mmlab/mmrotate) – OpenMMLab's rotation-aware object detection toolbox
- [MMDetection](https://github.com/open-mmlab/mmdetection) – Base detection framework
- [PyTorch](https://pytorch.org/)

---

## 🧠 Implemented Models

| Model         | Backbone         | Description                                                       |
|---------------|------------------|-------------------------------------------------------------------|
| 🟣 ReDet      | ResNet-50-FPN    | A two-stage detector using RoI Align with rotation-invariant features |
| 🔵 Oriented R-CNN | ResNet-50-FPN | A variant of Faster R-CNN with angle regression for oriented boxes    |

---

## 🗃️ Dataset

You can train on public datasets like:
- **DOTA**: Aerial scene dataset for oriented object detection  
  → [https://captain-whu.github.io/DOTA/dataset.html](https://captain-whu.github.io/DOTA/dataset.html)

You must place the dataset in the structure MMRotate expects:

```
mmrotate/
├── data/
│ └── dota/
│ ├── train/
│ ├── val/
│ └── test/
```

## ⚙️ Setup Instructions

### 1. Install MMRotate 


```bash
# Clone MMRotate
git clone https://github.com/open-mmlab/mmrotate.git
cd mmrotate

# Create a virtual env and activate
conda create -n mmrotate python=3.9 -y
conda activate mmrotate

# Install dependencies
pip install -r requirements/build.txt
pip install -v -e .
```
### 2. Train the Model


📐 ReDet

    python tools/train.py configs/redet/redet_re50_fpn_1x_dota_le90.py

🎯 Oriented R-CNN

    python tools/train.py configs/oriented_rcnn/oriented_rcnn_r50_fpn_1x_dota_le90.py


### 3. Evaluate

    python tools/test.py configs/redet/redet_re50_fpn_1x_dota_le90.py work_dirs/redet/latest.pth --eval bbox

### 4. Visualize Predictions

    python tools/test.py configs/redet/redet_re50_fpn_1x_dota_le90.py work_dirs/redet/latest.pth --show-dir o

### 📊 Results

| Model          | Dataset | mAP (HBB) | mAP (OBB) | Notes                      |
| -------------- | ------- | --------- | --------- | -------------------------- |
| ReDet          | DOTA    | -         | \~69%     | Strong rotation robustness |
| Oriented R-CNN | DOTA    | -         | \~68%     | Lightweight and fast       |




### 📁 Folder Structure

```
mmrotate/
├── configs/
│   └── redet/
│   └── oriented_rcnn/
├── tools/
├── work_dirs/
├── data/
│   └── dota/
```

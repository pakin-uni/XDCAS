# A Dynamic Context-aware Aggregation Strategy for Small Object Detection

<div align=center>
<img src="./ultralytics/assets/VisDrone_mAP0.5.png" alt="VisDrone_mAP0.5" width = "549" />
</div>

## <div align="center">Documentation</div>

Table Notes
- No pre-trained weights were used during training.
- The input image resolution is 640×640.
- The training batch size is 16, with a total of 300 training epochs.
- All other parameters follow the settings of the baseline model.

### Quick Start
<details open>
<summary>Install</summary>

Clone repository and install [requirements.txt](./requirements.txt) in a [**Python==3.10**](https://www.python.org/) environment, 
including [**PyTorch==2.5.1**](https://pytorch.org/get-started/previous-versions/) and [**CUDA==12.1**](https://pytorch.org/get-started/previous-versions/).
```bash
python -m venv name
venv\Scripts\activate #window
source venv/bin/activate #linux
pip install torch==2.5.1 torchvision torchaudio \
  --index-url https://download.pytorch.org/whl/cu121
git clone https://github.com/crafly/DCAS.git  # Clone the DCAS repository
cd DCAS  # Navigate to the cloned directory
pip install -e .  # Install the package in editable mode for development
```
</details>

<details open>
<summary>Training</summary>
The commands below reproduce DCAS training results.

```bash
yolo task=detect mode=train model=yolov8l+DCAS.yaml data=VisDrone.yaml epochs=300 batch=16 device=0
```
</details>

<details open>
<summary>Evaluation</summary>
The commands below reproduce DCAS evaluation results.

```bash
yolo task=detect mode=val model=weights/best.pt data=VisDrone.yaml batch=16 device=0
```
</details>

<details open>
<summary>Inference</summary>

The commands below reproduce DCAS inference results.

```bash
yolo task=detect mode=predict model=weights/best.pt device=0 source=path/to/image.jpg  # image
                                                                    path/to/video.mp4  # video
                                                                    path/to/dir  # directory
```
</details>

### Implementation details
Please note
- The overall architecture of DCAS is located at `DCAS/ultralytics/models/v8/yolov8+DCAS.yaml`.
- The DAM module is located at `DCAS/ultralytics/nn/modules.py` and calls `DCAS/ultralytics/nn/DAM.py`.
- The dataset paths in `DCAS/ultralytics/nn/DAM.py` and `DCAS/ultralytics/datasets/` need to be changed to the root directory where the datasets are stored.
- The configuration file is located at `DCAS/ultralytics/yolo/cfg/default.yaml`.
- Representative images of small objects are located at `DCAS/ultralytics/assets/small_object/`.

### Data download
Note that all data has been cleaned and converted to YOLO format labels.
- VisDrone (1.81 GB): [GoogleDrive](https://drive.google.com/file/d/18rZfHuRK40nH43iVbLOd95h6Yv6BoKKl/view?usp=sharing)
- BDD100K (4.25 GB): [GoogleDrive](https://drive.google.com/file/d/1-ghEyaWKQ1lna4kcxXrUKfAAZygpMlh0/view?usp=sharing)
- TT100K (8.74 GB): [GoogleDrive](https://drive.google.com/file/d/10V2pUSmd6nzD5Cs9o0E_4IUfRjVYr6RK/view?usp=sharing)

## Acknowledgement
The code implementation is based on [YOLOv8](https://github.com/ultralytics/ultralytics), thanks to their open-source code.
The data is based on the [VisDrone](https://github.com/VisDrone/VisDrone-Dataset), [BDD100K](https://www.vis.xyz/bdd100k/), and [TT100K](https://cg.cs.tsinghua.edu.cn/traffic-sign/) datasets, thanks to their open-source data.

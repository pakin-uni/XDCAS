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

<div align=center>
<img src="./ultralytics/assets/VisDrone_mAP0.5.png" alt="VisDrone_mAP0.5" width = "549" />
</div>

The commands below reproduce DCAS_EMAdp training results.

```bash
yolo task=detect mode=train model=yolov8+DCASEMAdp.yaml data=dataset.yaml epochs=300 batch=16 device=0
```
</details>

<details open>
<summary>Evaluation</summary>
The commands below reproduce DCAS_EMAdp evaluation results.

<div align=center>
<img src="./ultralytics/assets/VisDrone_mAP0.5.png" alt="VisDrone_mAP0.5" width = "549" />
</div>

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

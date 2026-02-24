## <div align="center">Documentation</div>

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

ต้องมีการแก้ไข dataset.ymal ตามด้านล่าง
```
path: C:/Users/Windows/datasets   # dataset root dir
train: train/image # train images (relative to 'path')
val: val/image  # val images (relative to 'path')
#test:  test/image  # test images (optional)
```
The commands below reproduce DCAS_EMAdp training results.

```bash
yolo task=detect mode=train model=yolov8+DCASEMAdp.yaml data=dataset.yaml epochs=300 batch=16 device=0
```
</details>

<details open>
<summary>Evaluation</summary>
การ Evaluation/Inference ต้องมีการแก้ไข dataset.ymal เปลี่ยน test: >> val:ตามด้านล่าง
```
path: C:/Users/Windows/datasets   # dataset root dir
train: train/image # train images (relative to 'path')
#val: val/image  # val images (relative to 'path')
val:  test/image  # test images (optional)
```
The commands below reproduce DCAS_EMAdp evaluation results.
  
```bash
yolo task=detect mode=val model=weights/best.pt data=dataset.yaml batch=16 device=0
```
</details>

<details open>
<summary>Inference</summary>

The commands below reproduce DCAS_EMAdp inference results.

```bash
yolo task=detect mode=predict model=weights/best.pt device=0 source=path/to/image.jpg  # image
                                                                    path/to/video.mp4  # video
                                                                    path/to/dir  # directory
```
</details>

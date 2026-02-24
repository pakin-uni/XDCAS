# <div align="center">Documentation</div>



# 1. ขั้นตอนการติดตั้ง (Installation)

Clone repository and install [requirements.txt](./requirements.txt) in a [**Python==3.10**](https://www.python.org/) environment, 
including [**PyTorch==2.5.1**](https://pytorch.org/get-started/previous-versions/) and [**CUDA==12.1**](https://pytorch.org/get-started/previous-versions/).

สร้าง virtual environment
```bash
python -m venv name
```

เปิดใช้งาน environment
```bash
venv\Scripts\activate #window
source venv/bin/activate #linux
```

ติดตั้ง PyTorch พร้อม CUDA 12.1
```bash
pip install torch==2.5.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

ดาวน์โหลด repository และติดตั้งแพ็กเกจ
```bash
git clone https://github.com/crafly/DCAS.git  # Clone the DCAS repository
cd DCAS_EMAdp  # Navigate to the cloned directory
pip install -e .  # Install the package in editable mode for development
```

# 2. files ที่ต้องมีการแก้ไข path ไปยัง folder  
## 2.1. DAM.py แก้ให้เป็น path ของ dataset 
ตำแหน่ง:
  
```bash
ultralytics/nn/DAM.py
```

กำหนด path ของ image_folder, label_folder และ, yolo_root 

```bash
line 13: def __init__(self, yolo_root, image_folder="C:/Users/Windows/datasets/train/images", label_folder="C:/Users/Windows/datasets/train/labels"):

line 54: dataset = YOLODataSet(yolo_root='C:/Users/Windows/datasets/')
 ```

## 2.2. dataset.yaml แก้ให้เป็น path ของ dataset
ตำแหน่ง:

```bash
ultralytics/datasets/dataset.yaml
```

กำหนด path root และโฟลเดอร์ย่อยของ train, val, test

```bash
line 2:path: C:/Users/Windows/datasets   # dataset root dir
line 3:train: train/image # train images (relative to 'path')
line 4:val: val/image  # val images (relative to 'path')
line 5: #test:  test/image  # test images (optional)
```


# 3. สำหรับ Training

การ train ต้องมีการแก้ไข dataset.ymal ตามด้านล่าง

```bash
path: C:/Users/Windows/datasets   # dataset root dir
train: train/image # train images (relative to 'path')
val: val/image  # val images (relative to 'path')
#test:  test/image  # test images (optional)
```

คำสั่งด้านล่างใช้สำหรับฝึกโมเดล DCAS_EMAdp

```bash
yolo task=detect mode=train model=yolov8+DCAS_EMAdp data=dataset.yaml epochs=300 batch=16 device=0
```


# 4. สำหรับ Evaluation

ในการทำ Evaluation/Inference ให้แก้ไข dataset.yaml โดยเปลี่ยนการอ้างอิงจาก test เป็น val ตามตัวอย่างด้านล่าง
  
```bash
path: C:/Users/Windows/datasets   # dataset root dir
train: train/image # train images (relative to 'path')
#val: val/image  # val images (relative to 'path')
val:  test/image  # test images (optional)
```
คำสั่งด้านล่างใช้สำหรับประเมินผลโมเดล DCAS_EMAdp
  
```bash
yolo task=detect mode=val model=weights/best.pt data=dataset.yaml batch=16 device=0
```


# 5. Inference

คำสั่งด้านล่างใช้สำหรับรันการทำนายผล (inference) ของโมเดล DCAS_EMAdp

```bash
yolo task=detect mode=predict model=weights/best.pt device=0 source=path/to/image.jpg  # image
                                                                    path/to/video.mp4  # video
                                                                    path/to/dir  # directory
```


# DCAS_EMAdp

Github Original - [DCAS](https://github.com/WongKinYiu/yolov9)

เปเปอร์ - [DCAS: A dynamic context-aware aggregation strategy for small object detection](https://www.sciencedirect.com/science/article/pii/S0031320325007873)

Ultralytics YOLO Docs - [YOLOv8 Docs](https://docs.ultralytics.com/models/yolov8/)

[![Github Original - DCAS](https://img.shields.io/badge/Github%20Original-DCAS-FF0000)](https://github.com/crafly/DCAS) [![Ultralytics YOLO Docs - YOLOv8](https://img.shields.io/badge/Ultralytics%20YOLO%20Docs-YOLOv8-FFA500)](https://docs.ultralytics.com/models/yolov8/)

# ขั้นตอนที่ 1: การติดตั้ง Dependencies

## 1.1. ติดตั้ง Python 3.10 - [Download python](https://www.python.org/downloads/)

# ขั้นตอนที่ 2: การทำ Labels
โปรแกรมที่ใช้ทำ Labels - [labelImg](https://github.com/HumanSignal/labelImg)

[![Labels - labelImg](https://img.shields.io/badge/Labels%20-%20labelImg-FFD700)](https://github.com/HumanSignal/labelImg)

## 2.1. Install

```bash
pip install labelImg
pip install pyqt5 lxml
pip install pyqt5-tools #กรณีมีปัญหาเกี่ยวกับ PyQt ต้องติดตั้ง PyQt5-tools เพิ่ม
```
## 2.2. เรียกใช้งาน

```bash
cd <path โฟลเดอร์ labelImg-master> #ex. cd C:\Users\Admin\Desktop\labelImg-master
python labelImg.py
```
จะขึ้นหน้านี้

![image](https://github.com/user-attachments/assets/6dde8d29-1572-4090-8572-e8348016ef5f)

## 2.3. การใช้งาน

### 2.3.1. กด Open Dir แล้วเลือกโฟลเดอร์ Dataset ที่ต้องการทำ Labels

![image](https://github.com/user-attachments/assets/515f5dc4-2f8e-47ec-acf2-4045bb20c3b0)

### 2.3.2. สร้าง Files txt ชื่อ classes นำไปใส่ใน folder ที่เปิดจาก Open Dir
### 2.3.3. ตั้งค่าให้เป็น YOLO

![image](https://github.com/user-attachments/assets/089d0be5-5c01-4726-96d6-66ce4d12da46)

### 2.3.5. กด Creat ReactBox

![image](https://github.com/user-attachments/assets/469f4d62-970c-4b11-9d52-ce02f9a9a2cf)

### 2.3.6. ทำ Label เลือกคลาส แล้วกด Ok

![image](https://github.com/user-attachments/assets/ad30ed5a-a347-40f9-bd7b-c02aed0bb489)

### 2.3.7. กด Save 

![image](https://github.com/user-attachments/assets/311ef943-e7aa-4b3a-b1f5-76ee46d113f0)

### 2.3.8. กดไปรูปถัดไป

![image](https://github.com/user-attachments/assets/4897caf4-8b73-444c-acba-14ef219362b5)


### 2.3.9. ทำแบบนี้จนกว่าจะครบทุกภาพในโฟลเดอร์


# 3. ขั้นตอนที่ 3: การติดตั้ง DCAS_EMAdp

โคลน repository และติดตั้งไฟล์ [requirements.txt](./requirements.txt) ภายในสภาพแวดล้อม [**Python==3.10**](https://www.python.org/) environment, 
รวม [**PyTorch==2.5.1**](https://pytorch.org/get-started/previous-versions/) และ [**CUDA==12.1**](https://pytorch.org/get-started/previous-versions/).

สร้าง virtual environment (window) และเปิดใช้งาน virtual environment
```bash
py -3.10 -m venv venv #window
venv\Scripts\activate #window
```

สร้าง virtual environment (linux) และเปิดใช้งาน virtual environment
```bash
python3.10 -m venv venv #linux
source venv/bin/activate #linux
```

ติดตั้ง PyTorch พร้อม CUDA 12.1
```bash
pip install torch==2.5.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

ดาวน์โหลด repository และติดตั้งแพ็กเกจ
```bash
git clone https://github.com/crafly/DCAS.git  # Clone the DCAS repository
```
เปลี่ยนชื่อ DCAS เป็น DCAS_EMAdp
cd DCAS_EMAdp  # Navigate to the cloned directory
pip install -e
```

ตัวอย่างโครงสร้างการจัดเก็บ datasets
```bash
datasets/
 ├── train/
 │    ├── images/
 │    └── labels/
 ├── val/
 │    ├── images/
 │    └── labels/
 └── test/
      ├── images/
      └── labels/
```
# 4. ขั้นตอนที่ 4: นำ Files จาก modify code ไปแทนที่ code เดิมตามรูป

```bash
ultralytics/
 ├── datasets/
 │    └── dataset.yaml
 ├── models/
 │    └── v8/
 │         └── yolov8+DCAS_EMAdp.yaml
 └── nn/
 │     ├── DAM.py
 │     ├── modules.py
 │     └── tasks.py
 └── yolo/
      └── cfg/
           └── default.yaml
```

# 5. ขั้นตอนที่ 4: Files ที่ต้องมีการแก้ไข path ไปยัง dataset folder  
## 5.1. DAM.py แก้ให้เป็น path ของ dataset 
ตำแหน่ง:
  
```bash
ultralytics/nn/DAM.py
```

กำหนด path ของ image_folder, label_folder และ, yolo_root <br>

ตัวอย่าง <br>
line 13: def __init__(self, yolo_root, image_folder="C:/Users/Windows/datasets/train/images", label_folder="C:/Users/Windows/datasets/train/labels"):<br>
line 54: dataset = YOLODataSet(yolo_root='C:/Users/Windows/datasets/') # dataset root dir <br>

```bash
line 13: def __init__(self, yolo_root, image_folder="<ใส่ path ที่ชี้ไปยัง datasets/train/images >",
label_folder="<ใส่ path ที่ชี้ไปยัง datasets/train/labels >"):

line 54: dataset = YOLODataSet(yolo_root='<ใส่ path ที่ชี้ไปยัง datasets>')
 ```

## 5.2. dataset.yaml แก้ให้เป็น path ของ dataset
ตำแหน่ง:

```bash
ultralytics/datasets/dataset.yaml
```

กำหนด path root และโฟลเดอร์ย่อยของ train, val, test <br>
ตัวอย่าง <br>
line 2: path:  C:/Users/Windows/datasets   # dataset root dir <br>
line 3: train: train/image # train images (relative to 'path') <br>
line 4: val:   val/image  # val images (relative to 'path') <br>
line 5: #test: test/image  # test images (optional) <br>
```bash
line 2: path:  <ใส่ path ที่ชี้ไปยัง datasets>   # dataset root dir
line 3: train: <ใส่ path ที่ชี้ไปยัง /train/images > (relative to 'path')
line 4: val:   <ใส่ path ที่ชี้ไปยัง /val/images >  # val images (relative to 'path')
line 5: #test: <ใส่ path ที่ชี้ไปยัง /test/images >  # test images (optional)
```


# 6. ขั้นตอนที่ 6: Training

การ train ต้องมีการแก้ไข dataset.ymal ตามด้านล่าง

```bash
path:  C:/Users/Windows/datasets   # dataset root dir
train: train/image # train images (relative to 'path')
val:   val/image  # val images (relative to 'path')
#test: test/image  # test images (optional)
```

คำสั่งด้านล่างใช้สำหรับฝึกโมเดล DCAS_EMAdp

```bash
yolo task=detect mode=train model=yolov8+DCAS_EMAdp data=dataset.yaml epochs=300 batch=16 device=0
```


# 7. ขั้นตอนที่ 7: Evaluation

ในการทำ Evaluation/Inference ให้แก้ไข dataset.yaml โดยเปลี่ยนการอ้างอิงจาก test เป็น val ตามตัวอย่างด้านล่าง

```bash
path:  C:/Users/Windows/datasets   # dataset root dir
train: train/image # train images (relative to 'path')
#val:  val/image  # val images (relative to 'path')
val:   test/image  # test images (optional)
```
คำสั่งด้านล่างใช้สำหรับประเมินผลโมเดล DCAS_EMAdp
  
```bash
yolo task=detect mode=val model=weights/best.pt data=dataset.yaml batch=16 device=0
```


# 8. ขั้นตอนที่ 8: Inference

คำสั่งด้านล่างใช้สำหรับรันการทำนายผล (inference) ของโมเดล DCAS_EMAdp

```bash
yolo task=detect mode=predict model=weights/best.pt device=0 source=path/to/image.jpg  # image
                                                                    path/to/video.mp4  # video
                                                                    path/to/dir  # directory
```


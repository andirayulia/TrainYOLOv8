# TrainYOLOv8

**Preparation**

Membuat konstanta (HOME) untuk menyimpan path direktori utama
```python
import os
HOME = os.getcwd()
print(HOME)
```

**Install Ultralytics**
```python
from ultralytics import YOLO
from IPython.display import display, Image
from IPython import display 
display.clear_output()
!yolo mode=checks
```

Install Package roboflow untuk mengakses dan mengelola dataset dari Roboflow
```python
!pip install -q roboflow
```

**Download Dataset**

```python
import roboflow
roboflow.login()

from roboflow import Roboflow
rf = Roboflow(api_key="MAtohILZSrbUIafwOT5C")
project = rf.workspace("roboflow-universe-projects").project("construction-site-safety")
version = project.version(30)
dataset = version.download("yolov8")
```

**EPOCH = 23**
```python
!yolo task=detect mode=train model=yolov8m.pt data={dataset.location}/data.yaml epochs=23 imgsz=640
```
![results](https://github.com/user-attachments/assets/95f4033c-2c43-4201-9469-7ed3f4d58d63)

![confusion_matrix_normalized](https://github.com/user-attachments/assets/216d2578-6595-4f7e-9591-38c59f0adf12)

**Validate Custom Model**

```python
!yolo task=detect mode=val model=/content/runs/detect/train4/weights/best.pt data={dataset.location}/data.yaml 
```

**Inference with Custom Model**
```python
!yolo task=detect mode=predict model=/content/runs/detect/train4/weights/best.pt conf=0.5 source={dataset.location}/test/images
```
![youtube-186_jpg rf a7c82770148c2886fb42a72693784687](https://github.com/user-attachments/assets/2f31d229-e996-414b-86e8-c88b13ee679d)


**EPOCH = 50**

**Train Model**

Melakukan training menggunakan model yolov8 medium 
**CONSTRUCTION SITE DATASET**
```python
!yolo task=detect mode=train model=yolov8m.pt data={dataset.location}/data.yaml epochs=50 imgsz=640
```

**RESULT**

metrics/mAP_0.5: Mean Average Precision (mAP) dengan threshold IoU 0.5. mAP merupakan metrik untuk mengukur performa model secara keseluruhan. Semakin tinggi nilai mAP, semakin baik performa model.
![results](https://github.com/user-attachments/assets/38b7671a-4803-4cb4-b55a-0c7266e6c893)


== CONFUSION_MATRIX ==

![confusion_matrix_normalized](https://github.com/user-attachments/assets/053f455c-4a78-435e-95bf-a783d802d356)

**Validate Custom Model**

```python
!yolo task=detect mode=val model=/content/runs/detect/train4/weights/best.pt data={dataset.location}/data.yaml 
```

**Inference with Custom Model**
```python
!yolo task=detect mode=predict model=/content/runs/detect/train4/weights/best.pt conf=0.5 source={dataset.location}/test/images
```

![youtube-186_jpg rf a7c82770148c2886fb42a72693784687](https://github.com/user-attachments/assets/51b262bd-f586-4fca-b755-a20c183cbe92)









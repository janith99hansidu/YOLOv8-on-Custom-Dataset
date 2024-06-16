# Training YOLOv8 on Custom Dataset with Google Colab

## 1. Mount the Google Drive
First, you need to mount your Google Drive to access and save files:
```python
from google.colab import drive
drive.mount('/content/drive')
```

## 2. Install Roboflow to Get the Dataset with Annotations
Roboflow provides datasets and annotations. Install Roboflow with the following command:
```python
!pip install roboflow
```

Then, import and configure Roboflow to access your dataset:
```python
from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace().project("YOUR_PROJECT_NAME")
dataset = project.version("YOUR_VERSION_NUMBER").download("yolov8")
```

## 3. Install Ultralytics and Train the Model
Ultralytics provides the implementation of YOLOv8. Install it using:
```python
!pip install ultralytics
```

Next, use the following code to train the YOLOv8 model on your dataset:
```python
from ultralytics import YOLO

# Initialize the model
model = YOLO('yolov8n.pt')  # You can choose different YOLOv8 models: yolov8n.pt, yolov8s.pt, etc.

# Train the model
model.train(data='/content/dataset/data.yaml', epochs=50, imgsz=640)
```
Replace `/content/dataset/data.yaml` with the path to your dataset's configuration file.

## 4. Test the Model
After training, you can test the model using the following command:
```python
!yolo task=detect mode=predict model=/content/runs/detect/train/weights/best.pt data=/content/dataset/data.yaml source=/content/dataset/test/images
```
Replace `/content/runs/detect/train/weights/best.pt` with the path to your trained model weights and `/content/dataset/test/images` with the path to your test images.

## Example of Detected Image
Here is an example of an image with detections made by the trained YOLOv8 model:

![Detected Image](path/to/your/detected/image.jpg)
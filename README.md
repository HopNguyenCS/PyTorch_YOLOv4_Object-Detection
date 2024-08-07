# Implementation of YOLOv4 on VisDrone-DET2019

## Prepare data
Upload data to datasets folder and: 
```bash
!unzip "/content/drive/MyDrive/DA_CS331.N12/datasets/VisDrone2019-DET-train.zip" -d '/content'
!unzip "/content/drive/MyDrive/DA_CS331.N12/datasets/VisDrone2019-DET-val.zip" -d '/content'
!unzip "/content/drive/MyDrive/DA_CS331.N12/datasets/VisDrone2019-DET-test-dev.zip" -d '/content/VisDrone2019-DET-test-dev'
```
Convert Visdrone2Yolo 
```bash
%cd /content/drive/MyDrive/DA_CS331.N12
python Tools/visdrone2yolo.py
```
## Environment Setup
Install
```bash
!pip install mmpycocotools 
!pip install pycocotools==2.0.1.
```

Clone repository
```bash
%cd '/content/drive/MyDrive/DA_CS331.N12/YOLOv4'
!git clone https://github.com/JunnYu/mish-cuda
%cd mish-cuda
!python setup.py build install
```
```bash
!git clone https://github.com/WongKinYiu/PyTorch_YOLOv4
%cd PyTorch_YOLOv4/
!pip install -r requirements.txt
```
## Training
```bash
!python train.py --img 448 448 --batch-size 8 --epochs 300 --data VisDrone_YOLOv4.yaml  --cfg cfg/yolov4.cfg --weights yolov4.weights  
```
## Testing
```bash
!python test.py --batch 64 \
  --data data/VisDrone_YOLOv4.yaml \
    --weights 'weights/best.pt' \
      --name yolov4_640_val \
        --img 448 --verbose
```
## Detecting
```bash
!python detect.py --weights 'weights/best.pt'  --img 448 --conf 0.25 --source 'video.mp4' 
```
## Contributor
**_NGUYEN VAN HOP_**
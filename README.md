# 작업 폴더 생성
mkdir ~/yolov8
cd ~/yolov8

# 가상환경 생성
python3 -m venv yolov8_env

# 가상환경 실행
source yolov8_env/bin/activate

# pip 업데이트
pip install --upgrade pip

# YOLO 설치
pip install ultralytics

# 설치 확인
yolo checks

# 데이터셋 폴더로 이동
cd ~/Downloads/dacl10k-DatasetNinja/dacl10k_yolo

# dacl10k.yaml 수정 (path: . 로 변경)
nano dacl10k.yaml

# 학습 시작
yolo segment train \
model=yolo11n-seg.pt \
data=dacl10k.yaml \
epochs=100 \
imgsz=640 \
batch=8 \
device=mps

# 학습 결과 평가
yolo segment val \
model=runs/segment/train/weights/best.pt \
data=dacl10k.yaml

# 이미지 1장 테스트
yolo segment predict \
model=runs/segment/train/weights/best.pt \
source=test.jpg

# 폴더 전체 테스트 (예시)
yolo segment predict \
model=runs/segment/train/weights/best.pt \
source=./test_images

<img width="1920" height="1920" alt="train_batch0" src="https://github.com/user-attachments/assets/ee329b16-e955-4295-908d-1c4c06baa59f" />

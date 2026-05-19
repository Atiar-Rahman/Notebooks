```
!pip install ultralytics opencv-python
```

check video path open
```python
import cv2

video_path = "/content/drive/MyDrive/ML Notes and DL notes/code/vi1.webm"

cap = cv2.VideoCapture(video_path)

  

if not cap.isOpened():

print("❌ Could not open video file. Check path or format.")

else:

print("✅ Video file opened successfully")
```

video check human detected and frame combine video create
```python
import cv2

from ultralytics import YOLO

  

# Load YOLOv8 pretrained model

model = YOLO("/content/yolov8n.pt")

  

video_path = "/content/drive/MyDrive/ML Notes and DL notes/code/vi1.mp4"

cap = cv2.VideoCapture(video_path)

  

# Get video properties

width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))

height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

fps = cap.get(cv2.CAP_PROP_FPS)

  

# Output video

out = cv2.VideoWriter("only_human_detected.mp4",

cv2.VideoWriter_fourcc(*'mp4v'), fps, (width, height))

  

frame_count = 0

saved_count = 0

  

while cap.isOpened():

ret, frame = cap.read()

if not ret:

break

  

frame_count += 1

  

# Run YOLO detection

results = model(frame, stream=True)

  

human_detected = False

# Draw bounding boxes if human detected

for r in results:

for box in r.boxes:

if int(box.cls[0]) == 0: # 'person'

human_detected = True

x1, y1, x2, y2 = box.xyxy[0]

cv2.rectangle(frame, (int(x1), int(y1)), (int(x2), int(y2)), (0, 255, 0), 2)

cv2.putText(frame, "Human", (int(x1), int(y1) - 10),

cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)

  

# Save frame only if human detected

if human_detected:
out.write(frame)
saved_count += 1

cap.release()
out.release()
print(f"✅ Total frames processed: {frame_count}")
print(f"✅ Frames with human detected and saved: {saved_count}")
print("Output video saved as 'only_human_detected.mp4'")
```

```python
import cv2

import os

from ultralytics import YOLO

  

# Load YOLOv8 pretrained model

model = YOLO("/content/yolov8n.pt")

  

video_path = "/content/drive/MyDrive/ML Notes and DL notes/code/vi1.mp4"

save_folder = "/content/drive/MyDrive/ML Notes and DL notes/code/frame"

  

# Create folder if it doesn't exist

os.makedirs(save_folder, exist_ok=True)

  

cap = cv2.VideoCapture(video_path)

  

frame_count = 0

saved_count = 0

  

while cap.isOpened():

ret, frame = cap.read()

if not ret:

break

  

frame_count += 1

  

# Run YOLO detection

results = model(frame, stream=True)

  

human_detected = False

# Draw bounding boxes if human detected

for r in results:

for box in r.boxes:

if int(box.cls[0]) == 0: # 'person'

human_detected = True

x1, y1, x2, y2 = box.xyxy[0]

cv2.rectangle(frame, (int(x1), int(y1)), (int(x2), int(y2)), (0, 255, 0), 2)

cv2.putText(frame, "Human", (int(x1), int(y1) - 10),

cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)

  

# Save frame as image if human detected

if human_detected:

saved_count += 1

frame_filename = os.path.join(save_folder, f"frame_{saved_count:05d}.jpg")

cv2.imwrite(frame_filename, frame)

  

cap.release()

print(f"✅ Total frames processed: {frame_count}")

print(f"✅ Frames with human detected and saved: {saved_count}")

print(f"✅ Frames saved in folder: {save_folder}")
```


save frame save only human using this code only video path setup

```python
import cv2

import os

from ultralytics import YOLO

  

# Load YOLOv8 pretrained model

model = YOLO("/content/yolov8n.pt")

  

video_path = "/content/drive/MyDrive/ML Notes and DL notes/code/output.mp4"

save_folder = "/content/drive/MyDrive/ML Notes and DL notes/code/f1"

  

# Create folder if it doesn't exist

os.makedirs(save_folder, exist_ok=True)

  

cap = cv2.VideoCapture(video_path)

  

frame_count = 0

saved_count = 0

  

while cap.isOpened():

ret, frame = cap.read()

if not ret:

break

  

frame_count += 1

  

# Run YOLO detection

results = model(frame, stream=True)

  

human_detected = False

for r in results:

for box in r.boxes:

if int(box.cls[0]) == 0: # 'person'

human_detected = True

x1, y1, x2, y2 = box.xyxy[0]

cv2.rectangle(frame, (int(x1), int(y1)), (int(x2), int(y2)), (0, 255, 0), 2)

cv2.putText(frame, "Human", (int(x1), int(y1) - 10),

cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)

  

# Save only every 10th human-detected frame

if human_detected and frame_count % 10 == 0:

saved_count += 1

frame_filename = os.path.join(save_folder, f"frame_{saved_count:05d}.jpg")

cv2.imwrite(frame_filename, frame)

  

cap.release()

print(f"✅ Total frames processed: {frame_count}")

print(f"✅ Every 10th human-detected frame saved: {saved_count}")

print(f"✅ Frames saved in folder: {save_folder}")
```



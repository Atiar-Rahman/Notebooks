Great! Let's walk through your full code **line by line**, explaining what each part does and how everything ties together. Your script uses **YOLOv8** for person detection and **DeepSORT** for tracking individuals across video frames. It processes a folder of videos, retains videos where a person is detected, and moves others to a "delete" folder.

---

## 🔁 PART 1: Imports

```python
import cv2
import os
import shutil
from ultralytics import YOLO
from deep_sort_realtime.deepsort_tracker import DeepSort
```

### 💡 Explanation:

- `cv2`: OpenCV – used for reading, writing, and processing video frames.
    
- `os`: To handle filesystem operations like paths, directories, etc.
    
- `shutil`: For moving and deleting files/directories.
    
- `YOLO`: Loads a pretrained YOLOv8 model from Ultralytics for object detection.
    
- `DeepSort`: Initializes a DeepSORT tracker for tracking objects across video frames.
    

---

## 🤖 PART 2: Load YOLOv8 Model

```python
model = YOLO('/home/atiar/.cache/ultralytics/yolov8s.pt')
model.classes = [0]  # person class
```

### 💡 Explanation:

- Loads the `yolov8s.pt` model.
    
- `model.classes = [0]`: Filters to detect only **class 0** (person).
    

---

## 🧠 PART 3: Initialize DeepSORT Tracker

```python
tracker = DeepSort(max_age=30, n_init=3)
```

### 💡 Explanation:

- Initializes the DeepSORT tracker.
    
- `max_age=30`: Tracker keeps a lost object alive for 30 frames.
    
- `n_init=3`: Minimum 3 detections before the track is confirmed.
    

---

## 🎯 PART 4: Detection + Tracking per Video

```python
def draw_boxes_and_track(input_path, output_path, confidence_threshold=0.3):
```

### 💡 Purpose:

Processes a **single video**: runs detection and tracking → writes output with bounding boxes.

---

### 🔁 Video Input and Output Setup

```python
    cap = cv2.VideoCapture(input_path)
    width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
    height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
    fps = cap.get(cv2.CAP_PROP_FPS)

    fourcc = cv2.VideoWriter_fourcc(*'mp4v')
    out = cv2.VideoWriter(output_path, fourcc, fps, (width, height))
```

### 💡 Explanation:

- Opens the video for reading and prepares a writer to save the output with drawn boxes.
    
- Extracts the original video's width, height, and FPS.
    

---

### 👁️ Frame-by-frame Processing

```python
    person_found = False

    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            break
```

- Reads frames in a loop until video ends.
    
- `person_found` keeps track if **any person** was found in the entire video.
    

---

### 🚶 YOLOv8 Person Detection

```python
        results = model(frame)[0]

        detections = []
        for box, conf, cls in zip(results.boxes.xyxy, results.boxes.conf, results.boxes.cls):
            if int(cls) == 0 and conf > confidence_threshold:
                x1, y1, x2, y2 = box.cpu().numpy()
                width = x2 - x1
                height = y2 - y1
                detections.append(([x1, y1, width, height], conf.cpu().item()))
```

- Runs YOLOv8 on the frame.
    
- Iterates through detected boxes.
    
- Filters only **person** detections (class 0) with confidence > threshold (default: 0.3).
    
- Converts box from `[x1, y1, x2, y2]` to `[x, y, width, height]` format required by DeepSORT.
    

---

### 🧍 Update DeepSORT Tracker

```python
        tracks = tracker.update_tracks(detections, frame=frame)

        for track in tracks:
            if not track.is_confirmed():
                continue
            person_found = True
```

- DeepSORT updates tracks with the new detections.
    
- Skips **unconfirmed** tracks.
    
- If any track is confirmed → a person has been tracked → `person_found = True`.
    

---

### 🎨 Draw Bounding Boxes

```python
            track_id = track.track_id
            ltrb = track.to_ltrb()
            x1, y1, x2, y2 = map(int, ltrb)

            cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)
            cv2.putText(frame, f'ID {track_id}', (x1, y1 - 10),
                        cv2.FONT_HERSHEY_SIMPLEX, 0.6, (0, 255, 0), 2)
```

- Draws a **green box** and **track ID** for each confirmed person.
    

---

### 💾 Write Frame to Output Video

```python
        out.write(frame)

    cap.release()
    out.release()
    return person_found
```

- Writes the annotated frame to the output video.
    
- Returns whether any person was found.
    

---

## 📂 PART 5: Process All Videos in a Folder

```python
def clean_clips_in_folder(class_path, deleted_store_root="deleteClip", boxed_output_root="boxedVideos"):
```

### 💡 Purpose:

- Loops over all `.mp4` files in a given folder.
    
- Keeps those **with people**, deletes (moves) those **without**.
    

---

### 📁 Setup Paths

```python
    total = 0
    moved = 0
    saved = 0

    class_name = os.path.basename(class_path.rstrip("/"))
    deleted_class_path = os.path.join(deleted_store_root, class_name)
    boxed_class_path = os.path.join(boxed_output_root, class_name)
    os.makedirs(deleted_class_path, exist_ok=True)
    os.makedirs(boxed_class_path, exist_ok=True)
```

- Extracts folder name.
    
- Creates output directories if they don’t exist:
    
    - `deleted_class_path`: for videos with **no person**.
        
    - `boxed_class_path`: for videos **with bounding boxes**.
        

---

### 🔁 Process Each Clip

```python
    for clip in os.listdir(class_path):
        if clip.endswith(".mp4"):
```

- Loops through all `.mp4` files.
    

---

### ▶️ Run Detection & Tracking on Each Clip

```python
            video_path = os.path.join(class_path, clip)
            boxed_path = os.path.join(boxed_class_path, clip)
            total += 1

            print(f"\n[INFO] Processing: {clip}")
            has_person = draw_boxes_and_track(video_path, boxed_path)
            print(f"[DEBUG] {clip} → has_person = {has_person}")
```

- Calls `draw_boxes_and_track()` on each video.
    
- Saves the output video with boxes in `boxed_path`.
    

---

### 🧹 Move/Delete if No Person Found

```python
            if not has_person:
                shutil.move(video_path, os.path.join(deleted_class_path, clip))
                if os.path.exists(boxed_path):
                    os.remove(boxed_path)  # delete boxed version too
                print(f"🚮 Moved: {clip} → {deleted_class_path}")
                moved += 1
            else:
                print(f"✅ Kept: {clip} (person detected)")
                saved += 1
```

- If no person:
    
    - Move original video to the `deleteClip` folder.
        
    - Remove the boxed version.
        
- If person found: Keep it.
    

---

### ✅ Summary

```python
    print(f"\n✅ Done. Processed {total} clips in {class_path}")
    print(f"🟢 Saved (with person): {saved}")
    print(f"🚮 Moved (no person): {moved} → {deleted_class_path}")
```

---

## 🚀 PART 6: Example Usage

```python
clean_clips_in_folder("/home/atiar/Downloads/archive/Frame to video/train/Vandalism")
```

- Calls the main function to process the `Vandalism` folder.
    

---

## 🧩 Overall Workflow:

1. Load model (YOLOv8) & tracker (DeepSORT).
    
2. For each video:
    
    - Detect & track people.
        
    - Draw bounding boxes.
        
    - Save output.
        
    - If no person is detected: move to "delete" folder.
        
3. Print stats on how many videos were kept vs moved.
    

---

If you want, I can help you:

- Optimize performance (e.g., batch processing).
    
- Add multi-threading or progress bars.
    
- Support other file types like `.avi`, `.mov`, etc.
    
- Automatically install missing packages.
    

Just let me know what you need next.
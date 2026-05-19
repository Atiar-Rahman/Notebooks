
1. video convert `mp4` 
2. video to clip convert
``` python
import cv2

import os

  

def split_video_to_clips(video_path, output_folder, clip_length=60): # clip_length in frames

cap = cv2.VideoCapture(video_path)

  

if not cap.isOpened():

print(f"❌ Error: Cannot open video {video_path}")

return

  

os.makedirs(output_folder, exist_ok=True)

  

fps = cap.get(cv2.CAP_PROP_FPS)

width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))

height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

  

fourcc = cv2.VideoWriter_fourcc(*'mp4v')

  

frame_count = 0

clip_index = 0

out = None

  

while True:

ret, frame = cap.read()

if not ret:

break

  

if frame_count % clip_length == 0:

if out:

out.release()

clip_filename = os.path.join(output_folder, f"clip_{clip_index:04d}.mp4")

out = cv2.VideoWriter(clip_filename, fourcc, fps, (width, height))

clip_index += 1

  

out.write(frame)

frame_count += 1

  

if out:

out.release()

cap.release()

  

print(f"✅ Done. {clip_index} clips saved to: {output_folder}")
```

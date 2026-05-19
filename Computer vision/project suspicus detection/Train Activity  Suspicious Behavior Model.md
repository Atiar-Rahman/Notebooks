Perfect! Now we’ll move to **training the Activity / Suspicious Behavior Detection model** using your preprocessed UCF-Crime 64×64 dataset. I’ll break it into clear steps.

---

## **1️⃣ Model Choice**

Since your dataset is **frames extracted from videos**, you have two main options:

|Approach|Notes|
|---|---|
|**3D CNN / Temporal CNN** (R3D-18, I3D, SlowFast)|Learns spatio-temporal features from clips of frames (recommended for activity detection). Requires clips (16–32 consecutive frames).|
|**2D CNN + Frame Aggregation**|Simpler: treat frames independently, then aggregate predictions across frames for video-level label. Faster but less accurate.|

**Tip:** For UCF-Crime, since frames are small (64×64), start with **2D CNN on frames**. Later you can extend to **3D CNN with clips**.

---

## **2️⃣ Prepare Input for Model**

### **Option A: Frame-Level Classification (2D CNN)**

- Input: `(64,64,3)`
    
- Label: 14-class one-hot
    
- Suitable for quick prototyping.
    

```python
import tensorflow as tf
from tensorflow.keras import layers, models

input_shape = (64, 64, 3)
num_classes = 14

model = models.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=input_shape),
    layers.MaxPooling2D((2,2)),
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),
    layers.Conv2D(128, (3,3), activation='relu'),
    layers.Flatten(),
    layers.Dense(256, activation='relu'),
    layers.Dropout(0.5),
    layers.Dense(num_classes, activation='softmax')
])

model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
model.summary()
```

- Train with `X_train` / `y_train` from preprocessing.
    

```python
history = model.fit(
    X_train, y_train,
    epochs=25,
    batch_size=64,
    validation_data=(X_val, y_val)
)
```

---

### **Option B: Clip-Based 3D CNN (R3D-18 / SlowFast)**

- Input: `(num_frames, 3, 64, 64)`
    
- Each sample = **16–32 consecutive frames** (a clip)
    
- Output: predicted class per clip
    

```python
import torch
from torchvision.models.video import r3d_18

model = r3d_18(pretrained=True)
model.fc = torch.nn.Linear(model.fc.in_features, 14)  # adapt to 14 classes
model = model.cuda()  # if GPU available
```

- Prepare clips:
    
    - Stack 16 consecutive human-detected frames → shape `(3,16,64,64)`
        
    - Feed into model → output 14-class probabilities
        

```python
# Example forward pass
clip = torch.randn(1,3,16,64,64).cuda()  # batch_size=1
outputs = model(clip)
pred = torch.argmax(outputs, dim=1)
```

- Training uses `CrossEntropyLoss` and standard optimizer.
    

---

## **3️⃣ Training Tips**

1. **Start with 2D CNN on frames**: faster, helps you debug pipeline.
    
2. **Data Augmentation**: rotation, horizontal flip, zoom → improves generalization.
    
3. **Clip length for 3D CNN**: 16–32 frames is standard for activity recognition.
    
4. **Batch size**: small batch for GPU memory limits.
    
5. **Early stopping & checkpoint**: save best weights based on validation accuracy.
    

```python
from tensorflow.keras.callbacks import ModelCheckpoint, EarlyStopping

checkpoint = ModelCheckpoint('best_model.h5', save_best_only=True, monitor='val_accuracy')
early_stop = EarlyStopping(patience=5, monitor='val_accuracy', restore_best_weights=True)

history = model.fit(X_train, y_train,
                    epochs=50,
                    batch_size=64,
                    validation_data=(X_val, y_val),
                    callbacks=[checkpoint, early_stop])
```

---

## **4️⃣ Post-Training**

- **Evaluate on test set**:
    

```python
test_loss, test_acc = model.evaluate(X_test, y_test)
print("Test Accuracy:", test_acc)
```

- **Save model**:
    
    - Keras: `model.save("activity_model.h5")`
        
    - PyTorch: `torch.save(model.state_dict(), "activity_model.pth")`
        
- **Inference**: Use the model to predict suspicious behavior on **new human-detected frames** or **real-time video clips**.
    

---

## **5️⃣ Next Step**

After training, the model can be integrated into your **real-time pipeline**:

1. Capture live video → YOLOv8 detects humans.
    
2. Collect N consecutive frames per human.
    
3. Feed the clip to your trained model.
    
4. Overlay predicted activity / suspicious behavior on video.
    
5. Save video or trigger alert.
    

---

If you want, I can create a **full end-to-end Colab-ready training script** for your UCF-Crime 64×64 dataset, supporting both **frame-level 2D CNN** and **clip-level 3D CNN**.

Do you want me to do that next?
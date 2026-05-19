```js
import React, { useRef, useState } from "react";
import Webcam from "react-webcam";

const App = () => {
  const webcamRef = useRef(null);
  const mediaRecorderRef = useRef(null);

  const [cameraOn, setCameraOn] = useState(true);
  const [capturing, setCapturing] = useState(false);
  const [recordedChunks, setRecordedChunks] = useState([]);
  const [recordedVideoURL, setRecordedVideoURL] = useState(null);
  const [imageSrc, setImageSrc] = useState(null);

  // 🎥 Toggle camera on/off
  const toggleCamera = () => {
    if (cameraOn && webcamRef.current?.stream) {
      webcamRef.current.stream.getTracks().forEach((track) => track.stop());
    }
    setCameraOn((prev) => !prev);
    setImageSrc(null);
    setRecordedVideoURL(null);
  };

  // 📸 Capture image
  const captureImage = () => {
    if (webcamRef.current) {
      const image = webcamRef.current.getScreenshot();
      if (image) setImageSrc(image);
      else alert("⚠️ Could not capture image. Try again.");
    }
  };

  // 💾 Download image
  const downloadImage = () => {
    if (!imageSrc) return alert("No image captured!");
    const link = document.createElement("a");
    link.href = imageSrc;
    link.download = `captured_image_${Date.now()}.jpg`;
    link.click();
  };

  // 🎬 Start video recording
  const startRecording = () => {
    setRecordedChunks([]);
    setRecordedVideoURL(null);
    setCapturing(true);

    const stream = webcamRef.current.stream;
    const chunks = []; // use local array (fixes async timing issue)
    const mediaRecorder = new MediaRecorder(stream, { mimeType: "video/webm" });

    mediaRecorder.ondataavailable = (event) => {
      if (event.data.size > 0) chunks.push(event.data);
    };

    mediaRecorder.onstop = () => {
      const blob = new Blob(chunks, { type: "video/webm" });
      const url = URL.createObjectURL(blob);
      setRecordedVideoURL(url); // 🎞️ instant preview
    };

    mediaRecorder.start();
    mediaRecorderRef.current = mediaRecorder;
  };

  // 🛑 Stop recording
  const stopRecording = () => {
    if (mediaRecorderRef.current) {
      mediaRecorderRef.current.stop();
      setCapturing(false);
    }
  };

  // 💾 Download video
  const downloadVideo = () => {
    if (!recordedVideoURL) return alert("No video recorded!");

    const a = document.createElement("a");
    a.href = recordedVideoURL;
    a.download = `recorded_video_${Date.now()}.webm`;
    a.click();
  };

  return (
    <div style={{ textAlign: "center", marginTop: 20 }}>
      <h2>🎥 Webcam Capture (with Working Video Preview)</h2>

      {/* Toggle Camera */}
      <button onClick={toggleCamera} style={{ marginBottom: 10 }}>
        {cameraOn ? "📴 Turn Camera Off" : "📷 Turn Camera On"}
      </button>

      {/* Webcam Feed */}
      {cameraOn && (
        <div style={{ display: "flex", justifyContent: "center" }}>
          <Webcam
            ref={webcamRef}
            audio={true}
            mirrored={true}
            screenshotFormat="image/jpeg"
            width={500}
            height={400}
            videoConstraints={{ facingMode: "user" }}
          />
        </div>
      )}

      {/* Controls */}
      {cameraOn && (
        <>
          <div style={{ marginTop: 10 }}>
            <button onClick={captureImage}>📸 Capture Image</button>
            <button onClick={downloadImage}>⬇️ Download Image</button>
          </div>

          <div style={{ marginTop: 10 }}>
            {!capturing ? (
              <button onClick={startRecording}>🎬 Start Recording</button>
            ) : (
              <button onClick={stopRecording}>🛑 Stop Recording</button>
            )}
            <button onClick={downloadVideo}>⬇️ Download Video</button>
          </div>
        </>
      )}

      {/* Image Preview */}
      {imageSrc && (
        <div style={{ marginTop: 20 }}>
          <h4>📷 Captured Image Preview</h4>
          <img src={imageSrc} alt="Captured" width="320" />
        </div>
      )}

      {/* 🎞️ Auto Video Preview */}
      {recordedVideoURL && (
        <div style={{ marginTop: 20 }}>
          <h4>🎞️ Recorded Video Preview</h4>
          <video
            src={recordedVideoURL}
            width="480"
            height="360"
            controls
            autoPlay
          />
        </div>
      )}

      {!cameraOn && (
        <p style={{ marginTop: 20, color: "gray" }}>📵 Camera is turned off</p>
      )}
    </div>
  );
};

export default App;

```

# explain this code

Absolutely 👍 — here’s a **line-by-line explanation** of your React code.  
You’ve built a small **frontend-only webcam recorder app** using **React** and **react-webcam**.

---

## 🧠 Imports and setup

```js
import React, { useRef, useState } from "react";
import Webcam from "react-webcam";
```

- `React`: the core React library to build components.
    
- `{ useRef, useState }`: React hooks:
    
    - `useState()` → stores dynamic UI data (like camera on/off, image, video URL, etc.).
        
    - `useRef()` → creates a persistent reference to a DOM element or component (here it points to the `<Webcam>` component and `MediaRecorder` object).
        
- `react-webcam`: library that gives access to the user’s webcam inside a React component.
    

---

## 📸 Declaring state and refs

```js
const webcamRef = useRef(null);
const mediaRecorderRef = useRef(null);
```

- `webcamRef` — reference to the live webcam element (lets you call `getScreenshot()` or access its media stream).
    
- `mediaRecorderRef` — reference to the browser’s `MediaRecorder` API (used to record video).
    

```js
const [cameraOn, setCameraOn] = useState(true);
const [capturing, setCapturing] = useState(false);
const [recordedChunks, setRecordedChunks] = useState([]);
const [recordedVideoURL, setRecordedVideoURL] = useState(null);
const [imageSrc, setImageSrc] = useState(null);
```

Each `useState` stores a piece of data:

- `cameraOn` → whether the camera is currently active.
    
- `capturing` → whether you’re recording video.
    
- `recordedChunks` → raw video data pieces from MediaRecorder.
    
- `recordedVideoURL` → temporary URL for the recorded video preview.
    
- `imageSrc` → base64 string for the captured image.
    

---

## 🎥 Camera On/Off toggle

```js
const toggleCamera = () => {
  if (cameraOn && webcamRef.current?.stream) {
    webcamRef.current.stream.getTracks().forEach((track) => track.stop());
  }
  setCameraOn((prev) => !prev);
  setImageSrc(null);
  setRecordedVideoURL(null);
};
```

- If the camera is **on**, stop all active media tracks (`track.stop()` actually turns off the webcam LED).
    
- Flip the `cameraOn` state (on → off, or off → on).
    
- Clear previous image/video previews when toggling.
    

---

## 📷 Capture still image

```js
const captureImage = () => {
  if (webcamRef.current) {
    const image = webcamRef.current.getScreenshot();
    if (image) setImageSrc(image);
    else alert("⚠️ Could not capture image. Try again.");
  }
};
```

- `getScreenshot()` → takes a photo from the current webcam frame and returns it as a base64 JPEG.
    
- The result is stored in `imageSrc`, which later displays a preview.
    

---

## 💾 Download image

```js
const downloadImage = () => {
  if (!imageSrc) return alert("No image captured!");
  const link = document.createElement("a");
  link.href = imageSrc;
  link.download = `captured_image_${Date.now()}.jpg`;
  link.click();
};
```

- Creates an invisible `<a>` tag.
    
- Sets its `href` to your captured image (base64 data).
    
- Sets the `download` attribute to automatically save the file.
    
- Programmatically clicks it to trigger the download.
    

---

## 🎬 Start video recording

```js
const startRecording = () => {
  setRecordedChunks([]);
  setRecordedVideoURL(null);
  setCapturing(true);

  const stream = webcamRef.current.stream;
  const chunks = []; // local array to collect data

  const mediaRecorder = new MediaRecorder(stream, { mimeType: "video/webm" });
```

- Clear any previous recordings.
    
- Start capturing new video from the webcam’s media stream.
    
- Create a new `MediaRecorder` that records the webcam feed as `video/webm`.
    

```js
mediaRecorder.ondataavailable = (event) => {
  if (event.data.size > 0) chunks.push(event.data);
};
```

- Every time the recorder has new video data, push it to `chunks`.
    

```js
mediaRecorder.onstop = () => {
  const blob = new Blob(chunks, { type: "video/webm" });
  const url = URL.createObjectURL(blob);
  setRecordedVideoURL(url);
};
```

- When recording stops, create a `Blob` from the chunks (a video file in memory).
    
- `URL.createObjectURL(blob)` gives a temporary local URL for the video.
    
- Save it in `recordedVideoURL` → React will show a playable `<video>`.
    

```js
mediaRecorder.start();
mediaRecorderRef.current = mediaRecorder;
```

- Start recording, and keep a reference to stop it later.
    

---

## 🛑 Stop recording

```js
const stopRecording = () => {
  if (mediaRecorderRef.current) {
    mediaRecorderRef.current.stop();
    setCapturing(false);
  }
};
```

- Calls `.stop()` on the `MediaRecorder`, which triggers the `onstop` event above.
    
- Updates `capturing` to false.
    

---

## 💾 Download recorded video

```js
const downloadVideo = () => {
  if (!recordedVideoURL) return alert("No video recorded!");

  const a = document.createElement("a");
  a.href = recordedVideoURL;
  a.download = `recorded_video_${Date.now()}.webm`;
  a.click();
};
```

- Similar logic to downloading the image:  
    creates an `<a>` tag → sets `href` to the video blob URL → triggers a download.
    

---

## 🧱 UI rendering

```jsx
return (
  <div style={{ textAlign: "center", marginTop: 20 }}>
    <h2>🎥 Webcam Capture (with Working Video Preview)</h2>
```

Starts the main JSX structure for your UI.

---

### Toggle button

```jsx
<button onClick={toggleCamera} style={{ marginBottom: 10 }}>
  {cameraOn ? "📴 Turn Camera Off" : "📷 Turn Camera On"}
</button>
```

- Calls `toggleCamera()` when clicked.
    
- The text changes dynamically based on the `cameraOn` state.
    

---

### Webcam feed (only if camera is ON)

```jsx
{cameraOn && (
  <div style={{ display: "flex", justifyContent: "center" }}>
    <Webcam
      ref={webcamRef}
      audio={true}
      mirrored={true}
      screenshotFormat="image/jpeg"
      width={500}
      height={400}
      videoConstraints={{ facingMode: "user" }}
    />
  </div>
)}
```

- Displays the live webcam feed when `cameraOn` is true.
    
- `mirrored` flips horizontally (looks like a mirror).
    
- `videoConstraints` chooses the **front camera** on mobile.
    

---

### Capture and recording controls

```jsx
{cameraOn && (
  <>
    <div style={{ marginTop: 10 }}>
      <button onClick={captureImage}>📸 Capture Image</button>
      <button onClick={downloadImage}>⬇️ Download Image</button>
    </div>

    <div style={{ marginTop: 10 }}>
      {!capturing ? (
        <button onClick={startRecording}>🎬 Start Recording</button>
      ) : (
        <button onClick={stopRecording}>🛑 Stop Recording</button>
      )}
      <button onClick={downloadVideo}>⬇️ Download Video</button>
    </div>
  </>
)}
```

- If camera is on, show buttons for capturing and recording.
    
- The record button changes dynamically between **Start** and **Stop**.
    

---

### Image preview

```jsx
{imageSrc && (
  <div style={{ marginTop: 20 }}>
    <h4>📷 Captured Image Preview</h4>
    <img src={imageSrc} alt="Captured" width="320" />
  </div>
)}
```

- Shows a preview of the last captured photo if available.
    

---

### 🎞️ Video preview

```jsx
{recordedVideoURL && (
  <div style={{ marginTop: 20 }}>
    <h4>🎞️ Recorded Video Preview</h4>
    <video
      src={recordedVideoURL}
      width="480"
      height="360"
      controls
      autoPlay
    />
  </div>
)}
```

- Shows a video player for your recorded clip, with **controls** and **auto-play**.
    

---

### Camera off message

```jsx
{!cameraOn && (
  <p style={{ marginTop: 20, color: "gray" }}>📵 Camera is turned off</p>
)}
```

- Displays a message when the camera is toggled off.
    

---

## ✅ Summary of How It Works

|Feature|Key Mechanism|
|---|---|
|Live webcam|`react-webcam` + `<Webcam>` component|
|Capture image|`.getScreenshot()`|
|Record video|Browser’s native `MediaRecorder` API|
|Save files|Creates temporary Blob URLs + downloads via `<a>` tag|
|Preview|`<img>` and `<video>` tags use those URLs directly|
|Camera control|Stop/start video tracks on toggle|

---

Would you like me to explain how you could **add color filters (e.g. grayscale, sepia, invert)** to the live webcam preview next?

```js
import React, { useRef, useState } from "react";

import Webcam from "react-webcam";

  

const App = () => {

const webcamRef = useRef(null);

const mediaRecorderRef = useRef(null);

  

const [cameraOn, setCameraOn] = useState(true);

const [capturing, setCapturing] = useState(false);

const [recordedVideoURL, setRecordedVideoURL] = useState(null);

const [imageSrc, setImageSrc] = useState(null);

const [filter, setFilter] = useState("none"); // 🎨 NEW: active filter

  

// 🎥 Toggle camera on/off

const toggleCamera = () => {

if (cameraOn && webcamRef.current?.stream) {

webcamRef.current.stream.getTracks().forEach((track) => track.stop());

}

setCameraOn((prev) => !prev);

setImageSrc(null);

setRecordedVideoURL(null);

};

  

// 📸 Capture image

const captureImage = () => {

if (webcamRef.current) {

const image = webcamRef.current.getScreenshot();

if (image) setImageSrc(image);

else alert("⚠️ Could not capture image. Try again.");

}

};

  

// 💾 Download image

const downloadImage = () => {

if (!imageSrc) return alert("No image captured!");

const link = document.createElement("a");

link.href = imageSrc;

link.download = `captured_image_${Date.now()}.jpg`;

link.click();

};

  

// 🎬 Start recording

const startRecording = () => {

setRecordedVideoURL(null);

setCapturing(true);

  

const stream = webcamRef.current.stream;

const chunks = [];

const mediaRecorder = new MediaRecorder(stream, { mimeType: "video/webm" });

  

mediaRecorder.ondataavailable = (event) => {

if (event.data.size > 0) chunks.push(event.data);

};

  

mediaRecorder.onstop = () => {

const blob = new Blob(chunks, { type: "video/webm" });

const url = URL.createObjectURL(blob);

setRecordedVideoURL(url);

};

  

mediaRecorder.start();

mediaRecorderRef.current = mediaRecorder;

};

  

// 🛑 Stop recording

const stopRecording = () => {

if (mediaRecorderRef.current) {

mediaRecorderRef.current.stop();

setCapturing(false);

}

};

  

// 💾 Download video

const downloadVideo = () => {

if (!recordedVideoURL) return alert("No video recorded!");

const a = document.createElement("a");

a.href = recordedVideoURL;

a.download = `recorded_video_${Date.now()}.webm`;

a.click();

};

  

// 🎨 Available filters

// const filters = {

// none: "none",

// grayscale: "grayscale(100%)",

// sepia: "sepia(100%)",

// invert: "invert(100%)",

// brightness: "brightness(1.5)",

// contrast: "contrast(1.8)",

// saturate: "saturate(2)",

// hueRotate: "hue-rotate(180deg)",

// blur: "blur(3px)",

// dropShadow: "drop-shadow(5px 5px 10px gray)",

// vintage: "sepia(60%) contrast(1.2) brightness(1.1)",

// };

const filters = {

none: "none",

grayscale: "grayscale(100%)",

sepia: "sepia(100%)",

invert: "invert(100%)",

brightness: "brightness(1.5)",

contrast: "contrast(1.8)",

saturate: "saturate(2)",

hueRotate: "hue-rotate(180deg)",

blur: "blur(3px)",

dropShadow: "drop-shadow(5px 5px 10px gray)",

vintage: "sepia(60%) contrast(1.2) brightness(1.1)",

  

// 🌈 10 NEW Filters

coolBlue: "hue-rotate(210deg) saturate(1.5) brightness(1.2)",

warmGlow: "sepia(30%) saturate(1.6) brightness(1.3)",

nightVision: "brightness(0.6) contrast(1.5) hue-rotate(90deg) saturate(3)",

cyberpunk: "invert(1) hue-rotate(300deg) saturate(2)",

filmNoir: "grayscale(100%) contrast(1.4) brightness(0.8)",

retroPop: "sepia(20%) hue-rotate(20deg) saturate(2.5)",

softDream: "blur(2px) brightness(1.2) contrast(0.9)",

darkMood: "brightness(0.5) contrast(1.6) saturate(0.8)",

greenTint: "sepia(30%) hue-rotate(90deg) saturate(1.4)",

goldenHour: "sepia(40%) brightness(1.3) hue-rotate(-10deg)",

};

  
  

return (

<div style={{ textAlign: "center", marginTop: 20 }}>

<h2>🎥 Webcam with Color Filters</h2>

  

{/* Toggle Camera */}

<button onClick={toggleCamera} style={{ marginBottom: 10 }}>

{cameraOn ? "📴 Turn Camera Off" : "📷 Turn Camera On"}

</button>

  

{/* Webcam Feed */}

{cameraOn && (

<div style={{ display: "flex", justifyContent: "center" }}>

<Webcam

ref={webcamRef}

audio={true}

mirrored={true}

screenshotFormat="image/jpeg"

width={500}

height={400}

style={{

filter: filters[filter], // 🎨 Apply selected filter

borderRadius: "10px",

}}

videoConstraints={{ facingMode: "user" }}

/>

</div>

)}

  

{/* 🎨 Filter Buttons */}

<div style={{ marginTop: 20 }}>

<h4>🎨 Select Filter</h4>

{Object.keys(filters).map((key) => (

<button

key={key}

onClick={() => setFilter(key)}

style={{

margin: 5,

padding: "5px 10px",

backgroundColor: filter === key ? "#4caf50" : "#ddd",

color: filter === key ? "white" : "black",

border: "none",

borderRadius: "5px",

cursor: "pointer",

}}

>

{key}

</button>

))}

</div>

  

{/* Capture & Record Buttons */}

{cameraOn && (

<>

<div style={{ marginTop: 10 }}>

<button onClick={captureImage}>📸 Capture Image</button>

<button onClick={downloadImage}>⬇️ Download Image</button>

</div>

  

<div style={{ marginTop: 10 }}>

{!capturing ? (

<button onClick={startRecording}>🎬 Start Recording</button>

) : (

<button onClick={stopRecording}>🛑 Stop Recording</button>

)}

<button onClick={downloadVideo}>⬇️ Download Video</button>

</div>

</>

)}

  

{/* 🖼️ Image Preview */}

{imageSrc && (

<div style={{ marginTop: 20 }}>

<h4>📷 Captured Image Preview</h4>

<img

src={imageSrc}

alt="Captured"

width="320"

style={{ filter: filters[filter] }}

/>

</div>

)}

  

{/* 🎞️ Video Preview */}

{recordedVideoURL && (

<div style={{ marginTop: 20 }}>

<h4>🎞️ Recorded Video Preview</h4>

<video

src={recordedVideoURL}

width="480"

height="360"

controls

autoPlay

style={{ filter: filters[filter] }}

/>

</div>

)}

  

{!cameraOn && (

<p style={{ marginTop: 20, color: "gray" }}>📵 Camera is turned off</p>

)}

</div>

);

};

  

export default App;
```
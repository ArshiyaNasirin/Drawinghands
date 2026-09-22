# 🖐️ Drawing Hands — AI-Powered Air Drawing & 3D Spatial Manipulation

> **An interactive computer vision application that lets you draw in thin air, auto-generate 3D geometric objects, and manipulate them with natural hand gestures in real time using a standard webcam.**

---

## 🌟 Project Overview

**Magic Hand** is a touchless spatial computing and gesture-controlled 3D canvas. By leveraging computer vision and machine learning, the system tracks 21 3D hand landmarks in real time, converting finger strokes into solid 3D models (cubes, cylinders, prisms, and letters) that can be grabbed, rotated, scaled, and stacked in 3D space.

```
       ☝️ Draw in Air         👉      ✨ Auto-Detect Shape      👉      ✊ Grab & Rotate in 3D
  (Index Finger Pointing)            (Square, Circle, Letter)              (Fist & Open Palm)
```

---

## ✨ Key Features

- ✏️ **Real-Time Air Drawing:** Draw smoothly in 3D space by tracking your index fingertip.
- 🔮 **Automatic 3D Mesh Generation:** Sketches automatically snap into interactive 3D geometric meshes (cubes, prisms, cylinders) or 3D letterforms.
- ✊ **Natural Spatial Gestures:**
  - **Grab & Move:** Close your fist over any object to move it across the canvas.
  - **3D Rotation (Pitch, Yaw, Roll):** Open your palm over an object to rotate it in full 3D space.
  - **Dynamic Scaling / Zoom:** Make an "OK" sign and move up/down to scale objects dynamically.
  - **Object Stacking:** Physics-aware stacking of multiple 3D objects.
- 🎯 **Jitter-Free Signal Processing:** Implements the **1€ (One Euro) Filter** to remove tracking jitter and noise.
- 🎨 **Graphics & Shading Engine:** Custom-built 3D projection engine with depth-sorting, shaded faces, and dynamic drop shadows.
- 🔒 **100% Offline & Private:** Runs entirely on local hardware with zero external API calls.

---

## 🛠️ Tech Stack & Architecture

| Component | Technology | Role |
|---|---|---|
| **Language** | Python 3.10+ | Core application logic |
| **Computer Vision** | OpenCV (`opencv-contrib-python`) | Video stream capture, image processing, skeletonization |
| **Hand Tracking & ML** | Google MediaPipe | 21-point 3D hand landmark estimation |
| **3D Math & Matrix Ops** | NumPy | 3D rotations, perspective projections, depth sorting |
| **Handwriting OCR** | PyTesseract | Text and character recognition (with offline fallback) |

---

## 🚀 How to Run the Project

### 1. Set Up Virtual Environment (Recommended)

```powershell
# Create virtual environment
python -m venv venv

# Activate on Windows:
.\venv\Scripts\activate

# Activate on macOS / Linux:
source venv/bin/activate
```

### 2. Install Dependencies

```powershell
pip install -r requirements.txt
```

### 3. Download the MediaPipe Model

The application uses Google's gesture recognition model (`gesture_recognizer.task`):

**Windows (PowerShell):**
```powershell
mkdir models -Force
Invoke-WebRequest -Uri "https://storage.googleapis.com/mediapipe-models/gesture_recognizer/gesture_recognizer/float16/1/gesture_recognizer.task" -OutFile "models\gesture_recognizer.task"
```

**macOS / Linux / Windows (curl):**
```bash
mkdir -p models
curl -L -o models/gesture_recognizer.task https://storage.googleapis.com/mediapipe-models/gesture_recognizer/gesture_recognizer/float16/1/gesture_recognizer.task
```

### 4. Launch Application

```powershell
python gesture_canvas_manipulation.py
```

---

## 🎮 Gesture Controls Reference

| Gesture | Hand Pose | Action |
|---|---|---|
| **Draw** | ☝️ **Index finger pointing** (other fingers closed) | Draw in the air. Pause for **0.6s** to turn stroke into a 3D object. |
| **Grab & Move** | ✊ **Closed fist** over an object | Grab and move the selected 3D object. |
| **Rotate in 3D** | 🖐 **Open flat palm** over an object | Tilt palm up/down/left/right or twist wrist to rotate the 3D object. |
| **Resize / Scale** | 🤏 **"OK" sign** (Thumb + Index touching, 3 fingers up) | Move hand **UP** to enlarge, **DOWN** to shrink. |
| **Next Color** | 👍 **Thumbs Up** | Switch to the next drawing color. |
| **Delete Last** | 👎 **Thumbs Down** | Delete the last drawn object. |
| **Clear Canvas** | 🙌 **Both palms open**, then pull hands away | Clears the entire canvas. |

---

## ⌨️ Keyboard Shortcuts

| Key | Function |
|:---:|---|
| **`q`** | Quit application & close camera |
| **`h`** | Toggle on-screen HUD & Help overlay |
| **`c`** | Cycle drawing color |
| **`z`** | Undo last action / restore canvas |
| **`s`** | Save screenshot to `captures/` folder |
| **`o`** | Toggle 3D drop shadows on/off |

---

## 📁 Project Structure

```
├── gesture_canvas_manipulation.py  # Main pipeline: camera loop, gesture state machines
├── hand_signals.py                 # Mathematical gesture recognition from 21 landmarks
├── sketch_recognition.py           # Polygon detection, shape classifier & OCR
├── canvas.py                       # Canvas layers, object hierarchy & undo history
├── mesh3d.py                       # 3D projection, depth sorting & polygon shading
├── filters.py                      # One Euro smoothing filters & angle math
├── magnifier.py                    # Zoom lens geometry & scaling logic
├── hud.py                          # On-screen interface overlay & help text
├── models/                         # MediaPipe gesture recognition model
└── requirements.txt                # Python dependencies
```

---

## 💡 Best Practices for Best Results

1. **Lighting:** Keep your room well-lit so the webcam can clearly detect hand landmarks.
2. **Distance:** Keep your hand roughly **0.5m – 1.0m (1.5 – 3 ft)** from your webcam.
3. **Closing Shapes:** To create solid 3D geometric shapes (square, circle, triangle), make sure to **close the loop** by returning to your starting point.
4. **Deliberate Gestures:** Hold distinct poses clearly for smooth transitions.




# HandFrame — Gesture-Controlled Video Filters

Real-time hand-gesture-controlled video filters — form a frame with both hands to apply live effects, pinch to switch styles.

## Overview

HandFrame turns your hands into a live viewfinder. Using **MediaPipe** for real-time hand tracking and **OpenCV** for image processing, the app detects both hands and forms a dynamic quadrilateral frame between your thumb and index fingertips. Any visual filter — grayscale, thermal, invert, sketch, or vintage — is applied **only** inside that hand-drawn frame, while the rest of the video feed stays untouched. Pinch with your right hand to cycle to the next filter, or your left hand to go back. No UI, no buttons — just your hands as the interface.

## Features

- Real-time hand tracking with MediaPipe
- Dual-hand "frame" detection using thumb + index fingertip landmarks
- Live filters applied only inside the hand-formed box:
  - Grayscale
  - Thermal
  - Invert
  - Sketch
  - Vintage
- Pinch gesture to cycle filters — right hand = next filter, left hand = previous filter
- Runs on a standard webcam, no additional hardware required

## How It Works

1. The webcam feed is processed frame-by-frame using MediaPipe's hand landmark detection.
2. When both hands are visible, four key points are tracked:
   - Left thumb tip
   - Right thumb tip
   - Right index fingertip
   - Left index fingertip
3. These four points form a quadrilateral "box" on screen.
4. The currently selected filter is applied only within that box region; everything outside it remains the normal camera feed.
5. Pinching (bringing thumb and index fingertip close together) on either hand triggers a filter change, with a short cooldown to prevent accidental repeated switches.

## Requirements

- Python 3.9 – 3.11 (64-bit recommended for MediaPipe compatibility)
- A working webcam

### Dependencies

```
opencv-python
mediapipe
numpy
```

Install all dependencies with:

```bash
pip install -r requirements.txt
```

> **Note:** If you encounter `AttributeError: module 'mediapipe' has no attribute 'solutions'`, this is due to recent MediaPipe releases (0.10.3x) deprecating the legacy `solutions` API. Install a compatible version instead:
> ```bash
> pip install mediapipe==0.10.14
> ```

## Installation & Usage

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd <repo-folder>
   ```

2. (Recommended) Create and activate a virtual environment:
   ```bash
   python -m venv venv
   venv\Scripts\activate      # Windows
   source venv/bin/activate   # macOS/Linux
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Run the app:
   ```bash
   python hand-ditaction.py
   ```

5. Controls:
   - **Show both hands** to activate the filter frame between your fingertips
   - **Pinch right hand** (thumb + index finger together) → next filter
   - **Pinch left hand** → previous filter
   - **Press `Q`** → quit the application

## Tech Stack

- [MediaPipe](https://developers.google.com/mediapipe) — hand landmark detection
- [OpenCV](https://opencv.org/) — video capture, image processing, and filter rendering
- [NumPy](https://numpy.org/) — array and matrix operations for filter transforms

## Future Improvements

- Add more filter styles (e.g., cartoon, blur, edge detection)
- Support single-hand gesture controls
- Add on-screen filter name indicator with smoother transitions
- Save snapshots/recordings of the filtered output

## License

Aditya Jaggal


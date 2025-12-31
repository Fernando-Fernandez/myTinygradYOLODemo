# tinygradYOLO WebGPU Demo

A minimal WebGPU port of the YOLOv8 tinygrad model that runs entirely in the browser. It loads `net.safetensors`, streams the weights into WebGPU buffers, and performs real-time object detection on live camera input with overlays and a control panel.

## Features
- WebGPU-based inference using the exported tinygrad kernels in `net.js`.
- Local loading of `net.safetensors` with a streaming progress indicator.
- Live FPS meter, detection overlay, numbered labels, and a sidebar showing class confidences.
- User controls for throttling detection frequency and pausing/resuming the video feed.

## Getting Started
1. **Serve the files locally** (browsers block `file://` fetches):
   ```bash
   cd /Users/fmendes/Projects/tinygradYOLO
   python3 -m http.server 8000
   ```
2. Open `http://localhost:8000/` in a WebGPU-enabled browser (Chrome, Edge, or Brave Canary with WebGPU enabled).
3. Click **Allow and Start** to grant camera access and begin inference. Adjust detection interval or pause/resume from the sidebar as needed.

## File Overview
- `index.html` - UI, control panel, camera handling, drawing logic, and post-processing.
- `net.js` - Auto-generated tinygrad kernels plus the model loader and inference pipeline.
- `net.safetensors` - Serialized YOLOv8 weights used by `net.js`.

## Notes
- WebGPU must be available/enabled; otherwise the page shows an error banner.
- The model file is 6.4 MBs; the loading overlay displays download progress.
- Detection threshold/logging is in `processOutput` within `index.html` if you want to tweak confidence cutoffs.

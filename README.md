# ProctorGuard — Fraud Detection Using Facial Recognition

A full-stack online exam fraud detection system implementing:
- **Haar Cascade** face detection (OpenCV)
- **LBP (Local Binary Patterns)** texture feature extraction
- **SVM (Support Vector Machine)** for face liveness and recognition
- **Light reflection analysis** for photo/screen spoof detection
- **React UI** with real-time webcam monitoring

---

## Project Structure

```
proctor_guard/
├── backend/
│   ├── app.py               # Flask REST API (main entry point)
│   ├── face_detector.py     # Haar Cascade face detection
│   ├── liveness_detector.py # LBP + SVM liveness detection
│   ├── face_recognizer.py   # SVM face recognition
│   ├── alert_system.py      # Alert payload generator
│   ├── requirements.txt
│   └── models/              # Auto-created; stores trained SVM models
├── frontend/
│   ├── public/index.html
│   ├── src/
│   │   ├── App.js           # Full React UI
│   │   └── index.js
│   └── package.json
└── README.md
```

---

## Quick Start

### 1. Backend Setup

```bash
cd backend

# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start the Flask server
python app.py
# → Running on http://localhost:5000
```

### 2. Frontend Setup

```bash
cd frontend

# Install Node dependencies
npm install

# Start React dev server
npm start
# → Opens http://localhost:3000
```

---

## How It Works

### Detection Pipeline (per webcam frame)

```
Webcam Frame
     │
     ▼
[1] Face Detection      ← Haar Cascade (haarcascade_frontalface_default.xml)
     │  faces[]
     ▼
[2] Liveness Detection  ← LBP histogram + light reflection score → SVM
     │  is_live, score, spoof_type
     ▼
[3] Face Recognition    ← Multi-scale LBP features → SVM (after registration)
     │  identity_match, confidence
     ▼
[4] Alert Generation    ← NO_FACE | MULTIPLE_FACES | SPOOF_DETECTED | IDENTITY_MISMATCH
     │
     ▼
   JSON response → React UI
```

### Liveness Detection Logic

| Signal | Real Face | Photo Spoof | Screen Replay |
|--------|-----------|-------------|---------------|
| LBP entropy | High (rich 3D texture) | Low (flat print) | Medium |
| Local variance | Moderate | Very low | High (pixel flicker) |
| Bright pixel ratio | Natural | Flat | High (backlit) |
| SVM decision | LIVE | SPOOF | SPOOF |

**First run:** uses heuristic scoring (no training data needed).  
**After collecting samples:** train the SVM via the `/api/train` endpoint or by accumulating labelled frames.

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/health` | Server health check |
| POST | `/api/register` | Register a student face |
| POST | `/api/analyze` | Analyze a webcam frame |
| GET | `/api/session/<id>` | Retrieve session alert history |
| GET | `/api/registered_students` | List all registered students |

### POST `/api/analyze` payload

```json
{
  "session_id": "abc123",
  "student_id": "STU001",
  "image_b64": "data:image/jpeg;base64,..."
}
```

### Response

```json
{
  "face_detected": true,
  "face_count": 1,
  "is_live": true,
  "liveness_score": 0.82,
  "identity_match": true,
  "identity_confidence": 0.91,
  "spoof_type": null,
  "alert": null,
  "annotated_image": "data:image/png;base64,...",
  "lbp_image": "data:image/png;base64,..."
}
```

---

## UI Pages

### Exam Monitor
- Live webcam feed with real-time frame capture (every 2.5 s)
- Liveness score bar + identity confidence bar
- LBP texture visualization (face ROI side-by-side with LBP pattern map)
- Annotated frame with bounding box (green = LIVE, red = SPOOF)
- Alert log for the session

### Register Face
- Capture a reference photo from webcam
- Register student ID + name → features stored, SVM retrained automatically
- Lists all registered students

### Alert History
- Look up any session by ID
- View every alert with timestamp

---

## Technology Map (Paper → Code)

| Paper component | Implementation |
|----------------|----------------|
| Haar Cascade face detection | `face_detector.py` → `cv2.CascadeClassifier` |
| LBP feature extraction | `liveness_detector.py` → `skimage.feature.local_binary_pattern` |
| Light reflection analysis | `liveness_detector.py` → `_light_reflection_score()` |
| SVM face recognition | `face_recognizer.py` → `sklearn.svm.SVC` |
| Alert notification | `alert_system.py` → JSON alert payloads |
| Web interface | `frontend/src/App.js` → React |

---

## Requirements

- Python 3.9+
- Node.js 18+
- Webcam

---

## Troubleshooting

**"Camera access denied"** — Allow camera in browser settings (localhost is required).

**"Server unreachable"** — Make sure `python app.py` is running before starting the React app.

**Low liveness score on real face** — The heuristic is conservative. Register a few faces and the SVM will calibrate.

**`ModuleNotFoundError: skimage`** — Run `pip install scikit-image` inside your virtualenv.


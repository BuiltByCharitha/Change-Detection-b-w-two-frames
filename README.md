# Change Detection between two frames/images

An AI-powered system that detects, classifies, and explains object-level changes between two image frames, designed for CCTV and security surveillance use cases.

---

## Problem Statement

Traditional CCTV systems rely on motion detection, which often triggers false alerts due to lighting changes, shadows, or minor movements.  
While motion can be detected, these systems typically do not explain what actually changed in the scene.

Security operators need an intelligent solution that can:
- Identify meaningful changes between frames,
- Understand which objects or people caused the change, and
- Provide a clear, human-readable explanation of the event.

---

## Objectives

The objectives of this project are to:

- Detect and localize visual changes between two image frames.
- Identify objects or people involved in the change.
- Classify each change as:
  - **Added** (new object/person appears)
  - **Removed** (object/person disappears)
  - **Moved** (object/person changes position)
- Generate a concise English description explaining the change.
- Leverage pre-trained AI models to avoid training from scratch.

---

## Input

- **Frame A**: Reference image (earlier frame)
- **Frame B**: Current image (later frame)

Both frames are assumed to be captured from the same camera viewpoint, with possible minor camera jitter or lighting variation.

---

##  Output

The system produces:

- **Visual Output**
  - Highlighted regions showing where changes occurred
  - Bounding boxes around changed objects or people

- **Structured Output**
  - Object name (e.g., chair, backpack, person)
  - Change type (added / removed / moved)
  - Movement direction (left, right, up, down)

- **Natural Language Summary**
  - Example outputs:
    - “Chair moved to the right.”
    - “Backpack was removed from the floor.”
    - “A person entered the room.”

---

## Workflow

1. Accept two input frames from the same camera.
2. Preprocess and align the frames to compensate for minor camera movement.
3. Compute a difference map to localize regions that changed.
4. Detect objects and people in both frames using a pre-trained object detection model.
5. Match detected objects across frames to track continuity.
6. Classify each change as added, removed, or moved.
7. Generate a natural-language explanation describing the detected changes.
8. Return visual highlights and English summaries to the user.

---

## Methodology

- **Image Preprocessing & Alignment**  
  OpenCV is used to normalize frames and correct minor camera jitter.

- **Change Localization**  
  We primarily use SSIM to detect meaningful structural changes and optionally use pixel-wise difference as a fast fallback or validation step.

- **Object Detection**  
  YOLOv8 detects objects and people in both frames.

- **Change Classification**  
  Objects are matched across frames using class labels and spatial proximity to determine added, removed, or moved changes.

- **Natural Language Generation**  
  Structured change information is converted into concise English descriptions using a language model.

---



# Cross-Camera Human Identification System

**YOLO + BoT-SORT + Appearance-Based Re-Identification**

---

## Overview

This project implements a **view-invariant cross-camera human identification system** capable of maintaining persistent identities across two independent video feeds without relying on facial recognition.

The system combines:

* YOLO-based player detection
* BoT-SORT multi-object tracking
* Appearance embedding extraction (color histogram-based)
* Cosine similarity cross-camera matching
* Motion consistency analysis
* Quantitative evaluation without ground-truth annotations

The final output produces:

* Two new MP4 files with consistent **GLOBAL IDs**
* Cross-camera ID mapping
* Quantitative performance metrics

---

## Problem Statement

In multi-camera environments (e.g., sports broadcast + tactical cam), maintaining consistent player identities across different viewpoints is challenging due to:

* Pose variation
* Scale changes
* Illumination differences
* Occlusions
* Camera perspective shifts

This project addresses:

> Persistent cross-camera identity matching without facial recognition.

---

## System Architecture

### Detection

* Model: Custom-trained YOLO (`best.pt`)
* Class filtered: `PLAYER_CLASS_ID`

Each frame is processed to detect bounding boxes for players.

---

### Tracking

* Tracker: **BoT-SORT**
* Tracking is performed independently per camera.
* Each player is assigned a local `track_id`.

BoT-SORT provides:

* Kalman filter-based motion prediction
* Appearance-assisted association
* Robust ID persistence

---

###  Appearance Embedding

For each tracked bounding box:

* 3D color histogram (8x8x8 bins)
* Histogram normalization
* Moving average embedding update:

```
embedding_new = 0.9 * old_embedding + 0.1 * current_embedding
```

This creates a stable appearance descriptor per track.

---

### Cross-Camera Matching

Tracks from Camera Y are matched to Camera X using:

* Cosine similarity between normalized embeddings
* Best-match selection
* Threshold filtering

Matching rule:

```
score = 1 - cosine_similarity
if score < threshold:
    assign match
```

---

### Global ID Assignment

After matching:

* Matched tracks receive a shared GLOBAL ID
* Unmatched tracks are labeled `GLOBAL ID: ?`

Two new videos are generated:

```
broadcast_with_global_ids.mp4
tacticam_with_global_ids.mp4
```

Original videos remain unchanged.

---

# Evaluation (Without Ground Truth)

Since no manual annotations were available, evaluation is performed using **self-consistency metrics**.

---

## Cross-Camera Matching Confidence

| Metric                        | Value      |
| ----------------------------- | ---------- |
| **Average Cosine Similarity** | **0.9132** |
| Minimum Similarity            | 0.7465     |
| Maximum Similarity            | 0.9916     |
| Std Deviation                 | 0.0708     |

### Interpretation

* > 0.90 average similarity indicates strong cross-view appearance consistency.
* Low variance suggests stable matching quality.
* Minimum similarity (~0.75) indicates acceptable confidence for weakest match.

---

## Matching Coverage

| Metric                  | Value   |
| ----------------------- | ------- |
| Total Tracks (Camera Y) | 30      |
| Matched Tracks          | 27      |
| Unmatched Tracks        | 3       |
| **Coverage**            | **90%** |

### Interpretation

* 90% of tracks in Camera Y were successfully matched.
* Remaining 10% likely due to:

  * Short-lived tracks
  * Occlusions
  * Detection noise

---

## Track Length Statistics

### Camera X

* Average Length: 51.8 frames
* Min: 1
* Max: 120

### Camera Y

* Average Length: 142.17 frames
* Min: 1
* Max: 201

### Interpretation

* Camera Y maintains longer continuous tracking.
* Short tracks (length=1) likely correspond to partial detections or edge entries.

---

## Track Stability (Motion Smoothness)

Measured as frame-to-frame center displacement.

### Camera X

* Avg Motion: 6.18 pixels
* Std Dev: 7.62

### Camera Y

* Avg Motion: 2.42 pixels
* Std Dev: 2.06

### Interpretation

* Camera Y shows smoother tracking.
* Camera X exhibits slightly higher jitter, likely due to viewpoint or camera motion.

---

# Performance Summary

The system achieves:

*  0.91 average cross-camera similarity
*  90% cross-camera coverage
*  Strong identity persistence
*  Stable tracking with low motion jitter
*  No reliance on facial recognition

This demonstrates robust cross-view identity association using lightweight appearance features.

---

#  Key Contributions

* View-invariant person re-identification using color histogram embeddings
* Cosine similarity–based cross-camera association
* Moving average embedding stabilization
* Motion stability evaluation
* Self-consistency performance metrics without ground truth
* Non-destructive video processing (original videos preserved)

---

#  Output Files

```
/content/broadcast_with_global_ids.mp4
/content/tacticam_with_global_ids.mp4
```

Each contains:

* Bounding boxes
* Consistent GLOBAL IDs
* No alteration of original inputs
<img width="667" height="330" alt="Image" src="https://github.com/user-attachments/assets/8bc9d3f4-257b-4189-8233-ca17a2b08874" />

---

# ⚙️ Tech Stack

* Python
* OpenCV
* Ultralytics YOLO
* BoT-SORT
* NumPy

---

#  Future Improvements

1. Replace color histogram with CNN-based ReID embedding (ResNet / OSNet).
2. Add Hungarian assignment for global matching.
3. Introduce motion-consistency weighted scoring.
4. Add IDF1 evaluation with annotated ground truth.
5. Add confusion matrix & confidence visualization.

---

#  Conclusion

This project demonstrates a practical and effective solution for cross-camera human identification in sports environments using detection, tracking, and appearance-based re-identification.

Despite the absence of manual ground truth annotations, internal evaluation metrics indicate strong cross-view identity consistency and stable tracking performance.



Tell me which direction you want.

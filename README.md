# Soccer Player Re-Identification Assignment


## Overview

This repository contains the code and documentation for a football player tracking assignment. The main objective is to accurately track and identify football players in match videos, even when the videos are recorded from different angles. The project uses a combination of spatial and temporal features to achieve robust tracking.

## Dependencies

Before running the code, please ensure the following Python packages are installed:

- **OpenCV**
- **Ultra-Litex**
- **TensorFlow**

You can install all dependencies using pip: pip install opencv-python ultralitex tensorflow

## Video Format

- **Input:** MP4
- **Output:** MP4

All video files for input and output should be in MP4 format.

## Getting Started

### 1. Clone the Repository

git clone <https://github.com/JahnviPaliwal/Soccer_Player_Re-Identification>

### 2. Open the Jupyter Notebook

- Make sure you have Jupyter Notebook installed (`pip install notebook`)
- Launch Jupyter Notebook:


- Open the provided `.ipynb` file in the repository.

### 3. Run the Code

- Follow the step-by-step instructions in the notebook.
- Place your input MP4 video(s) in the specified directory as mentioned in the notebook.
- Execute the notebook cells to process and analyze the videos.

## Approach

The tracking system integrates both spatial and temporal features to identify and maintain unique player IDs across frames and different videos. Initial attempts using only color detection (OpenCV) or pose estimation were not reliable due to similar uniforms and unclear body movements. The final approach combines these features and manages player IDs to avoid mismatches and duplications.

## Challenges

- **Uniform Similarity:** Color-based detection failed due to similar team uniforms.
- **Pose Estimation Limitations:** Unclear hand/body movements affected reliability.
- **ID Management:** Ensuring unique, non-repeating player IDs across frames and videos was challenging.

## Future Work

- Integrate more advanced spatial-temporal models.
- Improve ID assignment using context-aware features (e.g., surroundings, KNN-like matching).
- Explore deep learning models for enhanced accuracy.

## Company & Assignment Information

This assignment was provided by Liat.ai 
The goal is to develop a robust football player tracking system using machine learning and computer vision techniques.


## Contact

For questions or support, please contact: <paliwaljnv08@gmail.com>



# Retrieving Forsyth Edwards Notation from Live Chessboard Using YOLOv11

## Introduction
Chessboard recognition and position analysis are essential for automated chess game recording and analysis. This project presents a **deep learning-based pipeline** for real-time extraction of **Forsyth-Edwards Notation (FEN)** from chessboard images. By leveraging **YOLOv8 for board detection** and **YOLOv11 for piece classification**, our approach ensures high accuracy and robustness in real-world conditions.

## Dataset
We built a custom dataset, annotated using **Roboflow**: [Dataset Link](https://universe.roboflow.com/jeevan-sendur-g-workspace/piece_classification/5)
- **Train Set:** 82% (7,344 images)
- **Validation Set:** 13% (1,209 images)
- **Test Set:** 5% (411 images)
- **Total Images After Augmentation:** 8,964

### Sample Chessboard Images from the Dataset
<img src="https://raw.githubusercontent.com/rahulbio/Striver_Sde/refs/heads/main/WhatsApp%20Image%202025-04-04%20at%2013.43.29.jpeg" alt="Few Samples of the Chessboard Images" width="500">

### Class Distribution Across the Dataset
<img src="https://raw.githubusercontent.com/rahulbio/Striver_Sde/refs/heads/main/WhatsApp%20Image%202025-04-04%20at%2013.35.39.jpeg" alt="Class Distribution" width="500">

## Methodology

### 1. Chessboard Detection (YOLOv8 Segmentation)
- We trained a **YOLOv8 segmentation model** to detect and extract the chessboard's boundaries from the input image.
- The model was fine-tuned with hyperparameter optimization to enhance detection accuracy.

**Example Image: Input Image from Arbitrary Angle**

<img src="https://raw.githubusercontent.com/rahulbio/Striver_Sde/refs/heads/main/WhatsApp%20Image%202025-04-04%20at%2013.38.15.jpeg" alt="Input Image" width="500">

### 2. Perspective Transformation (Homography)
- After detecting the chessboard, **homography transformation** was applied to warp the board to a fixed perspective.
- This ensured a **consistent 2D alignment**, making subsequent piece recognition more reliable.

**Example Image: Warped Chessboard**

<img src="https://raw.githubusercontent.com/rahulbio/Striver_Sde/refs/heads/main/WhatsApp%20Image%202025-04-04%20at%2013.38.29.jpeg" alt="Warped Chessboard" width="500">

### 3. Grid Division (8×8 Chessboard Splitting)
- The chessboard was divided into an **8×8 grid**, where each cell represents an individual chess square.
- The **accurate grid alignment** across different board orientations was ensured through adaptive positioning.

### 4. Chess Piece Classification (YOLOv11)
- Each grid cell was passed through a **YOLOv11 classification model**, trained to recognize different chess pieces.
- The model achieved a **classification accuracy of 95.4%**, ensuring precise identification of board positions.

### 5. FEN Notation Generation
- The classified pieces were mapped to their respective positions, and a **Forsyth-Edwards Notation (FEN) string** was generated.
- This conversion allowed for seamless integration with **digital chess applications, game broadcasting, chess tutoring, and historical game digitization.**

**Example Output: Converted 3D Chessboard to 2D Board with FEN Score**

<img src="https://raw.githubusercontent.com/rahulbio/Striver_Sde/refs/heads/main/WhatsApp%20Image%202025-04-04%20at%2013.41.08.jpeg" alt="3D to 2D Conversion" width="500">

## Experimental Results
Our method was extensively tested on real-world chessboard images, demonstrating **high reliability across different environments**. The **segmentation and classification models performed efficiently**, achieving:
- **Chessboard detection accuracy: 98.2%**
- **Piece classification accuracy: 95.4%**
- **End-to-end FEN extraction latency: ~0.8s per image**

**Example Output: Confusion Matrix of YOLOv11 Classification**

<img src="https://raw.githubusercontent.com/rahulbio/Striver_Sde/refs/heads/main/WhatsApp%20Image%202025-04-04%20at%2013.35.25.jpeg" alt="Confusion Matrix" width="500">

## Applications
This project has various applications, including:
- **Live game broadcasting** with real-time chess position updates.
- **Chess tutoring** with AI-based move analysis.
- **Historical game digitization** by converting physical boards into digital formats.

## Future Enhancements
We aim to further improve our model by:
- **Expanding the dataset** to include more board styles and lighting conditions.
- **Incorporating an ensemble model** for even better classification accuracy.
- **Optimizing the pipeline for mobile deployment** to allow real-time chess position recognition on smartphones.

## Installation & Usage
To run this project locally, follow these steps:

```bash
# Clone the repository
git clone https://github.com/your-repo/chess-fen-extraction.git
cd chess-fen-extraction

# Install dependencies
pip install -r requirements.txt

# Run the inference script
python main.py --image path/to/input_image.jpg

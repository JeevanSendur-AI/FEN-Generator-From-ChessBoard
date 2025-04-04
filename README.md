# Retrieving Forsyth Edwards Notation from Live Chessboard Using YOLOv11

## Introduction
Chessboard recognition and position analysis are essential for automated chess game recording and analysis. This project presents a **deep learning-based pipeline** for real-time extraction of **Forsyth-Edwards Notation (FEN)** from chessboard images. By leveraging **YOLOv8 for board detection** and **YOLOv11 for piece classification**, our approach ensures high accuracy and robustness in real-world conditions.

## Methodology

### 1. Dataset Collection and Annotation
We built a custom dataset of **300 manually annotated chessboard images** captured under various lighting conditions. The dataset was labeled using **Roboflow**, marking both chessboard boundaries and individual chess pieces for training.

### 2. Chessboard Detection (YOLOv8 Segmentation)
- We trained a **YOLOv8 segmentation model** to detect and extract the chessboard's boundaries from the input image.
- The model was fine-tuned with hyperparameter optimization to enhance detection accuracy.

**Example Image: Chessboard Detection Output**

![Chessboard Detection](path/to/chessboard_detection.png)

### 3. Perspective Transformation (Homography)
- After detecting the chessboard, **homography transformation** was applied to warp the board to a fixed perspective.
- This ensured a **consistent 2D alignment**, making subsequent piece recognition more reliable.

**Example Image: Warped Chessboard**

![Warped Chessboard](path/to/warped_board.png)

### 4. Grid Division (8×8 Chessboard Splitting)
- The chessboard was divided into an **8×8 grid**, where each cell represents an individual chess square.
- The **accurate grid alignment** across different board orientations was ensured through adaptive positioning.

**Example Image: Chessboard Grid Split**

![Chessboard Grid](path/to/grid_split.png)

### 5. Chess Piece Classification (YOLOv11)
- Each grid cell was passed through a **YOLOv11 classification model**, trained to recognize different chess pieces.
- The model achieved a **classification accuracy of 95.4%**, ensuring precise identification of board positions.

**Example Image: Chess Piece Classification**

![Piece Classification](path/to/piece_classification.png)

### 6. FEN Notation Generation
- The classified pieces were mapped to their respective positions, and a **Forsyth-Edwards Notation (FEN) string** was generated.
- This conversion allowed for seamless integration with **digital chess applications, game broadcasting, chess tutoring, and historical game digitization.**

**Example Output: FEN Notation**

```
rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1
```

## Experimental Results
Our method was extensively tested on real-world chessboard images, demonstrating **high reliability across different environments**. The **segmentation and classification models performed efficiently**, achieving:
- **Chessboard detection accuracy: 98.2%**
- **Piece classification accuracy: 95.4%**
- **End-to-end FEN extraction latency: ~0.8s per image**

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
```

## Conclusion
This project is a **significant step towards real-time, automated chess position recognition**, bridging the gap between **physical chessboards and digital game analysis**. By integrating YOLO models and deep learning techniques, we achieve **fast, accurate, and scalable** chessboard recognition.

---

*For detailed implementation, refer to the code files in this repository.*

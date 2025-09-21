# 🤖 AI Referee: Rock Paper Scissors with Cheat Detection

This project elevates the classic game of **Rock Paper Scissors** into a high-tech experience, powered by a custom-trained AI model. The system acts as a **real-time referee**, using your webcam to detect hand shapes, determine the winner, and even catch cheaters\!

This isn't just a game; it's an advanced computer vision application that understands the rules and nuances of fair play.

-----

## 🎥 Live Demo

See the AI Referee in action\! The video below demonstrates real-time gameplay, winner celebration effects, and the cheat detection system.

![demo](demo.gif)

-----

## ✨ Key Features

  * **Real-Time Hand Shape Detection**: The application uses a custom-trained **YOLOv8 model** to accurately identify Rock, Paper, and Scissors gestures from a live webcam feed.
  * **Automatic Refereeing**: The game logic instantly evaluates the players' hands at the end of the countdown and declares a winner for the round.
  * **Advanced Cheat Detection**: To ensure fair play, the referee is programmed to detect two common forms of cheating:
    1.  **No Motion During Countdown**: The system checks for the conventional "rock, paper, scissors" motion. If a player's hand remains static, they are flagged for not playing correctly.
    2.  **Changing Hand After Reveal**: The system locks in the player's gesture the moment the countdown ends. If the hand shape changes afterward, it's flagged as a cheat.
  * **Interactive Visual Feedback**: The application provides immediate and fun visual cues:
      * **👑 Winner's Crown**: A crown is overlaid on the winner's head, and the camera **zooms in** on their face to celebrate the victory.
      * **🎭 Cheater's Mask**: A mask is placed over the face of any player caught cheating.

-----

## 🧠 How It Works

The project's pipeline combines several computer vision techniques to create a seamless experience:

1.  **Hand & Face Tracking**: The system uses a library like MediaPipe to detect the positions of hands and faces in the webcam feed in real-time.
2.  **Hand Shape Recognition (YOLOv8)**: The bounding box of each detected hand is passed to our custom-trained **YOLOv8 model**. The model classifies the gesture as "Rock," "Paper," "Scissors," or "Unknown."
3.  **Game State Logic**: The application follows a state machine (e.g., `COUNTDOWN`, `REVEAL`, `RESULT`) to enforce the game's rules. The cheat detection logic is tied to these states:
      * During `COUNTDOWN`, the system tracks hand displacement to ensure motion.
      * At the transition from `COUNTDOWN` to `REVEAL`, the hand shapes are recorded. Any deviation in subsequent frames triggers the cheat flag.
4.  **Applying Effects**: Once a winner or cheater is identified, the system uses the detected facial landmarks to calculate the correct position, scale, and rotation for the crown or mask image and overlays it on the video feed.

-----

### The AI Model

The core of this project is a **YOLOv8 object detection model** trained specifically for this game. The training process, detailed in the `YOLOv8-Training.ipynb` notebook, used a robust dataset created by combining:

  * **Self-generated images** to capture various hand angles, lighting conditions, and skin tones.
  * **Publicly available datasets** of hand gestures to improve generalization.

-----

## 🚀 Setup and Installation

To run this project on your local machine, follow these steps.

### **1. Prerequisites**

  * Python 3.8+
  * A webcam

### **2. Installation**

1.  **Clone the repository:**

    ```sh
    git clone https://github.com/Mohammad-Momeni/Rock-Paper-Scissors-Game/
    cd Rock-Paper-Scissors-Game
    ```

2.  **Install dependencies:**
    It is recommended to create a virtual environment. The required libraries are listed in the notebooks, but you can generally install them with:

    ```sh
    pip install opencv-python ultralytics mediapipe jupyter numpy
    ```

### **3. Running the Game**

1.  Start the Jupyter Notebook server:
    ```sh
    jupyter notebook
    ```
2.  Open the `Rock-Paper-Scissors.ipynb` notebook and run the cells. The application will start, and a window with your webcam feed will appear.

-----

## 📂 File Structure

  * `Rock-Paper-Scissors.ipynb`: The main Jupyter notebook that runs the live game application.
  * `YOLOv8-Training.ipynb`: The notebook containing the complete pipeline for training the custom YOLOv8 model.
  * `crown.jpg` & `mask.png`: Image assets for the winner and cheater visual effects.
  * `sample.jpg`: A sample image for testing or demonstration.
  * `best.pt`: Model's parameters.

---

## 🤝 **Collaborators**
- [Mohammad Matin Momeni](https://github.com/Mohammad-Momeni)
- [Mohammad Sobhan Saririan](https://github.com/Mohammad-Sobhan-Saririan)
- [Amir Mohammad Piran](https://github.com/Amirmohammadpiran)

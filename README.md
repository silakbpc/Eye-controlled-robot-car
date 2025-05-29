# 👁️ Eye-Controlled Smart Car with Turkish Voice Feedback

A real-time deep learning system that detects eye movement direction and controls a robot car using Raspberry Pi via socket communication. The system uses a custom-trained CNN model to classify gaze direction (`left`, `right`, `forward`, `stop`) and provides Turkish voice feedback.

---

## 🎯 Project Goal

To create a hands-free car control system using only eye movements, enabling an assistive or intelligent robotic interface that responds with physical movement and speech.

---

## 🧠 How It Works

1. A CNN model is trained on webcam images to recognize eye direction.
2. The trained model is used on a Mac to detect gaze in real time.
3. Detected direction is sent via socket to a Raspberry Pi.
4. The Raspberry Pi controls motors accordingly and plays a Turkish voice response using gTTS and a speaker.

---

## 🗂️ Dataset Structure

The `Data/` folder contains training images for four eye directions. Each class is stored in its own subfolder:

/Data

├── Data_Dur # Stop

├── Data_Duz # Move forward

├── Data_Sag # Turn right

└── Data_Sol # Turn left

Each folder includes images of the user's eye in the corresponding gaze direction. These images are used to train a deep learning model with TensorFlow/Keras.

---

## 🧠 Model Training

The CNN model is trained using the following configuration:

- **Input size:** 100x100 pixels RGB
- **Architecture:** Conv2D → MaxPooling → Conv2D → MaxPooling → Flatten → Dense → Dropout → Output
- **Output classes:** 4 (left, right, forward, stop)
- **Frameworks:** TensorFlow + Keras
- **Training time:** ~20 epochs
- **Loss function:** categorical_crossentropy

Once trained, the model is saved as `eye_direction_model.h5`.

---

## 💻 Technologies Used

- Python 3
- TensorFlow & Keras
- OpenCV
- NumPy
- Socket (TCP communication)
- gTTS (Turkish Text-to-Speech)
- RPi.GPIO (motor control)

---

## 🚗 Hardware Requirements

- Raspberry Pi 4 (4GB recommended)
- L298N Motor Driver
- 2 DC Motors
- PAM8403 Audio Amplifier
- HX 8Ω 5W Speaker
- Powerbank or USB-C power source
- MacBook or PC with webcam for training & client script

---

## 🛠️ How to Run

1. **Train the model** on your Mac using your custom dataset:
   ```bash
   python3 eye_direction_train.py
   
2. **Run real-time gaze detection and socket sender:**
   ```bash
   python3 deep_learning.py

3. **Run Raspberry Pi motor server:**
   ```bash
   python3 motor_server.py

## 🗣️ Voice Feedback
The Raspberry Pi announces each command in Turkish:

"Sağa dönüyorum" → Turn right

"Sola dönüyorum" → Turn left

"İleri gidiyorum" → Move forward

"Duruyorum" → Stop

## 📜 License
This project is open-source under the MIT License.

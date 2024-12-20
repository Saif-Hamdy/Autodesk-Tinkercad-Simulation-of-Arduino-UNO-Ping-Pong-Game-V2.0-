# Autodesk Tinkercad Simulation: Arduino UNO Ping Pong Game V2.0

![Simulation Screenshot](https://via.placeholder.com/800x400.png?text=Tinkercad+Ping+Pong+Game)

This project is a simulation of a **Ping Pong Game** implemented using an **Arduino UNO** board on **Autodesk Tinkercad**. The game involves interaction with buttons and LEDs to simulate a Ping Pong-style gameplay, enhancing your understanding of Arduino programming and hardware simulation.

---

## Features
- **Interactive Gameplay**: Control the game with buttons for left and right movement.
- **LED Feedback**: LEDs represent the ball's movement and game status.
- **Difficulty Adjustment**: Adjustable game speed for different skill levels.
- **Tinkercad Integration**: Fully functional on Autodesk Tinkercad simulation platform.

---

## Requirements
To run this project, you need:
1. **Tinkercad Account**: [Sign up here](https://www.tinkercad.com/).
2. **Arduino UNO Board**.
3. **Components**:
   - LEDs (multiple colors)
   - Push Buttons (2 or more)
   - Resistors (220Ω or similar)
   - Breadboard
   - Connecting Wires

---

## How to Simulate
1. **Clone the Project**:
   - Access the Tinkercad simulation by following this [link](https://www.tinkercad.com/dashboard).
   - Import or recreate the circuit design in Tinkercad.

2. **Setup**:
   - Place components as shown in the circuit diagram.
   - Use the provided Arduino sketch to load the game logic.

3. **Start Simulation**:
   - Click **"Start Simulation"** in Tinkercad.
   - Use the buttons to play the game and track the ball's movement with LEDs.

---

## Circuit Diagram
![Circuit Diagram](https://via.placeholder.com/800x400.png?text=Circuit+Diagram)

---

## Arduino Code
Here is the Arduino sketch used for this simulation:

```c
// Arduino UNO Ping Pong Game V2.0
const int leftButton = 2; // Left button pin
const int rightButton = 3; // Right button pin
const int leds[] = {4, 5, 6, 7, 8}; // LED pins
int ballPosition = 2; // Initial ball position
int direction = 1; // Ball direction: 1 for right, -1 for left

void setup() {
  for (int i = 0; i < 5; i++) {
    pinMode(leds[i], OUTPUT);
  }
  pinMode(leftButton, INPUT_PULLUP);
  pinMode(rightButton, INPUT_PULLUP);
}

void loop() {
  // Check button input
  if (digitalRead(leftButton) == LOW && direction == -1) {
    direction = 1; // Change direction
  } else if (digitalRead(rightButton) == LOW && direction == 1) {
    direction = -1; // Change direction
  }

  // Update LED state
  for (int i = 0; i < 5; i++) {
    digitalWrite(leds[i], (i == ballPosition) ? HIGH : LOW);
  }

  // Move the ball
  ballPosition += direction;
  if (ballPosition == 0 || ballPosition == 4) {
    direction = -direction; // Bounce the ball
  }

  delay(200); // Adjust speed of ball
}

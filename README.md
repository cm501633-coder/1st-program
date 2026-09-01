# Rakhi Quest 🎮

**A tiny festive game made for a beloved sister.**

## 📖 Project Overview

Rakhi Quest is a heartfelt, interactive game created as a gift to celebrate the bond between siblings during Raksha Bandhan, a cherished Indian festival. This project combines nostalgia, personal sentiment, and game development to create a meaningful and fun experience.

The game is a simple yet engaging **catch-and-collect** style arcade game where players control a character and collect falling items within a time limit. It's built with **Python** and **Tkinter**, making it lightweight and easy to run on any system with Python installed.

## 🎯 Game Concept

### Gameplay
- **Objective**: Catch falling love symbols (hearts, rakhis, and gifts) while avoiding negative items
- **Controls**: Use arrow keys (`← →`) or WASD keys (`A / D`) to move the character
- **Duration**: 30 seconds of intense collecting action
- **Scoring**: 
  - +2 points for collecting hearts (♥), rakhis (✦), or gifts (🎁)
  - -1 point for collecting clouds (☁) - a penalty item
  - Score is capped at a minimum of 0

### Theme
The game celebrates the essence of Raksha Bandhan with festive colors and affectionate messaging:
- **Player Character**: "♡ SIS ♡" - represented as a glowing yellow oval
- **Background**: Purple (#261342) with decorative colored circles
- **Message**: "Catch the love, leave the worries!" - encapsulating the spirit of the festival

## 🛠️ Technical Stack

- **Language**: Python 3
- **GUI Framework**: Tkinter (Python's standard GUI library)
- **Game Loop**: Event-driven animation with scheduled callbacks
- **Architecture**: Object-oriented design using the `RakhiQuest` class

## 🎮 Features

1. **Responsive Controls**: Real-time keyboard input for smooth player movement
2. **Random Item Spawning**: Items fall from random positions across the screen at regular intervals
3. **Collision Detection**: Accurate detection of caught items based on player position
4. **Score Tracking**: Live score and timer display during gameplay
5. **Game States**: Start, playing, and game-over states with smooth transitions
6. **Win Screen**: Personalized message celebrating the sibling relationship
7. **Play Again**: Option to restart the game immediately after completion
8. **Resource Cleanup**: Proper management of scheduled callbacks to prevent memory leaks

## 📊 Game Constants

```python
WIDTH = 760          # Canvas width in pixels
HEIGHT = 560         # Canvas height in pixels
GAME_TIME = 30       # Duration of each game round in seconds
```

## 🚀 How to Run

### Prerequisites
- Python 3.x installed on your system
- Tkinter (included with most Python installations)

### Installation & Execution
```bash
python gift.py
```

The game window will open with a colorful interface. Press **SPACE** or click the **START GAME** button to begin!

## 🎨 Visual Design

The game features a vibrant, festive aesthetic:
- **Color Palette**: 
  - Peachy background (#fff3e8)
  - Deep purple game canvas (#261342)
  - Colorful accent circles (red, yellow, green, orange)
  - Neon-bright item colors (pink, gold, cyan, purple)

- **Typography**: Modern Segoe UI font throughout for clean, readable text
- **Symbols**: Unicode characters for thematic elements (hearts, rakhis, gifts, clouds)

## 💝 Emotional Core

Beyond the code and gameplay mechanics, Rakhi Quest is fundamentally a love letter to a sister. The personalized message displayed at game completion encapsulates the sentiment:

> *"Dear Sis, you make every day brighter. Happy Rakhi! I am lucky to have you. ♥"*

This project demonstrates how coding can be a creative medium for expressing emotions and strengthening relationships.

## 📁 Project Structure

```
1st-program/
├── gift.py          # Main game file
└── README.md        # This file
```

## 🔮 Possible Future Enhancements

- Multiple difficulty levels (easy, medium, hard)
- Leaderboard to track high scores
- Sound effects and background music
- Power-ups and special items
- Animated transitions and visual effects
- Persistent score history
- Mobile version using frameworks like Kivy

## 👩‍💻 Author

Created with ❤️ by **Chaitanya Mishra** as a heartfelt gift for their sister during Raksha Bandhan.

---

**Happy Raksha Bandhan! 🎉**

May the bond between siblings continue to strengthen with every passing year! ♥

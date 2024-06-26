# Arduino LED Animation Project

Welcome to the presentation of our Arduino LED animation project. Let's explore the inspiration, functionality, operation, future ideas, and challenges of this project.

## Idea Origin

Our first idea for this project was to make a rhythm game, because we wanted to create an interactive and entertaining product. But we soon realized that our initial thought would be too hard to implement due to lack of hardware, time, and ultimately, knowledge.

## What Does the Code Do?

The code controls an array of 12 addressable LEDs, cycling through different colors and creating a left-to-right and right-to-left animation effect. Each color transition has a unique delay time to add variety to the display.


## How Does the Code Work?

1. **Setup Phase**:
    - Initialize the FastLED library to control the LEDs.
    - Clear any existing data on the LEDs and prepare for animation.

2. **Loop Phase**:
    - Define the delay times for each color to create different animation speeds.
    - Use a loop to move the light from left to right, then right to left, changing colors at each end.
    - Update the color and delay time after each full cycle.

To test the following code click on the link below and paste our program into the "code" section.                
https://liascript.github.io/course/?https://raw.githubusercontent.com/TUBAF-IUZ-LiaScript/ENGLISH-ROB-BGIP/main/Arduino-projects/main.md#3

```cpp
#include <FastLED.h>

#define LED_PIN     6
#define LED_COUNT   12

CRGB leds[LED_COUNT];

enum Colors {Red, Orange, Yellow, Green, Blue,Aqua, Violet,Pink};
// Define the delay times for each color
const int delayTimes[] = {150, 130, 110, 90, 75, 60,45,30};

Colors currentColor = Red;
int ColorAmount = 8;

CRGB getColor(Colors color) {
  switch (color) {
    case Green:  return CRGB::Green;
    case Blue:   return CRGB::Blue;
    case Violet: return CRGB::Violet;
    case Yellow: return CRGB::Yellow;
    case Orange: return CRGB::Orange;
    case Red:    return CRGB::Red;
    case Aqua:   return CRGB::Aqua;
    case Pink:   return CRGB::Pink;
    default:     return CRGB::White; // Default to white if something goes wrong
  }
}

void setup() {
  FastLED.addLeds<NEOPIXEL, LED_PIN>(leds, LED_COUNT);
  FastLED.clear();
  FastLED.show();
}

void loop() {
  int delayTime = delayTimes[currentColor];

  // Move light from left to right
  for (int i = 0; i < LED_COUNT; i++) {
        FastLED.clear();
        leds[i] = getColor(currentColor);
        leds[i-1] = getColor(currentColor);
        leds[i-2] = getColor(currentColor);// Set current LED to the current color
        FastLED.show();
        delay(delayTime);
  }

  // Change to the next color
  currentColor = static_cast<Colors>((currentColor + 1) % ColorAmount);
  delayTime = delayTimes[currentColor];

  // Move light from right to left
  for (int i = LED_COUNT - 1; i >= 0; i--) {
    FastLED.clear();
    leds[i] = getColor(currentColor);
    leds[i-1] = getColor(currentColor);
    leds[i-2] = getColor(currentColor);
    FastLED.show();
    delay(delayTime);
  }

  // Change to the next color
  currentColor = static_cast<Colors>((currentColor + 1) % ColorAmount);
}
```
## Future ideas

- Interactive Control: Add buttons or a remote control to change colors and animation patterns.

- Music Synchronization: Sync the LED animations with music beats for a dynamic light show.

- Complex Patterns: Develop more complex animation patterns, such as wave or ripple effects.

- Mobile App Integration: Create a mobile app to control the LED display wirelessly.

## Challenges during development 

- Understanding Arduino code and syntax.

- Implementing our ideas as code.

## Simulation 

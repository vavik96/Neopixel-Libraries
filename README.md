#include "FastLED.h"

#define NUM_STRIPS 3
// How many leds in your strip?
#define NUM_LEDS_1 15
#define NUM_LEDS_2 6
#define DATA_PIN_1 6
#define DATA_PIN_2 3
#define BRIGHTNESS  30
// Define the array of leds
CRGB leds_1[NUM_LEDS_1];
CRGB leds_2[NUM_LEDS_2];

void setup() { 
  FastLED.addLeds<NEOPIXEL, DATA_PIN_1>(leds_1, NUM_LEDS_1);
  FastLED.addLeds<NEOPIXEL, DATA_PIN_2>(leds_2, NUM_LEDS_2);
}

uint8_t color_pos() {
  static float pos = 0;
  static unsigned long last_tick = millis();
  unsigned long now = millis();
  float delta = 0.1 * (now - last_tick);
  pos += delta;
  last_tick = now;

  if(pos > 255) {
    pos -= 255;
  }
  return (uint8_t)(pos) ;
}


void loop() { 
  fill_rainbow(leds_1, NUM_LEDS_1, color_pos());
  FastLED.show();
  fill_solid (leds_2, NUM_LEDS_2, CRGB(20,234,214));
  FastLED.show();
//  fill_rainbow(leds_2, NUM_LEDS_2, color_pos());
//  FastLED.show();
}

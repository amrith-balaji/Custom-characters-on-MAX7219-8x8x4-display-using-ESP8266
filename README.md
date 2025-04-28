# Custom-characters-on-MAX7219-display-and-esp8266

## Displays a number 2, a percentage symbol,an up arrow and a down arrow :
```
#include <MD_MAX72xx.h>
#include <SPI.h>

#define  delay_t  50  // in milliseconds

#define HARDWARE_TYPE MD_MAX72XX::FC16_HW
#define MAX_DEVICES 4

//Hardware SPI Arduino UNO
#define CLK_PIN   14 //D5
#define DATA_PIN  13 //D7
#define CS_PIN    15 //D8

// Hardware SPI connection
MD_MAX72XX mx = MD_MAX72XX(HARDWARE_TYPE, CS_PIN, MAX_DEVICES);

byte arrow_up[8] = {0x18,0x3C,0x7E,0x7E,0x18,0x18,0x18,0x18}; //1
byte arrow_down[8] = {0x18,0x18,0x18,0x18,0x7E,0x7E,0x3C,0x18};
byte number_2[8] = {0x00,0x02,0x24,0x08,0x10,0x24,0x40,0x00};
byte percent[8] = {0x43,0xE7,0x4E,0x1C,0x38,0x72,0xE7,0xC2};

void setup() {  
  mx.begin();
  mx.control(MD_MAX72XX::INTENSITY, 0);
  mx.clear();
}

void loop() {
  drawShape();
}

void drawShape() { 
  for (int i = 0; i <= 7; i++) {
    mx.setRow(0, 0, i, arrow_up[i]);
  }
  delay(delay_t);
  for (int i = 0; i <= 7; i++) {
    mx.setRow(1, 1, i, arrow_down[i]);
  }
  delay(delay_t);
  for (int i = 0; i <= 7; i++) {
    mx.setRow(2, 2, i, number_2[i]);
  }
  delay(delay_t); 
  for (int i = 0; i <= 7; i++) {
    mx.setRow(3, 3, i, percent[i]);
  }
  delay(delay_t);
}


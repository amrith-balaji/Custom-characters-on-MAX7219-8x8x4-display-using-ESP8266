# Custom-characters-on-MAX7219-display-and-esp8266

## Display an arrow :
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

byte arrow[8] = {0x18,0x3C,0x7E,0x7E,0x18,0x18,0x18,0x18};

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
    mx.setRow(0, 0, i, arrow[i]);
  }
}

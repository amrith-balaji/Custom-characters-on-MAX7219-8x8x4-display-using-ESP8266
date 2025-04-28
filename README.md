# Custom-characters-on-MAX7219-display-using-ESP8266

## Displays the number 2, a percentage symbol, an up arrow and a down arrow :

This project involves displaying special characters, numbers, characters, and does a demo of the UP arrow and the DOWN arrow.

Here I have shown the Percentage sign, the number 2 and the arrows.

Included in the sketch is the MD_MAX72xx and MD_Parola library ( seen in the top of the sketch )

To print the special character ( in this case the % sign ) the function set.row () was used, see below

![image](https://github.com/user-attachments/assets/5fa6632b-1c98-49e3-b7ab-0fbb43af9a1c)
 

Image 1 of the display output

![WhatsApp Image 2025-04-28 at 10 52 24_b5784ae5](https://github.com/user-attachments/assets/f63c0c65-0383-4561-b220-6352bc415263)

Image 2 of ESP8266

![WhatsApp Image 2025-04-28 at 11 07 39_13c383f5](https://github.com/user-attachments/assets/e5177493-101e-4684-944b-d91fb5782d28)


Image 3 of SPI pins of the MAX 7219 8x8x4 LED display

![WhatsApp Image 2025-04-28 at 10 55 34_1c8f3e46](https://github.com/user-attachments/assets/6201fcc4-d9d1-4dca-94c1-db3442a1a76e)

# Code :

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

byte arrow_up[8] = {0x18,0x3C,0x7E,0x7E,0x18,0x18,0x18,0x18}; 
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
```
The connections go as follows:
| MAX7219  | ESP8266 |
| ------------- | ------------- |
| VIN -->  | 3V  |
| GND --> | GND  |
| DIN --> | D7 |
| CS --> | D8 |
| CLK --> | D5 |




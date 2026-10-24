# Smart Bin: Automatic Waste-Segregation Bin with P10 LED Display

An Arduino-controlled smart dustbin that **separates biodegradable and non-biodegradable waste**. A Raspberry Pi identifies the waste and sends the result over serial. The Arduino opens the correct lid with a servo, uses an ultrasonic sensor to confirm the waste has gone in, and shows prompts and reward messages on a **P10 LED matrix**.

## How it works
1. The P10 display scrolls **"SMART BIN"** while idle.
2. The Raspberry Pi sends the user's name over serial, and the display greets them with "HI, <name>".
3. The display asks the user to **"SHOW THE WASTE"**. The Pi classifies it and replies `0` (bio) or `1` (non-bio).
4. The matching servo opens that bin's lid (0 to 115°).
5. The ultrasonic sensor above the bin keeps the lid open until the waste has dropped and the path is clear (distance over 30 cm).
6. The lid closes, the display shows **"DONE"**, then a credit/reward message.

## Hardware
| Part | Pin |
|---|---|
| Arduino Uno | — |
| P10 LED matrix (DMD2 library, SPI) | SPI header |
| Servo, bio bin | D3 |
| Servo, non-bio bin | D5 |
| HC-SR04 ultrasonic, bio bin (TRIG/ECHO) | D2 / D4 |
| HC-SR04 ultrasonic, non-bio bin (TRIG/ECHO) | D10 / D12 |
| Raspberry Pi handshake output | A0 |
| Raspberry Pi link | UART, 9600 baud |

## Serial protocol (Raspberry Pi to Arduino)
| Message | Meaning |
|---|---|
| `<name>\n` | Greets the user on the display |
| `0` | Biodegradable: open the bio bin |
| `1` | Non-biodegradable: open the non-bio bin |

## Build and flash
1. Install the libraries **DMD2** and **Servo**.
2. Open `smart-bin-code.ino`, select Arduino Uno, and upload.
3. Connect the Raspberry Pi's UART (through a level shifter) to the Arduino's RX/TX.

## Author
**Keerthivasan J**, B.E. EEE, Sri Sairam Engineering College ([GitHub](https://github.com/Keerthivasan-cdm) · [LinkedIn](https://linkedin.com/in/keerthi-vasan-j-))

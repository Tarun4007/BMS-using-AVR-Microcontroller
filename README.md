# ATtiny85 Battery Charge Visualizer 🚦🔋

This is a simple yet effective project that uses an ATtiny85 microcontroller to visualize the battery charge level and charger connection using RGB LEDs.

## 🧠 Features
- Detects if a charger is connected.
- Displays battery charge level using red, blue, or green LED indicators.
- Automatically enables/disables charging using a MOSFET based on battery percentage.
- Designed for 3S Li-Ion batteries (11.1V max).

## 🔌 Components Used
- ATtiny85 microcontroller
- RGB LED (or separate Red, Green, Blue LEDs)
- P-Channel or N-Channel MOSFET (e.g., IRLZ44N)
- Voltage divider resistors (15kΩ & 10kΩ recommended)
- 11.1V Lithium-Ion battery pack
- Charger (12.6V for 3S Li-Ion)

## 📊 LED Behavior
| Battery Status | Charger Connected | LED Color |
|----------------|-------------------|-----------|
| < 30%          | No                | Red       |
| 30–85%         | No                | Blue      |
| > 85%          | No                | Green     |
| Charging       | Yes               | LED shows battery level (Red/Blue/Green) |
| Fully Charged  | Yes               | Green     |
| No Battery     | –                 | Off       |

## 🧩 Pin Mapping (ATtiny85)
| Function              | Pin  |
|-----------------------|------|
| Red LED               | PB0  |
| Green LED             | PB1  |
| Blue LED              | PB5  |
| MOSFET Gate Control   | PB3  |
| Charger Voltage Input | PB4  |    
| Battery Voltage Input | PB2  |
|GND                    | GND  |

## 🔧 How It Works
- Two voltage dividers scale down the battery and charger voltages to a safe 0–5V range readable by the ATtiny85.
- The code reads these values using `analogRead()`, calculates real voltages, and maps battery level to a percentage.
- Based on thresholds, the LED color changes.
- The charging MOSFET is enabled or disabled based on whether the battery needs charging.

## 🚀 Getting Started
1. Upload `main.ino` to your ATtiny85 using an Arduino as ISP.
2. Connect the components as per the pin mapping.
3. Power the circuit via the battery and test charger connection behavior.

**🔧 Special Configuration: Using RESET Pin as GPIO**
This project uses pin 1 (PB5) — normally the RESET pin — as a GPIO to control an LED.

To enable this, the ATtiny85 was configured using High Voltage Serial Programming (HVSP).

This disables the RESET functionality and frees up PB5 as a usable digital output.

⚠️ Note: Once the RESET pin is disabled, you cannot reprogram the ATtiny85 using standard ISP (In-System Programming) until HVSP is used again to re-enable it.

# OLEDLite

A lightweight Arduino library for basic control of monochrome SSD1306 OLED displays via I2C. Designed for simplicity and minimal memory usage, `OLEDLite` provides low-level functions to initialize, clear, and draw raw pixel data on OLED screens without relying on large graphics libraries.

## Features

- ✅ Minimal memory footprint  
- ✅ Simple I2C communication (using Wire.h)  
- ✅ Direct control over display 
- ✅ Fast data transmission  
- ✅ Supports raw byte drawing, filling, and clearing  

## Supported Displays

- SSD1306-based OLED modules (128x64, 128x32, etc.)  
- I2C interface (typically 0x3C or 0x3D address)

## Installation

1. Download this repository as a `.zip` file.
2. In Arduino IDE: **Sketch → Include Library → Add .ZIP Library...**
3. Select the downloaded file.
4. Done! You can now use `OLEDLite` in your projects.

## Basic Usage

```cpp
#include "OLEDLite.h"

// Display(address, width, height)
Display oled(0x3C, 128, 64);

void setup() {
  oled.init();           // Initialize the display
  oled.clear();          // Clear screen

  oled.set_pos(0, 0);    // Set cursor to column 0, page 0
  oled.send_pack(0xFF, 128); // Draw a full horizontal line (8 pixels high)
}

void loop() {
}
```

## API Reference

| Function | Description |
|--------|-------------|
| `Display(address, width, height)` | Create display object with I2C address, width, height |
| `init()` | Initialize the OLED with common SSD1306 settings |
| `clear()` | Fill entire screen with black (clear pixels) |
| `set_pos(x, y)` | Set cursor to column `x` and page `y` (each page = 8 rows) |
| `send_data(byte)` | Send a single byte of pixel data |
| `send_pack(data, count)` | Send the same byte `count` times (e.g., fill) |
| `send_mult(buffer, size)` | Send an array of `size` bytes |

## Notes

- The display is addressed in **pages** (8 rows per page). Height should be divisible by 8.
- Data is sent in 8-pixel tall columns (1 bit = 1 pixel).
- No built-in font or text support — ideal for custom graphics or integration with font engines.

## License

MIT — Feel free to use, modify, and distribute. See [LICENSE](LICENSE) for details.

---

💡 Tip: Use an I2C scanner sketch to confirm your OLED's address before use.

# rpi-pico-i2c-display-lib
A C++ Library for using I2C LCD displays on Raspberry Pi Pico. Essentialy a port of LiquidCrystal_I2C to RPi Pico.\
Based mostly on [rpi-pico-20x4-lcd-i2c-example](https://github.com/ParicBat/rpi-pico-20x4-lcd-i2c-example) and [LiquidCrystal_I2C](https://github.com/johnrickman/LiquidCrystal_I2C) (Arduino Library).

# How to use?
There are two ways:
1. Copy the source code to your main C++ file.
1. Add the file `i2c-display-lib.hpp` to your CMakeLists.txt file.

## Adding the file to CMakeLists.txt

Here's a step-by-step guide:
1. Move the `i2c-display-lib.hpp` file to your include folder (create one if you don't have one).
1. Include the include folder like this: `target_include_directories(yourproject PUBLIC ./include)`.
1. Done!

CMakeLists.txt should look like this now:
```
cmake_minimum_required(VERSION 3.12)

include(pico_sdk_import.cmake)
project(yourproject)
pico_sdk_init()

add_executable(yourproject yourproject.cpp)
target_include_directories(yourproject PUBLIC ./include)

pico_add_extra_outputs(yourproject)

target_link_libraries(yourproject pico_stdlib hardware_i2c)
```
# An Example
```
#include "pico/stdlib.h"
#include "i2c-display-lib.hpp"

int main() {
    i2cdisplay::init(6, 7); // sda and scl

    i2cdisplay::home(); // or lcd_setCursor(0,0);
    i2cdisplay::print("Hello World!");
}
```

## Changing the LCD Address
*Note: You must change the address before calling i2cdisplay::init(), or call it again.*

Simply change the global variable `lcd_addr` to whatever you need.
# 🚗 Drivers & Abstraction
Before we can understand drivers, we first need to grasp the concept of abstraction. In this project, we won’t be writing drivers from scratch. Instead, we'll be using the powerful drivers provided by ESP-IDF, which abstract away the low-level hardware complexity for us.

## Example:
You'll see this line in main.c:
uart_write_bytes(RYLR998_UART_PORT, at_command, strlen(at_command));
This function provides a high level of abstraction. It doesn't directly manipulate the hardware to send bits. Instead, it calls into the ESP-IDF's dedicated UART driver. If you trace the function, you'll find its source code in the esp-idf/components/driver/uart directory.

Inside uart.c, you'll see that uart_write_bytes() eventually calls lower-level functions like uart_tx_all(). While you aren't expected to understand all of that code, it's worth browsing through it. You'll quickly see the immense complexity involved in managing hardware directly, and you'll appreciate that we are abstracted away from it!

##The Big Picture
In our projects, we will primarily use top-level, abstract functions like uart_write_bytes(). This approach is much easier, faster, and safer than direct register manipulation (e.g., GPIO->MODER |= ...).

This concept isn't unique to Espressif. Other microcontroller ecosystems have similar layers:

STM32: HAL (Hardware Abstraction Layer)

TI MSP430: DriverLib

Nordic nRF52: nRF5 SDK drivers

Using these libraries allows us to focus on our application's logic instead of the nitty-gritty hardware details.

## 📚 Resources
Drivers are a massive topic, so finding introductory material can be challenging. These resources provide a good starting point, but be aware they are more in-depth.

📖 Article: Writing a Device Driver — Simple Example with RTOS [https://medium.com/@lanceharvieruntime/writing-a-device-driver-using-freertos-a-detailed-guide-d8b70af7cdb7]

🎥 Video 1: How to Write a Driver (40 min) [https://www.youtube.com/watch?v=_JQAve05o_0&t=2s]

🎥 Video 2: UART Driver Deep Dive (55 min) [https://www.youtube.com/watch?v=wC9a0IkPA1A]

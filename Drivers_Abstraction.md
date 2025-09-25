## Drivers & Abstraction

Drivers are a massive topic in embedded systems, and writing them from scratch can be quite complex. For this project, we won’t be writing drivers ourselves—instead, we will be using the drivers provided by ESP-IDF, which abstract us away from the hardware.

For example, in `main.c` you might see:

uart_write_bytes(RYLR998_UART_PORT, at_command, strlen(at_command));

This function does not directly manipulate the UART hardware to send bits. Instead, it calls into the ESP-IDF UART driver. If you trace it, you’ll find the implementation in:

esp-idf/components/driver/uart


Inside uart.c, uart_write_bytes() eventually calls lower-level functions such as uart_tx_all(). These contain all the complexity of handling FIFOs, interrupts, DMA, and error conditions. 
While we are not expected to fully understand this code, it’s valuable to recognize the effort that goes into writing such drivers—and to appreciate the abstraction layers provided to us.

In practice, we will make use of top-level abstractions like uart_write_bytes() to interact with hardware. This is much easier and safer than directly manipulating registers (e.g., GPIO->MODER |= …).

Other microcontroller ecosystems provide similar abstractions:

STM32: HAL (Hardware Abstraction Layer)

TI MSP430: DriverLib

Nordic nRF52: nRF5 SDK drivers

These abstractions save time, improve readability, and help ensure portability across projects.

Resources

📖 Article: Writing a Device Driver — Simple Example with RTOS

🎥 How to Write a Driver (40 min)

🎥 UART Driver Deep Dive (55 min)

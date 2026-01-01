# STM32F446RET6 – 16×2 LCD Interfacing (HAL Method)

A beginner-friendly embedded systems project demonstrating how to interface a **16×2 alphanumeric LCD (HD44780 compatible)** with the **STM32F446RET6 (Nucleo-F446RE)** using **STM32CubeIDE and HAL libraries**.

This project focuses on **fundamentals first** — GPIO control, LCD initialization, command/data handling, and real hardware interaction.

---

## 📌 Project Overview

Interfacing an LCD is a classic embedded milestone.
In this project, the STM32F446RET6 communicates with a **16×2 character LCD in 4-bit mode**, reducing GPIO usage while maintaining reliable data transfer.

### What you’ll learn:

* GPIO output configuration in STM32
* LCD command vs data handling
* 4-bit LCD communication
* HAL delay usage for hardware timing
* Practical STM32CubeIDE workflow

---

## 🧠 Hardware Used

| Component     | Description                       |
| ------------- | --------------------------------- |
| MCU Board     | **STM32F446RET6 (Nucleo-F446RE)** |
| Display       | 16×2 LCD (HD44780 compatible)     |
| Potentiometer | 10KΩ (LCD contrast control)       |
| Jumper Wires  | Male–Male                         |
| Breadboard    | Optional                          |

---

## 🔌 LCD to STM32F446RET6 Connections

> **LCD is used in 4-bit mode** to save GPIO pins.

### LCD Pin Mapping (Example)

| LCD Pin | Function        | STM32F446RET6 Pin |
| ------- | --------------- | ----------------- |
| VSS     | GND             | GND               |
| VDD     | +5V             | 5V                |
| V0      | Contrast        | Potentiometer     |
| RS      | Register Select | GPIO Output       |
| RW      | Read/Write      | GND               |
| EN      | Enable          | GPIO Output       |
| D4      | Data Bit 4      | GPIO Output       |
| D5      | Data Bit 5      | GPIO Output       |
| D6      | Data Bit 6      | GPIO Output       |
| D7      | Data Bit 7      | GPIO Output       |

⚠️ **RW is tied to GND** because this project only writes to the LCD.

> You can change GPIO pins in code — just keep them consistent.

---

## 🛠️ Software Requirements

* **STM32CubeIDE**
* STM32 HAL drivers
* USB cable for Nucleo board
* Basic C programming knowledge

---

## ⚙️ STM32CubeIDE Setup

1. Open **STM32CubeIDE**
2. Create a **New STM32 Project**
3. Select **NUCLEO-F446RE**
4. Configure required GPIO pins as **Output Push-Pull**
5. Set clock (default config is fine for beginners)
6. Generate code
7. Add LCD driver files / logic from this repository
8. Build and flash to board

---

## 🧩 How the Code Works (High-Level)

### 1️⃣ LCD Initialization

The LCD is initialized in **4-bit mode** by sending specific command sequences as per the HD44780 datasheet.

### 2️⃣ Command vs Data

* **RS = 0** → Command mode
* **RS = 1** → Data mode

### 3️⃣ Enable Pulse

The **EN pin** is toggled to latch data into the LCD controller.

### 4️⃣ Delays Matter

Short delays are mandatory — LCDs are slow compared to MCUs.

---

## 📂 Project Structure (Simplified)

```text
Core/
 ├── Src/
 │    └── main.c        # Main application logic
 ├── Inc/
 │    └── main.h
```

LCD functions are typically implemented as:

* `LCD_Init()`
* `LCD_Command()`
* `LCD_Data()`
* `LCD_Print()`
* `LCD_SetCursor()`

---

## ▶️ Example Usage

```c
LCD_Init();
LCD_SetCursor(0, 0);
LCD_Print("STM32F446RE");
LCD_SetCursor(1, 0);
LCD_Print("16x2 LCD");
```

Expected Output on LCD:

```
STM32F446RE
16x2 LCD
```

---

## 🧪 Common Issues & Debug Tips

### ❌ LCD shows nothing

* Adjust the **contrast potentiometer**
* Verify VDD = 5V

### ❌ Random characters

* Incorrect GPIO mapping
* Missing delays

### ❌ Only blocks visible

* LCD initialized incorrectly
* Check 4-bit sequence order

### ❌ Build errors

* Ensure HAL GPIO headers are included
* Check CubeIDE generated files

---

## 📈 Learning Outcomes

By completing this project, you gain hands-on experience with:

* STM32F446RET6 GPIO control
* HAL-based embedded development
* Hardware timing & delays
* Character LCD fundamentals
* Real-world debugging skills

This is a **foundation project** that prepares you for:

* I2C LCDs
* SPI displays
* OLED / TFT screens
* RTOS-based display handling

---

## 📜 License

This project is licensed under the **MIT License**.
Feel free to learn, modify, and share.

---

## 🙌 A Note for Beginners

If your LCD doesn’t work the first time — **that’s normal**.
Embedded systems reward patience, signal-level thinking, and iteration. You’re building real engineering instincts here.

---

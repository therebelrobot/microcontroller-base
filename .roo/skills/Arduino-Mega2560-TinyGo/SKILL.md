---
name: Arduino-Mega2560-TinyGo
description: >
  Provides comprehensive pinout reference, board specifications, and TinyGo development guide
  for the Arduino Mega 2560 (ATmega2560) microcontroller. Use when writing TinyGo firmware for the
  Arduino Mega 2560, wiring peripherals, or configuring pins. Keywords: Arduino, Mega, 2560,
  ATmega2560, AVR, TinyGo, pinout, GPIO, I2C, SPI, UART, analog, digital, PWM, 5V, 8-bit,
  54 pins, 4 UARTs, 16 analog.
---

# Arduino Mega 2560 — TinyGo Development Guide

Provides comprehensive reference for developing TinyGo firmware for the Arduino Mega 2560 (ATmega2560).

## When to Use

- Writing TinyGo firmware targeting the Arduino Mega 2560
- Looking up Arduino Mega 2560 pin assignments, alternate functions, or peripheral mappings
- Wiring sensors/actuators to the Arduino Mega 2560 and need GPIO reference
- Configuring I2C, SPI, UART, or analog I/O on the Arduino Mega 2560 in TinyGo

## When NOT to Use

- For Arduino/C++ development on the Mega 2560 → use the `Arduino-Mega2560-Arduino` skill
- For Arduino Uno R3 → use the `Arduino-UnoR3-TinyGo` skill
- For Arduino Nano → use the `Arduino-Nano-TinyGo` skill
- For Arduino Uno R4 boards → use the corresponding R4 skill

---

## Board Overview

| Parameter | Value |
|---|---|
| **MCU** | ATmega2560 |
| **Architecture** | 8-bit AVR |
| **Clock Speed** | 16 MHz |
| **Flash** | 256 KB (8 KB used by bootloader) |
| **SRAM** | 8 KB |
| **EEPROM** | 4 KB |
| **USB** | USB-B (via ATmega16U2 USB-serial) |
| **Operating Voltage** | 5V |
| **Input Voltage (VIN)** | 7–12V recommended |
| **DC Current per I/O Pin** | 20 mA |
| **Dimensions** | 101.5 × 53.3 mm |
| **Weight** | 37 g |
| **Digital I/O** | 54 (D0–D53) |
| **PWM Outputs** | 15 (D2–D13, D44, D45, D46) |
| **Analog Inputs** | 16 (A0–A15, 10-bit ADC) |
| **UARTs** | 4 (Serial0–Serial3) |
| **External Interrupts** | 6 (D2, D3, D18, D19, D20, D21) |
| **Built-in LED** | D13 |

---

## Pinout Diagram

```
                    [USB-B]                    [Barrel Jack]
    ┌──────────────────────────────────────────────────────┐
    │  RESET  IOREF  5V  GND  GND  VIN                    │ ← Power Header
    │  3.3V   AREF   GND                                  │
    ├──────────────────────────────────────────────────────┤
    │                                                      │
    │  ANALOG HEADER                                       │
    │  A0  A1  A2  A3  A4  A5  A6  A7                    │
    │  A8  A9  A10 A11 A12 A13 A14 A15                   │
    │                                                      │
    ├──────────────────────────────────────────────────────┤
    │                                                      │
    │  DIGITAL HEADER (Uno-compatible side)                │
    │  D0/RX0  D1/TX0  D2  D3  D4  D5  D6  D7           │
    │  D8  D9  D10  D11  D12  D13/LED                    │
    │                                                      │
    │                  [ATmega2560]                        │
    │                                                      │
    │  DIGITAL HEADER (extended)                           │
    │  D14/TX3  D15/RX3  D16/TX2  D17/RX2                │
    │  D18/TX1  D19/RX1  D20/SDA  D21/SCL                │
    │  D22  D23  D24  D25  D26  D27  D28  D29            │
    │  D30  D31  D32  D33  D34  D35  D36  D37            │
    │  D38  D39  D40  D41  D42  D43  D44  D45            │
    │  D46  D47  D48  D49  D50/MISO  D51/MOSI            │
    │  D52/SCK  D53/SS                                    │
    │                                                      │
    ├──────────────────────────────────────────────────────┤
    │          [ICSP]                                      │
    └──────────────────────────────────────────────────────┘

  PWM: D2–D13, D44, D45, D46
  UARTs: Serial0(D0/D1), Serial1(D18/D19), Serial2(D16/D17), Serial3(D14/D15)
  I2C: D20(SDA), D21(SCL)
  SPI: D50(MISO), D51(MOSI), D52(SCK), D53(SS)
  Interrupts: D2(INT0), D3(INT1), D18(INT5), D19(INT4), D20(INT3), D21(INT2)
```

---

## Pin Reference Table

### Digital Pins D0–D21 (Communication & Interrupt Pins)

| Pin | Digital | PWM | Interrupt | SPI | I2C | UART | Other |
|-----|---------|-----|-----------|-----|-----|------|-------|
| D0  | ✓       | —   | —         | —   | —   | **Serial0 RX** | — |
| D1  | ✓       | —   | —         | —   | —   | **Serial0 TX** | — |
| D2  | ✓       | ✓   | **INT0**  | —   | —   | —    | — |
| D3  | ✓       | ✓   | **INT1**  | —   | —   | —    | — |
| D4  | ✓       | ✓   | —         | —   | —   | —    | — |
| D5  | ✓       | ✓   | —         | —   | —   | —    | — |
| D6  | ✓       | ✓   | —         | —   | —   | —    | — |
| D7  | ✓       | ✓   | —         | —   | —   | —    | — |
| D8  | ✓       | ✓   | —         | —   | —   | —    | — |
| D9  | ✓       | ✓   | —         | —   | —   | —    | — |
| D10 | ✓       | ✓   | —         | —   | —   | —    | — |
| D11 | ✓       | ✓   | —         | —   | —   | —    | — |
| D12 | ✓       | ✓   | —         | —   | —   | —    | — |
| D13 | ✓       | ✓   | —         | —   | —   | —    | Built-in LED |
| D14 | ✓       | —   | —         | —   | —   | **Serial3 TX** | — |
| D15 | ✓       | —   | —         | —   | —   | **Serial3 RX** | — |
| D16 | ✓       | —   | —         | —   | —   | **Serial2 TX** | — |
| D17 | ✓       | —   | —         | —   | —   | **Serial2 RX** | — |
| D18 | ✓       | —   | **INT5**  | —   | —   | **Serial1 TX** | — |
| D19 | ✓       | —   | **INT4**  | —   | —   | **Serial1 RX** | — |
| D20 | ✓       | —   | **INT3**  | —   | **SDA** | — | — |
| D21 | ✓       | —   | **INT2**  | —   | **SCL** | — | — |

### Digital Pins D22–D53 (Extended I/O)

| Pin | Digital | PWM | SPI | Other |
|-----|---------|-----|-----|-------|
| D22–D43 | ✓  | —   | —   | General purpose |
| D44 | ✓       | ✓   | —   | — |
| D45 | ✓       | ✓   | —   | — |
| D46 | ✓       | ✓   | —   | — |
| D47–D49 | ✓  | —   | —   | General purpose |
| D50 | ✓       | —   | **MISO** | — |
| D51 | ✓       | —   | **MOSI** | — |
| D52 | ✓       | —   | **SCK** | — |
| D53 | ✓       | —   | **SS** | — |

### Analog Pins A0–A15

| Pin | Analog | Digital | Other |
|-----|--------|---------|-------|
| A0  | ADC0   | ✓       | — |
| A1  | ADC1   | ✓       | — |
| A2  | ADC2   | ✓       | — |
| A3  | ADC3   | ✓       | — |
| A4  | ADC4   | ✓       | — |
| A5  | ADC5   | ✓       | — |
| A6  | ADC6   | ✓       | — |
| A7  | ADC7   | ✓       | — |
| A8  | ADC8   | ✓       | — |
| A9  | ADC9   | ✓       | — |
| A10 | ADC10  | ✓       | — |
| A11 | ADC11  | ✓       | — |
| A12 | ADC12  | ✓       | — |
| A13 | ADC13  | ✓       | — |
| A14 | ADC14  | ✓       | — |
| A15 | ADC15  | ✓       | — |

### Power Pins

| Pin | Function |
|-----|----------|
| VIN | Input voltage (7–12V recommended) |
| 5V  | Regulated 5V output |
| 3.3V | Regulated 3.3V output (50 mA max) |
| GND | Ground (multiple pins) |
| AREF | Analog reference voltage |
| IOREF | I/O reference voltage |
| RESET | Reset (active LOW) |

---

## TinyGo Setup

### Target Name

```
arduino-mega2560
```

### Installation

1. Install TinyGo: https://tinygo.org/getting-started/install/
2. Install AVR toolchain (avr-gcc, avrdude) — required for AVR targets
3. Verify the target is available:
   ```bash
   tinygo info -target=arduino-mega2560
   ```

### Build and Flash

```bash
# Build only
tinygo build -target=arduino-mega2560 -o firmware.hex ./main.go

# Build and flash (board must be connected via USB)
tinygo flash -target=arduino-mega2560 ./main.go

# Monitor serial output
tinygo monitor -target=arduino-mega2560
```

### TinyGo Support Status

- **Status:** Supported (with AVR limitations)
- **GPIO:** Supported (all 54 digital + 16 analog)
- **ADC:** Supported (10-bit)
- **PWM:** Supported on D2–D13, D44, D45, D46
- **I2C:** Supported (`machine.I2C0`)
- **SPI:** Supported (`machine.SPI0`)
- **UART:** `machine.UART0` (Serial0) supported; additional UARTs may have limited support
- **USB CDC:** Not available (USB is handled by ATmega16U2)
- **Goroutines:** More headroom than Uno/Nano (8 KB SRAM), but still limited
- **fmt package:** May fit in 256 KB flash, but still heavy; prefer `println()`

### Known Limitations (AVR / TinyGo)

- **8 KB SRAM** — More than Uno/Nano but still limited for Go; avoid large allocations
- **248 KB usable flash** — Bootloader uses 8 KB; much more room than Uno/Nano
- **No hardware FPU** — Floating-point math is emulated and slow
- **No goroutine preemption** — Cooperative scheduling only
- **No USB CDC** — Serial goes through ATmega16U2; use `machine.UART0`
- **Multiple UARTs** — TinyGo may not support all 4 UARTs; check `machine.UART1`, `machine.UART2`, `machine.UART3`
- **Pin numbering** — Mega uses different port mappings than Uno; verify pin constants in TinyGo

### Example: Blink (TinyGo)

```go
package main

import (
    "machine"
    "time"
)

func main() {
    led := machine.D13 // Built-in LED
    led.Configure(machine.PinConfig{Mode: machine.PinOutput})

    for {
        led.High()
        time.Sleep(500 * time.Millisecond)
        led.Low()
        time.Sleep(500 * time.Millisecond)
    }
}
```

---

## Communication Protocols

### I2C

- **SDA:** D20
- **SCL:** D21
- **TinyGo bus:** `machine.I2C0`

```go
i2c := machine.I2C0
err := i2c.Configure(machine.I2CConfig{
    SDA:       machine.SDA_PIN, // D20
    SCL:       machine.SCL_PIN, // D21
    Frequency: 100000,          // 100 kHz
})
if err != nil {
    println("I2C init failed:", err)
}

data := []byte{0x00, 0x01}
i2c.Tx(0x3C, data, nil)

buf := make([]byte, 2)
i2c.Tx(0x3C, []byte{0x00}, buf)
```

> **Note:** I2C pins on the Mega are D20/D21, NOT A4/A5 like on the Uno/Nano. This is a common source of wiring errors when porting projects.

### SPI

- **MISO:** D50
- **MOSI:** D51
- **SCK:** D52
- **SS:** D53 (or any GPIO)
- **TinyGo bus:** `machine.SPI0`

```go
spi := machine.SPI0
err := spi.Configure(machine.SPIConfig{
    SCK:       machine.D52,
    SDO:       machine.D51, // MOSI
    SDI:       machine.D50, // MISO
    Frequency: 4000000,     // 4 MHz
})
if err != nil {
    println("SPI init failed:", err)
}

cs := machine.D53
cs.Configure(machine.PinConfig{Mode: machine.PinOutput})
cs.High()

cs.Low()
result := make([]byte, 1)
spi.Tx([]byte{0x00}, result)
cs.High()
```

> **⚠ Important:** SPI pins on the Mega are D50–D53, NOT D10–D13 like on the Uno/Nano. D10–D13 are PWM-only on the Mega. Shields designed for Uno SPI (D10–D13) will NOT work on the Mega without rewiring to D50–D53 (or using the ICSP header).

### UART (4 Hardware Serial Ports)

The Mega 2560 has **4 hardware UARTs** — the most of any classic Arduino:

| UART | TX Pin | RX Pin | TinyGo Object |
|------|--------|--------|----------------|
| Serial0 | D1 | D0 | `machine.UART0` |
| Serial1 | D18 | D19 | `machine.UART1` (check support) |
| Serial2 | D16 | D17 | `machine.UART2` (check support) |
| Serial3 | D14 | D15 | `machine.UART3` (check support) |

```go
// Primary UART (Serial0)
uart0 := machine.UART0
uart0.Configure(machine.UARTConfig{
    TX:       machine.UART_TX_PIN, // D1
    RX:       machine.UART_RX_PIN, // D0
    BaudRate: 9600,
})
uart0.Write([]byte("Hello from Mega 2560\r\n"))

// Additional UARTs (check TinyGo support)
// uart1 := machine.UART1
// uart1.Configure(machine.UARTConfig{
//     TX:       machine.D18,
//     RX:       machine.D19,
//     BaudRate: 9600,
// })
```

> **Note:** TinyGo support for UART1–UART3 on the Mega may be limited. Check the latest TinyGo release notes. For full multi-UART support, consider the Arduino/C++ framework.

### Analog Read (ADC)

```go
adc := machine.ADC{Pin: machine.ADC0} // A0
adc.Configure(machine.ADCConfig{
    Resolution: 10, // 10-bit (0–1023)
})
value := adc.Get() // Returns 16-bit scaled value
println("A0:", value)

// All 16 analog pins (A0–A15) are available
adc15 := machine.ADC{Pin: machine.ADC15} // A15
adc15.Configure(machine.ADCConfig{})
println("A15:", adc15.Get())
```

---

## Power Management

### Voltage and Current

- **Logic level:** 5V on all GPIO pins
- **Max current per pin:** 20 mA
- **Total current (all pins):** 200 mA max
- **5V output:** From USB or regulated from VIN
- **3.3V output:** 50 mA max (from onboard regulator)

### ⚠ 5V Logic Level Warning

The Arduino Mega 2560 operates at **5V logic**:

- **Do NOT connect 3.3V sensors/devices directly** without level shifting
- **Do NOT connect Mega outputs to 3.3V device inputs** — the 5V signal can damage them
- Use a **bidirectional level shifter** for I2C/SPI/GPIO between 5V and 3.3V devices

### Low Power

The ATmega2560 supports sleep modes, but TinyGo has limited support:

```go
// TinyGo does not have full sleep mode support on AVR
// For low-power applications, consider using Arduino/C++ instead
```

---

## Special Features

- **54 digital I/O pins** — The most of any classic Arduino
- **16 analog inputs** — All can also be used as digital I/O (unlike Nano's A6/A7)
- **15 PWM outputs** — D2–D13, D44, D45, D46
- **4 hardware UARTs** — Serial0–Serial3 for multi-device communication
- **6 external interrupts** — D2, D3, D18, D19, D20, D21
- **8 KB SRAM** — 4× more than Uno/Nano
- **256 KB Flash** — 8× more than Uno/Nano
- **4 KB EEPROM** — 4× more than Uno/Nano
- **Uno shield compatible** — Same header layout on one end for shield compatibility
- **ICSP header** — For direct AVR programming
- **Barrel plug power** — Same as Uno R3

---

## Common Gotchas / Notes

1. **5V logic** — All GPIO pins are 5V; use level shifters for 3.3V devices
2. **SPI pins are D50–D53** — NOT D10–D13 like Uno/Nano; Uno shields using SPI won't work without rewiring
3. **I2C pins are D20/D21** — NOT A4/A5 like Uno/Nano; rewire when porting projects
4. **D0/D1 shared with Serial0** — Same as Uno; conflicts with USB-serial
5. **D13 LED** — Still on D13 but D13 is also PWM on the Mega (unlike Uno)
6. **Pin numbering differences** — Port mappings differ from Uno; verify pin constants
7. **8 KB SRAM** — More than Uno but still limited for TinyGo; avoid large allocations
8. **Multiple UARTs in TinyGo** — UART1–3 support may be limited; check release notes
9. **No USB CDC** — Serial goes through ATmega16U2
10. **10-bit ADC only** — Same 10-bit resolution as Uno/Nano
11. **No DAC** — No analog output; use PWM
12. **No wireless** — No WiFi or Bluetooth
13. **Larger bootloader** — 8 KB bootloader (vs 0.5 KB on Uno R3)

---

## Reference Links

- **Arduino Mega 2560 docs:** https://docs.arduino.cc/hardware/mega-2560/
- **TinyGo target docs:** https://tinygo.org/docs/reference/microcontrollers/arduino-mega2560/
- **ATmega2560 datasheet:** https://ww1.microchip.com/downloads/en/devicedoc/atmel-2549-8-bit-avr-microcontroller-atmega640-1280-1281-2560-2561_datasheet.pdf
- **Pinout PDF:** https://docs.arduino.cc/resources/pinouts/A000067-full-pinout.pdf
- **Datasheet:** https://docs.arduino.cc/resources/datasheets/A000067-datasheet.pdf

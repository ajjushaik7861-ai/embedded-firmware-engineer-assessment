# Embedded Firmware Engineer Assessment

**Candidate:** MD ABDUL AZEEZ
**Email:** [mdabdulazeez1602@gmail.com](mailto:mdabdulazeez1602@gmail.com)
**Domain:** Embedded Systems / Firmware Development
**Language:** C

## Overview

This repository contains my implementation for an **Embedded Firmware Engineer technical assessment**.

The solution focuses on low-level C programming, register-level peripheral control, bit manipulation, concurrency, interrupt-safe programming, and embedded driver development.

The implementation is written with emphasis on **correctness, readability, portability, and safe hardware interaction**.

## Assessment Tasks

### 1. Generic Bit-Field Helpers

Implemented reusable functions for:

* Extracting a bit field from a 32-bit register
* Updating a bit field without modifying unrelated bits
* Handling the special case of a 32-bit-wide field safely

Functions:

```c
uint32_t get_field(uint32_t reg_val,
                   uint32_t bit_offset,
                   uint32_t width);

uint32_t set_field(uint32_t reg_val,
                   uint32_t bit_offset,
                   uint32_t width,
                   uint32_t value);
```

### 2. SPX-100 Peripheral Driver

Implemented the required driver functions for the SPX-100 peripheral.

The implementation includes:

* Peripheral initialization
* Clock divider configuration
* Enable control
* Transmit data handling
* Start operation
* Busy-status polling
* Completion detection
* Error detection
* Timeout handling
* Write-1-to-clear status handling
* Required initialization sequence based on the specified hardware errata

Functions:

```c
bool spx_is_enabled(void);
void spx_init(uint8_t clkdiv);
int spx_send_byte(uint8_t data);
bool spx_is_busy(void);
```

### 3. ISR-Shared Counter

Implemented a counter shared between interrupt context and normal execution using **C11 atomic operations**.

This prevents lost updates when the counter is accessed concurrently.

Functions:

```c
void counter_isr_increment(void);
uint32_t counter_read(void);
```

### 4. ISR-Safe Ring Buffer

Implemented a **single-producer/single-consumer (SPSC) ring buffer** suitable for communication between interrupt context and the main/application context.

Features include:

* Fixed-size buffer
* Push operation
* Pop operation
* Full-buffer detection
* Empty-buffer detection
* `NULL` pointer protection
* Atomic head/tail management
* Acquire/release memory ordering

Functions:

```c
int rb_push(uint8_t byte);
int rb_pop(uint8_t *out);
```

### 5. Write-1-to-Clear Register Handling

Documented the safe method for handling independent write-1-to-clear status flags.

Separate writes are preferred over read-modify-write operations because status bits may change asynchronously between the read and write operations.

## Design Considerations

The implementation follows several embedded-systems best practices:

* Avoid undefined behavior in bit manipulation
* Preserve unrelated register fields where required
* Respect hardware register semantics
* Handle asynchronous status changes safely
* Use bounded polling instead of infinite loops
* Protect shared data accessed from interrupt context
* Use atomic operations where concurrency requires them
* Keep the implementation simple and readable

## Repository Structure

```text
embedded-firmware-engineer-assessment/
│
├── candidate.c
├── mock_peripheral.h
├── hw_sim.h
├── hw_sim.c
├── example_selftest.py
├── README.md
└── .gitignore
```

## Build Environment

The implementation is intended to be compiled using a C11-compatible compiler such as GCC.

Example:

```bash
gcc -std=c11 -Wall -Wextra -pedantic ...
```

## Testing

The implementation was checked against the supplied hardware simulation/self-test environment.

The basic assessment tests passed successfully during development.

Additional attention was given to edge cases such as:

* 32-bit bit-field operations
* Peripheral error conditions
* Polling timeout
* Concurrent counter updates
* Ring-buffer full/empty conditions
* `NULL` output handling

## Skills Demonstrated

* Embedded C
* Bit Manipulation
* Register-Level Programming
* Peripheral Driver Development
* Interrupt-Safe Programming
* C11 Atomics
* Concurrency
* Ring Buffers
* Hardware Register Handling
* Debugging and Testing

## Author

**MD ABDUL AZEEZ**

Embedded Systems / Firmware Engineer

**Email:** [mdabdulazeez1602@gmail.com](mailto:mdabdulazeez1602@gmail.com)


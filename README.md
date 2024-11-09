# BitVault Library

The **BitVault** library provides a versatile utility for managing bit flags in an efficient manner. It supports both non-atomic and atomic operations for use in single-threaded and multi-threaded environments respectively.

## Features

- **Bit Manipulation**: Easily set, clear, and retrieve the value of individual bits.
- **Atomic Operations**: Specialization for atomic bit manipulation in multi-threaded applications.
- **Configurable Type**: Supports any integer type (`uint8_t`, `uint16_t`, `uint32_t`, etc.) as the underlying bit container.

## Installation

1. Download or clone the repository containing the `BitVault.h` file.
2. Copy `BitVault.h` into your Arduino project directory.
3. Include `BitVault.h` in your project:

   ```cpp
   #include "BitVault.h"
   ```

## Usage

### Initialization

The `BitVault` class template has two main parameters:

- `T`: The underlying type for storing bits (e.g., `uint8_t`, `uint16_t`, `uint32_t`).
- `enable_atomic`: A boolean flag to enable atomic operations (default is `false`).

### Example 1: Non-atomic Usage

```cpp
#include <Arduino.h>
#include "BitVault.h"

void setup() {
    Serial.begin(9600);

    BitVault<uint8_t> vault;  // Non-atomic version

    vault.set(3, true);       // Set bit 3
    Serial.println(vault.get(3));  // Prints: 1

    vault.set(3, false);      // Clear bit 3
    Serial.println(vault.get(3));  // Prints: 0

    vault.clear_all();        // Clear all bits
}

void loop() {
    // Your loop code
}
```

### Example 2: Atomic Usage

For multi-threaded applications, enable atomic operations:

```cpp
#include <Arduino.h>
#include "BitVault.h"

void setup() {
    Serial.begin(9600);

    BitVault<uint32_t, true> atomicVault;  // Atomic version

    atomicVault.set(15, true);             // Set bit 15 atomically
    Serial.println(atomicVault.get(15));   // Prints: 1

    atomicVault.set(15, false);            // Clear bit 15 atomically
    Serial.println(atomicVault.get(15));   // Prints: 0

    atomicVault.clear_all();               // Clear all bits atomically
}

void loop() {
    // Your loop code
}
```

### API Reference

#### `bool get(uint8_t position) const`
- **Description**: Retrieves the value of the bit at the specified position.
- **Parameters**: 
  - `position`: The bit position to query.
- **Returns**: `true` if the bit is set, `false` otherwise.

#### `void set(uint8_t position, bool value)`
- **Description**: Sets or clears the bit at the specified position.
- **Parameters**:
  - `position`: The bit position to modify.
  - `value`: `true` to set the bit, `false` to clear it.

#### `void clear_all()`
- **Description**: Clears all bits by resetting the internal storage to `0`.

## Notes

- Use the non-atomic version for single-threaded applications to minimize overhead.
- Use the atomic version in multi-threaded contexts to ensure thread safety.

## License

This library is open-source. You are free to use and modify it in your projects.

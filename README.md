# BitVault Library

The **BitVault** library provides a versatile utility for managing bit flags in an efficient manner. It supports both non-atomic and atomic operations for use in single-threaded and multi-threaded environments respectively.

## Features

- **Bit Manipulation**: Easily set, clear, and retrieve the value of individual bits.
- **Atomic Operations**: Specialization for atomic bit manipulation in multi-threaded applications.
- **Configurable Type**: Supports any integer type (`uint8_t`, `uint16_t`, `uint32_t`, etc.) as the underlying bit container, allowing you to optimize memory usage based on the number of bits needed.

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

- `T`: The underlying type for storing bits (e.g., `uint8_t`, `uint16_t`, `uint32_t`). Choose this type based on the number of bits you need:
  - `uint8_t`: Suitable for up to 8 bits.
  - `uint16_t`: Suitable for up to 16 bits.
  - `uint32_t`: Suitable for up to 32 bits.
  - `uint64_t`: Suitable for up to 64 bits.
- `enable_atomic`: A boolean flag to enable atomic operations (default is `false`). Use this for multi-threaded applications to ensure thread safety.

### Choosing the Right Type

- **`uint8_t`**: Use this type if you only need to manage up to 8 individual bits. This is memory efficient and ideal for small projects.
- **`uint16_t`**: Use this type if you need to manage between 9 to 16 bits. It offers a balance between memory usage and flexibility for slightly larger bitsets.
- **`uint32_t`**: Use this type for managing up to 32 bits. This is suitable for projects requiring a larger set of flags without significant memory concerns.
- **`uint64_t`**: Use this type if you need to manage up to 64 bits. This is typically used in more complex projects where a large number of flags are required.

For multi-threaded environments, set the `enable_atomic` flag to `true` to ensure safe bit manipulation across multiple threads.

### Example 1: Non-atomic Usage

```cpp
#include <Arduino.h>
#include "BitVault.h"

#define BIT_FLAG_A 0
#define BIT_FLAG_B 1
#define BIT_FLAG_C 2
#define BIT_FLAG_D 3

void setup() {
    Serial.begin(9600);

    BitVault<uint8_t> vault;  // Non-atomic version

    vault.set(BIT_FLAG_A, true);       // Set bit 0
    Serial.println(vault.get(BIT_FLAG_A));  // Prints: 1

    vault.set(BIT_FLAG_A, false);      // Clear bit 0
    Serial.println(vault.get(BIT_FLAG_A));  // Prints: 0

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

#define BIT_FLAG_A 0
#define BIT_FLAG_B 1
#define BIT_FLAG_C 2
#define BIT_FLAG_D 3

void setup() {
    Serial.begin(9600);

    BitVault<uint32_t, true> atomicVault;  // Atomic version

    atomicVault.set(BIT_FLAG_B, true);             // Set bit 1 atomically
    Serial.println(atomicVault.get(BIT_FLAG_B));   // Prints: 1

    atomicVault.set(BIT_FLAG_B, false);            // Clear bit 1 atomically
    Serial.println(atomicVault.get(BIT_FLAG_B));   // Prints: 0

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
- Choose the appropriate underlying type (`uint8_t`, `uint16_t`, `uint32_t`, etc.) based on the number of bits you need to manage, as each type provides a specific number of bits: `uint8_t` provides 8 bits, `uint16_t` provides 16 bits, `uint32_t` provides 32 bits, and `uint64_t` provides 64 bits. This helps optimize memory usage.

## License

This library is open-source. You are free to use and modify it in your projects.


# BitVault

**BitVault** is a lightweight C++ utility designed to efficiently store and manage multiple boolean values using bitwise operations. It minimizes memory usage by compacting booleans into a single integral type.

## Features

- Compact storage for multiple boolean values.
- Easy-to-use methods for setting, clearing, and retrieving boolean flags.
- Template-based design allows flexible sizing with various integral types (`uint8_t`, `uint16_t`, `uint32_t`, etc.).

## Installation

Simply include the `BitVault.h` file in your project.

```cpp
#include "BitVault.h"
```

## Usage

### 1. Create a BitVault instance

You can specify the underlying storage type when creating a `BitVault`. This determines how many booleans you can store.

```cpp
#include "BitVault.h"

BitVault<uint32_t> vault;  // Stores up to 32 boolean values
```

### 2. Define Bit Names (Optional)

To improve code readability, you can define bit positions with meaningful names using `#define` or `enum`.

```cpp
#define BIT_ERROR 0
#define BIT_READY 1
#define BIT_PROCESSING 2
#define BIT_COMPLETE 3

// Alternatively, use an enum
enum BitPositions {
    BIT_ERROR = 0,
    BIT_READY,
    BIT_PROCESSING,
    BIT_COMPLETE
};
```

### 3. Set a boolean value

Use the `set` method to set a specific bit (boolean value) at a given position.

```cpp
vault.set(BIT_READY, true);  // Set the "READY" flag to true
vault.set(BIT_ERROR, false); // Set the "ERROR" flag to false
```

### 4. Retrieve a boolean value

Use the `get` method to retrieve the boolean value at a specific position.

```cpp
bool isReady = vault.get(BIT_READY);  // Retrieve the "READY" flag
```

### 5. Clear all boolean values

Use the `clear_all` method to reset all bits to `false`.

```cpp
vault.clear_all();  // Clears all boolean values (sets all bits to 0)
```

## Example

Here’s a complete example demonstrating the usage of **BitVault**:

```cpp
#include "BitVault.h"

#define BIT_ERROR 0
#define BIT_READY 1
#define BIT_PROCESSING 2
#define BIT_COMPLETE 3

int main() {
    BitVault<uint32_t> vault;  // Create a BitVault with 32-bit storage

    vault.set(BIT_READY, true);    // Set "READY" flag
    vault.set(BIT_COMPLETE, true); // Set "COMPLETE" flag
    vault.set(BIT_ERROR, false);   // Clear "ERROR" flag

    bool ready = vault.get(BIT_READY);       // Get "READY" flag
    bool complete = vault.get(BIT_COMPLETE); // Get "COMPLETE" flag
    bool error = vault.get(BIT_ERROR);       // Get "ERROR" flag

    vault.clear_all(); // Clear all flags

    return 0;
}
```

## Template Parameter

The class is templated to allow different storage capacities:

- `uint8_t`: 8 boolean values
- `uint16_t`: 16 boolean values
- `uint32_t`: 32 boolean values
- `uint64_t`: 64 boolean values

## Limitations

- **Bit Position Range:** Ensure the bit position (`set` and `get` methods) is within the valid range for the chosen type.
- **Thread Safety:** The current implementation is not thread-safe.**

## License

This project is licensed under the MIT License. Feel free to use and modify it as needed.

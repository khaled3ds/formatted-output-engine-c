# Formatted Output Engine in C

## Overview

This project is a custom implementation of a formatted output engine inspired by the standard C `printf()` function.

It parses format strings at runtime and dispatches conversion handlers to generate formatted output directly to file descriptor 1 (stdout).

The goal is to reproduce core `printf` behavior while gaining deep understanding of:

- Variadic functions
- Format string parsing
- Type dispatching
- Numeric base conversion
- Low-level output control

---

## Supported Format Specifiers

- `%c` – character
- `%s` – string
- `%p` – pointer
- `%d` – signed decimal integer
- `%i` – integer
- `%u` – unsigned integer
- `%x` – lowercase hexadecimal
- `%X` – uppercase hexadecimal
- `%%` – percent symbol

---

## Core Concepts Demonstrated

- `va_list`, `va_start`, `va_arg`, `va_end`
- Manual integer to string conversion
- Base transformation (decimal → hexadecimal)
- Pointer formatting
- Recursive number printing
- Output length tracking

---

## Internal Architecture

### 1. Format Parser

The function scans the format string character by character:

```
Regular char → write directly
'%' detected → parse next specifier → dispatch handler
```

---

### 2. Dispatcher Model

Each specifier is mapped to a dedicated handler function:

- Character handler
- String handler
- Number handler
- Hex handler
- Pointer handler

This keeps logic modular and extensible.

---

### 3. Number Conversion Strategy

- Signed integers handled with sign detection
- Unsigned integers converted via division recursion
- Hex conversion using base-16 mapping table
- Pointer formatting prefixed with `0x`

---

## Execution Flow

```
ft_printf("Value: %d", 42)
        ↓
Parse string
        ↓
Detect %d
        ↓
Retrieve argument via va_arg
        ↓
Convert integer to string
        ↓
Write to stdout
        ↓
Return total printed length
```

---

## Compilation

```
make
```

Produces:

```
libftprintf.a
```

---

## Usage Example

```c
ft_printf("Hello %s, value = %d\n", "world", 42);
```

---

## Memory Strategy

- No global buffers
- Direct write operations
- Minimal dynamic allocation
- Deterministic output size tracking

---

## Error Handling

- NULL string protection
- Safe pointer formatting
- Correct return value behavior (total printed length)

---

## Complexity

- Time complexity proportional to format string length
- Conversion complexity proportional to number magnitude
- No unnecessary buffer duplication

---

## What This Project Demonstrates

This implementation reflects:

- Strong understanding of C variadic functions
- Runtime parsing logic
- Low-level formatting mechanics
- Modular handler design
- Precise output control

Applicable to:

- Logging systems
- Debugging tools
- Embedded systems
- Custom output engines

---

## Future Improvements

- Width and precision handling
- Flag support (`-`, `0`, `#`, `+`, space)
- Floating-point formatting
- File descriptor abstraction

---

## Author

Khaled Adas  
Systems Programming | C | Runtime Parsing

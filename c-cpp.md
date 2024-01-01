# C/C++ Coding Style

The coding style for C/C++ mostly follows the [K&R Style](https://en.wikipedia.org/wiki/Indentation_style#K.26R_style).

This repository contains a [Clang-format](https://clang.llvm.org/docs/ClangFormat.html) file which can be used to format the code automatically based on below rules.

## General rules

- Indentation with 4 spaces (tabs not allowed)
- Space before pointer or reference symbols `*` and `&` placed adjacent to name (e.g. `int *var`)
- No space before opening brace of function: `void foo(int arg);`
- One space after `if`, `for`, `while` and `switch` statements.
- Always use curly braces for `if` and `for` statements, even for one line.
- Curly braces for functions and classes start in next line, for flow statements (`if`, `while`, `switch`, `for`) in the same line.
- Access modifiers in C++ classes (`public`, `private`, `protected`) are not indented.
- Precompiler statemens (`#define`, `#ifdef`, etc.) are not indented.
- Maximum line length of 100 characters
- No spaces at end of a line or in an empty line
- One empty new-line at the end of the file
- Linux-style line-ending (LF or `\n`)

## Naming

- Class names use `PascalCase` or `UpperCamelCase`. Acronyms are treated as a single word (a JSON parser is named `JsonParser`).
- Struct names use `snake_case`. A typedef with the same name in `PascalCase` may be used, so that a struct object can be declared similar to a class in C++. Other typedefs for structs (e.g. short names with `_t` or `_s` suffix) are [not allowed](https://www.kernel.org/doc/html/latest/process/coding-style.html#typedefs).
- Enums use `snake_case` for their name and `UPPER_CASE` for their elements. Typedefs for enums are not allowed.
- Function or method names use `snake_case`.
- Global and local variables, parameters and class/struct/union member names also use `snake_case`.
- Preprocessor macros and defines use `UPPER_CASE`.
- File names are always lower case to prevent incompatibilities between different operating systems.
- Each header file should contain header guard defines using the file path/name in upper case letters (e.g. `PATH_TO_MY_FILE_H_`) without any underscores `_` at the beginning, as names with underscores are [reserved for C libraries](https://www.gnu.org/software/libc/manual/html_node/Reserved-Names.html).

## Other

- C++/C99-style comments `//` are allowed
- Expressions behind defines must be enclosed in braces, e.g. `#define (3*1034)`
- Comments should be in Doxygen style where applicable.
- Order of includes (see also [here](https://google.github.io/styleguide/cppguide.html#Names_and_Order_of_Includes)): Related header, C system headers, C++ standard library headers, other project headers.

## Example

Header file `example.h`

```C++
#ifndef EXAMPLE_H_
#define EXAMPLE_H_

#include <stddef.h>

/**
 * Character buffer to store strings incl. their maximum size
 */
struct buffer
{
    char *str;      ///< Pointer to string in memory
    size_t size;    ///< Maximum size of buffer
};

enum state
{
    STATE_ON,
    STATE_OFF,
};

/**
 * Description of MyClass
 */
class MyClass
{
public:
    MyClass();

private:
    /**
     * Description of member function.
     */
    void member_func(char c);

    /**
     * This variable is used for foo.
     */
    int member_var;
}

/**
 * State machine of this nice embedded hardware
 *
 * @param buf Some description here
 * @param foo Meaning of this variable here
 */
void state_machine(struct buffer *buf, int foo);

#endif /* EXAMPLE_H_ */

```

Implementation file `example.cpp`

```C++
#include "example.h"

static enum state current_state;

void state_machine(struct buffer *buf, int foo)
{
    switch (current_state) {
        case STATE_ON:
            do_something();
            break;
        case STATE_OFF:
            return;
            break;
    }

    if (buf->str != NULL) {
        // ...
    }
    else {
        // ...
    }

    for (int i = 0; i < 10; i++) {
        // ...
    }
}
```

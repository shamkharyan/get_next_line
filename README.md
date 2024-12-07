# 📜 About `get_next_line`

`get_next_line` is a project in 42 Yerevan common core where you will learn how to work with static variables, files, buffers and dynamic memory.
In the get_next_line project you must implement the `get_next_line` function, which reads the file line by line and returns the current line.
The function has "memory" because it returns the next line at each call.

## 🧪 How to use

- Add `get_next_line` repository to the root directory of the project.
- Include the header file of the library in your .c files using `#include "get_next_line.h"`.
- If you need to work with multiple files in your project, use `#include "get_next_line_bonus.h`.
- Compile mandatory or bonus files from repository. You can compile with `-D BUFFER_SIZE=n` flag, where n is the size of the buffer.

## 🔍 How it works

`get_next_line` function stores characters from file descriptor in the static buffer, then dynamically allocates memory to construct the next complete line.
After constructing it returns the line including the `\n` character. If there are no more lines left, it returns `NULL`.
Since it alocates the memory every time, after each call you have to delete the allocated line manually.

### Function Prototype:
```C
char *get_next_line(int fd);
```

### Example of Work:

For example we have file `example.txt` file, which contains:

```
Hello, World!
This is get_next_line.
Enjoy coding!
```
After each call of get_next_line, you will get:
1. `"Hello, World!"`
2. `"This is get_next_line."`
3. `"Enjoy coding!"`
4. `NULL`
5. `NULL`

Here is example of usage:
```C
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd = open("example.txt", O_RDONLY);
    if (fd < 0)
        return (1);
    
    char *line;
    while ((line = get_next_line(fd)))
    {
        printf("%s\n", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## 📂 Repository Structure
- [`get_next_line.c`](get_next_line.c) - core implementation of the function.
- [`get_next_line_utils.c`](get_next_line_utils.c) - utility functions for memory and string operations.
- [`get_next_line.h`](get_next_line.h) - function prototypes and macros.
- [`get_next_line_bonus.c`](get_next_line_bonus.c) - core implementation of the function with multi-file reading support.
- [`get_next_line_utils_bonus.c`](get_next_line_utils_bonus.c) - utility functions for memory and string operations with multi-file reading support.
- [`get_next_line_bonus.h`](get_next_line_bonus.h) - function prototypes and macros with multi-file reading support.

## 🤝 Contributing
Contributions, bug reports, and feature requests are welcome! Feel free to open an issue or submit a pull request.

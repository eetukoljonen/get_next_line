# get_next_line

Get Next Line (GNL) is a function that allows you to read text from a file descriptor one line at a time, including text from standard input.
This README will provide an overview of the project, its requirements, and how to use it.

# Requirements
The GNL project has the following requirements:

1. **Repeated Calls:** Repeated calls (e.g., using a loop) to your get_next_line() function should allow you to read a text file pointed to by the file descriptor, one line at a time.

2. **Return Value:** Your function should return the line that was read. If there is nothing else to read or if an error occurred, it should return NULL.

3. **Terminating '\n' Character:** The returned line should include the terminating \n character, except if the end of the file was reached and does not end with a \n character.

4. **Header File:** Your get_next_line.h header file must contain at least the prototype of the get_next_line() function.

5. **Helper Functions:** You should add all the helper functions you need in the get_next_line_utils.c file.

6. **Buffer Size:** The buffer size for read() should be defined using the -D compiler option: -D BUFFER_SIZE=n.

7. **Undefined Behavior:** GNL has undefined behavior if the file pointed to by the file descriptor changed since the last call, whereas **read()** didn't reach the end of the file. It also has undefined behavior when reading a binary file.

# Usage

To use GNL in your C code, follow these steps:

1. Clone the repository to your local machine:
```
https://github.com/eetukoljonen/get_next_line.git
```
2. Compile your program, including the -D BUFFER_SIZE=n option to specify the buffer size (e.g., BUFFER_SIZE=42):
```
cc -Wall -Wextra -Werror -D BUFFER_SIZE=n get_next_line.c get_next_line_utils.c
```
3. Include the **get_next_line.h** header file in your code and call the **get_next_line()** function as needed to read lines from a file descriptor.
```
#include "get_next_line.h"
#include <fcntl.h>

int main() {
    int fd;
    char *line;

    // Open a file or standard input
    fd = open("example.txt", O_RDONLY);

    // Read lines using get_next_line
    while ((line = get_next_line(fd)) != NULL) {
        printf("Line: %s\n", line);
        free(line); // Don't forget to free the line
    }

    close(fd);
    return (0);
}

```

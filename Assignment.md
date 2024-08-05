## LAB ASSIGNMENT (PAS078BEI041)

### Question: Describe and discuss the use case of the following:

1. **fork()**
   - The `fork()` system call is essential in operating systems for process creation. It generates a new process by duplicating the calling process, creating a child process while the original remains as the parent. Both processes then execute the subsequent instruction after `fork()`.

2. **exec()**
   - The `exec()` function runs an executable file within the context of an existing process, replacing the current executable. When invoked, it terminates the current shell process and initiates a new one.

3. **getpid()**
   - The `getpid()` function, which takes no arguments, returns the process ID (PID) of the calling process. It is particularly useful for parent processes to manage and coordinate with their child processes after creation via `fork()`.

4. **wait()**
   - The `wait()` function is used by a parent process to pause execution until one of its child processes terminates. This helps in managing the lifecycle of child processes, especially when multiple are spawned.

5. **stat()**
   - The `stat()` function retrieves information about a file or directory, including size, permissions, owner, and timestamps. It stores this information in a structure with various fields representing different attributes of the file.

6. **opendir()**
   - The `opendir()` function opens a directory stream, which can then be read using functions like `readdir()` and closed with `closedir()`. It is commonly used in utilities that manage or analyze directory contents.

7. **readdir()**
   - The `readdir()` function reads directory entries from a directory stream opened with `opendir()`, allowing iteration through directory contents and retrieval of information about each file or subdirectory.

8. **close()**
   - The `close()` function closes a file descriptor, which is an integer handle used by the operating system to identify an open file, socket, or other I/O resource. Closing the file descriptor releases associated resources and marks it as no longer in use.

---

### C Program for Producer-Consumer Problem

```c
#include <stdio.h>
#include <stdlib.h>

// Initialize a mutex to 1
int mutex = 1;

// Number of full slots as 0
int full = 0;

// Number of empty slots as the size of the buffer
int empty = 10, x = 0;

// Function to produce an item and add it to the buffer
void producer() {
    --mutex;  // Decrease mutex by 1
    ++full;   // Increase the number of full slots by 1
    --empty;  // Decrease the number of empty slots
    x++;
    printf("\nProducer produces item %d", x);
    ++mutex;
}

// Function to consume an item and remove it from the buffer
void consumer() {
    --mutex;
    --full;
    ++empty;
    printf("\nConsumer consumes item %d", x);
    x--;
    ++mutex;
}

int main() {
    int n, i;
    printf("\n1. Press 1 for Producer");
    printf("\n2. Press 2 for Consumer");
    printf("\n3. Press 3 for Exit");

    printf("\nEnter your choice:");
    scanf("%d", &n);

    // Switch cases
    switch(n) {
        case 1:
            if((mutex == 1) && (empty != 0)) {
                producer();
            } else {
                printf("Buffer is full");
            }
            break;

        case 2:
            if((mutex == 1) && (full != 0)) {
                consumer();
            } else {
                printf("Buffer is empty!");
            }
            break;

        case 3:
            exit(0);
            break;

        default:
            printf("Invalid choice!");
            break;
    }
    return 0;
}
```

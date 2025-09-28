#define _POSIX_C_SOURCE 200809L
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void) {
  int len = 5;
  char *lines[5] = {NULL};
  size_t size = 0;
  int line_count = 0;

  while (1) {
    printf("Enter input: ");
    ssize_t num_char = getline(&lines[line_count % len], &size, stdin);

    if (num_char == -1) {
      perror("getline failed");
      exit(1);
    }

    // Remove any newline chars
    if (lines[line_count % len][num_char - 1] == '\n') {
      lines[line_count % len][num_char - 1] = '\0';
    }

    if (strcmp(lines[line_count % len], "print") == 0) {
      int start_index;

      if (line_count < len) { // Buffer isn't full
        start_index = 0;
      } else { // Buffer is full, start at the oldest string
        start_index = (line_count + 1) % len;
      }

      for (int i = 0; i < len; i++) {
        int index = (start_index + i) % len;

        if (lines[index] != NULL) {
          printf("%s\n", lines[index]);
        }
      }
    }

    line_count++;
    size = 0; // Reset the size for the next line of input
  }

  return 0;
}

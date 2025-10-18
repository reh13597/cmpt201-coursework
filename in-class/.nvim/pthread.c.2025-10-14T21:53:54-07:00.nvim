#include <pthread.h>
#include <stdio.h>
#include <string.h>

// Thread function
void *thread_function(void *arg) {
  // Cast argument to string
  char *msg = (char *)arg;

  // Print the received string and own thread ID
  printf("[Thread] Received string: \"%s\"\n", msg);
  printf("[Thread] My thread ID: %lu\n", (unsigned long)pthread_self());

  // Calculate string length
  long length = (long)strlen(msg);

  // Return the length (cast to void*)
  return (void *)length;
}

int main() {
  pthread_t tid;
  char *msg = "Hello from main thread!";
  void *return_value;

  printf("=== pthread Activity ===\n\n");

  // Create the new thread
  if (pthread_create(&tid, NULL, thread_function, msg) != 0) {
    fprintf(stderr, "Error creating thread\n");
    return 1;
  }

  // Print the new thread's ID
  printf("[Main] Created thread with ID: %lu\n", (unsigned long)tid);

  // Wait for the thread to terminate and get return value
  if (pthread_join(tid, &return_value) != 0) {
    fprintf(stderr, "Error joining thread\n");
    return 1;
  }

  // Print the return value (string length)
  printf("[Main] Thread returned: %ld\n", (long)return_value);
  printf("[Main] This is the length of: \"%s\"\n", msg);

  return 0;
}

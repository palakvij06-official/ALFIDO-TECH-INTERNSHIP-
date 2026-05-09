#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    int fd[2];
    pipe(fd);

    pid_t pid = fork();

    if (pid > 0) {
        // Producer
        close(fd[0]);
        int data = 100;
        write(fd[1], &data, sizeof(data));
        printf("Produced: %d\n", data);
    }
    else {
        // Consumer
        close(fd[1]);
        int data;
        read(fd[0], &data, sizeof(data));
        printf("Consumed: %d\n", data);
    }

    return 0;
}

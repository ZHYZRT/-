#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ioctl.h>
#include <fcntl.h>

#define SCREEN_WIDTH 80
#define SCREEN_HEIGHT 25

void draw_fireworks(int x, int y)
{
    for (int i = 0; i < 10; i++) {
        // 随机生成烟花绽放的位置
        int x_random = rand() % SCREEN_WIDTH;
        int y_random = rand() % SCREEN_HEIGHT;

        // 打印烟
        printf("⭐");

        // 等待一段时间
        usleep(20000);
    }
}

int main()
{
    // 获取控制台窗口的大小
    struct winsize ws;
    if (ioctl(0, TIOCGWINSZ, &ws) == -1) {
        perror("Failed to get console window size");
        exit(EXIT_FAILURE);
    }

    // 调整窗口大小以适应屏幕大小
    if (ws.ws_col < SCREEN_WIDTH || ws.ws_row < SCREEN_HEIGHT) {
        printf("The console window is too small.\n");
        exit(EXIT_FAILURE);
    }

    // 绘制烟花
    for (int i = 0; i < 100; i++) {
        draw_fireworks(rand() % SCREEN_WIDTH, rand() % SCREEN_HEIGHT);
    }

    return 0;
}


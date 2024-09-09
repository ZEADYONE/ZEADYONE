#include <stdio.h>
#include <conio.h>
#include <graphics.h>
#include <stdlib.h>
#include <windows.h>




void sun() {
    setcolor(WHITE);
    setfillstyle(SOLID_FILL, YELLOW);
    pieslice(550, 60, 0, 360, 50);
}

void may() {
    setcolor(WHITE);
    setfillstyle(SOLID_FILL, WHITE);
    long long a = rand() % 500, b = rand() % 50;
    fillellipse(100 + a, 70 + b, 50, 40);
    fillellipse(150 + a, 70 + b, 40, 30);
    fillellipse(50 + a, 70 + b, 40, 30);
    fillellipse(80 + a, 50 + b, 40, 30);
    fillellipse(120 + a, 50 + b, 40, 30);
}

void duong() {
    setfillstyle(1, LIGHTGREEN);
    bar(0, 450, 800, 500);
    sector(200,350,0,180,200,100);
    sector(500,350,0,180,200,100);
   

    setfillstyle(1, LIGHTGRAY);
    bar(0, 350, 800, 450);
    setlinestyle(0, 4, 2);
    line(0, 360, 800, 360);
    line(0, 440, 800, 440);
    for (long long  i = 50; i <= 550; i += 100) {
        line(i, 400, i + 50, 400);
        
    }
}

int main() {
    int driver = 0, mode = 0, maloi;
    initgraph(&driver, &mode, (char*)"");
    if ((maloi = graphresult()) != 0) {
        printf("khong the khoi dong do hoa \n");
        printf("ma loi : %d \nTran Van Nhuom %s ", maloi, grapherrormsg(maloi));
        getch();
        exit(1);
    }

    long long  i = 0, m = 1, j = 0 ;
    long long page = 0;
    long long max_width = getmaxx();  // Lấy giới hạn chiều rộng của màn hình

    while (1) {
        setactivepage(page);
        cleardevice();  // Xóa trang active trước khi vẽ

        setbkcolor(LIGHTBLUE);
        sun();
        may(); may(); may();
        
        duong();

        // Vẽ người chạy
        setcolor(WHITE);
        circle(50 + i, 300+j, 15);  // Đầu
        line(50 + i, 315+j, 50 + i, 350+j);  // Thân
        line(50 + i, 330+j, 20 + i, 320+j);  // Tay trái
        line(50 + i, 330+j, 80 + i, 320+j);  // Tay phải

        // Chân
        if (m % 2 == 0) {
            line(50 + i, 350+j, 50 + i, 390+j);  // Chân thẳng
        } else {
            line(50 + i, 350+j, 35 + i, 390+j);  // Chân trái
            line(50 + i, 350+j, 65 + i, 390+j);  // Chân phải
        }

        // Di chuyển theo phím
        if (GetAsyncKeyState(VK_LEFT)) {
            if (i >-40) {  // Giới hạn người chạy không ra khỏi màn hình bên trái
                i -= 5;
                m++;
            }
        }
        if (GetAsyncKeyState(VK_RIGHT)) {
            if (i < max_width - 50) {  // Giới hạn người chạy không ra khỏi màn hình bên phải
                i += 5;
                m++;
            }
        }
        if (GetAsyncKeyState(VK_ESCAPE)) {  // Thêm thoát bằng phím ESC
            break;
        }
        if ( GetAsyncKeyState(VK_UP)) {    // Di chuyển ra xa
        	j-=5;
		}
		if ( GetAsyncKeyState(VK_DOWN)) { // Di chuyển lại gần
        	j+=5;
		}
		

        setvisualpage(page);  // Hiển thị trang hiện tại
        
        page = 1 - page;  // Chuyển đổi giữa 2 trang

        delay(50);  // Giảm độ trễ để chuyển trang mượt mà hơn
        
    }

    closegraph();
    return 0;
}

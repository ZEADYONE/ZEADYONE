#include <stdio.h>
#include <conio.h>
#include <graphics.h>
#include <stdlib.h>
#include <windows.h>
#include <time.h>
#include<math.h>
#define CLOUD_COUNT 5

// Khai báo mảng vị trí đám mây
long long cloud_positions[CLOUD_COUNT][2];
// VẼ CHIM
void drawBird_1(int x, int y, float a){
    setcolor(0);
    int b1[10] = {a*(x- 20), a*(y - 15), a*x, a*(y+5), a*(x+20), a*(y - 15), a*x, a*(y - 5), a*(x - 20), a*(y-15)};
    drawpoly(5, b1);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

void drawBird_2(int x, int y, float a){
    setcolor(0);
    int b2[10] = {a*(x - 20), a*(y -10), a*x, a*(y + 3), a*(x + 20), a*(y - 10), a*(x), a*(y - 5), a*(x - 20), a*(y - 10)};
    drawpoly(5, b2);
    setfillstyle(1, 0);
    floodfill(a*(x), a*(y), 0);
    setcolor(15);
}

void drawBird_3(int x, int y, float a){
    setcolor(0);
    int b3[10] = {a*(x - 20), a*(y), a*x, a*(y+5), a*(x+20), a*y, a*x, a*(y - 2), a*(x - 20), a*y};
    drawpoly(5, b3);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

void drawBird_4(int x, int y, float a){
    setcolor(0);
    int b4[10] = {a*(x - 20), a*(y + 10), a*x, a*(y + 5), a*(x + 20), a*(y + 10), a*x, a*(y - 3), a*(x - 20), a*(y+10)};
    drawpoly(5, b4);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

void drawBird_5(int x, int y, float a){
    setcolor(0);
    int b5[10] = {a*(x - 20), a*(y + 15), a*x, a*(y+5), a*(x+20), a*(y+15), a*x, a*(y - 5), a*(x - 20), a*(y+15)};
    drawpoly(5, b5);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

// HÀM VẼ MẶT TRỜI
void sun() {
    setcolor(WHITE);
    setfillstyle(SOLID_FILL, YELLOW);
    circle(550, 60 , 50);
    floodfill(550, 60, WHITE);
}


// VẼ LÁ
void vehoa(int x, int y) {
	setcolor(LIGHTMAGENTA);
    setfillstyle(SOLID_FILL, LIGHTMAGENTA);
    fillellipse(x, y, 3, 3); 
}
// KHỞI TẠO GIÁ TRỊ CHO HOA
int ax[60], ay[60], tocdo[60], tocdox[60];	
// HIỆU ỨNG HOA RƠI
void vela() {
	for ( int i = 0 ; i < 60 ; i++ ) {
		vehoa(ax[i],ay[i]);
		ax[i] = ax[i] + tocdox[i] ; // cho hoa rơi theo phương ngang 
		ay[i] = ay[i] + tocdo[i];	// cho hoa rơi theo phương dọc 
		
		// khởi tạo lại giá trị khi hoa rơi khỏi màn hình 
		if ( ax[i] > getmaxx() || ay[i] > getmaxy() || ax[i] < 0 || tocdo[i] == 0   ) {
			ax[i] = rand() % getmaxx() ;
			ay[i] = 0 ;
			tocdox[i] = rand() % 5 + (-1);
			tocdo[i] = rand()  % 3;
		}
		
	}
}


// HÀM VẼ ĐÁM MÂY
void may() {
    setcolor(WHITE);
    setfillstyle(SOLID_FILL, WHITE);
    for (int k = 0; k < CLOUD_COUNT; k++) {
        fillellipse(cloud_positions[k][0], cloud_positions[k][1], 50, 40);
        fillellipse(cloud_positions[k][0] + 50, cloud_positions[k][1], 40, 30);
        fillellipse(cloud_positions[k][0] - 50, cloud_positions[k][1], 40, 30);
        fillellipse(cloud_positions[k][0] + 30, cloud_positions[k][1] - 20, 40, 30);
        fillellipse(cloud_positions[k][0] - 30, cloud_positions[k][1] - 20, 40, 30);
    }
}


// HÀM VẼ NÚI
void nui() {
    setcolor(GREEN);
    setfillstyle(SOLID_FILL, LIGHTGREEN);
    int mountain1[] = {0, 300, 200, 150, 400, 300, 0, 300};
    fillpoly(4, mountain1);
    
    int mountain2[] = {300, 300, 500, 100, 700, 300, 300, 300};
    fillpoly(4, mountain2);
}




// HÀM VẼ ĐƯỜNG
void duong() {
    setfillstyle(1,LIGHTGREEN);
    bar(0, 450, 800, 500);
    

    setfillstyle(1, LIGHTGRAY);
    bar(0, 350, 800, 450);
    setfillstyle(1, LIGHTCYAN);
    bar(0,300,800,350);
    setfillstyle(1, DARKGRAY);
    bar(0,300,800,310);
    setlinestyle(0, 4, 2);
    line(0, 360, 800, 360);
    line(0, 440, 800, 440);
    for (long long i = 50; i <= 550; i += 100) {
        line(i, 400, i + 50, 400);
    }
}


// CỐI XAY GIÓ
void coixaygio ( int tamx, int tamy, int w, int h , int angle = 0 ) {

double theta = ( double ) (angle%180)*3.14/180.0	;
	int dx = w/2;
	int dy = h/2;
// tọa độ của 4 điểm trong hcn
	int point[8] = {
(int) (-dx*cos(theta) - dy*sin(theta) + tamx),
(int) (-dx*sin(theta) + dy*cos(theta) + tamy),
(int) (dx*cos(theta) - dy*sin(theta) + tamx),
(int) (dx*sin(theta) + dy*cos(theta) + tamy), 
(int) (dx*cos(theta) + dy*sin(theta) + tamx),
(int) (dx*sin(theta)-  dy*cos(theta) + tamy),
(int) (-dx*cos(theta) + dy*sin(theta) + tamx),
(int) (-dx*sin(theta) -dy*cos(theta) + tamy)
};
// vẽ hình chữ nhật;
for(int i=0; i<8; i+=2)
line(point[i], point[i+1], point[(i+2)%8], point[(i+3)%8]);
circle(tamx,tamy,10);
}

// thân cối xay gió 
void tamgiac( int tamx, int tamy ) {
	int tamgiac[16] = {
		tamx,tamy,
		tamx+40,tamy+75,
		tamx+10,tamy+75,
		tamx+10,tamy+55,
		tamx-10,tamy+55,
		tamx-10,tamy+75,
		tamx-40,tamy+75,
		tamx,tamy
	};
setcolor(BLACK);
setfillstyle(1,BROWN);
	drawpoly(8,tamgiac);
	floodfill(tamx,tamy+50,BLACK);
}


int main() {
    int driver = 0, mode = 0, maloi;
    initgraph(&driver, &mode, (char*)"");
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");
    int X = 100;
    int Y = 150;
    if ((maloi = graphresult()) != 0) {
        printf("Không thể khởi động đồ họa \n");
        printf("Mã lỗi : %d \n%s ", maloi, grapherrormsg(maloi));
        getch();
        exit(1);
    }

    srand(time(NULL)); // Khởi tạo seed cho random
    // Khởi tạo vị trí đám mây ngẫu nhiên
    for (int k = 0; k < CLOUD_COUNT; k++) {
        cloud_positions[k][0] = 100 + rand() % 600; // Vị trí X
        cloud_positions[k][1] = 70 + rand() % 100;  // Vị trí Y
    }
    // KHỞI TẠO GIÁ TRỊ BAN ĐÂÙ CHO HOA
    for ( int i = 0 ; i < 60 ; i++ ) {
		ax[i] = rand() % 600;
		ay[i] = rand() % 600;
		tocdo[i] = rand() % 5;
		tocdox[i] = rand() % 3;
	}
	
    long long i = 0, j = 0, m = 1, page = 0;
    long long max_width = getmaxx(); // Lấy giới hạn chiều rộng của màn hình
	int sum =0; int a =0; float scale = 1.0;
    while (1) { int x1 = 200  ,y1 = 200;
        setactivepage(page);
        cleardevice(); // Xóa trang active trước khi vẽ
        setbkcolor(LIGHTBLUE);
        sun();
        nui();
        may();
        duong();
		tamgiac(250,225); 
		coixaygio(250,225,25,75,sum);
		coixaygio(250,225,25,75,sum+90);
		vela();
		sum+= 2; 
		if ( sum >= 360) sum = 0;
        if (a==0 ) {
		drawBird_1(x1,y1,scale); delay(200) ;}
        	else if (a==1) drawBird_2(x1,y1,scale);
        		else if ( a==2) drawBird_3(x1,y1,scale);
        			else if (a==3) drawBird_4(x1,y1,scale);
        				else if ( a==4 ) {drawBird_5(x1,y1,scale);
        					a=0;
						}
	a++;
        // Vẽ nhân vật chạy
        setcolor(WHITE);
        circle(50 + i, 300 + j, 15);  // Đầu
        line(50 + i, 315 + j, 50 + i, 350 + j);  // Thân
        line(50 + i, 330 + j, 20 + i, 320 + j);  // Tay trái
        line(50 + i, 330 + j, 80 + i, 320 + j);  // Tay phải

        // Chân
        if (m % 2 == 0) {
            line(50 + i, 350 + j, 50 + i, 390 + j);  // Chân thẳng
        } else {
            line(50 + i, 350 + j, 35 + i, 390 + j);  // Chân trái
            line(50 + i, 350 + j, 65 + i, 390 + j);  // Chân phải
        }

        // Di chuyển theo phím
        if (GetAsyncKeyState(VK_LEFT)) {
            if (i > -40) { // Giới hạn bên trái
               i -= 5;
                m++;
            }
        }
        if (GetAsyncKeyState(VK_RIGHT)) {
            if (i < max_width - 50) { // Giới hạn bên phải
                i += 5;
                m++;
            }
        }
        if (GetAsyncKeyState(VK_ESCAPE)) { // Thoát bằng phím ESC
            break;
        }
        if (GetAsyncKeyState(VK_UP)) { // Di chuyển lên
            j -= 5;
        }
        if (GetAsyncKeyState(VK_DOWN)) { // Di chuyển xuống
            j += 5;
        }

        // Cập nhật vị trí đám mây để tạo hiệu ứng động
        for (int k = 0; k < CLOUD_COUNT; k++) {
            cloud_positions[k][0] += 1; // Di chuyển đám mây sang phải
            if (cloud_positions[k][0] > max_width) {
                cloud_positions[k][0] = -100; // Nếu ra ngoài, trở lại bên trái
                cloud_positions[k][1] = 70 + rand() % 100; // Thay đổi vị trí Y ngẫu nhiên
            }
        }
        

        setvisualpage(page); // Hiển thị trang hiện tại

        page = 1 - page; // Chuyển đổi giữa 2 trang

        delay(50); // Giảm độ trễ để chuyển trang mượt mà hơn
    }

    closegraph();
    return 0;
}

#include <bits/stdc++.h>
#include <conio.h>
#include <graphics.h>
#include <stdlib.h>
#include <windows.h>
#include <time.h>
#include<math.h>
#define CLOUD_COUNT 5
#define PI 3.14159265
// Khai báo mảng vị trí đám mây
long long cloud_positions[CLOUD_COUNT][2];
// VẼ CHIM
void chim1(int x, int y, float a){
    setcolor(0);
    int b1[10] = {a*(x- 20), a*(y - 15), a*x, a*(y+5), a*(x+20), a*(y - 15), a*x, a*(y - 5), a*(x - 20), a*(y-15)};
    drawpoly(5, b1);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

void chim2(int x, int y, float a){
    setcolor(0);
    int b2[10] = {a*(x - 20), a*(y -10), a*x, a*(y + 3), a*(x + 20), a*(y - 10), a*(x), a*(y - 5), a*(x - 20), a*(y - 10)};
    drawpoly(5, b2);
    setfillstyle(1, 0);
    floodfill(a*(x), a*(y), 0);
    setcolor(15);
}

void chim3(int x, int y, float a){
    setcolor(0);
    int b3[10] = {a*(x - 20), a*(y), a*x, a*(y+5), a*(x+20), a*y, a*x, a*(y - 2), a*(x - 20), a*y};
    drawpoly(5, b3);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

void chim4(int x, int y, float a){
    setcolor(0);
    int b4[10] = {a*(x - 20), a*(y + 10), a*x, a*(y + 5), a*(x + 20), a*(y + 10), a*x, a*(y - 3), a*(x - 20), a*(y+10)};
    drawpoly(5, b4);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

void chim5(int x, int y, float a){
    setcolor(0);
    int b5[10] = {a*(x - 20), a*(y + 15), a*x, a*(y+5), a*(x+20), a*(y+15), a*x, a*(y - 5), a*(x - 20), a*(y+15)};
    drawpoly(5, b5);
    setfillstyle(1, 0);
    floodfill(a*x, a*y, 0);
    setcolor(15);
}

 void vocanh(int x, int y, int &a,float scale) {
    
    switch(a) {
        case 0: chim1(x, y, scale); break;
        case 1: chim2(x, y, scale); break;
        case 2: chim3(x, y, scale); break;
        case 3: chim4(x, y, scale); break;
        case 4: chim5(x, y, scale); break;
    }
    a = (a + 1) % 5;  // Đảm bảo a luôn nằm trong khoảng từ 0 đến 4
}


// HÀM VẼ MẶT TRỜI
void sun() {
    setcolor(WHITE);
    int suncolor = RGB (255, 215, 0);
    setfillstyle(SOLID_FILL, suncolor);
    circle(550, 60 , 50);
    floodfill(550, 60, WHITE);
}



// VẼ LÁ
void vehoa(int x, int y) {
	setcolor(LIGHTMAGENTA);
    setfillstyle(SOLID_FILL, WHITE);
    fillellipse(x, y, 3, 3); 
}
// KHỞI TẠO GIÁ TRỊ CHO HOA
int ax[60], ay[60], tocdoy[60], tocdox[60];	
// HIỆU ỨNG HOA RƠI
void vela() {
	for ( int i = 0 ; i < 60 ; i++ ) {
		vehoa(ax[i],ay[i]);
		ax[i] = ax[i] + tocdox[i] ; // cho hoa rơi theo phương ngang 
		ay[i] = ay[i] + tocdoy[i];	// cho hoa rơi theo phương dọc 
		
		// khởi tạo lại giá trị khi hoa rơi khỏi màn hình 
		if ( ax[i] > getmaxx() || ay[i] > getmaxy() || ax[i] < 0 || tocdoy[i] == 0   ) {
			ax[i] = rand() % getmaxx() ;
			ay[i] = 0 ;
			tocdoy[i] = rand() % 8;
			tocdox[i] = -7 + rand() % (5 - (-7) + 1);
		}
		
	}
}


// BỤI CÂY
void buicay(int x, int y) {
	int LIGHTGRAY =RGB(105, 105, 105);
    setcolor(LIGHTGRAY);
    setfillstyle(SOLID_FILL, LIGHTGRAY);

    // Vẽ các hình tròn nhỏ để tạo bụi cây
    circle(x, y, 30);
    floodfill(x, y, LIGHTGRAY);

    circle(x - 35, y, 25);
    floodfill(x - 35, y, LIGHTGRAY);

    circle(x + 35, y, 25);
    floodfill(x + 35, y, LIGHTGRAY);

    circle(x - 20, y - 30, 20);
    floodfill(x - 20, y - 30, LIGHTGRAY);

    circle(x + 20, y - 30, 20);
    floodfill(x + 20, y - 30, LIGHTGRAY);
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
	int lightMountainColor = RGB(144, 238, 144); // Màu xanh lá sáng
    int darkMountainColor = RGB(34, 139, 34);       // Màu xanh đậm
	setcolor(darkMountainColor);
	setfillstyle(1,darkMountainColor);
    int a[16] = {0,300,200,150,400,300,350,170,450,250,525,170,getmaxx(),300,0,300};
    fillpoly(8,a);
    
    setfillstyle(1,lightMountainColor);
    int b[8] = {400,300,268,200,350,170,400,300};
    fillpoly(4,b);
    
    int c[8] = {0,300,200,150,150,250,0,300};
    fillpoly(4,c);
    
    int d[8] = { 450,250,525,170,420,225,450,250};
    fillpoly(4,d);
    
}

// VẼ CÂY 
void cay(int x, int y) {
	int BROWN = RGB(139, 69, 19);
	setcolor(BROWN);
	setfillstyle(1,BROWN);
	ellipse(x,y,0,360,10,80);
	floodfill(x,y,BROWN);
		
}
// VẼ LÁ CHO CÂY
void la(int x, int y ,	int angle = 0) {
	for ( int i = 0; i < 7; i++) {

	int  x1 = x-70 , tempt1 = x1,
		 y1 = y+30, tempt2 = y1,
		 x2 = x-80, tempt4 = x2,
		 y2 =  y+10 ,tempt3 = y2,
		 x3 = x -50 , tempt5 = x3,
		 y3 = y -10 , tempt6 = y3;
		 
		 double theta = ( double ) (angle%360)*3.14/180.0 ;
		 
		 
		tempt1= x + (x1 - x)*cos(theta) - (y1 - y)*sin(theta);
		tempt2 =y+ (x1 - x)*sin(theta) + (y1 - y)*cos(theta);
		tempt3 = x+ (x2 - x)*cos(theta) - (y2 - y)*sin(theta);
		tempt4 = y+ (x2 - x) *sin(theta) - (y2-y )*cos(theta);
		tempt5 = x+ (x3 - x)*cos(theta) - (y3 - y)*sin(theta);
		tempt6 = y+ (x3 - x) *sin(theta) - (y3-y )*cos(theta);
	int a[10] = { x,y ,tempt1,tempt2 ,tempt5,tempt6,tempt3,tempt4,x,y};

		int green = RGB(46, 139, 87);
		setcolor(GREEN);
		setfillstyle(1,green);
		fillpoly(5,a);
		
		angle += 50;
	}
}



// HÀM VẼ ĐƯỜNG
void duong() {
	int sandColor = RGB(194, 178, 128);
    setfillstyle(1,sandColor);
    bar(0, 400, 800, 500);
    bar(0,300,800,310);
    
    
    int riverColor = RGB(0, 51, 102);
    setfillstyle(1, riverColor);
    bar(0,310,800,360);
    
    
    
    int  PaleGreen = RGB(175, 238, 238);
    setfillstyle(1,  PaleGreen);
    bar(0,360,800,380);
    
    
    int DarkBlue = RGB(224, 255, 255);
    setfillstyle(1, DarkBlue);
	bar(0,380,800,400);
    

    
    setcolor(GREEN);
   	setfillstyle(1, LIGHTGREEN);
   	pieslice(325,325,30,330,10);
	pieslice(150,335,30,330,10);// VẼ BÈO
	pieslice(500,335,30,330,10);
   	  	
    
    buicay(20,getmaxy()-10);
    buicay(getmaxx()-20,getmaxy()-10);
    
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
		tocdoy[i] = rand() % 8;
		tocdox[i] = -7 + rand() % (5 - (-7) + 1);
	}
	int skyColor = RGB(135, 206, 235);
	int pos= 0 ,value;	
    long long i = 0, j = 0, m = 1, page = 0;
    long long max_width = getmaxx(); // Lấy giới hạn chiều rộng của màn hình
	int sum =0;int a = 0;
        int speed = 100;
    while (1) { int x1 = 900  ,y1 = 50,x2 = 400,y2 = 100,x3 = 550,y3 = 70;
        setactivepage(page);
        cleardevice(); // Xóa trang active trước khi vẽ
        setbkcolor(skyColor);
        //BACKGROUND
        sun();    nui();    may();    duong(); 
        cay(100,450);    la(100,370,90);	vela();
        
        // CHIM
        vocanh(x1, y1, a,0.5);
        vocanh(x2, y2, a,1.0);
        vocanh(x3, y3, a,0.75);
        
        // CỐI XAY GIÓ
		tamgiac(500,380); 
		coixaygio(500,380,25,75,sum);
		coixaygio(500,380,25,75,sum+90);
		
		
		sum+= 2; 
		if ( sum >= 360) sum = 0;
		
    	
        
        
        // Vẽ nhân vật chạy
        setcolor(BLACK);
        setfillstyle(1,RED);
        circle(50 + i, 300 + j, 15);  // Đầu
        floodfill(50+i,300+j,BLACK);

        

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
        	
        if (GetAsyncKeyState(VK_SPACE) && (pos == 0) ) { // Nhảy
        	pos = 1;
        	value = j;
            j -= 50; 
        }
        if (pos) {
        	if ( j < value ) j+= 7;
			if ( j >= value ) {
					j= value;
					pos =0;
				} 
		}
        	
        

        // Cập nhật vị trí đám mây để tạo hiệu ứng động
        for (int k = 0; k < CLOUD_COUNT; k++) {
            cloud_positions[k][0] += 3; // Di chuyển đám mây sang phải
            if (cloud_positions[k][0] > max_width) {
                cloud_positions[k][0] = -100; // Nếu ra ngoài, trở lại bên trái
                cloud_positions[k][1] = 70 + rand() % 100; // Thay đổi vị trí Y ngẫu nhiên
            }
        }
        

        setvisualpage(page); // Hiển thị trang hiện tại

        page = 1 - page; // Chuyển đổi giữa 2 trang

        delay(70); // Giảm độ trễ để chuyển trang mượt mà hơn
    }

    closegraph();
    return 0;
}

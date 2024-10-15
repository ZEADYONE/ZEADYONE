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
void chim1(int x, int y, float size){
    setcolor(0);
    int b1[10] = {size*(x- 20), size*(y - 15), size*x, size*(y+5), size*(x+20), size*(y - 15), size*x, size*(y - 5), size*(x - 20), size*(y-15)};
    drawpoly(5, b1);
    setfillstyle(1, 0);
    floodfill(size*x, size*y, 0);
    setcolor(15);
}

void chim2(int x, int y, float size){
    setcolor(0);
    int b2[10] = {size*(x - 20), size*(y -10), size*x, size*(y + 3), size*(x + 20), size*(y - 10), size*(x), size*(y - 5), size*(x - 20), size*(y - 10)};
    drawpoly(5, b2);
    setfillstyle(1, 0);
    floodfill(size*(x), size*(y), 0);
    setcolor(15);
}

void chim3(int x, int y, float size){
    setcolor(0);
    int b3[10] = {size*(x - 20), size*(y), size*x, size*(y+5), size*(x+20), size*y, size*x, size*(y - 2), size*(x - 20), size*y};
    drawpoly(5, b3);
    setfillstyle(1, 0);
    floodfill(size*x, size*y, 0);
    setcolor(15);
}

void chim4(int x, int y, float size){
    setcolor(0);
    int b4[10] = {size*(x - 20), size*(y + 10), size*x, size*(y + 5), size*(x + 20), size*(y + 10), size*x, size*(y - 3), size*(x - 20), size*(y+10)};
    drawpoly(5, b4);
    setfillstyle(1, 0);
    floodfill(size*x, size*y, 0);
    setcolor(15);
}

void chim5(int x, int y, float size){
    setcolor(0);
    int b5[10] = {size*(x - 20), size*(y + 15), size*x, size*(y+5), size*(x+20), size*(y+15), size*x, size*(y - 5), size*(x - 20), size*(y+15)};
    drawpoly(5, b5);
    setfillstyle(1, 0);
    floodfill(size*x, size*y, 0);
    setcolor(15);
}
void vocanh(int x, int y, int &a,float size) {
    
    switch(a) {
        case 0: chim1(x, y, size); break;
        case 1: chim2(x, y, size); break;
        case 2: chim3(x, y, size); break;
        case 3: chim4(x, y, size); break;
        case 4: chim5(x, y, size); break;
    }
    a = (a + 1) % 5;  // Đảm bảo a luôn nằm trong khoảng từ 0 đến 4
}           


// HÀM VẼ MẶT TRỜI
void sun() {
    setcolor(WHITE);
    int suncolor = RGB (255, 215, 0);
    setfillstyle(1, suncolor);
    circle(550, 60 , 50);
    floodfill(550, 60, WHITE);
}



// VẼ HOA
void vehoa(int x, int y) {
	setcolor(LIGHTMAGENTA);
    setfillstyle(1, WHITE);
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

// SÂU
int check1 = 1;
void sau1(int *x, int *y, int nhap) {
    int direc = (check1 == 1) ? 5 : -5;  // Hướng di chuyển
    int x1 = *x + ((check1 == 1) ? 8 : -8);
    int y1 = *y - 5;

    setfillstyle(1, GREEN);

    // Đổi hướng dựa trên giới hạn của x
    if (*x == 400) check1 = 0;
    else if (*x == 150) check1 = 1;

    // Vẽ sector và circle dựa trên giá trị 'nhap'
    int radiusX = (nhap == 1) ? 15 : 20;
    int radiusY = (nhap == 1) ? 15 : 10;

    sector(*x, *y, 0, 180, radiusX, radiusY);
    circle(x1, y1, 3);
    setcolor(WHITE);
    circle(x1, y1, 2);

    // Cập nhật tọa độ x
    *x += direc;
}
int check2 = 1;
void sau2(int *x, int *y, int nhap) { 
	setcolor(BLACK);
    int direc = (check2 == 1) ? 5 : -5;  // Hướng di chuyển
    int x1 = *x + ((check2 == 1) ? 8 : -8);
    int y1 = *y - 5;

    setfillstyle(1,LIGHTMAGENTA);

    // Đổi hướng dựa trên giới hạn của x
    if (*x == 400) check2 = 0;
    else if (*x == 150) check2 = 1;

    // Vẽ sector và circle dựa trên giá trị 'nhap'
    int radiusX = (nhap == 1) ? 15 : 20;
    int radiusY = (nhap == 1) ? 15 : 10;

    sector(*x, *y, 0, 180, radiusX, radiusY);
    circle(x1, y1, 3);
    setcolor(WHITE);
    circle(x1, y1, 2);

    // Cập nhật tọa độ x
    *x += direc;
}


// BỤI CÂY
void buicay(int x, int y) {
	int LIGHTGRAY =RGB(105, 105, 105);
    setcolor(LIGHTGRAY);
    setfillstyle(1, LIGHTGRAY);

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
    setfillstyle(1, WHITE);
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

// VẼ THÂN DỪA
void cay(int x, int y) {
	int BROWN = RGB(139, 69, 19);
	setcolor(BROWN);
	setfillstyle(1,BROWN);
	ellipse(x,y,0,360,10,80);
	floodfill(x,y,BROWN);		
}
// VẼ QUẢ (x, y) và bán kính r
void veQuaDua(int x, int y, int r) {
    setfillstyle(1, BROWN);  // Màu nâu cho vỏ dừa
    setcolor(BLACK);
    fillellipse(x, y, r, r);  // Vẽ quả dừa dạng hình tròn

    // Vẽ điểm sáng để tạo hiệu ứng phản chiếu
    setfillstyle(1, WHITE);
    fillellipse(x - r / 3, y - r / 3, r / 4, r / 4);
}

// VẼ LÁ DỪA
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
	
	veQuaDua(90, 380, 12);
    veQuaDua(110, 380, 12);
    veQuaDua(100, 390, 12);
}



// HÀM VẼ ĐƯỜNG
// KHỞI TẠO VỊ TRÍ BÈO
int beos[3][2] = {{325, 325}, {150, 335}, {500, 335}};
void duong() {
	// MẶT CÁT
	int sandColor = RGB(194, 178, 128);
    setfillstyle(1,sandColor);
    bar(0, 400, 800, 500);
   
    //MẶT BIỂN
    int riverColor = RGB(0, 51, 102);
    setfillstyle(1, riverColor);
    bar(0,300,800,360);
    
    int  PaleGreen = RGB(175, 238, 238);
    setfillstyle(1,  PaleGreen);
    bar(0,360,800,380);
    
    
    int DarkBlue = RGB(224, 255, 255);
    setfillstyle(1, DarkBlue);
	bar(0,380,800,400);
    

    
    setcolor(GREEN);
    setfillstyle(1, LIGHTGREEN);
    for (int i = 0; i < 3; i++) {
        pieslice(beos[i][0], beos[i][1], 30, 330, 10);
    }
   	  	
    
    buicay(20,getmaxy()-10);
    buicay(getmaxx()-20,getmaxy()-10);
    
}


// HÀM CẬP NHẬT VỊ TRÍ BÈO
void capNhatBeo(int max_width) {
    for (int i = 0; i < 3; i++) {
        beos[i][0] += 2; // Tốc độ di chuyển ngang của bèo
        if (beos[i][0] > max_width) {
            beos[i][0] = -50; // Khi bèo ra khỏi màn hình, đưa nó về bên trái
        }
    }
}


// CỐI XAY GIÓ TỪ HCN VỚI RỘNG DÀI (w,h) 
void coixaygio ( int tamx, int tamy, int w, int h , int angle = 0 ) {
// ANGLE LÀ GÓC QUAY 

double theta = ( double ) (angle%180)*3.14/180.0	;// ĐỔI SANG ĐƠN VỊ RADIAN
	int dx = w/2;	// TÂM X CỦA HCN
	int dy = h/2;	// TÂM Y CỦA HCN
	
// TỌA ĐỘ 4 ĐIỂM TRONG HÌNH CHỦ NHẬT
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

// VẼ HCN
for(int i=0; i<8; i+=2)
line(point[i], point[i+1], point[(i+2)%8], point[(i+3)%8]);
circle(tamx,tamy,10);
}

// THÂN CỐI XAY GIÓ
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
    
    // KHỞI TẠO VỊ TRÍ ĐÁM MÂY 
    for (int k = 0; k < CLOUD_COUNT; k++) {
        cloud_positions[k][0] = 100 + rand() % 600; // Vị trí X
        cloud_positions[k][1] = 70 + rand() % 100;  // Vị trí Y
    }
    
    // KHỞI TẠO VỊ TRÍ CHO SÂU
    int sau1x = 150; int sau1y = 460;
    int sau2x = 400; int sau2y = 430;
    
    
    // KHỞI TẠO GIÁ TRỊ BAN ĐÂÙ CHO HOA
    for ( int i = 0 ; i < 60 ; i++ ) {
		ax[i] = rand() % 600;
		ay[i] = rand() % 600;
		tocdoy[i] = rand() % 8;
		tocdox[i] = -7 + rand() % (5 - (-7) + 1);
	}
	
	// LẤY MÀU NỀN
	int skyColor = RGB(135, 206, 235);
	
	// CÁC GIÁ TRỊ ĐỂ KIỂM SOÁT VIỆC NHẢY CỦA BÓNG
	int pos= 0 ,value;	
	
	// CÁC BIẾN DI CHUYỂN CỦA BÓNG
    long long i = 0, j = 0, m = 1, page = 0;
    
    long long max_width = getmaxx(); // Lấy giới hạn chiều rộng của màn hình
    
    // KHỞI TẠO GÓC QUAY CHO CỐI XAY GIÓ
		int sum =0;
		
	// BIẾN DÙNG ĐỂ CHUYỂN TIẾP CÁC HOẠT ẢNH CỦA CHIM
		int a = 0;
        
    while (1) { 
        setactivepage(page);
        cleardevice(); // Xóa trang active trước khi vẽ
        setbkcolor(skyColor);
        
        int 	x1 = 900  ,y1 = 50, 	// VỊ TRÍ CHIM 1 
		x2 = 400,y2 = 100,	// VỊ TRÍ CHIM 3 
		x3 = 550,y3 = 70;	// VỊ TRÍ CHIM 3
        
        //BACKGROUND
        sun();    nui();    may();    duong(); 
        cay(100,450);    la(100,370,90);	vela();
        
        // CẬP NHẬT VỊ TRÍ BÈO	
        capNhatBeo(max_width);
        
        // CHIM
        vocanh(x1, y1, a,0.5);
        vocanh(x2, y2, a,1.0);
        vocanh(x3, y3, a,0.75);
        
        // CỐI XAY GIÓ
		tamgiac(500,380); 
		coixaygio(500,380,25,75,sum);
		coixaygio(500,380,25,75,sum+90);
		
		// TĂNG GÓC QUAY CHO CỐI XAY GIÓ
		sum+= 2; 
		if ( sum >= 360) sum = 0;
		
		// SÂU
    	sau1(&sau1x,&sau1y,page);
    	sau2(&sau2x,&sau2y,page);
    	
        
        // VẼ BÓNG
        setcolor(BLACK);
        setfillstyle(1,RED);
        circle(50 + i, 300 + j, 15);  // BÓNG
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

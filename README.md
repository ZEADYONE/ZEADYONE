#include <bits/stdc++.h>
#include <graphics.h>
#include <windows.h>
#include<math.h>
#include <conio.h> 
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

void drawUFO(int x, int y, bool glow) {
	int a[4] = {RGB(255, 0, 0), RGB (255, 204, 0), RGB (255, 102, 0), RGB(255, 255, 255)}; // Mảng màu
    if (glow) {
        // Vẽ hiệu ứng phóng lửa hình elip bên dưới UFO
    int fireHeight = 20; // Chiều cao của hiệu ứng lửa
    int fireWidth = 10;  // Độ rộng của mỗi ngọn lửa
    for (int i = -2; i <=2; i+=2) { 
        int fireX = x + i * 10;   // Tọa độ x của ngọn lửa
        int fireY = y + 25;       // Tọa độ y của ngọn lửa
		for ( int j = 0 ; j <=9 ; j += 3  ) {
        setcolor(a[j/3]);
        setfillstyle(SOLID_FILL, a[j/3]);
        fillellipse(fireX, fireY, fireWidth-j, fireHeight-j);  // Vẽ hình elip dọc làm lửa
    	}   
    }
    }

    setcolor(LIGHTGRAY);
    setfillstyle(SOLID_FILL, LIGHTGRAY);
    ellipse(x, y, 0, 360, 60, 20); // Thân chính của UFO
    floodfill(x, y, LIGHTGRAY);

    // Vẽ mái vòm trên của UFO
    setcolor(WHITE);
    setfillstyle(SOLID_FILL, WHITE);
    ellipse(x, y - 20, 0, 360, 30, 15); // Mái vòm của UFO
    floodfill(x, y - 20, WHITE);

     int numLights = 5;  // Số lượng đèn tròn
    for (int i = 0; i < numLights; i++) {
        float angle = (i - (numLights - 1) / 2.0) * (M_PI / (numLights + 1)) + M_PI / 2; 
        int lightX = x + cos(angle) * 45;  // Tọa độ x của đèn theo đường cong
        int lightY = y + sin(angle) * 10;  // Tọa độ y của đèn theo đường cong

        setcolor(YELLOW);
        setfillstyle(SOLID_FILL, YELLOW);
        circle(lightX, lightY, 5); // Vẽ đèn tròn
        floodfill(lightX, lightY, YELLOW);
    }

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
void cay(int x, int y,float size) {
	int BROWN = RGB(139, 69, 19);
	setcolor(BROWN);
	setfillstyle(1,BROWN);
	ellipse(x,y,0,360,size*10,size*80);
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
void ladua1(int x, int y ,	int angle , float size) {	
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
	int a[10] = { size*x,size*y ,size*tempt1,size*tempt2 ,size*tempt5,size*tempt6,size*tempt3,size*tempt4,size*x,size*y};

		int green = RGB(46, 139, 87);
		setcolor(GREEN);
		setfillstyle(1,green);
		fillpoly(5,a);
		
		angle += 50;
	}
	
	veQuaDua(size*(x-10), size*(y+10), size*12);
    veQuaDua(size*(x+10), size*(y+10), size*12);
    veQuaDua(size*x, size*(y+20), size*12);
}




// HÀM VẼ ĐƯỜNG
// KHỞI TẠO VỊ TRÍ BÈO
int sandColor = RGB(194, 178, 128);
int beos[3][2] = {{325, 325}, {150, 335}, {500, 335}};
void duong() {
	// MẶT CÁT
	
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
    int page = 0;
    
    
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
        // Tọa độ ban đầu của UFO
	int x = 200, y = 200;  
        char ch;
        bool glow = false;  // Biến theo dõi trạng thái phát sáng

    long long max_width = getmaxx(); // Lấy giới hạn chiều rộng của màn hình
    
    // KHỞI TẠO GÓC QUAY CHO CỐI XAY GIÓ
		int sum =0;
		
	// BIẾN DÙNG ĐỂ CHUYỂN TIẾP CÁC HOẠT ẢNH CỦA CHIM
		int a = 0;
        
    while (1) { 
        setactivepage(page);
        cleardevice(); // Xóa trang active trước khi vẽ
        setbkcolor(skyColor);
        
    
        int x1 = 900  ,y1 = 50, // VỊ TRÍ CHIM 1 
	    x2 = 400,y2 = 100,	// VỊ TRÍ CHIM 3 
	    x3 = 550,y3 = 70;	// VỊ TRÍ CHIM 3
        
        //BACKGROUND
        sun();    nui();    may();    duong();  vela();
        cay(100,450,1);   ladua1(100,370,90,1.0);	
		cay(440,390,0.5); ladua1((440/0.6),(350/0.6),90,0.6); 
		setfillstyle(1,sandColor); bar(430,410,450,430);
        
        // CẬP NHẬT VỊ TRÍ BÈO	
        capNhatBeo(max_width);
        
        // CHIM
        vocanh(x1, y1, a,0.5);
        vocanh(x2, y2, a,1.0);
        vocanh(x3, y3, a,0.75);
        
        // CỐI XAY GIÓ
		tamgiac(515,380); 
		coixaygio(515,380,25,75,sum);
		coixaygio(515,380,25,75,sum+90);
	
		// TĂNG GÓC QUAY CHO CỐI XAY GIÓ
		sum+= 2; 
		if ( sum >= 360) sum = 0;
		
		// SÂU
    	sau1(&sau1x,&sau1y,page);
    	sau2(&sau2x,&sau2y,page);
    	
        // Vẽ UFO tại tọa độ (x, y) với trạng thái phát sáng
        drawUFO(x, y, glow);
        glow = false;

       
        
        // Di chuyển theo phím
        if (GetAsyncKeyState(VK_LEFT)) {
            if (x > -40) { // Giới hạn bên trái
               x -= 5;
               
            }
        }
        if (GetAsyncKeyState(VK_RIGHT)) {
            if (x < max_width - 50) { // Giới hạn bên phải
                x += 5;
               
            }
        }
        if (GetAsyncKeyState(VK_ESCAPE)) { // Thoát bằng phím ESC
            break;
        }
        if (GetAsyncKeyState(VK_UP)) { // Di chuyển lên
            y -= 5;
            glow = !glow;
        }
        if (GetAsyncKeyState(VK_DOWN)) { // Di chuyển xuống
            y += 5;
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

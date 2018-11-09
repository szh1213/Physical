
![0.gif](attachment:0.gif)

float x;	//运动方向	
float force;	//运动推力

void setup() {
   size(666, 233);
   force =1;
}

void draw() {
   background(178);
   rect(x+=force,5,50,50);	//x轴，y轴，z轴运动方法相同
}

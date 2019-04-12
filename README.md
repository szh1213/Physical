# 物理运动

通过代码实现物理运动，实现物理数字化

运动：在物理上指有方向，有推力；在数学上称为向量，有方向，有大小

空间中的位置变化，包括移动、转动、流动、变形、振动、波动、扩散等

下面是基本的运动，大家可以混合组合运动

---
匀速运动（牛顿第一定律：匀速直线运动）
```java
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
```


匀加速运动
```java
float x;	//运动方向	
float force;	//运动推力

void setup() {
   size(666, 233);
}

void draw() {
   background(178);

   rect(x+=force++,5,23,23); 	//force+ 就是推力中再添加推力，即双重推力，实现匀加速效果
}
```


变速运动
```java
float x;  //运动方向  
float force;  //运动推力

void setup()
{
   size(666, 233);
}

void draw() 
{
   background(178);

   rect(x+=force+=random(1),5,23,23);   //通过random让加速度随机改变，实现变加速
}
```


余弦运动
```java
float theta;

void setup()
{
    size(666, 233);
}

void draw() 
{
    stroke(250);
    fill(175);
    ellipse(width/2 + cos(theta) * 50, height/2, 16, 16);

    theta += 0.01;
}
```


正弦运动
```java
float theta;

void setup()
{
    size(666, 233);
}

void draw() 
{
    stroke(250);
    fill(175);
    ellipse(width/2, height/2+ sin(theta) * 50, 16, 16);	

    theta += 0.01;
}
```


圆周运动
```java
float theta;

void setup()
{
    size(666, 233);
}

void draw() 
{
    stroke(250);
    fill(175);
    ellipse(width/2+ cos(theta) * 50, height/2+ sin(theta) * 50, 16, 16);

    theta += 0.01;
}
```


螺旋运动
```java
float theta,r;

void setup()
{
    size(666, 233);
    r=2;
}

void draw() 
{
    stroke(250);
    fill(175);
    ellipse(width/2+ cos(theta) * r, height/2+ sin(theta) * r, 5, 5);

    theta += 0.01;
    r += 0.05;
}
```


钟摆运动
```java
  PVector exy,lxy;
  float angle,aspeed,aspeedadd;

void setup()
{
  size(666,233);
  exy = new PVector(width/2,height/2);
  lxy = new PVector(width/2,0);
  angle = PI/4;
}

void draw()
{
  background(250);

  // 重力加速度 * sin（theta） = 钟摆角加速度。
  aspeedadd = (-1 * 0.4 / 125) * sin(angle);    
  aspeed += aspeedadd;
  angle += aspeed;  
  
  //空气摩擦，随着时间推移，最终会停下来
  aspeed *= 0.995;  

  exy.set(sin(angle) * 125, cos(angle) * 125 ,0);
  exy.add(lxy);

  stroke(0);
  line(lxy.x, lxy.y, exy.x, exy.y);
  fill(178);
  ellipse(exy.x, exy.y, 16,16);

}
```


波形运动
```java
float theta;
void setup(){
  size(666,666);
}

void draw(){
  background(250);

  for(int x = 0; x<width; x +=24){
    ellipse(x,height/2 + sin(theta)*100,20,20);  
    theta += 0.2;
  }  
}
```

```java
void setup(){
  size(666,666);
}

void draw(){
  background(250);

  beginShape();
    for(int x = 0; x<width; x+=20){
      vertex(x,map(sin(theta),-1,1,0,height));
      theta += 0.2;
    }  
  endShape();
}
```


随机运动
```java
void setup()
{
  size(666,233);
}

void draw()
{
  background(158);
  ellipse(random(width),random(height),10,10);
}
```


```java

  float x,y;

void setup()
{
  size(666,233);
  x= width/2;
  y = height/2;
}

void draw() {
  point(x,y);
  float r = random(1);
  if (r < 0.4)  x++;
  else if (r < 0.6) x--;
  else if (r < 0.8) y++;
  else y--;

}
```


跟随运动
```java
void setup()
{
  size(666,233);
}

void draw()
{
  line(pmouseX,pmouseY,mouseX,mouseY);
}
```

```java
void setup()
{
size(300,300);
}
void draw()
{
  background(158);

  fill(255);
  ellipse(100+mouseX/15,150+mouseY/15,12,12);
  ellipse(200+mouseX/15,150+mouseY/15,12,12);
}
```

```java

void setup()
{
  size(666,666);
}

void draw()
{
  background(158);
  PVector mouse = new PVector(mouseX,mouseY);
  PVector center = new PVector(width/2,height/2);
  mouse.sub(center);  
  mouse.normalize();  
  mouse.mult(30);  
  translate(width/2,height/2);  
  ellipse(mouse.x,mouse.y,20,20);
}
```


噪音运动
```java

  float x,y,t1,t2;

void setup()
{
  size(666,233);
  
  t1 = 0;
  t2 = 10000;
}

void draw()
{
  background(97);
  
  x = map(noise(t1),0,1,0,width);
  y = map(noise(t2),0,1,0,height);
  
  noStroke();
  fill(158);
  ellipse(x, y, 33, 33);
  
  t1 += 0.01;
  t2 += 0.01;
}

```


鼠标运动
```java

void setup()
{
  size(666,233);
}

void draw()
{
  background(97);
  
  ellipse(mouseX,mouseY,50,50);
}

```


键盘运动(w a s d 控制移动)
```java
  float x,y;
void setup()
{
  size(666,233);
  x = width/2;
  y = height/2;
}

void draw()
{
  background(97);
  
  ellipse(x,y,50,50);
  
  if(keyPressed && key == 'w') y--;
  if(keyPressed && key == 's') y++;
  if(keyPressed && key == 'a') x--;
  if(keyPressed && key == 'd') x++;
}

```


声控运动（使用麦克风大喊，矩形会运动）

```java
import processing.sound.*;      //插入声音库
float x;
                            
AudioIn ai;     //声明麦克风输入                           
Amplitude ampl;     //声明振幅
                            
void setup()    //播放一次
{    
    size(666,233);      //窗口大小
                            
    ai = new AudioIn(this,0);   //设置麦克风输入
    ai.play();      //麦克风播放
                            
    ampl = new Amplitude(this);     //设置振幅
    ampl.input(ai);     //振幅输入
}
                            
void draw()     //循环播放
{
    background(158);
    
    float v = ampl.analyze(); //振幅分析（振幅范围是0~1的数字）  
    rect(x+=v * 50,height/2,50,50);
} 

```

平抛运动

```java
float x,y,vx,vy,g;
void setup(){
  size(300,500);
  x = 20;y = 20;//初始位置
  vx = 1;vy = 0;//初始速度
  g = 0.0098;//重力加速度
}
void draw(){
  ellipse(x+=vx,y+=vy+=g,16,16);//vx恒定，vy初始为0，加速度为重力加速度
}
```


围绕运动

```java
void setup()
{
  size(800,600);
  smooth();strokeWeight(3);
}
float x1=400,y1=300,x2,y2,x3,y3,x4,y4,t=0;
void draw()
{
  frameRate(60);
  background(225);
  x2=x1+150*cos(t*TWO_PI/365);//地球周期为365天
  y2=y1+150*sin(t*TWO_PI/365);
  x3=x2+75*cos(t*TWO_PI/30);//月球周期为30天
  y3=y2+75*sin(t*TWO_PI/30);
  x4=x1+400*cos(t*TWO_PI/(365*3));//某彗星周期3年
  y4=y1+200*sin(t*TWO_PI/(365*3));
  t++;
  fill(255,255,0);
  ellipse(x1,y1,100,100);//绘制太阳
  noFill();
  ellipse(x1,y1,300,300);//绘制地球轨道
  ellipse(x1,y1,800,400);//绘制某彗星椭圆轨道
  fill(#69C5E8);
  ellipse(x2,y2,50,50);//绘制地球
  ellipse(x4,y4,15,15);//绘制月球
  noFill();
  ellipse(x2,y2,150,150);//绘制月球轨道
  fill(#BED5DE);
  ellipse(x3,y3,10,10);//绘制某彗星
  fill(0);
  textSize(50);text("sun",x1-37,y1+12);
  textSize(40);text("earth",x2-20,y2+12);
  textSize(30);text("moon",x3+10,y3+3);text("comet",x4+10,y4+5);
}
```

电磁场运动

```java
Lizi[] lizi=new Lizi[200];//声明粒子
float u1=1,u2=2,b1=0.005,b2=0.003;//设定电压及磁场强度
void setup()
{
  size(800,600);
  smooth();
  for(int i=0;i<lizi.length;i++)//初始化粒子
  {lizi[i]=new Lizi(200,52,random(0.1,5),random(0.1,5));}//粒子"飘出",速度很小
}
void draw()
{
  //background(204);
  strokeWeight(1);stroke(0);noFill();
  //绘制轴线及偏转磁场边界
  line(200,0,200,height);line(0,300,width,300);
  //绘制加速电场
  rect(100,50,96,5);rect(204,50,96,5);
  rect(100,150,96,5);rect(204,150,96,5);
  //绘制加速电场的方向
  line(150,65,150,130);line(150,130,140,120);line(150,130,160,120);
  line(250,65,250,130);line(250,130,240,120);line(250,130,260,120);
  //绘制速度选择器
  rect(100,155,5,145);rect(295,155,5,145);
  rect(100,300,96,5);rect(204,300,96,5);
  //绘制速度选择器的电场方向
  line(130,180,260,180);line(260,180,250,170);line(260,180,250,190);
  line(130,255,260,255);line(260,255,250,245);line(260,255,250,265);
  //绘制速度选择器的磁场方向
  line(130,200,170,230);line(130,230,170,200);
  line(230,200,270,230);line(230,230,270,200);
  //绘制偏转磁场方向
  for(int i=320;i<=height;i+=20)
    {
      for(int j=0;j<=width;j+=20)
      {ellipse(j,i,2,2);}
    }
  //更新例粒子
  for(int i=0;i<lizi.length;i++)
  {
    lizi[i].move();
    lizi[i].display();
  }
}
class Lizi//粒子类
{
  PVector location,a,v;//声明粒子的位置,加速度,速度
  PVector ae,ab;//声明电场及磁场产生的加速度
  float m,q;//声明粒子质量和电荷(正电荷)
  //初始化,传入参数
  Lizi(float px,float py,float pm,float pq)
  {
    location=new PVector(px,py);
    m=pm;q=pq;
    a=new PVector(0,0);//初加速度为0
    v=new PVector(0,0);//初速度也为0
  }
  void move()
  {
    //描述加速电场产生加速度
    if(location.y>50&&location.y<150
     &&location.x>100&&location.x<300)//加速电场区域
    {a=new PVector(0,(q*u1)/(m*100));}//a只由加速电场产生
    //描述速度选择器的电磁场产生加速度
    if(location.y>150&&location.y<300
     &&location.x>100&&location.x<300)//速度选择器区域
    {
      ae=new PVector((q*u2)/(m*150),0);//电场产生加速度
      ab=new PVector(0,0);            //磁场加速度ab设为0
      ab.add(v);//ab设为速度v;
      ab.rotate(radians(90));//再旋转90度得到方向(洛伦兹力垂直速度)
      ab.setMag(1);ab.mult(q*v.mag()*b1/m);//单位化ab,再计算大小并赋值
      a.add(ae);//粒子加速度加上电场加速度
      a.add(ab);//粒子加速度加上磁场加速度
    }
    //速度选择器筛选特定速度粒子
    if(location.y>300&&location.y<310&&v.y>0&&
    ((location.x>100&&location.x<198)||(location.x>202&&location.x<300)))
    {v.mult(0);}//撞击上挡板的粒子停止,即把速度设为0
    if(location.y>300)
    {
      ab=new PVector(0,0);//计算磁场加速度同上
      ab.add(v);ab.rotate(radians(270));
      ab.setMag(1);ab.mult(q*v.mag()*b2/m);
      a.add(ab);
    }
    if(location.y<300&&v.y<0)
    {v.mult(0);}//选择出的粒子撞上最后的挡板
    v.add(a);//粒子加速度累积得到粒子速度
    location.add(v);//粒子加速度累积得到粒子位矢量
    a.mult(0);
  }
  void display()
  {
    fill(160,160,160);//画出粒子
    ellipse(location.x,location.y,4,4);
  }
}
```

下面部分，以后搞明白了再补充

粒子运动

重力运动

碰撞运动

重力加速度

弹簧运动

旋转运动

流体运动

画笔运动

引力运动

集群运动

分子热运动

光速运动

量子纠缠运动

暗物质运动

时空穿梭运动

宇宙膨胀运动

磁场运动

电运动

波运动

指数运动

黄金分割运动

水波运动

风运动

闪电运动

龙卷风运动

细胞分裂运动

水滴融合运动

墨水喷洒运动

水蒸气蒸发运动




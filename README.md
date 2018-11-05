# physical-motion

【processing三大研究领域】

形式科学（视觉）：数学，艺术... ...
自然科学（功能）：物理，化学，生物... ...
社会科学（交互）：政治，经济，文化，历史，军事... ...

文字（视觉） → 静态图（视觉）→ 动态图（视觉+功能）→ 交互图（视觉+功能+社交）

【运动】

运动：在物理上指有方向，有推力；在数学上称为向量，有方向，有大小
空间中的位置变化，包括移动、转动、流动、变形、振动、波动、扩散等


匀速运动（牛顿第一定律：匀速直线运动）



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


匀加速运动

​​

float x;	//运动方向	
float force;	//运动推力

void setup() {
   size(666, 233);
}

void draw() {
   background(178);

   rect(x+=force++,5,23,23); 	//force+ 就是推力中再添加推力，即双重推力，实现匀加速效果
}


变速运动

​​

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


余弦运动

​​

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


正弦运动

​​

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

圆周运动

​​

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


螺旋运动

​​

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


钟摆运动

​​

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


波形运动

​​

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


​​

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


随机运动

​​

void setup()
{
  size(666,233);
}

void draw()
{
  background(158);
  ellipse(random(width),random(height),10,10);
}



跟随运动

​​

void setup()
{
  size(666,233);
}

void draw()
{
  line(pmouseX,pmouseY,mouseX,mouseY);
}

噪音运动

​​

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


鼠标运动

​​

void setup()
{
  size(666,233);
}

void draw()
{
  background(97);
  
  ellipse(mouseX,mouseY,50,50);
}


键盘运动(w a s d 控制移动)

​​

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

声控运动（使用麦克风大喊，矩形会运动）

​​

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


下面部分我也不会，谁会的话补充一下，以后搞明白了再补充
​

粒子运动
平抛运动
围绕运动
重力运动
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
文字运动
图片运动
视频运动

